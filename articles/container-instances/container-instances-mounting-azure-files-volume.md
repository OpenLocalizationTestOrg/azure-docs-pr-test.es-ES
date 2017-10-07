---
title: aaaMounting un volumen de archivos de Azure en instancias de contenedor de Azure
description: "Obtenga información acerca de cómo toomount un Azure los archivos de estado de toopersist de volumen con instancias de contenedor de Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="b4228-103">Montaje de un recurso compartido de archivos de Azure en Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="b4228-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="b4228-104">De forma predeterminada, Azure Container Instances no tiene estado.</span><span class="sxs-lookup"><span data-stu-id="b4228-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="b4228-105">Si el contenedor de Hola se bloquea o se detiene, se pierde todo su estado.</span><span class="sxs-lookup"><span data-stu-id="b4228-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="b4228-106">toopersist estado más allá de duración de Hola Hola del contenedor de, debe montar un volumen desde un almacén externo.</span><span class="sxs-lookup"><span data-stu-id="b4228-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="b4228-107">En este artículo se muestra cómo toomount compartir de un archivo de Azure para su uso con instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4228-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="b4228-108">Creación de un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="b4228-108">Create an Azure file share</span></span>

<span data-ttu-id="b4228-109">Antes de utilizar un recurso compartido de archivos de Azure en Azure Container Instances, debe crearlo.</span><span class="sxs-lookup"><span data-stu-id="b4228-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="b4228-110">Ejecute hello después de la secuencia de comandos toocreate un recurso compartido de archivos de almacenamiento cuenta toohost Hola y Hola compartan propio.</span><span class="sxs-lookup"><span data-stu-id="b4228-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="b4228-111">Tenga en cuenta que ese nombre de cuenta de almacenamiento de hello debe ser único globalmente, por lo que el script de Hola agrega una cadena en base toohello valor aleatorio.</span><span class="sxs-lookup"><span data-stu-id="b4228-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="b4228-112">Adquisición de detalles de acceso de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b4228-112">Acquire storage account access details</span></span>

<span data-ttu-id="b4228-113">toomount compartir un archivo de Azure como un volumen en instancias de contenedor de Azure, necesita tres valores: Hola nombre de la cuenta de almacenamiento, el nombre del recurso compartido de Hola y clave de acceso de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4228-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="b4228-114">Si ha usado el script de Hola anterior, nombre de cuenta de almacenamiento de Hola se creó con un valor aleatorio final Hola.</span><span class="sxs-lookup"><span data-stu-id="b4228-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="b4228-115">tooquery Hola final cadena (incluidos Hola aleatorio parte), utilice hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="b4228-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="b4228-116">Hello nombre de recurso compartido ya lo conoce (es *acishare* en script de Hola anterior), por lo que todo lo que queda es la clave de cuenta de almacenamiento de hello, que puede encontrarse con Hola el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b4228-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="b4228-117">Almacenamiento de los detalles de acceso de la cuenta de almacenamiento con un almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="b4228-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="b4228-118">Claves de la cuenta de almacenamiento protegen los datos de tooyour de acceso, por lo que recomendamos almacenarlas en un almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4228-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="b4228-119">Crear un almacén de claves con hello CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4228-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="b4228-120">Hola `enabled-for-template-deployment` conmutador permite toopull de administrador de recursos de Azure secretos desde el almacén de claves durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="b4228-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="b4228-121">Almacenar la clave de cuenta de almacenamiento de Hola como un secreto nuevo en el almacén de claves de hello:</span><span class="sxs-lookup"><span data-stu-id="b4228-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="b4228-122">Monte el volumen de Hola</span><span class="sxs-lookup"><span data-stu-id="b4228-122">Mount hello volume</span></span>

<span data-ttu-id="b4228-123">El montaje de un recurso compartido de archivos de Azure como un volumen en un contenedor es un proceso que consta de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="b4228-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="b4228-124">En primer lugar, se proporcionan detalles de Hola de recurso compartido de hello como parte de la definición de grupo del contenedor de hello, a continuación, especificar cómo desea que el volumen de hello montado en uno o varios contenedores de hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4228-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="b4228-125">volúmenes de hello toodefine desea toomake disponible para el montaje, agregue un `volumes` toohello definición de grupo de contenedor de plantilla de Azure Resource Manager Hola de matriz, a continuación, hacer referencia a ellos en la definición de Hola de contenedores individuales Hola.</span><span class="sxs-lookup"><span data-stu-id="b4228-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

<span data-ttu-id="b4228-126">plantilla de Hello incluye nombre de cuenta de almacenamiento de Hola y clave como parámetros, que se pueden proporcionar en un archivo de parámetros separados.</span><span class="sxs-lookup"><span data-stu-id="b4228-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="b4228-127">archivo de parámetros de hello toopopulate, necesitará tres valores: Hola nombre de la cuenta de almacenamiento, Hola Id. de recurso de su almacén de claves de Azure y Hola nombre secreto del almacén de claves que usa la clave de almacenamiento de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="b4228-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="b4228-128">Si ha seguido los pasos anteriores, puede obtener estos valores con hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="b4228-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="b4228-129">Insertar valores de hello en el archivo de parámetros de hello:</span><span class="sxs-lookup"><span data-stu-id="b4228-129">Insert hello values into hello parameters file:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="b4228-130">Contenedor de Hola de implementar y administrar archivos</span><span class="sxs-lookup"><span data-stu-id="b4228-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="b4228-131">Con definida por la plantilla de hello, puede crear el contenedor de Hola y montar el volumen mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4228-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="b4228-132">Suponiendo que hello archivo de plantilla se denomina *azuredeploy.json* y ese archivo de parámetros de Hola se denomina *azuredeploy.parameters.json*, línea de comandos de hello es:</span><span class="sxs-lookup"><span data-stu-id="b4228-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="b4228-133">Una vez que se inicia el contenedor de hello, puede usar la aplicación web simple de hello implementado a través de Hola **seanmckenna/aci-hellofiles** toohello de imagen, administrar archivos en el recurso compartido de archivos de Azure de hello en la ruta de acceso de montaje de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="b4228-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="b4228-134">Obtener dirección ip de hello para la aplicación web de Hola a través de la siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="b4228-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="b4228-135">Puede usar una herramienta como hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve e inspeccionar el recurso compartido de archivos de hello archivo escritos toohello.</span><span class="sxs-lookup"><span data-stu-id="b4228-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="b4228-136">toolearn más información acerca de utilizar plantillas del Administrador de recursos de Azure, archivos de parámetros e implementar con hello CLI de Azure, consulte [implementar los recursos con plantillas de administrador de recursos y la CLI de Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b4228-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4228-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4228-137">Next steps</span></span>

- <span data-ttu-id="b4228-138">Implementar para el primer contenedor mediante instancias de contenedor de Azure de hello [inicio rápido](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="b4228-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="b4228-139">Obtenga información acerca de hello [relación entre las instancias de contenedor de Azure y orchestrators de contenedor](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="b4228-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>

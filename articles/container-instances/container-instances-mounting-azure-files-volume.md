---
title: Montaje de un volumen de Azure Files en Azure Container Instances
description: "Obtenga información sobre cómo montar un volumen de Azure Files para conservar el estado con Azure Container Instances"
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
ms.openlocfilehash: 4248a3769ba8a0fb067b3904d55d487fe67e5778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="80c3c-103">Montaje de un recurso compartido de archivos de Azure en Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="80c3c-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="80c3c-104">De forma predeterminada, Azure Container Instances no tiene estado.</span><span class="sxs-lookup"><span data-stu-id="80c3c-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="80c3c-105">Si el contenedor se bloquea o se detiene, se pierde todo su estado.</span><span class="sxs-lookup"><span data-stu-id="80c3c-105">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="80c3c-106">Para conservar el estado más allá de la duración del contenedor, debe montar un volumen desde un almacén externo.</span><span class="sxs-lookup"><span data-stu-id="80c3c-106">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span> <span data-ttu-id="80c3c-107">Este artículo muestra cómo montar un recurso compartido de archivos de Azure para su uso con Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="80c3c-107">This article shows how to mount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="80c3c-108">Creación de un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="80c3c-108">Create an Azure file share</span></span>

<span data-ttu-id="80c3c-109">Antes de utilizar un recurso compartido de archivos de Azure en Azure Container Instances, debe crearlo.</span><span class="sxs-lookup"><span data-stu-id="80c3c-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="80c3c-110">Ejecute el script siguiente para crear una cuenta de almacenamiento para hospedar el recurso compartido de archivos y el propio recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="80c3c-110">Run the following script to create a storage account to host the file share and the share itself.</span></span> <span data-ttu-id="80c3c-111">Tenga en cuenta que el nombre de la cuenta de almacenamiento debe ser globalmente único, por lo que el script agrega un valor aleatorio en la cadena base.</span><span class="sxs-lookup"><span data-stu-id="80c3c-111">Note that the storage account name must be globally unique, so the script adds a random value to the base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create the storage account with the parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="80c3c-112">Adquisición de detalles de acceso de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="80c3c-112">Acquire storage account access details</span></span>

<span data-ttu-id="80c3c-113">Para montar un recurso compartido de archivos de Azure como un volumen en Azure Container Instances, necesita tres valores: el nombre de la cuenta de almacenamiento, el nombre del recurso compartido y la clave de acceso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="80c3c-113">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage access key.</span></span> 

<span data-ttu-id="80c3c-114">Si ha usado el script anterior, el nombre de la cuenta de almacenamiento se creó con un valor aleatorio al final.</span><span class="sxs-lookup"><span data-stu-id="80c3c-114">If you used the script above, the storage account name was created with a random value at the end.</span></span> <span data-ttu-id="80c3c-115">Para consultar la cadena final (incluida la parte aleatoria), use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="80c3c-115">To query the final string (including the random portion), use the following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="80c3c-116">El nombre del recurso compartido ya se conoce (es *acishare* en el script anterior), por lo que todo lo que queda es la clave de cuenta de almacenamiento, que puede encontrarse con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="80c3c-116">The share name is already known (it is *acishare* in the script above), so all that remains is the storage account key, which can be found using the following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="80c3c-117">Almacenamiento de los detalles de acceso de la cuenta de almacenamiento con un almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="80c3c-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="80c3c-118">Las claves de cuenta de almacenamiento protegen el acceso a los datos, por lo que recomendamos almacenarlas en un almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="80c3c-118">Storage account keys protect access to your data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="80c3c-119">Cree un almacén de claves con la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="80c3c-119">Create a key vault with the Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="80c3c-120">El conmutador `enabled-for-template-deployment` permite a Azure Resource Manager extraer secretos del almacén de claves durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="80c3c-120">The `enabled-for-template-deployment` switch allows Azure Resource Manager to pull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="80c3c-121">Almacene la clave de cuenta de almacenamiento como un secreto nuevo en el almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="80c3c-121">Store the storage account key as a new secret in the key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-the-volume"></a><span data-ttu-id="80c3c-122">Monte el volumen</span><span class="sxs-lookup"><span data-stu-id="80c3c-122">Mount the volume</span></span>

<span data-ttu-id="80c3c-123">El montaje de un recurso compartido de archivos de Azure como un volumen en un contenedor es un proceso que consta de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="80c3c-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="80c3c-124">En primer lugar, proporcione los detalles del recurso compartido como parte de la definición del grupo de contenedores; luego, especifique cómo desea que el volumen se monte dentro de uno o varios de los contenedores del grupo.</span><span class="sxs-lookup"><span data-stu-id="80c3c-124">First, you provide the details of the share as part of defining the container group, then you specify how you want the volume mounted within one or more of the containers in the group.</span></span>

<span data-ttu-id="80c3c-125">Para definir los volúmenes que desea que estén disponibles para el montaje, agregue una matriz `volumes` a la definición del grupo de contenedores en la plantilla de Azure Resource Manager; luego, haga referencia a ellos en la definición de los contenedores individuales.</span><span class="sxs-lookup"><span data-stu-id="80c3c-125">To define the volumes you want to make available for mounting, add a `volumes` array to the container group definition in the Azure Resource Manager template, then reference them in the definition of the individual containers.</span></span>

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

<span data-ttu-id="80c3c-126">La plantilla incluye el nombre y la clave de la cuenta de almacenamiento como parámetros, que se pueden proporcionar en un archivo de parámetros independiente.</span><span class="sxs-lookup"><span data-stu-id="80c3c-126">The template includes the storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="80c3c-127">Para rellenar el archivo de parámetros, necesitará tres valores: el nombre de la cuenta de almacenamiento, el identificador de recursos del almacén de claves de Azure y el nombre de secreto del almacén de claves que utilizó para almacenar la clave de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="80c3c-127">To populate the parameters file, you will need three values: the storage account name, the resource ID of your Azure key vault, and the key vault secret name that you used to store the storage key.</span></span> <span data-ttu-id="80c3c-128">Si ha seguido los pasos anteriores, puede obtener estos valores con el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="80c3c-128">If you have followed previous steps, you can get these values with the following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="80c3c-129">Inserte los valores en el archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="80c3c-129">Insert the values into the parameters file:</span></span>

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

## <a name="deploy-the-container-and-manage-files"></a><span data-ttu-id="80c3c-130">Implementación del contenedor y administración de archivos</span><span class="sxs-lookup"><span data-stu-id="80c3c-130">Deploy the container and manage files</span></span>

<span data-ttu-id="80c3c-131">Con la plantilla definida, puede crear el contenedor y montar el volumen de este mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="80c3c-131">With the template defined, you can create the container and mount its volume using the Azure CLI.</span></span> <span data-ttu-id="80c3c-132">Suponiendo que el archivo de plantilla y el archivo de parámetros se denominan *azuredeploy.json* y *azuredeploy.parameters.json*, respectivamente, la línea de comandos es:</span><span class="sxs-lookup"><span data-stu-id="80c3c-132">Assuming that the template file is named *azuredeploy.json* and that the parameters file is named *azuredeploy.parameters.json*, then the command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="80c3c-133">Una vez que se inicie el contenedor, puede usar la aplicación web simple que se implementó mediante la imagen **seanmckenna/aci-hellofiles** en los archivos de administración en el recurso compartido de archivos de Azure en la ruta de montaje que especificó.</span><span class="sxs-lookup"><span data-stu-id="80c3c-133">Once the container starts up, you can use the simple web app deployed via the **seanmckenna/aci-hellofiles** image, to the manage files in the Azure file share at the mount path that you specified.</span></span> <span data-ttu-id="80c3c-134">Obtenga la dirección IP de la aplicación web mediante lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="80c3c-134">Obtain the ip address for the web app via the following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="80c3c-135">Puede usar una herramienta como el [Explorador de Microsoft Azure Storage](http://storageexplorer.com) para recuperar e inspeccionar el archivo escrito en el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="80c3c-135">You can use a tool like the [Microsoft Azure Storage Explorer](http://storageexplorer.com) to retrieve and inspect the file writen to the file share.</span></span>

>[!NOTE]
> <span data-ttu-id="80c3c-136">Para más información sobre el uso de plantillas de Azure Resource Manager, archivos de parámetros y la implementación con la CLI de Azure, consulte [Implementación de recursos con plantillas de Resource Manager y la CLI de Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="80c3c-136">To learn more about using Azure Resource Manager templates, parameter files, and deploying with the Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80c3c-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80c3c-137">Next steps</span></span>

- <span data-ttu-id="80c3c-138">Implementación para el primer contenedor utilizando el [inicio rápido](container-instances-quickstart.md) de Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="80c3c-138">Deploy for your first container using the Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="80c3c-139">Obtener información sobre la [relación entre Azure Container Instances y orquestadores de contenedor](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="80c3c-139">Learn about the [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>

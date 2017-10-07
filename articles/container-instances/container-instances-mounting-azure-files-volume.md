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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Montaje de un recurso compartido de archivos de Azure en Azure Container Instances

De forma predeterminada, Azure Container Instances no tiene estado. Si el contenedor de Hola se bloquea o se detiene, se pierde todo su estado. toopersist estado más allá de duración de Hola Hola del contenedor de, debe montar un volumen desde un almacén externo. En este artículo se muestra cómo toomount compartir de un archivo de Azure para su uso con instancias de contenedor de Azure.

## <a name="create-an-azure-file-share"></a>Creación de un recurso compartido de archivos de Azure

Antes de utilizar un recurso compartido de archivos de Azure en Azure Container Instances, debe crearlo. Ejecute hello después de la secuencia de comandos toocreate un recurso compartido de archivos de almacenamiento cuenta toohost Hola y Hola compartan propio. Tenga en cuenta que ese nombre de cuenta de almacenamiento de hello debe ser único globalmente, por lo que el script de Hola agrega una cadena en base toohello valor aleatorio.

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

## <a name="acquire-storage-account-access-details"></a>Adquisición de detalles de acceso de la cuenta de almacenamiento

toomount compartir un archivo de Azure como un volumen en instancias de contenedor de Azure, necesita tres valores: Hola nombre de la cuenta de almacenamiento, el nombre del recurso compartido de Hola y clave de acceso de almacenamiento de Hola. 

Si ha usado el script de Hola anterior, nombre de cuenta de almacenamiento de Hola se creó con un valor aleatorio final Hola. tooquery Hola final cadena (incluidos Hola aleatorio parte), utilice hello siguientes comandos:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Hello nombre de recurso compartido ya lo conoce (es *acishare* en script de Hola anterior), por lo que todo lo que queda es la clave de cuenta de almacenamiento de hello, que puede encontrarse con Hola el siguiente comando:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Almacenamiento de los detalles de acceso de la cuenta de almacenamiento con un almacén de claves de Azure

Claves de la cuenta de almacenamiento protegen los datos de tooyour de acceso, por lo que recomendamos almacenarlas en un almacén de claves de Azure. 

Crear un almacén de claves con hello CLI de Azure:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Hola `enabled-for-template-deployment` conmutador permite toopull de administrador de recursos de Azure secretos desde el almacén de claves durante la implementación.

Almacenar la clave de cuenta de almacenamiento de Hola como un secreto nuevo en el almacén de claves de hello:

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Monte el volumen de Hola

El montaje de un recurso compartido de archivos de Azure como un volumen en un contenedor es un proceso que consta de dos pasos. En primer lugar, se proporcionan detalles de Hola de recurso compartido de hello como parte de la definición de grupo del contenedor de hello, a continuación, especificar cómo desea que el volumen de hello montado en uno o varios contenedores de hello en el grupo de Hola.

volúmenes de hello toodefine desea toomake disponible para el montaje, agregue un `volumes` toohello definición de grupo de contenedor de plantilla de Azure Resource Manager Hola de matriz, a continuación, hacer referencia a ellos en la definición de Hola de contenedores individuales Hola.

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

plantilla de Hello incluye nombre de cuenta de almacenamiento de Hola y clave como parámetros, que se pueden proporcionar en un archivo de parámetros separados. archivo de parámetros de hello toopopulate, necesitará tres valores: Hola nombre de la cuenta de almacenamiento, Hola Id. de recurso de su almacén de claves de Azure y Hola nombre secreto del almacén de claves que usa la clave de almacenamiento de hello toostore. Si ha seguido los pasos anteriores, puede obtener estos valores con hello siguiente secuencia de comandos:

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Insertar valores de hello en el archivo de parámetros de hello:

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

## <a name="deploy-hello-container-and-manage-files"></a>Contenedor de Hola de implementar y administrar archivos

Con definida por la plantilla de hello, puede crear el contenedor de Hola y montar el volumen mediante Hola CLI de Azure. Suponiendo que hello archivo de plantilla se denomina *azuredeploy.json* y ese archivo de parámetros de Hola se denomina *azuredeploy.parameters.json*, línea de comandos de hello es:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Una vez que se inicia el contenedor de hello, puede usar la aplicación web simple de hello implementado a través de Hola **seanmckenna/aci-hellofiles** toohello de imagen, administrar archivos en el recurso compartido de archivos de Azure de hello en la ruta de acceso de montaje de Hola que especificó. Obtener dirección ip de hello para la aplicación web de Hola a través de la siguiente hello:

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

Puede usar una herramienta como hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve e inspeccionar el recurso compartido de archivos de hello archivo escritos toohello.

>[!NOTE]
> toolearn más información acerca de utilizar plantillas del Administrador de recursos de Azure, archivos de parámetros e implementar con hello CLI de Azure, consulte [implementar los recursos con plantillas de administrador de recursos y la CLI de Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Pasos siguientes

- Implementar para el primer contenedor mediante instancias de contenedor de Azure de hello [inicio rápido](container-instances-quickstart.md)
- Obtenga información acerca de hello [relación entre las instancias de contenedor de Azure y orchestrators de contenedor](container-instances-orchestrator-relationship.md)

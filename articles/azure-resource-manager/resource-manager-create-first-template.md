---
title: plantilla de Azure Resource Manager primera aaaCreate | Documentos de Microsoft
description: "Una guía paso a paso toocreating la primera plantilla de Azure Resource Manager. Muestra cómo toouse Hola referencia de plantilla para una plantilla de Hola de toocreate de cuenta de almacenamiento."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Creación e implementación de la primera plantilla de Azure Resource Manager
En este tema le guiará por los pasos de Hola de creación de la primera plantilla de Azure Resource Manager. Las plantillas de administrador de recursos son archivos JSON que definen los recursos de hello necesita toodeploy para su solución. conceptos de hello toounderstand asociados con la implementación y administración de sus soluciones de Azure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md). Si dispone de recursos existentes y desea tooget una plantilla para esos recursos, consulte [exportar una plantilla de Azure Resource Manager de los recursos existentes](resource-manager-export-template.md).

plantillas de toocreate y revisar, necesita un editor de JSON. [Visual Studio Code](https://code.visualstudio.com/) es un editor de código ligero, de código abierto y multiplataforma. Se recomienda encarecidamente usar código de Visual Studio para crear plantillas de Resource Manager. En este tema se da por supuesto que se utiliza Visual Studio Code; sin embargo, si tiene otro editor de JSON (por ejemplo, Visual Studio), puede usarlo.

## <a name="prerequisites"></a>Requisitos previos

* Código de Visual Studio. Si es necesario, instálelo desde [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Una suscripción de Azure. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="create-template"></a>Creación de una plantilla

Puede empezar con una plantilla sencilla que implementa una suscripción de tooyour de cuenta de almacenamiento.

1. Seleccione **Archivo** > **Nuevo archivo**. 

   ![Nuevo archivo](./media/resource-manager-create-first-template/new-file.png)

2. Copie y pegue Hola siguiendo la sintaxis de JSON en el archivo:

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   Nombres de cuenta de almacenamiento tienen varias restricciones específicas que resultan difíciles de tooset. nombre de Hello debe tener entre 3 y 24 caracteres de longitud, utilice sólo números y letras en minúsculas y ser únicos. plantilla anterior Hello usa hello [uniqueString](resource-group-template-functions-string.md#uniquestring) función toogenerate un valor hash. toogive este hash valor más lo que significa que, agrega el prefijo de hello *almacenamiento*. 

3. Guarde este archivo como **azuredeploy.json** tooa de carpeta local.

   ![Guardar plantilla](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Implementar plantilla

Se está listo toodeploy esta plantilla. Usar PowerShell o CLI de Azure toocreate un grupo de recursos. A continuación, implemente un grupo de recursos de toothat de cuenta de almacenamiento.

* Para PowerShell, use Hola siguientes comandos de carpeta de Hola que contiene la plantilla de hello:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Para una instalación local de CLI de Azure, use Hola siguientes comandos de carpeta de Hola que contiene la plantilla de hello:

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Cuando finalice la implementación, la cuenta de almacenamiento existe en el grupo de recursos de Hola.

## <a name="deploy-template-from-cloud-shell"></a>Implementación de una plantilla desde Cloud Shell

Puede usar [Shell en la nube](../cloud-shell/overview.md) toorun hello Azure CLI comandos para la implementación de la plantilla. Sin embargo, primero debe cargar la plantilla en el recurso compartido de archivos de hello del shell en la nube. Si no ha usado Cloud Shell, vea [Introducción a Azure Cloud Shell](../cloud-shell/overview.md) para más información sobre su configuración.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).   

2. Seleccione el grupo de recursos de Cloud Shell. patrón de nombre de Hello es `cloud-shell-storage-<region>`.

   ![Selección de un grupo de recursos](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Seleccione la cuenta de almacenamiento de hello del shell en la nube.

   ![Selección de la cuenta de almacenamiento](./media/resource-manager-create-first-template/select-storage.png)

4. Seleccione **Archivos**.

   ![Seleccionar archivos](./media/resource-manager-create-first-template/select-files.png)

5. Seleccione el recurso compartido de archivos de Hola de Shell en la nube. patrón de nombre de Hello es `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Selección de recurso compartido de archivos](./media/resource-manager-create-first-template/select-file-share.png)

6. Seleccione **Agregar directorio**.

   ![Agregar directorio](./media/resource-manager-create-first-template/select-add-directory.png)

7. Asígnele el nombre **plantillas** y seleccione **Correcto**.

   ![Nombre de directorio](./media/resource-manager-create-first-template/name-templates.png)

8. Seleccione el nuevo directorio.

   ![Selección de directorio](./media/resource-manager-create-first-template/select-templates.png)

9. Seleccione **Cargar**.

   ![Selección de carga](./media/resource-manager-create-first-template/select-upload.png)

10. Busque y cargue la plantilla.

   ![Carga de archivo](./media/resource-manager-create-first-template/upload-files.png)

11. Mensaje de Hola abierto.

   ![Apertura de Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Escriba Hola siguientes comandos de hello Shell en la nube:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

Cuando finalice la implementación, la cuenta de almacenamiento existe en el grupo de recursos de Hola.

## <a name="customize-hello-template"></a>Personalizar la plantilla de Hola

plantilla de Hello funciona bien, pero no es flexible. Siempre se implementa un tooSouth de almacenamiento con redundancia local Central US. siempre es el nombre de Hello *almacenamiento* seguido por un valor de hash. tooenable mediante la plantilla de Hola para diferentes escenarios, agregar parámetros toohello plantilla.

Hello en el ejemplo siguiente se muestra hello sección de parámetros con dos parámetros. Hola primer parámetro `storageSKU` le permite el tipo de hello toospecify de redundancia. Limita los valores de hello que puede pasar en toovalues que son válidos para una cuenta de almacenamiento. También especifica un valor predeterminado. Hola segundo parámetro `storageNamePrefix` es conjunto tooallow un máximo de 11 caracteres. Especifica un valor predeterminado.

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

En la sección de variables de hello, agregue una variable denominada `storageName`. Combina el valor de prefijo de Hola de parámetros de Hola y un valor de hash de hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (función). Usa hello [toLower](resource-group-template-functions-string.md#tolower) función tooconvert toolowercase de todos los caracteres.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse estos nuevos valores para la cuenta de almacenamiento, cambie la definición de recurso de hello:

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

Tenga en cuenta que Hola nombre de cuenta de almacenamiento de Hola ahora se establece la variable toohello que agregó. nombre SKU de Hola se establece toohello valor de parámetro hello. se establece la ubicación de Hola Hola la misma ubicación que el grupo de recursos de Hola.

Guarde el archivo. 

Después de completar los pasos de hello en este artículo, la plantilla ahora el siguiente aspecto:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>Volver a implementar la plantilla

Volver a implementar la plantilla de hello con valores diferentes.

Para PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Para la CLI de Azure, utilice:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Para hello Shell en la nube, cargue el recurso compartido de archivos de plantilla se ha cambiado toohello. Sobrescribir el archivo existente de Hola. A continuación, utilice el siguiente comando de hello:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando ya no necesite, limpiar los recursos de hello implementadas mediante la eliminación de grupo de recursos de Hola.

Para PowerShell, use:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Para la CLI de Azure, utilice:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de la estructura de Hola de una plantilla, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).
* toolearn acerca de las propiedades de Hola para una cuenta de almacenamiento, consulte [referencia de plantillas de cuentas de almacenamiento](/azure/templates/microsoft.storage/storageaccounts).
* tooview completa plantillas para muchos tipos distintos de soluciones, vea hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).

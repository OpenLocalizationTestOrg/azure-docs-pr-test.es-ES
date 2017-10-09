---
title: recursos de aaaDeploy con CLI de Azure y plantilla | Documentos de Microsoft
description: Use el Administrador de recursos de Azure y Azure CLI toodeploy un tooAzure de recursos. recursos de Hola se definen en una plantilla de administrador de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Implementación de recursos con plantillas de Resource Manager y la CLI de Azure

Este tema se explica cómo toouse 2.0 de CLI de Azure con el Administrador de recursos plantillas toodeploy su tooAzure de recursos. Si no está familiarizado con conceptos de Hola de implementar y administrar sus soluciones de Azure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).  

plantilla de administrador de recursos de Hello que implementar puede ser un archivo local en su equipo, o un archivo externo que se encuentra en un repositorio como GitHub. plantilla de Hola se implementan en este artículo está disponible en hello [plantilla de ejemplo](#sample-template) sección, o como un [plantilla de la cuenta de almacenamiento en GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Si no tiene instalado de CLI de Azure, puede usar hello [Shell en la nube](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Implementar una plantilla local

Al implementar tooAzure de recursos,:

1. Inicie sesión en tooyour cuenta de Azure
2. Crear un grupo de recursos que actúa como contenedor de Hola de recursos de hello implementado. nombre de Hola Hola del grupo de recursos solo puede incluir caracteres alfanuméricos, puntos, caracteres de subrayado, guiones y paréntesis. Puede ser una too90 caracteres. No puede terminar en punto.
3. Implementar la plantilla de Hola de grupo de recursos de toohello que define Hola recursos toocreate

Una plantilla puede incluir parámetros que permiten la implementación de hello toocustomize. Por ejemplo, puede proporcionar valores que están diseñados para un entorno concreto (como desarrollo, prueba y producción). plantilla de ejemplo de Hola define un parámetro para la cuenta de almacenamiento de hello SKU. 

Hola de ejemplo siguiente crea un grupo de recursos e implementa una plantilla desde el equipo local:

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

implementación de Hello puede tardar unos toocomplete minutos. Cuando termine, verá un mensaje que incluye el resultado de hello:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Implementar una plantilla externa

En lugar de almacenar las plantillas de administrador de recursos en el equipo local, es posible que prefiera toostore ellas en una ubicación externa. Puede almacenar plantillas en un repositorio de control de código fuente (por ejemplo, GitHub). O bien, puede almacenarlas en una cuenta de Azure Storage para el acceso compartido en su organización.

toodeploy una plantilla externa, use hello **plantilla uri** parámetro. Usar hello URI en la plantilla de ejemplo de Hola ejemplo toodeploy Hola desde GitHub.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

Hello en el ejemplo anterior se requiere un URI accesible públicamente para plantilla de hello, que funciona con la mayoría de los escenarios, porque la plantilla no debe incluir datos confidenciales. Si necesita toospecify datos confidenciales (por ejemplo, una contraseña de administrador), pase ese valor como un parámetro seguro. Sin embargo, si no desea que la plantilla toobe accesible públicamente, puede proteger mediante el almacenamiento en un contenedor de almacenamiento privado. Para más información sobre la implementación de una plantilla que requiere un token de Firma de acceso compartido (SAS), consulte [Implementación de una plantilla privada con el token de SAS](resource-manager-cli-sas-token.md).

## <a name="deploy-template-from-cloud-shell"></a>Implementación de una plantilla desde Cloud Shell

Puede usar [Shell en la nube](../cloud-shell/overview.md) toorun hello Azure CLI comandos para la implementación de la plantilla. Sin embargo, primero debe cargar la plantilla en el recurso compartido de archivos de hello del shell en la nube. Si no ha usado Cloud Shell, vea [Introducción a Azure Cloud Shell](../cloud-shell/overview.md) para más información sobre su configuración.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).   

2. Seleccione el grupo de recursos de Cloud Shell. patrón de nombre de Hello es `cloud-shell-storage-<region>`.

   ![Selección de un grupo de recursos](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. Seleccione la cuenta de almacenamiento de hello del shell en la nube.

   ![Selección de la cuenta de almacenamiento](./media/resource-group-template-deploy-cli/select-storage.png)

4. Seleccione **Archivos**.

   ![Seleccionar archivos](./media/resource-group-template-deploy-cli/select-files.png)

5. Seleccione el recurso compartido de archivos de Hola de Shell en la nube. patrón de nombre de Hello es `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Selección de recurso compartido de archivos](./media/resource-group-template-deploy-cli/select-file-share.png)

6. Seleccione **Agregar directorio**.

   ![Agregar directorio](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. Asígnele el nombre **plantillas** y seleccione **Correcto**.

   ![Nombre de directorio](./media/resource-group-template-deploy-cli/name-templates.png)

8. Seleccione el nuevo directorio.

   ![Selección de directorio](./media/resource-group-template-deploy-cli/select-templates.png)

9. Seleccione **Cargar**.

   ![Selección de carga](./media/resource-group-template-deploy-cli/select-upload.png)

10. Busque y cargue la plantilla.

   ![Carga de archivo](./media/resource-group-template-deploy-cli/upload-files.png)

11. Mensaje de Hola abierto.

   ![Apertura de Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Escriba Hola siguientes comandos de hello Shell en la nube:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a>Archivos de parámetros

En lugar de pasar parámetros como valores en línea en la secuencia de comandos, quizá le resulte más fácil toouse un archivo JSON que contiene los valores de parámetro de Hola. archivo de parámetros de Hello debe Hola siguiendo el formato:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Tenga en cuenta que la sección de parámetros de hello incluye un nombre de parámetro que coincida con el parámetro hello definido en la plantilla (storageAccountType). archivo de parámetros de Hello contiene un valor para el parámetro hello. Este valor se pasa automáticamente toohello plantilla durante la implementación. Puede crear varios archivos de parámetros para diferentes escenarios de implementación y, a continuación, pase Hola parámetro apropiado archivo. 

Copie el anterior ejemplo de Hola y guárdelo como un archivo denominado `storage.parameters.json`.

toopass un archivo de parámetros local, use `@` toospecify un archivo local denominado storage.parameters.json.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>Prueba de una implementación de plantilla

tootest los valores de parámetro y de plantilla sin implementar realmente los recursos, utilice [validar la implementación del grupo az](/cli/azure/group/deployment#validate). 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

Si no se detectan errores, el comando de hello devuelve información acerca de la implementación de prueba de Hola. En concreto, tenga en cuenta que hello **error** valor es null.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Si se detecta un error, el comando de hello devuelve un mensaje de error. Por ejemplo, al intentar toopass un valor incorrecto para la cuenta de almacenamiento de hello SKU, se devuelve Hola siguiente error:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Si la plantilla tiene un error de sintaxis, comando hello devuelve un error que indica que no pudo analizar plantilla Hola. mensajes de bienvenida indica el número de línea de Hola y posición del error de análisis de Hola.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

modo de toouse completa, use hello `mode` parámetro:

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a>Plantilla de ejemplo

Hello siguiente plantilla se usa para obtener ejemplos de hello en este tema. Cópiela y guárdela como un archivo denominado storage.json. toounderstand cómo toocreate esta plantilla, consulte [crear la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>Pasos siguientes
* ejemplos de Hello en este artículo implementación grupo de recursos de tooa de recursos en su suscripción de manera predeterminada. toouse otra suscripción, vea [administrar varias suscripciones de Azure](/cli/azure/manage-azure-subscriptions-azure-cli).
* Para obtener un script de ejemplo completo que implementa una plantilla, vea [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md) (Script de implementación de plantilla de Resource Manager).
* toounderstand toodefine parámetros de la plantilla, vea [comprender la estructura de Hola y la sintaxis de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).
* Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-cli-sas-token.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

---
title: aaaDeploy recursos con PowerShell y plantilla | Documentos de Microsoft
description: Use el Administrador de recursos de Azure y Azure PowerShell toodeploy un tooAzure de recursos. recursos de Hola se definen en una plantilla de administrador de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell

Este tema se explica cómo toouse PowerShell de Azure con el Administrador de recursos plantillas toodeploy su tooAzure de recursos. Si no está familiarizado con conceptos de Hola de implementar y administrar sus soluciones de Azure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).

plantilla de administrador de recursos de Hello que implementar puede ser un archivo local en su equipo, o un archivo externo que se encuentra en un repositorio como GitHub. plantilla de Hola se implementan en este artículo está disponible en hello [plantilla de ejemplo](#sample-template) sección, o como [plantilla de la cuenta de almacenamiento en GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Implementación de una plantilla desde la máquina local

Al implementar tooAzure de recursos,:

1. Inicie sesión en tooyour cuenta de Azure
2. Crear un grupo de recursos que actúa como contenedor de Hola de recursos de hello implementado. nombre de Hola Hola del grupo de recursos solo puede incluir caracteres alfanuméricos, puntos, caracteres de subrayado, guiones y paréntesis. Puede ser una too90 caracteres. No puede terminar en punto.
3. Implementar la plantilla de Hola de grupo de recursos de toohello que define Hola recursos toocreate

Una plantilla puede incluir parámetros que permiten la implementación de hello toocustomize. Por ejemplo, puede proporcionar valores que están diseñados para un entorno concreto (como desarrollo, prueba y producción). plantilla de ejemplo de Hola define un parámetro para la cuenta de almacenamiento de hello SKU.

Hola de ejemplo siguiente crea un grupo de recursos e implementa una plantilla desde el equipo local:

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

implementación de Hello puede tardar unos toocomplete minutos. Cuando termine, verá un mensaje que incluye el resultado de hello:

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Implementación de una plantilla desde un origen externo

En lugar de almacenar las plantillas de administrador de recursos en el equipo local, es posible que prefiera toostore ellas en una ubicación externa. Puede almacenar plantillas en un repositorio de control de código fuente (por ejemplo, GitHub). O bien, puede almacenarlas en una cuenta de Azure Storage para el acceso compartido en su organización.

toodeploy una plantilla externa, use hello **TemplateUri** parámetro. Usar hello URI en la plantilla de ejemplo de Hola ejemplo toodeploy Hola desde GitHub.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Hello en el ejemplo anterior se requiere un URI accesible públicamente para plantilla de hello, que funciona con la mayoría de los escenarios, porque la plantilla no debe incluir datos confidenciales. Si necesita toospecify datos confidenciales (por ejemplo, una contraseña de administrador), pase ese valor como un parámetro seguro. Sin embargo, si no desea que la plantilla toobe accesible públicamente, puede proteger mediante el almacenamiento en un contenedor de almacenamiento privado. Para más información sobre la implementación de una plantilla que requiere un token de Firma de acceso compartido (SAS), consulte [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).

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

toopass un archivo de parámetros local, usar hello **TemplateParameterFile** parámetro:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass un archivo de parámetros externo, use hello **TemplateParameterUri** parámetro:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

Puede usar parámetros en línea y un parámetro local en el archivo hello misma operación de implementación. Por ejemplo, puede especificar algunos valores en el archivo de parámetro local hello y agregar otros valores en línea durante la implementación. Si proporciona valores para un parámetro en el archivo de hello parámetro local y en línea, valor de hello en línea tiene prioridad.

Sin embargo, cuando se utiliza un archivo de parámetros externo, no se pueden pasar otros valores ya sea en línea o desde un archivo local. Cuando se especifica un archivo de parámetros en hello **TemplateParameterUri** parámetro, conjuntamente todos los parámetros se omiten. Proporcione todos los valores de parámetro de archivo externo de Hola. Si la plantilla incluye un valor confidencial que no se incluyen en el archivo de parámetros de hello, agregue ese almacén de claves de valor tooa o proporcionar todos los valores de parámetro en línea de forma dinámica.

Si la plantilla incluye un parámetro con el mismo nombre como uno de los parámetros de Hola Hola comando de PowerShell de hello, PowerShell presenta parámetro hello desde la plantilla con el sufijo de hello **FromTemplate**. Por ejemplo, un parámetro denominado **ResourceGroupName** en sus conflictos de plantillas con hello **ResourceGroupName** parámetro Hola [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet. Son tooprovide solicitada un valor para **ResourceGroupNameFromTemplate**. En general, debe evitar esta confusión por no nombrar parámetros con el mismo nombre como parámetros que se utilizan para las operaciones de implementación de Hola.

## <a name="test-a-template-deployment"></a>Prueba de una implementación de plantilla

tootest los valores de parámetro y de plantilla sin implementar realmente los recursos, utilice [AzureRmResourceGroupDeployment prueba](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Si no se detectan errores, finaliza el comando de hello sin una respuesta. Si se detecta un error, el comando de hello devuelve un mensaje de error. Por ejemplo, al intentar toopass un valor incorrecto para la cuenta de almacenamiento de hello SKU, se devuelve Hola siguiente error:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Si la plantilla tiene un error de sintaxis, comando hello devuelve un error que indica que no pudo analizar plantilla Hola. mensajes de bienvenida indica el número de línea de Hola y posición del error de análisis de Hola.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

modo de toouse completa, use hello `Mode` parámetro:

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
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
* ejemplos de Hello en este artículo implementación grupo de recursos de tooa de recursos en su suscripción de manera predeterminada. toouse otra suscripción, vea [administrar varias suscripciones de Azure](/powershell/azure/manage-subscriptions-azureps).
* Para obtener un script de ejemplo completo que implementa una plantilla, vea [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md) (Script de implementación de plantilla de Resource Manager).
* toounderstand toodefine parámetros de la plantilla, vea [comprender la estructura de Hola y la sintaxis de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).
* Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).


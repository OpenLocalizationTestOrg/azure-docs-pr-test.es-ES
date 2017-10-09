---
title: "plantillas de aaaLink para la implementación de Azure | Documentos de Microsoft"
description: "Describe cómo toouse vinculadas a plantillas en un toocreate de plantilla de Azure Resource Manager una solución de plantilla modular. Muestra cómo especificar un archivo de parámetros toopass los valores de parámetros y crea dinámicamente las direcciones URL."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Uso de plantillas vinculadas al implementar recursos de Azure
Desde dentro de una plantilla de Azure Resource Manager, puede vincular plantilla tooanother, lo que permite toodecompose la implementación en un conjunto de plantillas de destino, propósito específico. Como ocurre con la descomposición de una aplicación en varias clases de código, la descomposición proporciona ventajas en cuanto a las pruebas, la reutilización y la legibilidad.  

Puede pasar parámetros de plantilla vinculada tooa principal de plantillas, y esos parámetros pueden asignar directamente tooparameters o variables expuestas por hello llamando a la plantilla. plantilla vinculada Hello también puede pasar una plantilla de origen de la variable toohello back-de salida, lo que permite un intercambio de datos bidireccional entre las plantillas de.

## <a name="linking-tooa-template"></a>Vinculación de tooa de plantilla
Crear un vínculo entre dos plantillas mediante la adición de un recurso de implementación dentro de la plantilla principal Hola esa plantilla vinculada toohello de puntos. Establecer hello **templateLink** toohello propiedad URI de plantilla vinculada Hola. Puede proporcionar valores de parámetro de plantilla vinculada Hola directamente en la plantilla o en un archivo de parámetros. Hello en el ejemplo siguiente se usa hello **parámetros** propiedad toospecify directamente un valor de parámetro.

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

Al igual que otros tipos de recursos, puede establecer dependencias entre plantilla vinculada hello y otros recursos. Por lo tanto, cuando los otros recursos requieren un valor de salida de plantilla vinculada hello, puede asegurarse de que se implementa la plantilla vinculada Hola antes de ellos. O bien, cuando la plantilla vinculada Hola se basa en otros recursos, puede asegurarse de que otros recursos se implementan antes de plantilla vinculada Hola. Puede recuperar un valor de una plantilla vinculada con la sintaxis de hello:

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Hola servicio Administrador de recursos debe ser plantilla vinculada de tooaccess capaz de Hola. No se puede especificar un archivo local o un archivo que solo está disponible en la red local para la plantilla vinculada Hola. Solo se puede proporcionar un valor de URI que incluya **http** o **https**. Una opción es tooplace la plantilla vinculada en una cuenta de almacenamiento y usar Hola URI para ese elemento, como se muestra en el siguiente ejemplo de Hola:

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Aunque la plantilla vinculada Hola debe estar disponible externamente, no es necesario toobe toohello disponible con carácter general público. Puede agregar su cuenta de almacenamiento privado de tooa de plantilla que es propietario de la cuenta de almacenamiento de tooonly accesible Hola. A continuación, cree un acceso tooenable token de firma (SAS) de acceso compartido durante la implementación. Agregue ese toohello token de SAS URI para la plantilla vinculada Hola. Para obtener información sobre cómo configurar una plantilla en una cuenta de almacenamiento y generar un token de SAS, consulte [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Implementación de recursos con plantillas de Resource Manager y Azure PowerShell) o [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md) (Implementación de recursos con plantillas de Azure Manager y la CLI de Azure). 

Hola de ejemplo siguiente muestra una plantilla de primario esa plantilla tooanother de vínculos. plantilla vinculada Hola se tiene acceso con un token SAS que se pasa como un parámetro.

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

Aunque el símbolo (token) de Hola se pasa como una cadena segura, hello URI de plantilla vinculada hello, incluido el token de SAS de hello, se registra en las operaciones de implementación de Hola. exposición de toolimit, establecer una expiración de token de Hola.

Resource Manager controla cada plantilla vinculada como una implementación independiente. En el historial de implementación de hello para el grupo de recursos de hello, vea implementaciones independientes para primario hello y las plantillas anidadas.

![Historial de implementación](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Archivo de parámetros de vinculación tooa
Hola siguiente ejemplo usa hello **parametersLink** archivo de parámetros de propiedad toolink tooa.

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

Hola URI valor para el archivo de parámetros vinculados de hello no puede ser un archivo local y debe incluir **http** o **https**. archivo de parámetros de Hello también puede ser limitada tooaccess a través de un token de SAS.

## <a name="using-variables-toolink-templates"></a>Uso de plantillas de toolink de variables
en los ejemplos anteriores Hola mostraron valores de dirección URL codificada de forma rígida para los vínculos de la plantilla de Hola. Este enfoque puede funcionar en una plantilla sencilla pero no funciona bien cuando se trabaja con un gran conjunto de plantillas modulares. En su lugar, puede crear una variable estática que almacena una dirección URL base para la plantilla principal de hello y, a continuación, crear dinámicamente las direcciones URL para las plantillas de hello vinculado desde esa dirección URL base. ventaja de Hola de este enfoque es que le resultará muy fácil mover o bifurcar plantilla Hola porque solo se debe variable estática de hello toochange en la plantilla principal Hola. plantilla principal Hola pasa Hola correcto de que URI a lo largo de hello descomponen la plantilla.

Hello en el ejemplo siguiente se muestra cómo toouse una toocreate de dirección URL base dos direcciones URL para vinculan plantillas (**sharedTemplateUrl** y **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

También puede usar [deployment()](resource-group-template-functions-deployment.md#deployment) tooget Hola dirección URL base para la plantilla actual hello y utilizar esa dirección URL Hola de tooget para otras plantillas de hello misma ubicación. Este enfoque resulta útil si cambia la ubicación de la plantilla (quizás due tooversioning) o quiere que tooavoid disco duro de codificación de direcciones URL en el archivo de plantilla de hello. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Ejemplo completo
Hola siguiendo las plantillas de ejemplo muestra una organización simplificada de plantillas vinculadas tooillustrate algunos de los conceptos de hello en este artículo. Se supone que se agregaron plantillas hello toohello mismo contenedor en una cuenta de almacenamiento con acceso público se ha desactivado. plantilla vinculada Hola pasa una plantilla de valores de toohello atrás principal de hello **genera** sección.

Hola **parent.json** archivo consta de:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

Hola **helloworld.json** archivo consta de:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

En PowerShell, obtener un token para el contenedor de Hola e implementar plantillas Hola con:

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

En Azure CLI 2.0, obtener un token para el contenedor de Hola e implementar plantillas Hola con hello siguiente código:

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a>Pasos siguientes
* toolearn sobre Hola definir el orden de implementación de Hola para sus recursos, consulte [definir las dependencias en las plantillas de Azure Resource Manager](resource-group-define-dependencies.md)
* toolearn cómo toodefine un recurso pero crean muchas instancias del mismo, consulte [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md)


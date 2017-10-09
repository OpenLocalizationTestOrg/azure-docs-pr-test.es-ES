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
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="1cdc4-104">Uso de plantillas vinculadas al implementar recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="1cdc4-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="1cdc4-105">Desde dentro de una plantilla de Azure Resource Manager, puede vincular plantilla tooanother, lo que permite toodecompose la implementación en un conjunto de plantillas de destino, propósito específico.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="1cdc4-106">Como ocurre con la descomposición de una aplicación en varias clases de código, la descomposición proporciona ventajas en cuanto a las pruebas, la reutilización y la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="1cdc4-107">Puede pasar parámetros de plantilla vinculada tooa principal de plantillas, y esos parámetros pueden asignar directamente tooparameters o variables expuestas por hello llamando a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="1cdc4-108">plantilla vinculada Hello también puede pasar una plantilla de origen de la variable toohello back-de salida, lo que permite un intercambio de datos bidireccional entre las plantillas de.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="1cdc4-109">Vinculación de tooa de plantilla</span><span class="sxs-lookup"><span data-stu-id="1cdc4-109">Linking tooa template</span></span>
<span data-ttu-id="1cdc4-110">Crear un vínculo entre dos plantillas mediante la adición de un recurso de implementación dentro de la plantilla principal Hola esa plantilla vinculada toohello de puntos.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="1cdc4-111">Establecer hello **templateLink** toohello propiedad URI de plantilla vinculada Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="1cdc4-112">Puede proporcionar valores de parámetro de plantilla vinculada Hola directamente en la plantilla o en un archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="1cdc4-113">Hello en el ejemplo siguiente se usa hello **parámetros** propiedad toospecify directamente un valor de parámetro.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

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

<span data-ttu-id="1cdc4-114">Al igual que otros tipos de recursos, puede establecer dependencias entre plantilla vinculada hello y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="1cdc4-115">Por lo tanto, cuando los otros recursos requieren un valor de salida de plantilla vinculada hello, puede asegurarse de que se implementa la plantilla vinculada Hola antes de ellos.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="1cdc4-116">O bien, cuando la plantilla vinculada Hola se basa en otros recursos, puede asegurarse de que otros recursos se implementan antes de plantilla vinculada Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="1cdc4-117">Puede recuperar un valor de una plantilla vinculada con la sintaxis de hello:</span><span class="sxs-lookup"><span data-stu-id="1cdc4-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="1cdc4-118">Hola servicio Administrador de recursos debe ser plantilla vinculada de tooaccess capaz de Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="1cdc4-119">No se puede especificar un archivo local o un archivo que solo está disponible en la red local para la plantilla vinculada Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="1cdc4-120">Solo se puede proporcionar un valor de URI que incluya **http** o **https**.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="1cdc4-121">Una opción es tooplace la plantilla vinculada en una cuenta de almacenamiento y usar Hola URI para ese elemento, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="1cdc4-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="1cdc4-122">Aunque la plantilla vinculada Hola debe estar disponible externamente, no es necesario toobe toohello disponible con carácter general público.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="1cdc4-123">Puede agregar su cuenta de almacenamiento privado de tooa de plantilla que es propietario de la cuenta de almacenamiento de tooonly accesible Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="1cdc4-124">A continuación, cree un acceso tooenable token de firma (SAS) de acceso compartido durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="1cdc4-125">Agregue ese toohello token de SAS URI para la plantilla vinculada Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="1cdc4-126">Para obtener información sobre cómo configurar una plantilla en una cuenta de almacenamiento y generar un token de SAS, consulte [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Implementación de recursos con plantillas de Resource Manager y Azure PowerShell) o [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md) (Implementación de recursos con plantillas de Azure Manager y la CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="1cdc4-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="1cdc4-127">Hola de ejemplo siguiente muestra una plantilla de primario esa plantilla tooanother de vínculos.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="1cdc4-128">plantilla vinculada Hola se tiene acceso con un token SAS que se pasa como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="1cdc4-129">Aunque el símbolo (token) de Hola se pasa como una cadena segura, hello URI de plantilla vinculada hello, incluido el token de SAS de hello, se registra en las operaciones de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="1cdc4-130">exposición de toolimit, establecer una expiración de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="1cdc4-131">Resource Manager controla cada plantilla vinculada como una implementación independiente.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="1cdc4-132">En el historial de implementación de hello para el grupo de recursos de hello, vea implementaciones independientes para primario hello y las plantillas anidadas.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![Historial de implementación](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="1cdc4-134">Archivo de parámetros de vinculación tooa</span><span class="sxs-lookup"><span data-stu-id="1cdc4-134">Linking tooa parameter file</span></span>
<span data-ttu-id="1cdc4-135">Hola siguiente ejemplo usa hello **parametersLink** archivo de parámetros de propiedad toolink tooa.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

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

<span data-ttu-id="1cdc4-136">Hola URI valor para el archivo de parámetros vinculados de hello no puede ser un archivo local y debe incluir **http** o **https**.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="1cdc4-137">archivo de parámetros de Hello también puede ser limitada tooaccess a través de un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="1cdc4-138">Uso de plantillas de toolink de variables</span><span class="sxs-lookup"><span data-stu-id="1cdc4-138">Using variables toolink templates</span></span>
<span data-ttu-id="1cdc4-139">en los ejemplos anteriores Hola mostraron valores de dirección URL codificada de forma rígida para los vínculos de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="1cdc4-140">Este enfoque puede funcionar en una plantilla sencilla pero no funciona bien cuando se trabaja con un gran conjunto de plantillas modulares.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="1cdc4-141">En su lugar, puede crear una variable estática que almacena una dirección URL base para la plantilla principal de hello y, a continuación, crear dinámicamente las direcciones URL para las plantillas de hello vinculado desde esa dirección URL base.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="1cdc4-142">ventaja de Hola de este enfoque es que le resultará muy fácil mover o bifurcar plantilla Hola porque solo se debe variable estática de hello toochange en la plantilla principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="1cdc4-143">plantilla principal Hola pasa Hola correcto de que URI a lo largo de hello descomponen la plantilla.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="1cdc4-144">Hello en el ejemplo siguiente se muestra cómo toouse una toocreate de dirección URL base dos direcciones URL para vinculan plantillas (**sharedTemplateUrl** y **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="1cdc4-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="1cdc4-145">También puede usar [deployment()](resource-group-template-functions-deployment.md#deployment) tooget Hola dirección URL base para la plantilla actual hello y utilizar esa dirección URL Hola de tooget para otras plantillas de hello misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="1cdc4-146">Este enfoque resulta útil si cambia la ubicación de la plantilla (quizás due tooversioning) o quiere que tooavoid disco duro de codificación de direcciones URL en el archivo de plantilla de hello.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="1cdc4-147">Ejemplo completo</span><span class="sxs-lookup"><span data-stu-id="1cdc4-147">Complete example</span></span>
<span data-ttu-id="1cdc4-148">Hola siguiendo las plantillas de ejemplo muestra una organización simplificada de plantillas vinculadas tooillustrate algunos de los conceptos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="1cdc4-149">Se supone que se agregaron plantillas hello toohello mismo contenedor en una cuenta de almacenamiento con acceso público se ha desactivado.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="1cdc4-150">plantilla vinculada Hola pasa una plantilla de valores de toohello atrás principal de hello **genera** sección.</span><span class="sxs-lookup"><span data-stu-id="1cdc4-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="1cdc4-151">Hola **parent.json** archivo consta de:</span><span class="sxs-lookup"><span data-stu-id="1cdc4-151">hello **parent.json** file consists of:</span></span>

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

<span data-ttu-id="1cdc4-152">Hola **helloworld.json** archivo consta de:</span><span class="sxs-lookup"><span data-stu-id="1cdc4-152">hello **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="1cdc4-153">En PowerShell, obtener un token para el contenedor de Hola e implementar plantillas Hola con:</span><span class="sxs-lookup"><span data-stu-id="1cdc4-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="1cdc4-154">En Azure CLI 2.0, obtener un token para el contenedor de Hola e implementar plantillas Hola con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="1cdc4-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1cdc4-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1cdc4-155">Next steps</span></span>
* <span data-ttu-id="1cdc4-156">toolearn sobre Hola definir el orden de implementación de Hola para sus recursos, consulte [definir las dependencias en las plantillas de Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="1cdc4-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="1cdc4-157">toolearn cómo toodefine un recurso pero crean muchas instancias del mismo, consulte [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="1cdc4-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>


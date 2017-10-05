---
title: "Plantillas vinculadas para la implementación de Azure | Microsoft Docs"
description: "Describe cómo usar plantillas vinculadas en una plantilla del Administrador de recursos de Azure para crear una solución de plantilla modular. Muestra cómo pasar valores de parámetros y especificar un archivo de parámetros y las direcciones URL creadas dinámicamente."
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
ms.openlocfilehash: 8b58a83ffd473500dd3f76c09e251f9208527d4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="09ddc-104">Uso de plantillas vinculadas al implementar recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="09ddc-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="09ddc-105">Desde dentro de una plantilla de Azure Resource Manager, puede realizar la vinculación con otra plantilla que le permita descomponer la implementación en un conjunto de plantillas con fines específicos y dirigidas.</span><span class="sxs-lookup"><span data-stu-id="09ddc-105">From within one Azure Resource Manager template, you can link to another template, which enables you to decompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="09ddc-106">Como ocurre con la descomposición de una aplicación en varias clases de código, la descomposición proporciona ventajas en cuanto a las pruebas, la reutilización y la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="09ddc-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="09ddc-107">Puede pasar parámetros de una plantilla principal a una plantilla vinculada de nuevo, y esos parámetros pueden asignarse directamente a parámetros o variables expuestas por la plantilla de llamada.</span><span class="sxs-lookup"><span data-stu-id="09ddc-107">You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template.</span></span> <span data-ttu-id="09ddc-108">La plantilla vinculada también puede pasar una variable de salida de nuevo a la plantilla de origen, lo que permite un intercambio de datos bidireccional entre las plantillas.</span><span class="sxs-lookup"><span data-stu-id="09ddc-108">The linked template can also pass an output variable back to the source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-to-a-template"></a><span data-ttu-id="09ddc-109">Vinculación con una plantilla</span><span class="sxs-lookup"><span data-stu-id="09ddc-109">Linking to a template</span></span>
<span data-ttu-id="09ddc-110">Cree un vínculo entre dos plantillas mediante la adición de un recurso de implementación dentro de la plantilla principal que apunta a la plantilla vinculada.</span><span class="sxs-lookup"><span data-stu-id="09ddc-110">You create a link between two templates by adding a deployment resource within the main template that points to the linked template.</span></span> <span data-ttu-id="09ddc-111">Para ello, debe establecer la propiedad **templateLink** en el URI de la plantilla vinculada.</span><span class="sxs-lookup"><span data-stu-id="09ddc-111">You set the **templateLink** property to the URI of the linked template.</span></span> <span data-ttu-id="09ddc-112">Los valores de los parámetros de la plantilla se pueden proporcionar directamente en la plantilla o en archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="09ddc-112">You can provide parameter values for the linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="09ddc-113">El siguiente ejemplo usa la propiedad **parameters** para especificar un valor de parámetro directamente.</span><span class="sxs-lookup"><span data-stu-id="09ddc-113">The following example uses the **parameters** property to specify a parameter value directly.</span></span>

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

<span data-ttu-id="09ddc-114">Al igual que otros tipos de recursos, puede establecer dependencias entre la plantilla vinculada y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="09ddc-114">Like other resource types, you can set dependencies between the linked template and other resources.</span></span> <span data-ttu-id="09ddc-115">Por lo tanto, cuando los otros recursos requieren un valor de salida de la plantilla vinculada, puede asegurarse de que la plantilla vinculada se implementa antes que ellos.</span><span class="sxs-lookup"><span data-stu-id="09ddc-115">Therefore, when other resources require an output value from the linked template, you can make sure the linked template is deployed before them.</span></span> <span data-ttu-id="09ddc-116">O bien, cuando la plantilla vinculada se basa en otros recursos, puede asegurarse de que otros recursos se implementan antes que la plantilla vinculada.</span><span class="sxs-lookup"><span data-stu-id="09ddc-116">Or, when the linked template relies on other resources, you can make sure other resources are deployed before the linked template.</span></span> <span data-ttu-id="09ddc-117">Puede recuperar un valor de una plantilla vinculada con la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="09ddc-117">You can retrieve a value from a linked template with the following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="09ddc-118">El servicio Resource Manager debe tener acceso a la plantilla vinculada.</span><span class="sxs-lookup"><span data-stu-id="09ddc-118">The Resource Manager service must be able to access the linked template.</span></span> <span data-ttu-id="09ddc-119">No se puede especificar un archivo local o un archivo que solo está disponible en la red local para la plantilla vinculada.</span><span class="sxs-lookup"><span data-stu-id="09ddc-119">You cannot specify a local file or a file that is only available on your local network for the linked template.</span></span> <span data-ttu-id="09ddc-120">Solo se puede proporcionar un valor de URI que incluya **http** o **https**.</span><span class="sxs-lookup"><span data-stu-id="09ddc-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="09ddc-121">Una opción es colocar la plantilla vinculada en una cuenta de almacenamiento y usar el URI para dicho elemento, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="09ddc-121">One option is to place your linked template in a storage account, and use the URI for that item, such as shown in the following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="09ddc-122">Aunque la plantilla vinculada debe estar disponible externamente, no es necesario que esté generalmente disponible para el público.</span><span class="sxs-lookup"><span data-stu-id="09ddc-122">Although the linked template must be externally available, it does not need to be generally available to the public.</span></span> <span data-ttu-id="09ddc-123">Puede agregar la plantilla a una cuenta de almacenamiento privada que sea accesible solo al propietario de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09ddc-123">You can add your template to a private storage account that is accessible to only the storage account owner.</span></span> <span data-ttu-id="09ddc-124">Ahora cree un token de Firma de acceso compartido (SAS) para permitir el acceso durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="09ddc-124">Then, you create a shared access signature (SAS) token to enable access during deployment.</span></span> <span data-ttu-id="09ddc-125">Ese token SAS se agrega al identificador URI para la plantilla vinculada.</span><span class="sxs-lookup"><span data-stu-id="09ddc-125">You add that SAS token to the URI for the linked template.</span></span> <span data-ttu-id="09ddc-126">Para obtener información sobre cómo configurar una plantilla en una cuenta de almacenamiento y generar un token de SAS, consulte [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Implementación de recursos con plantillas de Resource Manager y Azure PowerShell) o [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md) (Implementación de recursos con plantillas de Azure Manager y la CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="09ddc-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="09ddc-127">En el ejemplo siguiente se muestra una plantilla principal que se vincula a otra plantilla.</span><span class="sxs-lookup"><span data-stu-id="09ddc-127">The following example shows a parent template that links to another template.</span></span> <span data-ttu-id="09ddc-128">El acceso a la plantilla anidada se obtiene con un token de SAS que se pasa como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="09ddc-128">The linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="09ddc-129">Aunque el token se pasa como una cadena segura, el identificador URI de la plantilla vinculada, incluido el token de SAS, se registra en las operaciones de implementación.</span><span class="sxs-lookup"><span data-stu-id="09ddc-129">Even though the token is passed in as a secure string, the URI of the linked template, including the SAS token, is logged in the deployment operations.</span></span> <span data-ttu-id="09ddc-130">Para limitar la exposición, establezca una caducidad para el token.</span><span class="sxs-lookup"><span data-stu-id="09ddc-130">To limit exposure, set an expiration for the token.</span></span>

<span data-ttu-id="09ddc-131">Resource Manager controla cada plantilla vinculada como una implementación independiente.</span><span class="sxs-lookup"><span data-stu-id="09ddc-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="09ddc-132">En el historial de implementación para el grupo de recursos, vea implementaciones independientes del elemento primario y las plantillas anidadas.</span><span class="sxs-lookup"><span data-stu-id="09ddc-132">In the deployment history for the resource group, you see separate deployments for the parent and nested templates.</span></span>

![Historial de implementación](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-to-a-parameter-file"></a><span data-ttu-id="09ddc-134">Vinculación con un archivo de parámetros</span><span class="sxs-lookup"><span data-stu-id="09ddc-134">Linking to a parameter file</span></span>
<span data-ttu-id="09ddc-135">El siguiente ejemplo utiliza la propiedad **parametersLink** para vincular a un archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="09ddc-135">The next example uses the **parametersLink** property to link to a parameter file.</span></span>

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

<span data-ttu-id="09ddc-136">El valor del URI para el archivo del parámetro vinculado no puede ser un archivo local y debe incluir **http** o **https**.</span><span class="sxs-lookup"><span data-stu-id="09ddc-136">The URI value for the linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="09ddc-137">También se puede limitar el acceso al archivo de parámetros a través de un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="09ddc-137">The parameter file can also be limited to access through a SAS token.</span></span>

## <a name="using-variables-to-link-templates"></a><span data-ttu-id="09ddc-138">Uso de variables para vincular plantillas</span><span class="sxs-lookup"><span data-stu-id="09ddc-138">Using variables to link templates</span></span>
<span data-ttu-id="09ddc-139">Los ejemplos anteriores mostraron valores de dirección URL codificadas de forma rígida para los vínculos de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="09ddc-139">The previous examples showed hard-coded URL values for the template links.</span></span> <span data-ttu-id="09ddc-140">Este enfoque puede funcionar en una plantilla sencilla pero no funciona bien cuando se trabaja con un gran conjunto de plantillas modulares.</span><span class="sxs-lookup"><span data-stu-id="09ddc-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="09ddc-141">En su lugar, puede crear una variable estática que almacene una dirección URL base para la plantilla principal y, luego, crear dinámicamente direcciones URL para las plantillas vinculadas desde esa dirección URL base.</span><span class="sxs-lookup"><span data-stu-id="09ddc-141">Instead, you can create a static variable that stores a base URL for the main template and then dynamically create URLs for the linked templates from that base URL.</span></span> <span data-ttu-id="09ddc-142">La ventaja de este enfoque es que puede mover fácilmente o bifurcar la plantilla porque solo tendrá que cambiar la variable estática en la plantilla principal.</span><span class="sxs-lookup"><span data-stu-id="09ddc-142">The benefit of this approach is you can easily move or fork the template because you only need to change the static variable in the main template.</span></span> <span data-ttu-id="09ddc-143">La plantilla principal pasa los URI correctos por toda la plantilla descompuesta.</span><span class="sxs-lookup"><span data-stu-id="09ddc-143">The main template passes the correct URIs throughout the decomposed template.</span></span>

<span data-ttu-id="09ddc-144">En el ejemplo siguiente se muestra cómo usar una dirección URL base para crear dos direcciones URL para las plantillas vinculadas (**sharedTemplateUrl** y **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="09ddc-144">The following example shows how to use a base URL to create two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="09ddc-145">También puede usar la función [deployment()](resource-group-template-functions-deployment.md#deployment) para obtener la dirección URL base de la plantilla actual y usar esta información para obtener la dirección URL de otras plantillas en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="09ddc-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) to get the base URL for the current template, and use that to get the URL for other templates in the same location.</span></span> <span data-ttu-id="09ddc-146">Este enfoque resulta útil si cambia la ubicación de la plantilla (probablemente debido al control de versiones) o desea evitar la codificación de forma rígida de las direcciones URL en el archivo de plantilla.</span><span class="sxs-lookup"><span data-stu-id="09ddc-146">This approach is useful if your template location changes (maybe due to versioning) or you want to avoid hard coding URLs in the template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="09ddc-147">Ejemplo completo</span><span class="sxs-lookup"><span data-stu-id="09ddc-147">Complete example</span></span>
<span data-ttu-id="09ddc-148">Las plantillas de ejemplo siguientes muestran una organización simplificada de plantillas vinculadas para ilustrar algunos de los conceptos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="09ddc-148">The following example templates show a simplified arrangement of linked templates to illustrate several of the concepts in this article.</span></span> <span data-ttu-id="09ddc-149">Se supone que las plantillas se agregaron en el mismo contenedor en una cuenta de almacenamiento con el acceso público desactivado.</span><span class="sxs-lookup"><span data-stu-id="09ddc-149">It assumes the templates have been added to the same container in a storage account with public access turned off.</span></span> <span data-ttu-id="09ddc-150">La plantilla vinculada pasa un valor de vuelta a la plantilla principal en la sección **salidas** .</span><span class="sxs-lookup"><span data-stu-id="09ddc-150">The linked template passes a value back to the main template in the **outputs** section.</span></span>

<span data-ttu-id="09ddc-151">El archivo **parent.json** consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="09ddc-151">The **parent.json** file consists of:</span></span>

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

<span data-ttu-id="09ddc-152">El archivo **helloworld.json** consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="09ddc-152">The **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="09ddc-153">En PowerShell, se obtiene un token para el contenedor y se implementan las plantillas con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="09ddc-153">In PowerShell, you get a token for the container and deploy the templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="09ddc-154">En la CLI de Azure 2.0, se obtiene un token para el contenedor y se implementan las plantillas con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="09ddc-154">In Azure CLI 2.0, you get a token for the container and deploy the templates with the following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="09ddc-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09ddc-155">Next steps</span></span>
* <span data-ttu-id="09ddc-156">Para obtener información sobre cómo definir el orden de implementación de los recursos, consulte [Definición de dependencias en plantillas de Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="09ddc-156">To learn about the defining the deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="09ddc-157">Para obtener información sobre cómo definir un recurso y crear numerosas instancias de este, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="09ddc-157">To learn how to define one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>


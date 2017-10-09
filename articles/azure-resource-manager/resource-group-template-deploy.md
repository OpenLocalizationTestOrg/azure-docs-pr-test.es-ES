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
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="7dba6-104">Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7dba6-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="7dba6-105">Este tema se explica cómo toouse PowerShell de Azure con el Administrador de recursos plantillas toodeploy su tooAzure de recursos.</span><span class="sxs-lookup"><span data-stu-id="7dba6-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="7dba6-106">Si no está familiarizado con conceptos de Hola de implementar y administrar sus soluciones de Azure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7dba6-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="7dba6-107">plantilla de administrador de recursos de Hello que implementar puede ser un archivo local en su equipo, o un archivo externo que se encuentra en un repositorio como GitHub.</span><span class="sxs-lookup"><span data-stu-id="7dba6-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="7dba6-108">plantilla de Hola se implementan en este artículo está disponible en hello [plantilla de ejemplo](#sample-template) sección, o como [plantilla de la cuenta de almacenamiento en GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7dba6-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="7dba6-109">Implementación de una plantilla desde la máquina local</span><span class="sxs-lookup"><span data-stu-id="7dba6-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="7dba6-110">Al implementar tooAzure de recursos,:</span><span class="sxs-lookup"><span data-stu-id="7dba6-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="7dba6-111">Inicie sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="7dba6-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="7dba6-112">Crear un grupo de recursos que actúa como contenedor de Hola de recursos de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="7dba6-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="7dba6-113">nombre de Hola Hola del grupo de recursos solo puede incluir caracteres alfanuméricos, puntos, caracteres de subrayado, guiones y paréntesis.</span><span class="sxs-lookup"><span data-stu-id="7dba6-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="7dba6-114">Puede ser una too90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7dba6-114">It can be up too90 characters.</span></span> <span data-ttu-id="7dba6-115">No puede terminar en punto.</span><span class="sxs-lookup"><span data-stu-id="7dba6-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="7dba6-116">Implementar la plantilla de Hola de grupo de recursos de toohello que define Hola recursos toocreate</span><span class="sxs-lookup"><span data-stu-id="7dba6-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="7dba6-117">Una plantilla puede incluir parámetros que permiten la implementación de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="7dba6-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="7dba6-118">Por ejemplo, puede proporcionar valores que están diseñados para un entorno concreto (como desarrollo, prueba y producción).</span><span class="sxs-lookup"><span data-stu-id="7dba6-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="7dba6-119">plantilla de ejemplo de Hola define un parámetro para la cuenta de almacenamiento de hello SKU.</span><span class="sxs-lookup"><span data-stu-id="7dba6-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="7dba6-120">Hola de ejemplo siguiente crea un grupo de recursos e implementa una plantilla desde el equipo local:</span><span class="sxs-lookup"><span data-stu-id="7dba6-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="7dba6-121">implementación de Hello puede tardar unos toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="7dba6-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="7dba6-122">Cuando termine, verá un mensaje que incluye el resultado de hello:</span><span class="sxs-lookup"><span data-stu-id="7dba6-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="7dba6-123">Implementación de una plantilla desde un origen externo</span><span class="sxs-lookup"><span data-stu-id="7dba6-123">Deploy a template from an external source</span></span>

<span data-ttu-id="7dba6-124">En lugar de almacenar las plantillas de administrador de recursos en el equipo local, es posible que prefiera toostore ellas en una ubicación externa.</span><span class="sxs-lookup"><span data-stu-id="7dba6-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="7dba6-125">Puede almacenar plantillas en un repositorio de control de código fuente (por ejemplo, GitHub).</span><span class="sxs-lookup"><span data-stu-id="7dba6-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="7dba6-126">O bien, puede almacenarlas en una cuenta de Azure Storage para el acceso compartido en su organización.</span><span class="sxs-lookup"><span data-stu-id="7dba6-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="7dba6-127">toodeploy una plantilla externa, use hello **TemplateUri** parámetro.</span><span class="sxs-lookup"><span data-stu-id="7dba6-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="7dba6-128">Usar hello URI en la plantilla de ejemplo de Hola ejemplo toodeploy Hola desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="7dba6-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="7dba6-129">Hello en el ejemplo anterior se requiere un URI accesible públicamente para plantilla de hello, que funciona con la mayoría de los escenarios, porque la plantilla no debe incluir datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="7dba6-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="7dba6-130">Si necesita toospecify datos confidenciales (por ejemplo, una contraseña de administrador), pase ese valor como un parámetro seguro.</span><span class="sxs-lookup"><span data-stu-id="7dba6-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="7dba6-131">Sin embargo, si no desea que la plantilla toobe accesible públicamente, puede proteger mediante el almacenamiento en un contenedor de almacenamiento privado.</span><span class="sxs-lookup"><span data-stu-id="7dba6-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="7dba6-132">Para más información sobre la implementación de una plantilla que requiere un token de Firma de acceso compartido (SAS), consulte [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="7dba6-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="7dba6-133">Archivos de parámetros</span><span class="sxs-lookup"><span data-stu-id="7dba6-133">Parameter files</span></span>

<span data-ttu-id="7dba6-134">En lugar de pasar parámetros como valores en línea en la secuencia de comandos, quizá le resulte más fácil toouse un archivo JSON que contiene los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dba6-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="7dba6-135">archivo de parámetros de Hello debe Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="7dba6-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="7dba6-136">Tenga en cuenta que la sección de parámetros de hello incluye un nombre de parámetro que coincida con el parámetro hello definido en la plantilla (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="7dba6-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="7dba6-137">archivo de parámetros de Hello contiene un valor para el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="7dba6-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="7dba6-138">Este valor se pasa automáticamente toohello plantilla durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="7dba6-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="7dba6-139">Puede crear varios archivos de parámetros para diferentes escenarios de implementación y, a continuación, pase Hola parámetro apropiado archivo.</span><span class="sxs-lookup"><span data-stu-id="7dba6-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="7dba6-140">Copie el anterior ejemplo de Hola y guárdelo como un archivo denominado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="7dba6-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="7dba6-141">toopass un archivo de parámetros local, usar hello **TemplateParameterFile** parámetro:</span><span class="sxs-lookup"><span data-stu-id="7dba6-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="7dba6-142">toopass un archivo de parámetros externo, use hello **TemplateParameterUri** parámetro:</span><span class="sxs-lookup"><span data-stu-id="7dba6-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="7dba6-143">Puede usar parámetros en línea y un parámetro local en el archivo hello misma operación de implementación.</span><span class="sxs-lookup"><span data-stu-id="7dba6-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="7dba6-144">Por ejemplo, puede especificar algunos valores en el archivo de parámetro local hello y agregar otros valores en línea durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="7dba6-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="7dba6-145">Si proporciona valores para un parámetro en el archivo de hello parámetro local y en línea, valor de hello en línea tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="7dba6-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="7dba6-146">Sin embargo, cuando se utiliza un archivo de parámetros externo, no se pueden pasar otros valores ya sea en línea o desde un archivo local.</span><span class="sxs-lookup"><span data-stu-id="7dba6-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="7dba6-147">Cuando se especifica un archivo de parámetros en hello **TemplateParameterUri** parámetro, conjuntamente todos los parámetros se omiten.</span><span class="sxs-lookup"><span data-stu-id="7dba6-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="7dba6-148">Proporcione todos los valores de parámetro de archivo externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dba6-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="7dba6-149">Si la plantilla incluye un valor confidencial que no se incluyen en el archivo de parámetros de hello, agregue ese almacén de claves de valor tooa o proporcionar todos los valores de parámetro en línea de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="7dba6-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="7dba6-150">Si la plantilla incluye un parámetro con el mismo nombre como uno de los parámetros de Hola Hola comando de PowerShell de hello, PowerShell presenta parámetro hello desde la plantilla con el sufijo de hello **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="7dba6-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="7dba6-151">Por ejemplo, un parámetro denominado **ResourceGroupName** en sus conflictos de plantillas con hello **ResourceGroupName** parámetro Hola [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7dba6-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="7dba6-152">Son tooprovide solicitada un valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="7dba6-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="7dba6-153">En general, debe evitar esta confusión por no nombrar parámetros con el mismo nombre como parámetros que se utilizan para las operaciones de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dba6-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="7dba6-154">Prueba de una implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="7dba6-154">Test a template deployment</span></span>

<span data-ttu-id="7dba6-155">tootest los valores de parámetro y de plantilla sin implementar realmente los recursos, utilice [AzureRmResourceGroupDeployment prueba](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="7dba6-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="7dba6-156">Si no se detectan errores, finaliza el comando de hello sin una respuesta.</span><span class="sxs-lookup"><span data-stu-id="7dba6-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="7dba6-157">Si se detecta un error, el comando de hello devuelve un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="7dba6-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="7dba6-158">Por ejemplo, al intentar toopass un valor incorrecto para la cuenta de almacenamiento de hello SKU, se devuelve Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="7dba6-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="7dba6-159">Si la plantilla tiene un error de sintaxis, comando hello devuelve un error que indica que no pudo analizar plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="7dba6-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="7dba6-160">mensajes de bienvenida indica el número de línea de Hola y posición del error de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="7dba6-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="7dba6-161">modo de toouse completa, use hello `Mode` parámetro:</span><span class="sxs-lookup"><span data-stu-id="7dba6-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="7dba6-162">Plantilla de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7dba6-162">Sample template</span></span>

<span data-ttu-id="7dba6-163">Hello siguiente plantilla se usa para obtener ejemplos de hello en este tema.</span><span class="sxs-lookup"><span data-stu-id="7dba6-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="7dba6-164">Cópiela y guárdela como un archivo denominado storage.json.</span><span class="sxs-lookup"><span data-stu-id="7dba6-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="7dba6-165">toounderstand cómo toocreate esta plantilla, consulte [crear la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="7dba6-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="7dba6-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7dba6-166">Next steps</span></span>
* <span data-ttu-id="7dba6-167">ejemplos de Hello en este artículo implementación grupo de recursos de tooa de recursos en su suscripción de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7dba6-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="7dba6-168">toouse otra suscripción, vea [administrar varias suscripciones de Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="7dba6-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="7dba6-169">Para obtener un script de ejemplo completo que implementa una plantilla, vea [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md) (Script de implementación de plantilla de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="7dba6-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="7dba6-170">toounderstand toodefine parámetros de la plantilla, vea [comprender la estructura de Hola y la sintaxis de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7dba6-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7dba6-171">Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="7dba6-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="7dba6-172">Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="7dba6-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="7dba6-173">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="7dba6-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>


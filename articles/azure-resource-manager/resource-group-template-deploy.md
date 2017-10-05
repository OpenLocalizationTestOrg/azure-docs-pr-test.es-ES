---
title: "Implementación de recursos con la plantilla y PowerShell | Microsoft Docs"
description: Use Azure Resource Manager y Azure PowerShell para implementar recursos en Azure. Los recursos se definen en una plantilla de Resource Manager.
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
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="553a5-104">Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="553a5-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="553a5-105">En este tema se explica cómo usar Azure PowerShell con plantillas de Resource Manager para implementar sus recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="553a5-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="553a5-106">Si no está familiarizado con los conceptos asociados a la implementación y administración de sus soluciones de Azure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="553a5-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="553a5-107">La plantilla de Resource Manager que ha implementado puede ser un archivo local en su equipo, o un archivo externo ubicado en un repositorio como GitHub.</span><span class="sxs-lookup"><span data-stu-id="553a5-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="553a5-108">La plantilla que se implementa en este artículo está disponible en la sección [Plantilla de ejemplo](#sample-template), o como [plantilla de la cuenta de almacenamiento en GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="553a5-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="553a5-109">Implementación de una plantilla desde la máquina local</span><span class="sxs-lookup"><span data-stu-id="553a5-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="553a5-110">Al implementar recursos en Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="553a5-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="553a5-111">Inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="553a5-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="553a5-112">Cree un grupo de recursos que actúe como contenedor para los recursos implementados.</span><span class="sxs-lookup"><span data-stu-id="553a5-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="553a5-113">El nombre del grupo de recursos solo puede incluir caracteres alfanuméricos, puntos, guiones bajos, guiones y paréntesis.</span><span class="sxs-lookup"><span data-stu-id="553a5-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="553a5-114">Puede tener hasta 90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="553a5-114">It can be up to 90 characters.</span></span> <span data-ttu-id="553a5-115">No puede terminar en punto.</span><span class="sxs-lookup"><span data-stu-id="553a5-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="553a5-116">Implemente en el grupo de recursos la plantilla que define los recursos que se van a crear.</span><span class="sxs-lookup"><span data-stu-id="553a5-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="553a5-117">Una plantilla puede incluir parámetros que le permiten personalizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="553a5-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="553a5-118">Por ejemplo, puede proporcionar valores que están diseñados para un entorno concreto (como desarrollo, prueba y producción).</span><span class="sxs-lookup"><span data-stu-id="553a5-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="553a5-119">La plantilla de ejemplo define un parámetro para la SKU de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="553a5-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="553a5-120">En el ejemplo siguiente se crea un grupo de recursos y se implementa una plantilla desde la máquina local:</span><span class="sxs-lookup"><span data-stu-id="553a5-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="553a5-121">La implementación puede demorar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="553a5-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="553a5-122">Cuando termine, verá un mensaje que incluye el resultado:</span><span class="sxs-lookup"><span data-stu-id="553a5-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="553a5-123">Implementación de una plantilla desde un origen externo</span><span class="sxs-lookup"><span data-stu-id="553a5-123">Deploy a template from an external source</span></span>

<span data-ttu-id="553a5-124">En lugar de almacenar las plantillas de Resource Manager en el equipo local, quizás prefiera almacenarlas en una ubicación externa.</span><span class="sxs-lookup"><span data-stu-id="553a5-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="553a5-125">Puede almacenar plantillas en un repositorio de control de código fuente (por ejemplo, GitHub).</span><span class="sxs-lookup"><span data-stu-id="553a5-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="553a5-126">O bien, puede almacenarlas en una cuenta de Azure Storage para el acceso compartido en su organización.</span><span class="sxs-lookup"><span data-stu-id="553a5-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="553a5-127">Para implementar una plantilla externa, use el parámetro **TemplateUri**.</span><span class="sxs-lookup"><span data-stu-id="553a5-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="553a5-128">Use el identificador URI en el ejemplo para implementar la plantilla de ejemplo de GitHub.</span><span class="sxs-lookup"><span data-stu-id="553a5-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="553a5-129">En el ejemplo anterior, se requiere un identificador URI accesible públicamente para la plantilla, que funciona con la mayoría de los escenarios porque la plantilla no debe incluir datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="553a5-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="553a5-130">Si tiene que especificar datos confidenciales (por ejemplo, una contraseña de administrador), pase ese valor como un parámetro seguro.</span><span class="sxs-lookup"><span data-stu-id="553a5-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="553a5-131">Sin embargo, si no desea que la plantilla sea accesible públicamente, puede protegerla mediante el almacenamiento en un contenedor de almacenamiento privado.</span><span class="sxs-lookup"><span data-stu-id="553a5-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="553a5-132">Para más información sobre la implementación de una plantilla que requiere un token de Firma de acceso compartido (SAS), consulte [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="553a5-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="553a5-133">Archivos de parámetros</span><span class="sxs-lookup"><span data-stu-id="553a5-133">Parameter files</span></span>

<span data-ttu-id="553a5-134">En lugar de pasar parámetros como valores en línea en el script, quizá le resulte más fácil usar un archivo JSON que contiene los valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="553a5-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="553a5-135">El archivo de parámetros debe estar en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="553a5-135">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="553a5-136">Tenga en cuenta que la sección de parámetros incluye un nombre de parámetro que coincide con el parámetro definido en la plantilla (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="553a5-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="553a5-137">El archivo de parámetros contiene un valor para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="553a5-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="553a5-138">Este valor se pasa automáticamente a la plantilla durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="553a5-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="553a5-139">Puede crear varios archivos de parámetros para diferentes escenarios de implementación y, después, pasar el archivo de parámetros adecuado.</span><span class="sxs-lookup"><span data-stu-id="553a5-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="553a5-140">Copie el ejemplo anterior y guárdelo como un archivo denominado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="553a5-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="553a5-141">Para pasar un archivo de parámetros local, use el parámetro **TemplateParameterFile**:</span><span class="sxs-lookup"><span data-stu-id="553a5-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="553a5-142">Para pasar un archivo de parámetros externo, use el parámetro **TemplateParameterUri**:</span><span class="sxs-lookup"><span data-stu-id="553a5-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="553a5-143">Puede usar parámetros en línea y un archivo de parámetros local en la misma operación de implementación.</span><span class="sxs-lookup"><span data-stu-id="553a5-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="553a5-144">Por ejemplo, puede especificar algunos valores en el archivo de parámetros local y agregar otros valores en línea durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="553a5-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="553a5-145">Si proporciona valores para un parámetro en el archivo de parámetros local y en línea, el valor en línea tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="553a5-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="553a5-146">Sin embargo, cuando se utiliza un archivo de parámetros externo, no se pueden pasar otros valores ya sea en línea o desde un archivo local.</span><span class="sxs-lookup"><span data-stu-id="553a5-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="553a5-147">Cuando se especifica un archivo de parámetros en el parámetro **TemplateParameterUri**, se omiten todos los parámetros en línea.</span><span class="sxs-lookup"><span data-stu-id="553a5-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="553a5-148">Proporcione todos los valores de parámetro en el archivo externo.</span><span class="sxs-lookup"><span data-stu-id="553a5-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="553a5-149">Si la plantilla incluye un valor confidencial que no puede incluir en el archivo de parámetros, agregue ese valor a un almacén de claves o proporcione dinámicamente todos los valores de parámetro en línea.</span><span class="sxs-lookup"><span data-stu-id="553a5-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="553a5-150">Si la plantilla incluye un parámetro con el mismo nombre que uno de los parámetros del comando de PowerShell, PowerShell presenta el parámetro de la plantilla con el postfijo **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="553a5-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="553a5-151">Por ejemplo, un parámetro denominado **ResourceGroupName** de su plantilla entra en conflicto con el parámetro **ResourceGroupName** del cmdlet [AzureRmResourceGroupDeployment nuevo](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="553a5-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="553a5-152">Se le pedirá que proporcione un valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="553a5-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="553a5-153">Por lo general, debe evitar esta confusión no nombrando los parámetros con el mismo nombre que los parámetros utilizados para operaciones de implementación.</span><span class="sxs-lookup"><span data-stu-id="553a5-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="553a5-154">Prueba de una implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="553a5-154">Test a template deployment</span></span>

<span data-ttu-id="553a5-155">Para probar los valores de parámetro y de plantilla sin implementar realmente ningún recurso, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="553a5-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="553a5-156">Si no se detectan errores, el comando finaliza sin una respuesta.</span><span class="sxs-lookup"><span data-stu-id="553a5-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="553a5-157">Si se detecta un error, el comando devuelve un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="553a5-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="553a5-158">Por ejemplo, si se intenta pasar un valor incorrecto a la SKU de la cuenta de almacenamiento, se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="553a5-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="553a5-159">Si la plantilla tiene un error de sintaxis, el comando devuelve un error que indica que no se pudo analizar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="553a5-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="553a5-160">El mensaje indica el número de línea y la posición del error de análisis.</span><span class="sxs-lookup"><span data-stu-id="553a5-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="553a5-161">Para usar el modo completo, emplee el parámetro `Mode`:</span><span class="sxs-lookup"><span data-stu-id="553a5-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="553a5-162">Plantilla de ejemplo</span><span class="sxs-lookup"><span data-stu-id="553a5-162">Sample template</span></span>

<span data-ttu-id="553a5-163">La plantilla siguiente se usa para los ejemplos de este tema.</span><span class="sxs-lookup"><span data-stu-id="553a5-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="553a5-164">Cópiela y guárdela como un archivo denominado storage.json.</span><span class="sxs-lookup"><span data-stu-id="553a5-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="553a5-165">Para comprender cómo crear esta plantilla, consulte [Creación de la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="553a5-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="553a5-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="553a5-166">Next steps</span></span>
* <span data-ttu-id="553a5-167">Los ejemplos de este artículo implementan recursos en un grupo de recursos de su suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="553a5-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="553a5-168">Para usar una suscripción diferente, consulte [Administración de varias suscripciones de Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="553a5-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="553a5-169">Para obtener un script de ejemplo completo que implementa una plantilla, vea [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md) (Script de implementación de plantilla de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="553a5-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="553a5-170">Para entender cómo definir parámetros en la plantilla, consulte [Nociones sobre la estructura y la sintaxis de las plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="553a5-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="553a5-171">Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="553a5-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="553a5-172">Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="553a5-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="553a5-173">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="553a5-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>


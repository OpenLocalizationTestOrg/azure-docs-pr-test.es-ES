---
title: "Implementación de recursos con la plantilla y la CLI de Azure | Microsoft Docs"
description: Use Azure Resource Manager y la CLI de Azure para implementar recursos en Azure. Los recursos se definen en una plantilla de Resource Manager.
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
ms.openlocfilehash: 4f1d5f4cc48470f8906edb28628006dd1996bd3a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="fb2fd-104">Implementación de recursos con plantillas de Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fb2fd-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="fb2fd-105">En este tema se explica cómo usar la CLI de Azure 2.0 con plantillas de Resource Manager para implementar recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-105">This topic explains how to use Azure CLI 2.0 with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="fb2fd-106">Si no está familiarizado con los conceptos asociados a la implementación y administración de sus soluciones de Azure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="fb2fd-107">La plantilla de Resource Manager que ha implementado puede ser un archivo local en su equipo, o un archivo externo ubicado en un repositorio como GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="fb2fd-108">La plantilla que se implementa en este artículo está disponible en la sección [Plantilla de ejemplo](#sample-template), o como [plantilla de la cuenta de almacenamiento en GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="fb2fd-109">Si no tiene instalada la CLI de Azure, puede usar [Cloud Shell](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-109">If you do not have Azure CLI installed, you can use the [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="fb2fd-110">Implementar una plantilla local</span><span class="sxs-lookup"><span data-stu-id="fb2fd-110">Deploy local template</span></span>

<span data-ttu-id="fb2fd-111">Al implementar recursos en Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fb2fd-111">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="fb2fd-112">Inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-112">Log in to your Azure account</span></span>
2. <span data-ttu-id="fb2fd-113">Cree un grupo de recursos que actúe como contenedor para los recursos implementados.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-113">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="fb2fd-114">El nombre del grupo de recursos solo puede incluir caracteres alfanuméricos, puntos, guiones bajos, guiones y paréntesis.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-114">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="fb2fd-115">Puede tener hasta 90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-115">It can be up to 90 characters.</span></span> <span data-ttu-id="fb2fd-116">No puede terminar en punto.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="fb2fd-117">Implemente en el grupo de recursos la plantilla que define los recursos que se van a crear.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-117">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="fb2fd-118">Una plantilla puede incluir parámetros que le permiten personalizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-118">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="fb2fd-119">Por ejemplo, puede proporcionar valores que están diseñados para un entorno concreto (como desarrollo, prueba y producción).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="fb2fd-120">La plantilla de ejemplo define un parámetro para la SKU de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-120">The sample template defines a parameter for the storage account SKU.</span></span> 

<span data-ttu-id="fb2fd-121">En el ejemplo siguiente se crea un grupo de recursos y se implementa una plantilla desde la máquina local:</span><span class="sxs-lookup"><span data-stu-id="fb2fd-121">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="fb2fd-122">La implementación puede demorar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-122">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="fb2fd-123">Cuando termine, verá un mensaje que incluye el resultado:</span><span class="sxs-lookup"><span data-stu-id="fb2fd-123">When it finishes, you see a message that includes the result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="fb2fd-124">Implementar una plantilla externa</span><span class="sxs-lookup"><span data-stu-id="fb2fd-124">Deploy external template</span></span>

<span data-ttu-id="fb2fd-125">En lugar de almacenar las plantillas de Resource Manager en el equipo local, quizás prefiera almacenarlas en una ubicación externa.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-125">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="fb2fd-126">Puede almacenar plantillas en un repositorio de control de código fuente (por ejemplo, GitHub).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="fb2fd-127">O bien, puede almacenarlas en una cuenta de Azure Storage para el acceso compartido en su organización.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="fb2fd-128">Para implementar una plantilla externa, use el parámetro **template-uri**.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-128">To deploy an external template, use the **template-uri** parameter.</span></span> <span data-ttu-id="fb2fd-129">Use el identificador URI en el ejemplo para implementar la plantilla de ejemplo de GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-129">Use the URI in the example to deploy the sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="fb2fd-130">En el ejemplo anterior, se requiere un identificador URI accesible públicamente para la plantilla, que funciona con la mayoría de los escenarios porque la plantilla no debe incluir datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-130">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="fb2fd-131">Si tiene que especificar datos confidenciales (por ejemplo, una contraseña de administrador), pase ese valor como un parámetro seguro.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-131">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="fb2fd-132">Sin embargo, si no desea que la plantilla sea accesible públicamente, puede protegerla mediante el almacenamiento en un contenedor de almacenamiento privado.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-132">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="fb2fd-133">Para más información sobre la implementación de una plantilla que requiere un token de Firma de acceso compartido (SAS), consulte [Implementación de una plantilla privada con el token de SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="fb2fd-134">Implementación de plantilla desde Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="fb2fd-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="fb2fd-135">Puede usar [Cloud Shell](../cloud-shell/overview.md) para ejecutar los comandos de la CLI de Azure para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-135">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="fb2fd-136">Pero primero debe cargar la plantilla en el recurso compartido de archivos de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-136">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="fb2fd-137">Si no ha usado Cloud Shell, vea [Introducción a Azure Cloud Shell](../cloud-shell/overview.md) para más información sobre su configuración.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="fb2fd-138">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="fb2fd-139">Seleccione el grupo de recursos de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="fb2fd-140">El patrón de nombre es `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-140">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Selección de un grupo de recursos](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="fb2fd-142">Seleccione la cuenta de almacenamiento de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-142">Select the storage account for your Cloud Shell.</span></span>

   ![Selección de la cuenta de almacenamiento](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="fb2fd-144">Seleccione **Archivos**.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-144">Select **Files**.</span></span>

   ![Seleccionar archivos](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="fb2fd-146">Seleccione el recurso compartido de archivos de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-146">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="fb2fd-147">El patrón de nombre es `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-147">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selección de recurso compartido de archivos](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="fb2fd-149">Seleccione **Agregar directorio**.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-149">Select **Add directory**.</span></span>

   ![Agregar directorio](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="fb2fd-151">Asígnele el nombre **plantillas** y seleccione **Correcto**.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-151">Name it **templates**, and select **Okay**.</span></span>

   ![Nombre de directorio](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="fb2fd-153">Seleccione el nuevo directorio.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-153">Select your new directory.</span></span>

   ![Selección de directorio](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="fb2fd-155">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-155">Select **Upload**.</span></span>

   ![Selección de carga](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="fb2fd-157">Busque y cargue la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-157">Find and upload your template.</span></span>

   ![Carga de archivo](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="fb2fd-159">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-159">Open the prompt.</span></span>

   ![Apertura de Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="fb2fd-161">En Cloud Shell, escriba los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb2fd-161">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="fb2fd-162">Archivos de parámetros</span><span class="sxs-lookup"><span data-stu-id="fb2fd-162">Parameter files</span></span>

<span data-ttu-id="fb2fd-163">En lugar de pasar parámetros como valores en línea en el script, quizá le resulte más fácil usar un archivo JSON que contiene los valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-163">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="fb2fd-164">El archivo de parámetros debe estar en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="fb2fd-164">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="fb2fd-165">Tenga en cuenta que la sección de parámetros incluye un nombre de parámetro que coincide con el parámetro definido en la plantilla (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-165">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="fb2fd-166">El archivo de parámetros contiene un valor para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-166">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="fb2fd-167">Este valor se pasa automáticamente a la plantilla durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-167">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="fb2fd-168">Puede crear varios archivos de parámetros para diferentes escenarios de implementación y, después, pasar el archivo de parámetros adecuado.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-168">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="fb2fd-169">Copie el ejemplo anterior y guárdelo como un archivo denominado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-169">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="fb2fd-170">Para pasar un archivo de parámetros local, use `@` para especificar un archivo local denominado storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-170">To pass a local parameter file, use `@` to specify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="fb2fd-171">Prueba de una implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="fb2fd-171">Test a template deployment</span></span>

<span data-ttu-id="fb2fd-172">Para probar los valores de parámetro y de plantilla sin implementar realmente ningún recurso, use [az group deployment validate](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-172">To test your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="fb2fd-173">Si no se detectan errores, el comando devuelve información sobre la implementación de prueba.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-173">If no errors are detected, the command returns information about the test deployment.</span></span> <span data-ttu-id="fb2fd-174">En concreto, tenga en cuenta que el valor **error** es null.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-174">In particular, notice that the **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="fb2fd-175">Si se detecta un error, el comando devuelve un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-175">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="fb2fd-176">Por ejemplo, si se intenta pasar un valor incorrecto a la SKU de la cuenta de almacenamiento, se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb2fd-176">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'The provided value 'badSKU' for the template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. The parameter value is not part of the allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="fb2fd-177">Si la plantilla tiene un error de sintaxis, el comando devuelve un error que indica que no se pudo analizar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-177">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="fb2fd-178">El mensaje indica el número de línea y la posición del error de análisis.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-178">The message indicates the line number and position of the parsing error.</span></span>

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

<span data-ttu-id="fb2fd-179">Para usar el modo completo, emplee el parámetro `mode`:</span><span class="sxs-lookup"><span data-stu-id="fb2fd-179">To use complete mode, use the `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="fb2fd-180">Plantilla de ejemplo</span><span class="sxs-lookup"><span data-stu-id="fb2fd-180">Sample template</span></span>

<span data-ttu-id="fb2fd-181">La plantilla siguiente se usa para los ejemplos de este tema.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-181">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="fb2fd-182">Cópiela y guárdela como un archivo denominado storage.json.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="fb2fd-183">Para comprender cómo crear esta plantilla, consulte [Creación de la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-183">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="fb2fd-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb2fd-184">Next steps</span></span>
* <span data-ttu-id="fb2fd-185">Los ejemplos de este artículo implementan recursos en un grupo de recursos de su suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fb2fd-185">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="fb2fd-186">Para usar una suscripción diferente, consulte [Administración de varias suscripciones de Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-186">To use a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="fb2fd-187">Para obtener un script de ejemplo completo que implementa una plantilla, vea [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md) (Script de implementación de plantilla de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="fb2fd-188">Para entender cómo definir parámetros en la plantilla, consulte [Nociones sobre la estructura y la sintaxis de las plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-188">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fb2fd-189">Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="fb2fd-190">Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="fb2fd-191">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="fb2fd-191">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

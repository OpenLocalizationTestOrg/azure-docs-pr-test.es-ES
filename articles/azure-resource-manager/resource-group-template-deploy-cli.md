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
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="e1e6f-104">Implementación de recursos con plantillas de Resource Manager y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e1e6f-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="e1e6f-105">Este tema se explica cómo toouse 2.0 de CLI de Azure con el Administrador de recursos plantillas toodeploy su tooAzure de recursos.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="e1e6f-106">Si no está familiarizado con conceptos de Hola de implementar y administrar sus soluciones de Azure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="e1e6f-107">plantilla de administrador de recursos de Hello que implementar puede ser un archivo local en su equipo, o un archivo externo que se encuentra en un repositorio como GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="e1e6f-108">plantilla de Hola se implementan en este artículo está disponible en hello [plantilla de ejemplo](#sample-template) sección, o como un [plantilla de la cuenta de almacenamiento en GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="e1e6f-109">Si no tiene instalado de CLI de Azure, puede usar hello [Shell en la nube](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="e1e6f-110">Implementar una plantilla local</span><span class="sxs-lookup"><span data-stu-id="e1e6f-110">Deploy local template</span></span>

<span data-ttu-id="e1e6f-111">Al implementar tooAzure de recursos,:</span><span class="sxs-lookup"><span data-stu-id="e1e6f-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="e1e6f-112">Inicie sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="e1e6f-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="e1e6f-113">Crear un grupo de recursos que actúa como contenedor de Hola de recursos de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="e1e6f-114">nombre de Hola Hola del grupo de recursos solo puede incluir caracteres alfanuméricos, puntos, caracteres de subrayado, guiones y paréntesis.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="e1e6f-115">Puede ser una too90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-115">It can be up too90 characters.</span></span> <span data-ttu-id="e1e6f-116">No puede terminar en punto.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="e1e6f-117">Implementar la plantilla de Hola de grupo de recursos de toohello que define Hola recursos toocreate</span><span class="sxs-lookup"><span data-stu-id="e1e6f-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="e1e6f-118">Una plantilla puede incluir parámetros que permiten la implementación de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="e1e6f-119">Por ejemplo, puede proporcionar valores que están diseñados para un entorno concreto (como desarrollo, prueba y producción).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="e1e6f-120">plantilla de ejemplo de Hola define un parámetro para la cuenta de almacenamiento de hello SKU.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="e1e6f-121">Hola de ejemplo siguiente crea un grupo de recursos e implementa una plantilla desde el equipo local:</span><span class="sxs-lookup"><span data-stu-id="e1e6f-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="e1e6f-122">implementación de Hello puede tardar unos toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="e1e6f-123">Cuando termine, verá un mensaje que incluye el resultado de hello:</span><span class="sxs-lookup"><span data-stu-id="e1e6f-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="e1e6f-124">Implementar una plantilla externa</span><span class="sxs-lookup"><span data-stu-id="e1e6f-124">Deploy external template</span></span>

<span data-ttu-id="e1e6f-125">En lugar de almacenar las plantillas de administrador de recursos en el equipo local, es posible que prefiera toostore ellas en una ubicación externa.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="e1e6f-126">Puede almacenar plantillas en un repositorio de control de código fuente (por ejemplo, GitHub).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="e1e6f-127">O bien, puede almacenarlas en una cuenta de Azure Storage para el acceso compartido en su organización.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="e1e6f-128">toodeploy una plantilla externa, use hello **plantilla uri** parámetro.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="e1e6f-129">Usar hello URI en la plantilla de ejemplo de Hola ejemplo toodeploy Hola desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="e1e6f-130">Hello en el ejemplo anterior se requiere un URI accesible públicamente para plantilla de hello, que funciona con la mayoría de los escenarios, porque la plantilla no debe incluir datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="e1e6f-131">Si necesita toospecify datos confidenciales (por ejemplo, una contraseña de administrador), pase ese valor como un parámetro seguro.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="e1e6f-132">Sin embargo, si no desea que la plantilla toobe accesible públicamente, puede proteger mediante el almacenamiento en un contenedor de almacenamiento privado.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="e1e6f-133">Para más información sobre la implementación de una plantilla que requiere un token de Firma de acceso compartido (SAS), consulte [Implementación de una plantilla privada con el token de SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="e1e6f-134">Implementación de una plantilla desde Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="e1e6f-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="e1e6f-135">Puede usar [Shell en la nube](../cloud-shell/overview.md) toorun hello Azure CLI comandos para la implementación de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="e1e6f-136">Sin embargo, primero debe cargar la plantilla en el recurso compartido de archivos de hello del shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="e1e6f-137">Si no ha usado Cloud Shell, vea [Introducción a Azure Cloud Shell](../cloud-shell/overview.md) para más información sobre su configuración.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="e1e6f-138">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="e1e6f-139">Seleccione el grupo de recursos de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="e1e6f-140">patrón de nombre de Hello es `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Selección de un grupo de recursos](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="e1e6f-142">Seleccione la cuenta de almacenamiento de hello del shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-142">Select hello storage account for your Cloud Shell.</span></span>

   ![Selección de la cuenta de almacenamiento](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="e1e6f-144">Seleccione **Archivos**.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-144">Select **Files**.</span></span>

   ![Seleccionar archivos](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="e1e6f-146">Seleccione el recurso compartido de archivos de Hola de Shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="e1e6f-147">patrón de nombre de Hello es `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selección de recurso compartido de archivos](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="e1e6f-149">Seleccione **Agregar directorio**.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-149">Select **Add directory**.</span></span>

   ![Agregar directorio](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="e1e6f-151">Asígnele el nombre **plantillas** y seleccione **Correcto**.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-151">Name it **templates**, and select **Okay**.</span></span>

   ![Nombre de directorio](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="e1e6f-153">Seleccione el nuevo directorio.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-153">Select your new directory.</span></span>

   ![Selección de directorio](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="e1e6f-155">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-155">Select **Upload**.</span></span>

   ![Selección de carga](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="e1e6f-157">Busque y cargue la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-157">Find and upload your template.</span></span>

   ![Carga de archivo](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="e1e6f-159">Mensaje de Hola abierto.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-159">Open hello prompt.</span></span>

   ![Apertura de Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="e1e6f-161">Escriba Hola siguientes comandos de hello Shell en la nube:</span><span class="sxs-lookup"><span data-stu-id="e1e6f-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="e1e6f-162">Archivos de parámetros</span><span class="sxs-lookup"><span data-stu-id="e1e6f-162">Parameter files</span></span>

<span data-ttu-id="e1e6f-163">En lugar de pasar parámetros como valores en línea en la secuencia de comandos, quizá le resulte más fácil toouse un archivo JSON que contiene los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="e1e6f-164">archivo de parámetros de Hello debe Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="e1e6f-164">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="e1e6f-165">Tenga en cuenta que la sección de parámetros de hello incluye un nombre de parámetro que coincida con el parámetro hello definido en la plantilla (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="e1e6f-166">archivo de parámetros de Hello contiene un valor para el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="e1e6f-167">Este valor se pasa automáticamente toohello plantilla durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="e1e6f-168">Puede crear varios archivos de parámetros para diferentes escenarios de implementación y, a continuación, pase Hola parámetro apropiado archivo.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="e1e6f-169">Copie el anterior ejemplo de Hola y guárdelo como un archivo denominado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="e1e6f-170">toopass un archivo de parámetros local, use `@` toospecify un archivo local denominado storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="e1e6f-171">Prueba de una implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="e1e6f-171">Test a template deployment</span></span>

<span data-ttu-id="e1e6f-172">tootest los valores de parámetro y de plantilla sin implementar realmente los recursos, utilice [validar la implementación del grupo az](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="e1e6f-173">Si no se detectan errores, el comando de hello devuelve información acerca de la implementación de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="e1e6f-174">En concreto, tenga en cuenta que hello **error** valor es null.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="e1e6f-175">Si se detecta un error, el comando de hello devuelve un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="e1e6f-176">Por ejemplo, al intentar toopass un valor incorrecto para la cuenta de almacenamiento de hello SKU, se devuelve Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="e1e6f-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

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

<span data-ttu-id="e1e6f-177">Si la plantilla tiene un error de sintaxis, comando hello devuelve un error que indica que no pudo analizar plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="e1e6f-178">mensajes de bienvenida indica el número de línea de Hola y posición del error de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-178">hello message indicates hello line number and position of hello parsing error.</span></span>

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

<span data-ttu-id="e1e6f-179">modo de toouse completa, use hello `mode` parámetro:</span><span class="sxs-lookup"><span data-stu-id="e1e6f-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="e1e6f-180">Plantilla de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1e6f-180">Sample template</span></span>

<span data-ttu-id="e1e6f-181">Hello siguiente plantilla se usa para obtener ejemplos de hello en este tema.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="e1e6f-182">Cópiela y guárdela como un archivo denominado storage.json.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="e1e6f-183">toounderstand cómo toocreate esta plantilla, consulte [crear la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="e1e6f-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1e6f-184">Next steps</span></span>
* <span data-ttu-id="e1e6f-185">ejemplos de Hello en este artículo implementación grupo de recursos de tooa de recursos en su suscripción de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e1e6f-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="e1e6f-186">toouse otra suscripción, vea [administrar varias suscripciones de Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="e1e6f-187">Para obtener un script de ejemplo completo que implementa una plantilla, vea [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md) (Script de implementación de plantilla de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="e1e6f-188">toounderstand toodefine parámetros de la plantilla, vea [comprender la estructura de Hola y la sintaxis de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e1e6f-189">Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e1e6f-190">Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="e1e6f-191">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e1e6f-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

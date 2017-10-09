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
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="f0706-104">Creación e implementación de la primera plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f0706-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="f0706-105">En este tema le guiará por los pasos de Hola de creación de la primera plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f0706-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="f0706-106">Las plantillas de administrador de recursos son archivos JSON que definen los recursos de hello necesita toodeploy para su solución.</span><span class="sxs-lookup"><span data-stu-id="f0706-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="f0706-107">conceptos de hello toounderstand asociados con la implementación y administración de sus soluciones de Azure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0706-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="f0706-108">Si dispone de recursos existentes y desea tooget una plantilla para esos recursos, consulte [exportar una plantilla de Azure Resource Manager de los recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="f0706-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="f0706-109">plantillas de toocreate y revisar, necesita un editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="f0706-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="f0706-110">[Visual Studio Code](https://code.visualstudio.com/) es un editor de código ligero, de código abierto y multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="f0706-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="f0706-111">Se recomienda encarecidamente usar código de Visual Studio para crear plantillas de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f0706-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="f0706-112">En este tema se da por supuesto que se utiliza Visual Studio Code; sin embargo, si tiene otro editor de JSON (por ejemplo, Visual Studio), puede usarlo.</span><span class="sxs-lookup"><span data-stu-id="f0706-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0706-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f0706-113">Prerequisites</span></span>

* <span data-ttu-id="f0706-114">Código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0706-114">Visual Studio Code.</span></span> <span data-ttu-id="f0706-115">Si es necesario, instálelo desde [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="f0706-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="f0706-116">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f0706-116">An Azure subscription.</span></span> <span data-ttu-id="f0706-117">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="f0706-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="f0706-118">Creación de una plantilla</span><span class="sxs-lookup"><span data-stu-id="f0706-118">Create template</span></span>

<span data-ttu-id="f0706-119">Puede empezar con una plantilla sencilla que implementa una suscripción de tooyour de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f0706-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="f0706-120">Seleccione **Archivo** > **Nuevo archivo**.</span><span class="sxs-lookup"><span data-stu-id="f0706-120">Select **File** > **New File**.</span></span> 

   ![Nuevo archivo](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="f0706-122">Copie y pegue Hola siguiendo la sintaxis de JSON en el archivo:</span><span class="sxs-lookup"><span data-stu-id="f0706-122">Copy and paste hello following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="f0706-123">Nombres de cuenta de almacenamiento tienen varias restricciones específicas que resultan difíciles de tooset.</span><span class="sxs-lookup"><span data-stu-id="f0706-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="f0706-124">nombre de Hello debe tener entre 3 y 24 caracteres de longitud, utilice sólo números y letras en minúsculas y ser únicos.</span><span class="sxs-lookup"><span data-stu-id="f0706-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="f0706-125">plantilla anterior Hello usa hello [uniqueString](resource-group-template-functions-string.md#uniquestring) función toogenerate un valor hash.</span><span class="sxs-lookup"><span data-stu-id="f0706-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="f0706-126">toogive este hash valor más lo que significa que, agrega el prefijo de hello *almacenamiento*.</span><span class="sxs-lookup"><span data-stu-id="f0706-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="f0706-127">Guarde este archivo como **azuredeploy.json** tooa de carpeta local.</span><span class="sxs-lookup"><span data-stu-id="f0706-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Guardar plantilla](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="f0706-129">Implementar plantilla</span><span class="sxs-lookup"><span data-stu-id="f0706-129">Deploy template</span></span>

<span data-ttu-id="f0706-130">Se está listo toodeploy esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="f0706-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="f0706-131">Usar PowerShell o CLI de Azure toocreate un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f0706-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="f0706-132">A continuación, implemente un grupo de recursos de toothat de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f0706-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="f0706-133">Para PowerShell, use Hola siguientes comandos de carpeta de Hola que contiene la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="f0706-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="f0706-134">Para una instalación local de CLI de Azure, use Hola siguientes comandos de carpeta de Hola que contiene la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="f0706-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="f0706-135">Cuando finalice la implementación, la cuenta de almacenamiento existe en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0706-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="f0706-136">Implementación de una plantilla desde Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f0706-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="f0706-137">Puede usar [Shell en la nube](../cloud-shell/overview.md) toorun hello Azure CLI comandos para la implementación de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="f0706-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="f0706-138">Sin embargo, primero debe cargar la plantilla en el recurso compartido de archivos de hello del shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="f0706-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="f0706-139">Si no ha usado Cloud Shell, vea [Introducción a Azure Cloud Shell](../cloud-shell/overview.md) para más información sobre su configuración.</span><span class="sxs-lookup"><span data-stu-id="f0706-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="f0706-140">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f0706-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="f0706-141">Seleccione el grupo de recursos de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="f0706-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="f0706-142">patrón de nombre de Hello es `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="f0706-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Selección de un grupo de recursos](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="f0706-144">Seleccione la cuenta de almacenamiento de hello del shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="f0706-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Selección de la cuenta de almacenamiento](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="f0706-146">Seleccione **Archivos**.</span><span class="sxs-lookup"><span data-stu-id="f0706-146">Select **Files**.</span></span>

   ![Seleccionar archivos](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="f0706-148">Seleccione el recurso compartido de archivos de Hola de Shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="f0706-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="f0706-149">patrón de nombre de Hello es `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="f0706-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selección de recurso compartido de archivos](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="f0706-151">Seleccione **Agregar directorio**.</span><span class="sxs-lookup"><span data-stu-id="f0706-151">Select **Add directory**.</span></span>

   ![Agregar directorio](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="f0706-153">Asígnele el nombre **plantillas** y seleccione **Correcto**.</span><span class="sxs-lookup"><span data-stu-id="f0706-153">Name it **templates**, and select **Okay**.</span></span>

   ![Nombre de directorio](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="f0706-155">Seleccione el nuevo directorio.</span><span class="sxs-lookup"><span data-stu-id="f0706-155">Select your new directory.</span></span>

   ![Selección de directorio](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="f0706-157">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="f0706-157">Select **Upload**.</span></span>

   ![Selección de carga](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="f0706-159">Busque y cargue la plantilla.</span><span class="sxs-lookup"><span data-stu-id="f0706-159">Find and upload your template.</span></span>

   ![Carga de archivo](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="f0706-161">Mensaje de Hola abierto.</span><span class="sxs-lookup"><span data-stu-id="f0706-161">Open hello prompt.</span></span>

   ![Apertura de Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="f0706-163">Escriba Hola siguientes comandos de hello Shell en la nube:</span><span class="sxs-lookup"><span data-stu-id="f0706-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="f0706-164">Cuando finalice la implementación, la cuenta de almacenamiento existe en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0706-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="f0706-165">Personalizar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="f0706-165">Customize hello template</span></span>

<span data-ttu-id="f0706-166">plantilla de Hello funciona bien, pero no es flexible.</span><span class="sxs-lookup"><span data-stu-id="f0706-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="f0706-167">Siempre se implementa un tooSouth de almacenamiento con redundancia local Central US.</span><span class="sxs-lookup"><span data-stu-id="f0706-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="f0706-168">siempre es el nombre de Hello *almacenamiento* seguido por un valor de hash.</span><span class="sxs-lookup"><span data-stu-id="f0706-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="f0706-169">tooenable mediante la plantilla de Hola para diferentes escenarios, agregar parámetros toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="f0706-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="f0706-170">Hello en el ejemplo siguiente se muestra hello sección de parámetros con dos parámetros.</span><span class="sxs-lookup"><span data-stu-id="f0706-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="f0706-171">Hola primer parámetro `storageSKU` le permite el tipo de hello toospecify de redundancia.</span><span class="sxs-lookup"><span data-stu-id="f0706-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="f0706-172">Limita los valores de hello que puede pasar en toovalues que son válidos para una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f0706-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="f0706-173">También especifica un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f0706-173">It also specifies a default value.</span></span> <span data-ttu-id="f0706-174">Hola segundo parámetro `storageNamePrefix` es conjunto tooallow un máximo de 11 caracteres.</span><span class="sxs-lookup"><span data-stu-id="f0706-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="f0706-175">Especifica un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f0706-175">It specifies a default value.</span></span>

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

<span data-ttu-id="f0706-176">En la sección de variables de hello, agregue una variable denominada `storageName`.</span><span class="sxs-lookup"><span data-stu-id="f0706-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="f0706-177">Combina el valor de prefijo de Hola de parámetros de Hola y un valor de hash de hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (función).</span><span class="sxs-lookup"><span data-stu-id="f0706-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="f0706-178">Usa hello [toLower](resource-group-template-functions-string.md#tolower) función tooconvert toolowercase de todos los caracteres.</span><span class="sxs-lookup"><span data-stu-id="f0706-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="f0706-179">toouse estos nuevos valores para la cuenta de almacenamiento, cambie la definición de recurso de hello:</span><span class="sxs-lookup"><span data-stu-id="f0706-179">toouse these new values for your storage account, change hello resource definition:</span></span>

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

<span data-ttu-id="f0706-180">Tenga en cuenta que Hola nombre de cuenta de almacenamiento de Hola ahora se establece la variable toohello que agregó.</span><span class="sxs-lookup"><span data-stu-id="f0706-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="f0706-181">nombre SKU de Hola se establece toohello valor de parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="f0706-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="f0706-182">se establece la ubicación de Hola Hola la misma ubicación que el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0706-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="f0706-183">Guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="f0706-183">Save your file.</span></span> 

<span data-ttu-id="f0706-184">Después de completar los pasos de hello en este artículo, la plantilla ahora el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="f0706-184">After completing hello steps in this article, your template now looks like:</span></span>

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

## <a name="redeploy-template"></a><span data-ttu-id="f0706-185">Volver a implementar la plantilla</span><span class="sxs-lookup"><span data-stu-id="f0706-185">Redeploy template</span></span>

<span data-ttu-id="f0706-186">Volver a implementar la plantilla de hello con valores diferentes.</span><span class="sxs-lookup"><span data-stu-id="f0706-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="f0706-187">Para PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f0706-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="f0706-188">Para la CLI de Azure, utilice:</span><span class="sxs-lookup"><span data-stu-id="f0706-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="f0706-189">Para hello Shell en la nube, cargue el recurso compartido de archivos de plantilla se ha cambiado toohello.</span><span class="sxs-lookup"><span data-stu-id="f0706-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="f0706-190">Sobrescribir el archivo existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0706-190">Overwrite hello existing file.</span></span> <span data-ttu-id="f0706-191">A continuación, utilice el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="f0706-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="f0706-192">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="f0706-192">Clean up resources</span></span>

<span data-ttu-id="f0706-193">Cuando ya no necesite, limpiar los recursos de hello implementadas mediante la eliminación de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0706-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="f0706-194">Para PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f0706-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="f0706-195">Para la CLI de Azure, utilice:</span><span class="sxs-lookup"><span data-stu-id="f0706-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="f0706-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f0706-196">Next steps</span></span>
* <span data-ttu-id="f0706-197">toolearn más información acerca de la estructura de Hola de una plantilla, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f0706-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f0706-198">toolearn acerca de las propiedades de Hola para una cuenta de almacenamiento, consulte [referencia de plantillas de cuentas de almacenamiento](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="f0706-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="f0706-199">tooview completa plantillas para muchos tipos distintos de soluciones, vea hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="f0706-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>

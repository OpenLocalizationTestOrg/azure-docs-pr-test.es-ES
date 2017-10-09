---
title: plantillas de toocheck aaaUse validador de plantilla para la pila de Azure | Documentos de Microsoft
description: "Compruebe las plantillas de implementación tooAzure pila"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: helaw
ms.openlocfilehash: ee649f2ebf77486ca5036116dd73a45d66884704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a><span data-ttu-id="d4ccd-103">Compruebe las plantillas para Azure Stack con el validador de plantilla</span><span class="sxs-lookup"><span data-stu-id="d4ccd-103">Check your templates for Azure Stack with Template Validator</span></span>
<span data-ttu-id="d4ccd-104">Puede usar Hola plantilla validación herramienta toocheck si el Administrador de recursos de Azure [plantillas](azure-stack-arm-templates.md) están listos para la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-104">You can use hello template validation tool toocheck if your Azure Resource Manager [templates](azure-stack-arm-templates.md) are ready for Azure Stack.</span></span> <span data-ttu-id="d4ccd-105">herramienta de validación de plantilla de Hello está disponible como parte de herramientas de la pila de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-105">hello template validation tool is available as a part of hello Azure Stack tools.</span></span> <span data-ttu-id="d4ccd-106">Descargar herramientas de Azure pila hello mediante pasos de hello descritos en hello [descargar herramientas de GitHub](azure-stack-powershell-download.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-106">Download hello Azure Stack tools by using hello steps described in hello [download tools from GitHub](azure-stack-powershell-download.md) article.</span></span> 

<span data-ttu-id="d4ccd-107">plantillas de toovalidate, utilice Hola después de módulos de PowerShell y Hola JSON archivo ubicado en **TemplateValidator** y **CloudCapabilities** carpetas:</span><span class="sxs-lookup"><span data-stu-id="d4ccd-107">toovalidate templates, you use hello following PowerShell modules and hello JSON file located in **TemplateValidator** and **CloudCapabilities** folders:</span></span> 

 - <span data-ttu-id="d4ccd-108">AzureRM.CloudCapabilities.psm1 crea un archivo JSON de las capacidades de nube que representa los servicios de Hola y las versiones en una nube como Azure pila.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-108">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing hello services and versions in a cloud like Azure Stack.</span></span>
 - <span data-ttu-id="d4ccd-109">AzureRM.TemplateValidator.psm1 usa capacidades de la nube plantillas de tootest de archivos JSON para la implementación en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-109">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file tootest templates for deployment in Azure Stack.</span></span>
 - <span data-ttu-id="d4ccd-110">AzureStackCloudCapabilities_with_AddOns_20170627.json es un archivo predeterminado de funcionalidades de la nube.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-110">AzureStackCloudCapabilities_with_AddOns_20170627.json is a default cloud capabilities file.</span></span>  <span data-ttu-id="d4ccd-111">Puede crear sus propios o utilizar este tooget archivo iniciado.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-111">You can create your own, or use this file tooget started.</span></span> 

<span data-ttu-id="d4ccd-112">En este tema, ejecute la validación en las plantillas y, opcionalmente, genere un archivo de funcionalidades de la nube.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-112">In this topic, you run validation against your templates, and optionally build a cloud capabilities file.</span></span>

## <a name="validate-templates"></a><span data-ttu-id="d4ccd-113">Validar plantillas</span><span class="sxs-lookup"><span data-stu-id="d4ccd-113">Validate templates</span></span>
<span data-ttu-id="d4ccd-114">En estos pasos, valida plantillas mediante Hola módulo AzureRM.TemplateValidator PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-114">In these steps, you validate templates by using hello AzureRM.TemplateValidator PowerShell module.</span></span> <span data-ttu-id="d4ccd-115">Puede usar sus propias plantillas o validar hello [plantillas de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="d4ccd-115">You can use your own templates, or validate hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

1.  <span data-ttu-id="d4ccd-116">Importe el módulo de PowerShell de AzureRM.TemplateValidator.psm1 de hello:</span><span class="sxs-lookup"><span data-stu-id="d4ccd-116">Import hello AzureRM.TemplateValidator.psm1 PowerShell module:</span></span>
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  <span data-ttu-id="d4ccd-117">Ejecute el validador de plantilla hello:</span><span class="sxs-lookup"><span data-stu-id="d4ccd-117">Run hello template validator:</span></span>

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path tootemplate.json or template folder> `
    -CapabilitiesPath <path toocloudcapabilities.json> `
    -Verbose
    ```

<span data-ttu-id="d4ccd-118">Cualquier error o advertencia de validación de plantilla es registrados toohello consola de PowerShell y también es archivo HTML de tooan registrado en el directorio de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-118">Any template validation warnings or errors are logged toohello PowerShell console, and are also logged tooan HTML file in hello source directory.</span></span> <span data-ttu-id="d4ccd-119">Un ejemplo de salida de informe de validación de hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="d4ccd-119">An example of hello validation report output looks like this:</span></span>

![informe de validación de ejemplo](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a><span data-ttu-id="d4ccd-121">parameters</span><span class="sxs-lookup"><span data-stu-id="d4ccd-121">Parameters</span></span>

| <span data-ttu-id="d4ccd-122">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d4ccd-122">Parameter</span></span> | <span data-ttu-id="d4ccd-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="d4ccd-123">Description</span></span> | <span data-ttu-id="d4ccd-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d4ccd-124">Required</span></span> |
| ----- | -----| ----- |
| <span data-ttu-id="d4ccd-125">TemplatePath</span><span class="sxs-lookup"><span data-stu-id="d4ccd-125">TemplatePath</span></span> | <span data-ttu-id="d4ccd-126">Especifica toorecursively de ruta de acceso de hello buscar plantillas de administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="d4ccd-126">Specifies hello path toorecursively find Resource Manager templates</span></span> | <span data-ttu-id="d4ccd-127">Sí</span><span class="sxs-lookup"><span data-stu-id="d4ccd-127">Yes</span></span> | 
| <span data-ttu-id="d4ccd-128">TemplatePattern</span><span class="sxs-lookup"><span data-stu-id="d4ccd-128">TemplatePattern</span></span> | <span data-ttu-id="d4ccd-129">Especifica el nombre de Hola de toomatch de archivos de plantilla.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-129">Specifies hello name of template files toomatch.</span></span> | <span data-ttu-id="d4ccd-130">No</span><span class="sxs-lookup"><span data-stu-id="d4ccd-130">No</span></span> |
| <span data-ttu-id="d4ccd-131">CapabilitiesPath</span><span class="sxs-lookup"><span data-stu-id="d4ccd-131">CapabilitiesPath</span></span> | <span data-ttu-id="d4ccd-132">Especifica el archivo JSON capacidades de hello ruta de acceso toocloud</span><span class="sxs-lookup"><span data-stu-id="d4ccd-132">Specifies hello path toocloud capabilities JSON file</span></span> | <span data-ttu-id="d4ccd-133">Sí</span><span class="sxs-lookup"><span data-stu-id="d4ccd-133">Yes</span></span> | 
| <span data-ttu-id="d4ccd-134">IncludeComputeCapabilities</span><span class="sxs-lookup"><span data-stu-id="d4ccd-134">IncludeComputeCapabilities</span></span> | <span data-ttu-id="d4ccd-135">Incluye la evaluación de recursos de IaaS como tamaños de máquina virtual y extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d4ccd-135">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span></span> | <span data-ttu-id="d4ccd-136">No</span><span class="sxs-lookup"><span data-stu-id="d4ccd-136">No</span></span> |
| <span data-ttu-id="d4ccd-137">IncludeStorageCapabilities</span><span class="sxs-lookup"><span data-stu-id="d4ccd-137">IncludeStorageCapabilities</span></span> | <span data-ttu-id="d4ccd-138">Incluye la evaluación de recursos de almacenamiento como los tipos SKU</span><span class="sxs-lookup"><span data-stu-id="d4ccd-138">Includes evaluation of storage resources like SKU types</span></span> | <span data-ttu-id="d4ccd-139">No</span><span class="sxs-lookup"><span data-stu-id="d4ccd-139">No</span></span> |
| <span data-ttu-id="d4ccd-140">Informe</span><span class="sxs-lookup"><span data-stu-id="d4ccd-140">Report</span></span> | <span data-ttu-id="d4ccd-141">Especifica el nombre del programa Hola genera informes HTML</span><span class="sxs-lookup"><span data-stu-id="d4ccd-141">Specifies name of hello generated HTML report</span></span> | <span data-ttu-id="d4ccd-142">No</span><span class="sxs-lookup"><span data-stu-id="d4ccd-142">No</span></span> |
| <span data-ttu-id="d4ccd-143">Detallado</span><span class="sxs-lookup"><span data-stu-id="d4ccd-143">Verbose</span></span> | <span data-ttu-id="d4ccd-144">Registra errores y advertencias consola toohello</span><span class="sxs-lookup"><span data-stu-id="d4ccd-144">Logs errors and warnings toohello console</span></span> | <span data-ttu-id="d4ccd-145">No</span><span class="sxs-lookup"><span data-stu-id="d4ccd-145">No</span></span>|


### <a name="examples"></a><span data-ttu-id="d4ccd-146">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d4ccd-146">Examples</span></span>
<span data-ttu-id="d4ccd-147">En este ejemplo valida todos los hello [plantillas de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates) descargado localmente y también valida los tamaños de máquinas virtuales de Hola y extensiones con las funciones del Kit de desarrollo de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-147">This example validates all hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded locally, and also validates hello VM sizes and extensions against Azure Stack Development Kit capabilities.</span></span>

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a><span data-ttu-id="d4ccd-148">Genere el archivo de funcionalidades de la nube</span><span class="sxs-lookup"><span data-stu-id="d4ccd-148">Build cloud capabilities file</span></span>
<span data-ttu-id="d4ccd-149">los archivos descargados Hello incluyen un valor predeterminado *AzureStackCloudCapabilities_with_AddOns_20170627.json* archivo, que describe las versiones de servicio de hello disponibles en el Kit de desarrollo de pila de Azure con los servicios de PaaS instalados.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-149">hello downloaded files include a default *AzureStackCloudCapabilities_with_AddOns_20170627.json* file, which describes hello service versions available in Azure Stack Development Kit with PaaS services installed.</span></span>  <span data-ttu-id="d4ccd-150">Si instala a proveedores de recursos adicionales, puede usar hello toobuild de módulo de AzureRM.CloudCapabilities PowerShell un archivo JSON, incluidos los nuevos servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-150">If you install additional Resource Providers, you can use hello AzureRM.CloudCapabilities PowerShell module toobuild a JSON file including hello new services.</span></span>  

1.  <span data-ttu-id="d4ccd-151">Asegúrese de que tiene conectividad tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-151">Make sure you have connectivity tooAzure Stack.</span></span>  <span data-ttu-id="d4ccd-152">Estos pasos se pueden realizar desde el host de kit de desarrollo de Azure pila hello, o puede usar [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect desde su estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d4ccd-152">These steps can be performed from hello Azure Stack development kit host, or you can use [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect from your workstation.</span></span> 
2.  <span data-ttu-id="d4ccd-153">Hola de importar el módulo de AzureRM.CloudCapabilities PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d4ccd-153">Import hello AzureRM.CloudCapabilities PowerShell module:</span></span>

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  <span data-ttu-id="d4ccd-154">Utilizan versiones de hello CloudCapabilities Get cmdlet tooretrieve service y cree un archivo JSON de las capacidades de nube:</span><span class="sxs-lookup"><span data-stu-id="d4ccd-154">Use hello Get-CloudCapabilities cmdlet tooretrieve service versions and create a cloud capabilities JSON file:</span></span>

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a><span data-ttu-id="d4ccd-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4ccd-155">Next steps</span></span>
 - [<span data-ttu-id="d4ccd-156">Implementar plantillas tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="d4ccd-156">Deploy templates tooAzure Stack</span></span>](azure-stack-arm-templates.md)
 - <span data-ttu-id="d4ccd-157">[Desarrollar plantillas para Azure Stack] (azure-stack-develop-templates.md)</span><span class="sxs-lookup"><span data-stu-id="d4ccd-157">[Develop templates for Azure Stack] (azure-stack-develop-templates.md)</span></span>


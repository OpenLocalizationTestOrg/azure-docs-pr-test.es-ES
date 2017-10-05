---
title: "Extensión de script personalizado de Azure para Windows | Microsoft Docs"
description: "Automatización de tareas de configuración de máquinas virtuales Windows mediante la extensión de script personalizado"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: a6f417ea6575b81258998ae3b31c10e9df59b603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="86306-103">Extensión de la secuencia de comandos personalizada para Windows</span><span class="sxs-lookup"><span data-stu-id="86306-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="86306-104">La extensión de script personalizado descarga y ejecuta scripts en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="86306-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="86306-105">Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración.</span><span class="sxs-lookup"><span data-stu-id="86306-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="86306-106">Los scripts se pueden descargar desde Azure Storage o GitHub, o se pueden proporcionar a Azure Portal en el tiempo de ejecución de la extensión.</span><span class="sxs-lookup"><span data-stu-id="86306-106">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="86306-107">La extensión de script personalizado se integra con las plantillas de Azure Resource Manager y también se puede ejecutar mediante la CLI de Azure, PowerShell, Azure Portal o la API de REST de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="86306-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="86306-108">En este documento se detalla cómo usar la extensión de script personalizado mediante el módulo de Azure PowerShell y plantillas de Azure Resource Manager, y se detallan también los pasos para solucionar problemas en los sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="86306-108">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86306-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="86306-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="86306-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="86306-110">Operating System</span></span>

<span data-ttu-id="86306-111">La extensión de script personalizado para Windows se puede ejecutar en Windows Server 2008 R2, 2012, 2012 R2 y 2016.</span><span class="sxs-lookup"><span data-stu-id="86306-111">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="86306-112">Ubicación del script</span><span class="sxs-lookup"><span data-stu-id="86306-112">Script Location</span></span>

<span data-ttu-id="86306-113">El script debe almacenarse en Azure Blob Storage o en cualquier otra ubicación a la que se pueda tener acceso a través de una dirección URL válida.</span><span class="sxs-lookup"><span data-stu-id="86306-113">The script needs to be stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="86306-114">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="86306-114">Internet Connectivity</span></span>

<span data-ttu-id="86306-115">La extensión de script personalizado para Windows requiere que la máquina virtual de destino esté conectada a Internet.</span><span class="sxs-lookup"><span data-stu-id="86306-115">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="86306-116">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="86306-116">Extension schema</span></span>

<span data-ttu-id="86306-117">El siguiente JSON muestra el esquema para la extensión de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="86306-117">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="86306-118">La extensión requiere una ubicación de script (Azure Storage u otra ubicación con dirección URL válida) y un comando para ejecutar.</span><span class="sxs-lookup"><span data-stu-id="86306-118">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="86306-119">Si usa Azure Storage como origen del script, se requiere un nombre y una clave de cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="86306-119">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="86306-120">Estos elementos se deben tratar como datos confidenciales y se deben especificar en la configuración protegida de las extensiones.</span><span class="sxs-lookup"><span data-stu-id="86306-120">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="86306-121">Los datos de configuración protegida de la extensión de VM de Azure están cifrados y solo se descifran en la máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="86306-121">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
        "[variables('musicstoresqlName')]"
    ],
    "tags": {
        "displayName": "config-app"
    },
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="86306-122">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="86306-122">Property values</span></span>

| <span data-ttu-id="86306-123">Nombre</span><span class="sxs-lookup"><span data-stu-id="86306-123">Name</span></span> | <span data-ttu-id="86306-124">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="86306-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="86306-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="86306-125">apiVersion</span></span> | <span data-ttu-id="86306-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="86306-126">2015-06-15</span></span> |
| <span data-ttu-id="86306-127">publisher</span><span class="sxs-lookup"><span data-stu-id="86306-127">publisher</span></span> | <span data-ttu-id="86306-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="86306-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="86306-129">type</span><span class="sxs-lookup"><span data-stu-id="86306-129">type</span></span> | <span data-ttu-id="86306-130">extensions</span><span class="sxs-lookup"><span data-stu-id="86306-130">extensions</span></span> |
| <span data-ttu-id="86306-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="86306-131">typeHandlerVersion</span></span> | <span data-ttu-id="86306-132">1.9</span><span class="sxs-lookup"><span data-stu-id="86306-132">1.9</span></span> |
| <span data-ttu-id="86306-133">fileUris (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="86306-133">fileUris (e.g)</span></span> | <span data-ttu-id="86306-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="86306-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="86306-135">commandToExecute (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="86306-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="86306-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="86306-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="86306-137">storageAccountName (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="86306-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="86306-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="86306-138">examplestorageacct</span></span> |
| <span data-ttu-id="86306-139">storageAccountKey (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="86306-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="86306-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="86306-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="86306-141">**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="86306-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="86306-142">Use los nombres tal y como se ha mostrado anteriormente para evitar problemas de implementación.</span><span class="sxs-lookup"><span data-stu-id="86306-142">Use the names as seen above to avoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="86306-143">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="86306-143">Template deployment</span></span>

<span data-ttu-id="86306-144">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86306-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="86306-145">El esquema JSON detallado en la sección anterior se puede usar en una plantilla de Azure Resource Manager para ejecutar la extensión de script personalizado durante la implementación de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86306-145">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="86306-146">Aquí ([GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)) puede encontrar una plantilla de ejemplo que incluye la extensión de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="86306-146">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="86306-147">Implementación de PowerShell</span><span class="sxs-lookup"><span data-stu-id="86306-147">PowerShell deployment</span></span>

<span data-ttu-id="86306-148">El comando `Set-AzureRmVMCustomScriptExtension` se puede usar para agregar la extensión de script personalizado a una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="86306-148">The `Set-AzureRmVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="86306-149">Para más información, consulte [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="86306-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="86306-150">Solución de problemas y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="86306-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="86306-151">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="86306-151">Troubleshoot</span></span>

<span data-ttu-id="86306-152">Los datos sobre el estado de las implementaciones de extensiones pueden recuperarse desde Azure Portal y mediante el módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86306-152">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="86306-153">Para ver el estado de implementación de las extensiones de una VM determinada, ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="86306-153">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="86306-154">La salida de la ejecución de las extensiones se registra en los archivos que se encuentran en el siguiente directorio de la máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="86306-154">Extension execution output is logged to files found under the following directory on the target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="86306-155">Los archivos especificados se descargan en el siguiente directorio de la máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="86306-155">The specified files are downloaded into the following directory on the target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="86306-156">donde `<n>` es un entero decimal que puede variar entre las ejecuciones de la extensión.</span><span class="sxs-lookup"><span data-stu-id="86306-156">where `<n>` is a decimal integer which may change between executions of the extension.</span></span>  <span data-ttu-id="86306-157">El valor `1.*` coincide con el valor `typeHandlerVersion` actual y real de la extensión.</span><span class="sxs-lookup"><span data-stu-id="86306-157">The `1.*` value matches the actual, current `typeHandlerVersion` value of the extension.</span></span>  <span data-ttu-id="86306-158">Por ejemplo, el directorio real podría ser `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="86306-158">For example, the actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="86306-159">Cuando se ejecute el comando `commandToExecute`, la extensión tendrá establecido este directorio (por ejemplo, `...\Downloads\2`) como directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="86306-159">When executing the `commandToExecute` command, the extension will have set this directory (e.g., `...\Downloads\2`) as the current working directory.</span></span> <span data-ttu-id="86306-160">Esto permite el uso de rutas de acceso relativas para buscar los archivos descargados a través de la propiedad `fileURIs`.</span><span class="sxs-lookup"><span data-stu-id="86306-160">This enables the use of relative paths to locate the files downloaded via the `fileURIs` property.</span></span> <span data-ttu-id="86306-161">En la tabla siguiente se muestran algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="86306-161">See the table below for examples.</span></span>

<span data-ttu-id="86306-162">Dado que la ruta de acceso absoluta de descarga puede variar con el paso del tiempo, es mejor optar por rutas de acceso relativas de archivo o script en la cadena `commandToExecute`, siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="86306-162">Since the absolute download path may vary over time, it is better to opt for relative script/file paths in the `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="86306-163">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86306-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="86306-164">La información de ruta de acceso después del primer segmento de URI se conserva para los archivos descargados a través de la lista de propiedades `fileUris`.</span><span class="sxs-lookup"><span data-stu-id="86306-164">Path information after the first URI segment is retained for files downloaded via the `fileUris` property list.</span></span>  <span data-ttu-id="86306-165">Como se muestra en la tabla siguiente, los archivos descargados se asignan en los subdirectorios de descarga para reflejar la estructura de los valores `fileUris`.</span><span class="sxs-lookup"><span data-stu-id="86306-165">As shown in the table below, downloaded files are mapped into download subdirectories to reflect the structure of the `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="86306-166">Ejemplos de archivos descargados</span><span class="sxs-lookup"><span data-stu-id="86306-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="86306-167">URI en fileUris</span><span class="sxs-lookup"><span data-stu-id="86306-167">URI in fileUris</span></span> | <span data-ttu-id="86306-168">Ubicación descargada relativa</span><span class="sxs-lookup"><span data-stu-id="86306-168">Relative downloaded location</span></span> | <span data-ttu-id="86306-169">Ubicación descargada absoluta *</span><span class="sxs-lookup"><span data-stu-id="86306-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="86306-170">\*Como anteriormente, las rutas de acceso absolutas al directorio cambiarán a lo largo del ciclo de vida de la VM, pero no dentro de una ejecución única de la extensión CustomScript.</span><span class="sxs-lookup"><span data-stu-id="86306-170">\* As above, the absolute directory paths will change over the lifetime of the VM, but not within a single execution of the CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="86306-171">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="86306-171">Support</span></span>

<span data-ttu-id="86306-172">Si necesita más ayuda con cualquier aspecto de este artículo, puede ponerse en contacto con los expertos de Azure en los [foros de MSDN Azure y Stack Overflow] (https://azure.microsoft.com/es-es/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="86306-172">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="86306-173">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="86306-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="86306-174">Vaya al [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione Obtener soporte.</span><span class="sxs-lookup"><span data-stu-id="86306-174">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="86306-175">Para obtener información sobre el uso del soporte técnico, lea las [Preguntas más frecuentes de soporte técnico de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="86306-175">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

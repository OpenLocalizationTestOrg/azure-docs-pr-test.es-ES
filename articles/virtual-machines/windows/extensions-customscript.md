---
title: "aaaAzure extensión del Script personalizado para Windows | Documentos de Microsoft"
description: "Automatizar tareas de configuración de máquina virtual de Windows con la extensión de Script personalizado de Hola"
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
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="32356-103">Extensión de la secuencia de comandos personalizada para Windows</span><span class="sxs-lookup"><span data-stu-id="32356-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="32356-104">Extensión de Script personalizado de Hello descarga y ejecuta scripts en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="32356-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="32356-105">Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración.</span><span class="sxs-lookup"><span data-stu-id="32356-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="32356-106">Las secuencias de comandos pueden descargarse desde el almacenamiento de Azure o GitHub, o proporcionarse toohello portal de Azure en tiempo de ejecución de extensión.</span><span class="sxs-lookup"><span data-stu-id="32356-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="32356-107">Hola extensión de Script personalizado se integra con plantillas de Azure Resource Manager y también se puede ejecutar mediante Hola CLI de Azure, PowerShell, portal de Azure u Hola API de REST de máquina Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="32356-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="32356-108">Este documento detalla cómo toouse Hola extensión de Script personalizado utilizando Hola módulo Azure PowerShell, las plantillas de administrador de recursos de Azure y detalles de la solución de problemas de pasos en los sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="32356-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32356-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="32356-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="32356-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="32356-110">Operating System</span></span>

<span data-ttu-id="32356-111">Hola extensión de Script personalizado para Windows se pueden ejecutar en Windows Server 2008 R2, 2012, 2012 R2 y 2016 libera.</span><span class="sxs-lookup"><span data-stu-id="32356-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="32356-112">Ubicación del script</span><span class="sxs-lookup"><span data-stu-id="32356-112">Script Location</span></span>

<span data-ttu-id="32356-113">script de Hola debe toobe almacenado en almacenamiento de blobs de Azure, o cualquier otra ubicación accesible a través de una dirección URL válida.</span><span class="sxs-lookup"><span data-stu-id="32356-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="32356-114">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="32356-114">Internet Connectivity</span></span>

<span data-ttu-id="32356-115">Hello extensión para ventanas de Script personalizado requiere esa máquina virtual de destino de hello es toohello conectado internet.</span><span class="sxs-lookup"><span data-stu-id="32356-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="32356-116">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="32356-116">Extension schema</span></span>

<span data-ttu-id="32356-117">Hello JSON siguiente muestra esquema Hola Hola extensión de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="32356-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="32356-118">extensión de Hello requiere una ubicación de la secuencia de comandos (almacenamiento de Azure u otra ubicación con dirección URL válida) y un tooexecute de comando.</span><span class="sxs-lookup"><span data-stu-id="32356-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="32356-119">Si utiliza almacenamiento de Azure como origen de la secuencia de comandos de hello, se requiere una clave de nombre y la cuenta de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="32356-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="32356-120">Estos elementos se deben tratar como datos confidenciales y especificados en la configuración de configuración protegida de extensiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="32356-121">Datos de configuración de extensión protegido de VM de Azure cifrados y solo descifrados en la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="32356-122">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="32356-122">Property values</span></span>

| <span data-ttu-id="32356-123">Nombre</span><span class="sxs-lookup"><span data-stu-id="32356-123">Name</span></span> | <span data-ttu-id="32356-124">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="32356-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="32356-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="32356-125">apiVersion</span></span> | <span data-ttu-id="32356-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="32356-126">2015-06-15</span></span> |
| <span data-ttu-id="32356-127">publisher</span><span class="sxs-lookup"><span data-stu-id="32356-127">publisher</span></span> | <span data-ttu-id="32356-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="32356-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="32356-129">type</span><span class="sxs-lookup"><span data-stu-id="32356-129">type</span></span> | <span data-ttu-id="32356-130">extensions</span><span class="sxs-lookup"><span data-stu-id="32356-130">extensions</span></span> |
| <span data-ttu-id="32356-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="32356-131">typeHandlerVersion</span></span> | <span data-ttu-id="32356-132">1.9</span><span class="sxs-lookup"><span data-stu-id="32356-132">1.9</span></span> |
| <span data-ttu-id="32356-133">fileUris (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="32356-133">fileUris (e.g)</span></span> | <span data-ttu-id="32356-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="32356-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="32356-135">commandToExecute (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="32356-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="32356-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="32356-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="32356-137">storageAccountName (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="32356-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="32356-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="32356-138">examplestorageacct</span></span> |
| <span data-ttu-id="32356-139">storageAccountKey (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="32356-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="32356-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="32356-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="32356-141">**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="32356-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="32356-142">Utilice nombres de hello tal como se muestra anteriormente tooavoid problemas de implementación.</span><span class="sxs-lookup"><span data-stu-id="32356-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="32356-143">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="32356-143">Template deployment</span></span>

<span data-ttu-id="32356-144">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="32356-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="32356-145">esquema JSON de Hello detallado en la sección anterior de hello puede usarse en un hello toorun de plantilla de Azure Resource Manager extensión de Script personalizado durante la implementación de plantilla Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="32356-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="32356-146">Una plantilla de ejemplo que incluya Hola extensión de Script personalizado puede encontrarse aquí, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="32356-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="32356-147">Implementación de PowerShell</span><span class="sxs-lookup"><span data-stu-id="32356-147">PowerShell deployment</span></span>

<span data-ttu-id="32356-148">Hola `Set-AzureRmVMCustomScriptExtension` comando puede ser usado tooadd Hola Script personalizado extensión tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="32356-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="32356-149">Para más información, consulte [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="32356-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="32356-150">Solución de problemas y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="32356-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="32356-151">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="32356-151">Troubleshoot</span></span>

<span data-ttu-id="32356-152">Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el módulo de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="32356-153">estado de implementación de hello toosee de extensiones para una máquina virtual determinada, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="32356-154">Ejecución de la extensión de salida es toofiles registrado en hello posterior directorio en la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="32356-155">Hola especifica los archivos se descargan en hello después de directorio en la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="32356-156">donde `<n>` es un entero decimal que puede variar entre las ejecuciones de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="32356-157">Hola `1.*` Hola real, actual coincide con el valor `typeHandlerVersion` valor de extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="32356-158">Por ejemplo, pudieron ser reales del directorio hello `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="32356-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="32356-159">Al ejecutar hello `commandToExecute` comando extensión Hola activados este directorio (p. ej., `...\Downloads\2`) como directorio de trabajo actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="32356-160">Este uso de hello habilita de archivos de rutas de acceso relativas toolocate Hola descarga a través de hello `fileURIs` propiedad.</span><span class="sxs-lookup"><span data-stu-id="32356-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="32356-161">Consulte la tabla de hello siguiente para obtener ejemplos.</span><span class="sxs-lookup"><span data-stu-id="32356-161">See hello table below for examples.</span></span>

<span data-ttu-id="32356-162">Puesto que la ruta de acceso de descarga absoluta Hola puede variar con el tiempo, es mejor tooopt para rutas de acceso de archivo o script relativa en hello `commandToExecute` cadena, siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="32356-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="32356-163">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32356-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="32356-164">Información de ruta de acceso después de que se conserva el primer segmento URI Hola para los archivos se descarga a través de Hola `fileUris` lista de propiedades.</span><span class="sxs-lookup"><span data-stu-id="32356-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="32356-165">Tal y como se muestra en la siguiente tabla se hello, archivos descargados se asignan a la estructura de descarga subdirectorios tooreflect Hola de hello `fileUris` valores.</span><span class="sxs-lookup"><span data-stu-id="32356-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="32356-166">Ejemplos de archivos descargados</span><span class="sxs-lookup"><span data-stu-id="32356-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="32356-167">URI en fileUris</span><span class="sxs-lookup"><span data-stu-id="32356-167">URI in fileUris</span></span> | <span data-ttu-id="32356-168">Ubicación descargada relativa</span><span class="sxs-lookup"><span data-stu-id="32356-168">Relative downloaded location</span></span> | <span data-ttu-id="32356-169">Ubicación descargada absoluta *</span><span class="sxs-lookup"><span data-stu-id="32356-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="32356-170">\*Como anteriormente, las rutas de acceso absoluta al directorio de hello cambia con el período de duración de Hola de hello VM, pero no dentro de una ejecución única de la extensión CustomScript de Hola.</span><span class="sxs-lookup"><span data-stu-id="32356-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="32356-171">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="32356-171">Support</span></span>

<span data-ttu-id="32356-172">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="32356-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="32356-173">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="32356-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="32356-174">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="32356-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="32356-175">Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="32356-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

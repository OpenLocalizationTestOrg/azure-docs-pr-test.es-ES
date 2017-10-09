---
title: "aaaCustom extensión de Script en una máquina virtual de Windows | Documentos de Microsoft"
description: "Automatizar tareas de configuración de máquina virtual de Azure mediante scripts de PowerShell de toorun de extensión de Script personalizado de hello en una máquina virtual de Windows remoto"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="483d2-103">Script extensión para ventanas personalizadas mediante el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="483d2-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="483d2-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="483d2-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="483d2-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="483d2-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="483d2-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="483d2-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="483d2-107">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="483d2-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="483d2-108">Extensión de Script personalizado de Hello descarga y ejecuta scripts en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="483d2-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="483d2-109">Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración.</span><span class="sxs-lookup"><span data-stu-id="483d2-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="483d2-110">Las secuencias de comandos pueden descargarse desde el almacenamiento de Azure o GitHub, o proporcionarse toohello portal de Azure en tiempo de ejecución de extensión.</span><span class="sxs-lookup"><span data-stu-id="483d2-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="483d2-111">Hola extensión de Script personalizado se integra con plantillas de Azure Resource Manager y también se puede ejecutar mediante Hola CLI de Azure, PowerShell, portal de Azure u Hola API de REST de máquina Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="483d2-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="483d2-112">Este documento detalla cómo toouse Hola extensión de Script personalizado utilizando Hola módulo Azure PowerShell, las plantillas de administrador de recursos de Azure y detalles de la solución de problemas de pasos en los sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="483d2-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="483d2-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="483d2-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="483d2-114">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="483d2-114">Operating System</span></span>

<span data-ttu-id="483d2-115">Hola extensión de Script personalizado para Windows se pueden ejecutar en Windows Server 2008 R2, 2012, 2012 R2 y 2016 libera.</span><span class="sxs-lookup"><span data-stu-id="483d2-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="483d2-116">Ubicación del script</span><span class="sxs-lookup"><span data-stu-id="483d2-116">Script Location</span></span>

<span data-ttu-id="483d2-117">script de Hola debe toobe almacenado en almacenamiento de Azure, o cualquier otra ubicación accesible a través de una dirección URL válida.</span><span class="sxs-lookup"><span data-stu-id="483d2-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="483d2-118">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="483d2-118">Internet Connectivity</span></span>

<span data-ttu-id="483d2-119">Hello extensión para ventanas de Script personalizado requiere esa máquina virtual de destino de hello es toohello conectado internet.</span><span class="sxs-lookup"><span data-stu-id="483d2-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="483d2-120">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="483d2-120">Extension schema</span></span>

<span data-ttu-id="483d2-121">Hello JSON siguiente muestra esquema Hola Hola extensión de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="483d2-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="483d2-122">extensión de Hello requiere una ubicación de la secuencia de comandos (almacenamiento de Azure u otra ubicación con dirección URL válida) y un tooexecute de comando.</span><span class="sxs-lookup"><span data-stu-id="483d2-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="483d2-123">Si utiliza almacenamiento de Azure como origen de la secuencia de comandos de hello, se requiere una clave de nombre y la cuenta de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="483d2-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="483d2-124">Estos elementos se deben tratar como datos confidenciales y especificados en la configuración de configuración protegida de extensiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="483d2-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="483d2-125">Datos de configuración de extensión protegido de VM de Azure cifrados y solo descifrados en la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="483d2-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="483d2-126">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="483d2-126">Property values</span></span>

| <span data-ttu-id="483d2-127">Nombre</span><span class="sxs-lookup"><span data-stu-id="483d2-127">Name</span></span> | <span data-ttu-id="483d2-128">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="483d2-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="483d2-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="483d2-129">apiVersion</span></span> | <span data-ttu-id="483d2-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="483d2-130">2015-06-15</span></span> |
| <span data-ttu-id="483d2-131">publisher</span><span class="sxs-lookup"><span data-stu-id="483d2-131">publisher</span></span> | <span data-ttu-id="483d2-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="483d2-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="483d2-133">extensión</span><span class="sxs-lookup"><span data-stu-id="483d2-133">extension</span></span> | <span data-ttu-id="483d2-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="483d2-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="483d2-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="483d2-135">typeHandlerVersion</span></span> | <span data-ttu-id="483d2-136">1.8</span><span class="sxs-lookup"><span data-stu-id="483d2-136">1.8</span></span> |
| <span data-ttu-id="483d2-137">fileUris (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="483d2-137">fileUris (e.g)</span></span> | <span data-ttu-id="483d2-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="483d2-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="483d2-139">commandToExecute (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="483d2-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="483d2-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="483d2-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="483d2-141">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="483d2-141">Template deployment</span></span>

<span data-ttu-id="483d2-142">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="483d2-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="483d2-143">esquema JSON de Hello detallado en la sección anterior de hello puede usarse en un hello toorun de plantilla de Azure Resource Manager extensión de Script personalizado durante la implementación de plantilla Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="483d2-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="483d2-144">Una plantilla de ejemplo que incluya Hola extensión de Script personalizado puede encontrarse aquí, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="483d2-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="483d2-145">Implementación de PowerShell</span><span class="sxs-lookup"><span data-stu-id="483d2-145">PowerShell deployment</span></span>

<span data-ttu-id="483d2-146">Hola `Set-AzureVMCustomScriptExtension` comando puede ser usado tooadd Hola Script personalizado extensión tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="483d2-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="483d2-147">Para más información, consulte [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="483d2-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="483d2-148">Solución de problemas y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="483d2-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="483d2-149">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="483d2-149">Troubleshoot</span></span>

<span data-ttu-id="483d2-150">Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el módulo de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="483d2-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="483d2-151">estado de implementación de hello toosee de extensiones para una máquina virtual determinada, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="483d2-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="483d2-152">Ejecución de la extensión de salida nos registrado toofiles encuentra Hola después de directorio en la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="483d2-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="483d2-153">script de Hola se descarga en hello después de directorio en la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="483d2-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="483d2-154">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="483d2-154">Support</span></span>

<span data-ttu-id="483d2-155">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="483d2-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="483d2-156">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="483d2-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="483d2-157">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="483d2-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="483d2-158">Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="483d2-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>

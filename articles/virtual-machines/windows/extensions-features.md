---
title: "aaaVirtual máquina extensiones y características de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué extensiones están disponibles para máquinas virtuales de Azure, agrupadas por lo que proporcionan o mejoran."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="e3c94-103">Características y extensiones de las máquinas virtuales para Windows</span><span class="sxs-lookup"><span data-stu-id="e3c94-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="e3c94-104">Las extensiones de máquina virtual de Azure son pequeñas aplicaciones que realizan tareas de automatización y configuración posterior a la implementación en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c94-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="e3c94-105">Por ejemplo, si una máquina virtual requiere la instalación de software, la protección antivirus o configuración de Docker, una extensión de máquina virtual puede ser usado toocomplete estas tareas.</span><span class="sxs-lookup"><span data-stu-id="e3c94-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="e3c94-106">Extensiones de VM de Azure pueden realizarse mediante el uso de hello CLI de Azure, PowerShell, plantillas de Azure Resource Manager y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c94-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="e3c94-107">Las extensiones pueden empaquetar con una nueva implementación de máquina virtual o se pueden ejecutar en cualquier sistema existente.</span><span class="sxs-lookup"><span data-stu-id="e3c94-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="e3c94-108">Este documento proporciona información general sobre las extensiones de máquina virtual, requisitos previos para usar las extensiones de máquina virtual e instrucciones sobre cómo administrar toodetect y quitar extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e3c94-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="e3c94-109">Este documento proporciona información generalizada porque muchas extensiones de máquina virtual están disponibles, cada una con una configuración potencialmente única.</span><span class="sxs-lookup"><span data-stu-id="e3c94-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="e3c94-110">Los detalles específicos de una extensión pueden encontrarse en cada extensión individuales toohello específico de documento.</span><span class="sxs-lookup"><span data-stu-id="e3c94-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="e3c94-111">Casos de uso y ejemplos</span><span class="sxs-lookup"><span data-stu-id="e3c94-111">Use cases and samples</span></span>

<span data-ttu-id="e3c94-112">Hay muchas extensiones de máquina virtual de Azure diferentes disponibles, cada una con un caso de uso específico.</span><span class="sxs-lookup"><span data-stu-id="e3c94-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="e3c94-113">Algunos casos de uso de ejemplo son:</span><span class="sxs-lookup"><span data-stu-id="e3c94-113">Some example use cases are:</span></span>

- <span data-ttu-id="e3c94-114">Máquina virtual de estado deseado de PowerShell configuraciones tooa se aplican mediante el uso de extensión de DSC de Hola para Windows.</span><span class="sxs-lookup"><span data-stu-id="e3c94-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="e3c94-115">Para obtener más información, consulte la sección sobre la [extensión de configuración de estado deseado de Azure](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e3c94-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="e3c94-116">Configurar la supervisión de la máquina virtual con la extensión de máquina virtual de agente de supervisión de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="e3c94-117">Para obtener más información, consulte [tooLog de máquinas virtuales de Azure conectarse análisis](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e3c94-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="e3c94-118">Configurar la supervisión de la infraestructura de Azure con hello Datadog extensión.</span><span class="sxs-lookup"><span data-stu-id="e3c94-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="e3c94-119">Para obtener más información, vea hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="e3c94-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="e3c94-120">Configure una máquina virtual de Azure mediante Chef.</span><span class="sxs-lookup"><span data-stu-id="e3c94-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="e3c94-121">Para obtener más información, consulte [Automatización de la implementación de la máquina virtual de Azure con Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="e3c94-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="e3c94-122">Además extensiones específicas de tooprocess, una extensión de Script personalizado está disponible para máquinas virtuales Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="e3c94-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="e3c94-123">extensión de Script personalizado para Windows Hello permite cualquier toobe de script de PowerShell que ejecute en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e3c94-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="e3c94-124">Esto resulta útil al diseñar implementaciones de Azure que requieren una configuración más allá de lo que las herramientas de Azure nativas pueden proporcionar.</span><span class="sxs-lookup"><span data-stu-id="e3c94-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="e3c94-125">Para obtener más información, consulte la sección sobre la [extensión de script personalizado de máquina virtual Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e3c94-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e3c94-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e3c94-126">Prerequisites</span></span>

<span data-ttu-id="e3c94-127">Cada extensión de máquina virtual puede tener su propio conjunto de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="e3c94-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="e3c94-128">Por ejemplo, hello extensión de máquina virtual Docker tiene un requisito previo de la distribución de Linux compatible.</span><span class="sxs-lookup"><span data-stu-id="e3c94-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="e3c94-129">Requisitos de extensiones individuales se detallan en la documentación específica de la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="e3c94-130">Agente de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="e3c94-130">Azure VM agent</span></span>
<span data-ttu-id="e3c94-131">agente de máquina virtual de Azure de Hello administra la interacción entre una máquina virtual de Azure y el controlador de tejido de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="e3c94-132">agente de máquina virtual de Hello es responsable de muchos aspectos funcionales de la implementación y administración de máquinas virtuales de Azure, incluida la ejecución de extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e3c94-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="e3c94-133">agente de máquina virtual de Azure de Hello está preinstalado en imágenes de Azure Marketplace y se puede instalar en sistemas operativos compatibles.</span><span class="sxs-lookup"><span data-stu-id="e3c94-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="e3c94-134">Para obtener información sobre las instrucciones de instalación y los sistemas operativos compatibles, consulte [Agente de máquina virtual de Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e3c94-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="e3c94-135">Detección de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e3c94-135">Discover VM extensions</span></span>
<span data-ttu-id="e3c94-136">Hay muchas extensiones de máquina virtual diferentes disponibles para su uso con máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c94-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="e3c94-137">toosee una lista completa, ejecute hello siguiente comando con el módulo de PowerShell de administrador de recursos de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="e3c94-138">Establecer ubicación de hello deseado de toospecify seguro de si ejecuta este comando.</span><span class="sxs-lookup"><span data-stu-id="e3c94-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="e3c94-139">Ejecución de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e3c94-139">Run VM extensions</span></span>

<span data-ttu-id="e3c94-140">Extensiones de máquina virtual de Azure se pueden ejecutar en máquinas virtuales existentes, lo que resulta útil cuando necesita cambios de configuración de toomake o recuperar conectividad en una máquina virtual ya implementada.</span><span class="sxs-lookup"><span data-stu-id="e3c94-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="e3c94-141">Las extensiones de máquina virtual también pueden agruparse con las implementaciones de plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e3c94-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="e3c94-142">Mediante el uso de las extensiones con plantillas de administrador de recursos, puede habilitar máquinas virtuales de Azure toobe implementado y configurado sin necesidad de hello sea necesaria la intervención posterior a la implementación.</span><span class="sxs-lookup"><span data-stu-id="e3c94-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="e3c94-143">Hola siguiendo métodos puede ser toorun usa una extensión en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="e3c94-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="e3c94-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3c94-144">PowerShell</span></span>

<span data-ttu-id="e3c94-145">Existen varios comandos de PowerShell para ejecutar extensiones individuales.</span><span class="sxs-lookup"><span data-stu-id="e3c94-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="e3c94-146">toosee una lista, ejecute hello siga los comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3c94-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="e3c94-147">Esto proporciona la siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="e3c94-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="e3c94-148">Hello en el ejemplo siguiente se usa toodownload de extensión de Script personalizado de hello una secuencia de comandos desde un repositorio de GitHub en la máquina virtual de destino de hello y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="e3c94-149">Para obtener más información sobre la extensión de Script personalizado de hello, consulte [Introducción a la extensión Script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e3c94-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="e3c94-150">En este ejemplo, hello extensión de acceso de VM es la contraseña administrativa de hello tooreset utilizadas de una máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="e3c94-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="e3c94-151">Para obtener más información sobre Hola extensión de acceso a máquinas virtuales, consulte [servicio de restablecimiento de escritorio remoto en una VM de Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="e3c94-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="e3c94-152">Hola `Set-AzureRmVMExtension` comando puede ser usado toostart cualquier extensión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e3c94-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="e3c94-153">Para obtener más información, vea hello [referencia de conjunto AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3c94-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="e3c94-154">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e3c94-154">Azure portal</span></span>

<span data-ttu-id="e3c94-155">Una extensión de máquina virtual puede ser tooan aplicada de máquina virtual existente a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c94-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="e3c94-156">toodo por lo tanto, seleccione la máquina virtual de hello desea toouse, elija **extensiones**y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3c94-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="e3c94-157">Esto proporciona una lista de extensiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="e3c94-157">This provides a list of available extensions.</span></span> <span data-ttu-id="e3c94-158">Seleccione Hola uno que desee y siga los pasos de hello en el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="e3c94-159">Hello siguiente imagen muestra instalación Hola de hello extensión de Microsoft Antimalware de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c94-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![Instalar la extensión de antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="e3c94-161">Plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3c94-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="e3c94-162">Extensiones de máquina virtual pueden ser plantilla de Azure Resource Manager tooan agregada y ejecutan con la implementación de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="e3c94-163">La implementación de extensiones con una plantilla es útil para crear implementaciones de Azure completamente configuradas.</span><span class="sxs-lookup"><span data-stu-id="e3c94-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="e3c94-164">Por ejemplo, hello que JSON siguiente procede de una plantilla de administrador de recursos que implementa un conjunto de máquinas virtuales de equilibrio de carga y una base de datos de SQL Azure y, a continuación, instala una aplicación de .NET Core en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e3c94-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="e3c94-165">Hola extensión de máquina virtual se encarga de la instalación de software de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="e3c94-166">Para obtener más información, vea hello [plantilla de administrador de recursos completo](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="e3c94-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="e3c94-167">Para obtener más información, consulte [Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="e3c94-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="e3c94-168">Protección de datos de extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e3c94-168">Secure VM extension data</span></span>

<span data-ttu-id="e3c94-169">Si estás ejecutando una extensión de máquina virtual, puede ser necesario tooinclude información confidencial, como las credenciales y los nombres de cuenta de almacenamiento, las teclas de acceso de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e3c94-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="e3c94-170">Muchas de las extensiones de VM incluyen una configuración protegida, que cifra los datos y los descifra solo dentro de la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="e3c94-171">Cada extensión tiene un esquema específico de configuración protegida que se detallará en la documentación específica de extensión.</span><span class="sxs-lookup"><span data-stu-id="e3c94-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e3c94-172">Hola de ejemplo siguiente muestra una instancia de hello extensión de Script personalizado para Windows.</span><span class="sxs-lookup"><span data-stu-id="e3c94-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="e3c94-173">Tenga en cuenta que tooexecute de comando hello incluye un conjunto de credenciales.</span><span class="sxs-lookup"><span data-stu-id="e3c94-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="e3c94-174">En este ejemplo, no se cifrarán Hola comando tooexecute.</span><span class="sxs-lookup"><span data-stu-id="e3c94-174">In this example, hello command tooexecute will not be encrypted.</span></span>


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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="e3c94-175">Proteger la cadena de ejecución de hello moviendo hello **comando tooexecute** propiedad toohello **protegido** configuración.</span><span class="sxs-lookup"><span data-stu-id="e3c94-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="e3c94-176">Solución de problemas de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e3c94-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="e3c94-177">Cada extensión de máquina virtual puede tener unos pasos de solución de problemas específicos.</span><span class="sxs-lookup"><span data-stu-id="e3c94-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="e3c94-178">Por ejemplo, cuando se usa la extensión de Script personalizado de hello, detalles de ejecución de script encontrará localmente en la máquina virtual de hello en el que se ejecutó la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="e3c94-179">Todos los pasos de solución de problemas específicos de extensión aparecen detallados en la documentación específica de extensión.</span><span class="sxs-lookup"><span data-stu-id="e3c94-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e3c94-180">Hola siguiendo los pasos de solución de problemas aplica tooall extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e3c94-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="e3c94-181">Consulta del estado de la extensión</span><span class="sxs-lookup"><span data-stu-id="e3c94-181">View extension status</span></span>

<span data-ttu-id="e3c94-182">Después de una extensión de máquina virtual se ha ejecutado en una máquina virtual, use Hola siguiendo el estado de extensión de tooreturn de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3c94-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="e3c94-183">Reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="e3c94-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="e3c94-184">Hola `Name` parámetro toma el nombre de hello dado toohello extensión en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e3c94-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="e3c94-185">salida de Hello aspecto Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e3c94-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="e3c94-186">Estado de ejecución de extensión también puede encontrarse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c94-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="e3c94-187">estado de hello tooview de una extensión, la máquina virtual de hello seleccione, elija **extensiones**, y seleccione Hola extensión deseada.</span><span class="sxs-lookup"><span data-stu-id="e3c94-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="e3c94-188">Repetición de ejecución de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e3c94-188">Rerun VM extensions</span></span>

<span data-ttu-id="e3c94-189">Puede haber casos en que una extensión de máquina virtual necesita toobe vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="e3c94-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="e3c94-190">Para ello, quite la extensión hello y, a continuación, volver a ejecutar la extensión de hello con un método de ejecución de su elección.</span><span class="sxs-lookup"><span data-stu-id="e3c94-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="e3c94-191">tooremove una extensión, ejecute hello siguiente comando con el módulo de Azure PowerShell Hola.</span><span class="sxs-lookup"><span data-stu-id="e3c94-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="e3c94-192">Reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="e3c94-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="e3c94-193">También se puede quitar una extensión mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c94-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="e3c94-194">toodo para:</span><span class="sxs-lookup"><span data-stu-id="e3c94-194">toodo so:</span></span>

1. <span data-ttu-id="e3c94-195">Seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e3c94-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="e3c94-196">Seleccione **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="e3c94-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="e3c94-197">Elija la extensión de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="e3c94-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="e3c94-198">Seleccione **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="e3c94-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="e3c94-199">Referencia de extensiones de máquina virtual comunes</span><span class="sxs-lookup"><span data-stu-id="e3c94-199">Common VM extensions reference</span></span>
| <span data-ttu-id="e3c94-200">Nombre de la extensión</span><span class="sxs-lookup"><span data-stu-id="e3c94-200">Extension name</span></span> | <span data-ttu-id="e3c94-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="e3c94-201">Description</span></span> | <span data-ttu-id="e3c94-202">Más información</span><span class="sxs-lookup"><span data-stu-id="e3c94-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3c94-203">Extensión de la secuencia de comandos personalizada para Windows</span><span class="sxs-lookup"><span data-stu-id="e3c94-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="e3c94-204">Ejecución de scripts en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="e3c94-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="e3c94-205">Extensión de la secuencia de comandos personalizada para Windows</span><span class="sxs-lookup"><span data-stu-id="e3c94-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e3c94-206">Extensión de DSC para Windows</span><span class="sxs-lookup"><span data-stu-id="e3c94-206">DSC Extension for Windows</span></span> |<span data-ttu-id="e3c94-207">Extensión DSC (configuración de estado deseado) de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3c94-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="e3c94-208">Extensión DSC para Windows</span><span class="sxs-lookup"><span data-stu-id="e3c94-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e3c94-209">Extensión de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="e3c94-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="e3c94-210">Administración de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="e3c94-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="e3c94-211">Extensión de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="e3c94-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="e3c94-212">Extensión de acceso a máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="e3c94-212">Azure VM Access Extension</span></span> |<span data-ttu-id="e3c94-213">Administración de usuarios y credenciales</span><span class="sxs-lookup"><span data-stu-id="e3c94-213">Manage users and credentials</span></span> |[<span data-ttu-id="e3c94-214">Extensión de acceso a máquina virtual para Linux</span><span class="sxs-lookup"><span data-stu-id="e3c94-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |

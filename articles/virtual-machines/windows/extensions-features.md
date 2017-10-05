---
title: "Características y extensiones de máquinas virtuales para Windows en Azure | Microsoft Docs"
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
ms.openlocfilehash: 1ce0eebd2585c9457d7f922898d7f2fa3e7ffad7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="a67e0-103">Características y extensiones de las máquinas virtuales para Windows</span><span class="sxs-lookup"><span data-stu-id="a67e0-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="a67e0-104">Las extensiones de máquina virtual de Azure son pequeñas aplicaciones que realizan tareas de automatización y configuración posterior a la implementación en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="a67e0-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="a67e0-105">Por ejemplo, si una máquina virtual necesita que se instale software, protección antivirus o configuración de Docker, se puede usar una extensión de máquina virtual para completar estas tareas.</span><span class="sxs-lookup"><span data-stu-id="a67e0-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="a67e0-106">Las extensiones de máquina virtual de Azure se pueden ejecutar con la CLI de Azure, PowerShell, plantillas de Azure Resource Manager y Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a67e0-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="a67e0-107">Las extensiones pueden empaquetar con una nueva implementación de máquina virtual o se pueden ejecutar en cualquier sistema existente.</span><span class="sxs-lookup"><span data-stu-id="a67e0-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="a67e0-108">Este documento proporciona información general sobre las extensiones de máquina virtual, requisitos previos para usar las extensiones de máquina virtual e instrucciones sobre cómo detectar, administrar y quitar extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a67e0-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="a67e0-109">Este documento proporciona información generalizada porque muchas extensiones de máquina virtual están disponibles, cada una con una configuración potencialmente única.</span><span class="sxs-lookup"><span data-stu-id="a67e0-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="a67e0-110">En cada documento específico de la extensión individual pueden encontrarse detalles específicos de extensión.</span><span class="sxs-lookup"><span data-stu-id="a67e0-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="a67e0-111">Casos de uso y ejemplos</span><span class="sxs-lookup"><span data-stu-id="a67e0-111">Use cases and samples</span></span>

<span data-ttu-id="a67e0-112">Hay muchas extensiones de máquina virtual de Azure diferentes disponibles, cada una con un caso de uso específico.</span><span class="sxs-lookup"><span data-stu-id="a67e0-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="a67e0-113">Algunos casos de uso de ejemplo son:</span><span class="sxs-lookup"><span data-stu-id="a67e0-113">Some example use cases are:</span></span>

- <span data-ttu-id="a67e0-114">Aplique configuraciones de estado deseado de PowerShell a una máquina virtual mediante la extensión DSC para Windows.</span><span class="sxs-lookup"><span data-stu-id="a67e0-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span></span> <span data-ttu-id="a67e0-115">Para obtener más información, consulte la sección sobre la [extensión de configuración de estado deseado de Azure](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a67e0-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="a67e0-116">Configure la supervisión de máquina virtual mediante la extensión de máquina virtual de Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="a67e0-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="a67e0-117">Para obtener más información, consulte [Conexión de máquinas virtuales de Azure a Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a67e0-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="a67e0-118">Configure la supervisión de su infraestructura de Azure con la extensión de Datadog.</span><span class="sxs-lookup"><span data-stu-id="a67e0-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="a67e0-119">Para obtener más información, consulte el [blog de Datadog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="a67e0-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="a67e0-120">Configure una máquina virtual de Azure mediante Chef.</span><span class="sxs-lookup"><span data-stu-id="a67e0-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="a67e0-121">Para obtener más información, consulte [Automatización de la implementación de la máquina virtual de Azure con Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="a67e0-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="a67e0-122">Además de las extensiones específicas de proceso, una extensión de script personalizado está disponible tanto para máquinas virtuales Windows como para máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="a67e0-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="a67e0-123">La extensión de script personalizado para Windows permite que se ejecute cualquier script de PowerShell en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a67e0-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span></span> <span data-ttu-id="a67e0-124">Esto resulta útil al diseñar implementaciones de Azure que requieren una configuración más allá de lo que las herramientas de Azure nativas pueden proporcionar.</span><span class="sxs-lookup"><span data-stu-id="a67e0-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="a67e0-125">Para obtener más información, consulte la sección sobre la [extensión de script personalizado de máquina virtual Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="a67e0-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a67e0-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a67e0-126">Prerequisites</span></span>

<span data-ttu-id="a67e0-127">Cada extensión de máquina virtual puede tener su propio conjunto de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="a67e0-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="a67e0-128">Por ejemplo, la extensión de máquina virtual de Docker tiene un requisito previo de una distribución de Linux compatible.</span><span class="sxs-lookup"><span data-stu-id="a67e0-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="a67e0-129">En la documentación específica de extensión se detallan los requisitos de extensiones individuales.</span><span class="sxs-lookup"><span data-stu-id="a67e0-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="a67e0-130">Agente de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="a67e0-130">Azure VM agent</span></span>
<span data-ttu-id="a67e0-131">El agente de máquina virtual de Azure administra la interacción entre una máquina virtual de Azure y el controlador de tejido de Azure.</span><span class="sxs-lookup"><span data-stu-id="a67e0-131">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="a67e0-132">El agente de máquina virtual es responsable de muchos aspectos funcionales de la implementación y administración de máquinas virtuales de Azure, incluida la ejecución de extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a67e0-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="a67e0-133">El agente de máquina virtual de Azure está preinstalado en imágenes de Azure Marketplace y se puede instalar en sistemas operativos compatibles.</span><span class="sxs-lookup"><span data-stu-id="a67e0-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="a67e0-134">Para obtener información sobre las instrucciones de instalación y los sistemas operativos compatibles, consulte [Agente de máquina virtual de Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="a67e0-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="a67e0-135">Detección de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a67e0-135">Discover VM extensions</span></span>
<span data-ttu-id="a67e0-136">Hay muchas extensiones de máquina virtual diferentes disponibles para su uso con máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="a67e0-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="a67e0-137">Para ver una lista completa, ejecute el siguiente comando con el módulo de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a67e0-137">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="a67e0-138">Asegúrese de especificar la ubicación deseada al ejecutar este comando.</span><span class="sxs-lookup"><span data-stu-id="a67e0-138">Make sure to specify the desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="a67e0-139">Ejecución de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a67e0-139">Run VM extensions</span></span>

<span data-ttu-id="a67e0-140">Las extensiones de máquina virtual de Azure pueden ejecutarse en máquinas virtuales existentes, lo que resulta útil si es preciso realizar cambios de configuración o recuperar la conectividad en una máquina virtual ya implementada.</span><span class="sxs-lookup"><span data-stu-id="a67e0-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="a67e0-141">Las extensiones de máquina virtual también pueden agruparse con las implementaciones de plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a67e0-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="a67e0-142">Al usar las extensiones con plantillas de Resource Manager, puede permitir la implementación y configuración de las máquinas virtuales de Azure sin necesidad de ninguna intervención después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="a67e0-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span></span>

<span data-ttu-id="a67e0-143">Los siguientes métodos pueden usarse para ejecutar una extensión en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="a67e0-143">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="a67e0-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a67e0-144">PowerShell</span></span>

<span data-ttu-id="a67e0-145">Existen varios comandos de PowerShell para ejecutar extensiones individuales.</span><span class="sxs-lookup"><span data-stu-id="a67e0-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="a67e0-146">Para ver una lista, ejecute los siguientes comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a67e0-146">To see a list, run the following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="a67e0-147">Esto proporciona una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a67e0-147">This provides output similar to the following:</span></span>

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

<span data-ttu-id="a67e0-148">En el ejemplo siguiente se usa la extensión de script personalizado para descargar un script desde un repositorio de GitHub en la máquina virtual de destino y, a continuación, ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="a67e0-148">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span></span> <span data-ttu-id="a67e0-149">Para obtener más información sobre la extensión de script personalizado, consulte [Introducción a la extensión de script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="a67e0-149">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="a67e0-150">En este ejemplo, la extensión de acceso a la máquina virtual se usa para restablecer la contraseña administrativa de una máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="a67e0-150">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="a67e0-151">Para obtener más información sobre la extensión de acceso a la máquina virtual, consulte la sección sobre cómo [restablecer el servicio Escritorio remoto en una máquina virtual Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="a67e0-151">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="a67e0-152">El comando `Set-AzureRmVMExtension` se puede usar para iniciar cualquier extensión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a67e0-152">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span></span> <span data-ttu-id="a67e0-153">Para obtener más información, consulte la [referencia de Set-AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="a67e0-153">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="a67e0-154">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a67e0-154">Azure portal</span></span>

<span data-ttu-id="a67e0-155">Una extensión de máquina virtual se puede aplicar a una máquina virtual existente a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a67e0-155">A VM extension can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="a67e0-156">Para ello, seleccione la máquina virtual que desea usar, elija **Extensiones** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a67e0-156">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="a67e0-157">Esto proporciona una lista de extensiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="a67e0-157">This provides a list of available extensions.</span></span> <span data-ttu-id="a67e0-158">Seleccione aquella que desee y siga los pasos del asistente.</span><span class="sxs-lookup"><span data-stu-id="a67e0-158">Select the one you want and follow the steps in the wizard.</span></span>

<span data-ttu-id="a67e0-159">En la siguiente imagen se muestra la instalación de la extensión de Microsoft Antimalware desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a67e0-159">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span></span>

![Instalar la extensión de antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="a67e0-161">Plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a67e0-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="a67e0-162">Las extensiones de máquina virtual se pueden agregar a una plantilla de Azure Resource Manager y ejecutar con la implementación de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="a67e0-162">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="a67e0-163">La implementación de extensiones con una plantilla es útil para crear implementaciones de Azure completamente configuradas.</span><span class="sxs-lookup"><span data-stu-id="a67e0-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="a67e0-164">Por ejemplo, el siguiente JSON procede de una plantilla de Resource Manager que implementa un conjunto de máquinas virtuales de carga equilibrada y una base de datos Azure SQL Database y, a continuación, instala una aplicación .NET Core en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a67e0-164">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="a67e0-165">La extensión de máquina virtual se encarga de la instalación de software.</span><span class="sxs-lookup"><span data-stu-id="a67e0-165">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="a67e0-166">Para obtener más información, consulte la [plantilla completa de Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="a67e0-166">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

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

<span data-ttu-id="a67e0-167">Para obtener más información, consulte [Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="a67e0-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="a67e0-168">Protección de datos de extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a67e0-168">Secure VM extension data</span></span>

<span data-ttu-id="a67e0-169">Al ejecutar una extensión de máquina virtual, puede que sea necesario incluir información confidencial como credenciales, nombres de cuenta de almacenamiento y claves de acceso de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a67e0-169">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="a67e0-170">Muchas extensiones de máquina virtual incluyen una configuración protegida que cifra datos y los descifra solo dentro de la máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="a67e0-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="a67e0-171">Cada extensión tiene un esquema específico de configuración protegida que se detallará en la documentación específica de extensión.</span><span class="sxs-lookup"><span data-stu-id="a67e0-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="a67e0-172">En el ejemplo siguiente se muestra una instancia de la extensión de script personalizado para Windows.</span><span class="sxs-lookup"><span data-stu-id="a67e0-172">The following example shows an instance of the Custom Script extension for Windows.</span></span> <span data-ttu-id="a67e0-173">Tenga en cuenta que el comando que se ejecutará incluye un conjunto de credenciales.</span><span class="sxs-lookup"><span data-stu-id="a67e0-173">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="a67e0-174">En este ejemplo, el comando que se ejecutará no se cifrará.</span><span class="sxs-lookup"><span data-stu-id="a67e0-174">In this example, the command to execute will not be encrypted.</span></span>


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

<span data-ttu-id="a67e0-175">Proteja la cadena de ejecución moviendo la propiedad **command to execute** a la configuración **protegida**.</span><span class="sxs-lookup"><span data-stu-id="a67e0-175">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="a67e0-176">Solución de problemas de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a67e0-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="a67e0-177">Cada extensión de máquina virtual puede tener unos pasos de solución de problemas específicos.</span><span class="sxs-lookup"><span data-stu-id="a67e0-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="a67e0-178">Por ejemplo, al usar la extensión de script personalizado, se pueden encontrar detalles de ejecución de script localmente en la máquina virtual donde se ejecutó la extensión.</span><span class="sxs-lookup"><span data-stu-id="a67e0-178">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="a67e0-179">Todos los pasos de solución de problemas específicos de extensión aparecen detallados en la documentación específica de extensión.</span><span class="sxs-lookup"><span data-stu-id="a67e0-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="a67e0-180">Los pasos de solución de problemas siguientes se aplican a todas las extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a67e0-180">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="a67e0-181">Consulta del estado de la extensión</span><span class="sxs-lookup"><span data-stu-id="a67e0-181">View extension status</span></span>

<span data-ttu-id="a67e0-182">Una vez que una extensión de máquina virtual se haya ejecutado en una máquina virtual, use el siguiente comando de PowerShell para volver al estado de la extensión.</span><span class="sxs-lookup"><span data-stu-id="a67e0-182">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span></span> <span data-ttu-id="a67e0-183">Reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="a67e0-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="a67e0-184">El parámetro `Name` recibe el nombre asignado a la extensión en el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a67e0-184">The `Name` parameter takes the name given to the extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="a67e0-185">El resultado tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="a67e0-185">The output looks like the following:</span></span>

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

<span data-ttu-id="a67e0-186">El estado de ejecución de extensión también puede encontrarse en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a67e0-186">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="a67e0-187">Para ver el estado de una extensión, seleccione la máquina virtual, elija **Extensiones** y seleccione la extensión deseada.</span><span class="sxs-lookup"><span data-stu-id="a67e0-187">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="a67e0-188">Repetición de ejecución de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a67e0-188">Rerun VM extensions</span></span>

<span data-ttu-id="a67e0-189">Puede haber casos en los que sea necesario volver a ejecutar una extensión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a67e0-189">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="a67e0-190">Puede hacerlo quitando la extensión y, a continuación, volviendo a ejecutar la extensión con un método de ejecución de su elección.</span><span class="sxs-lookup"><span data-stu-id="a67e0-190">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="a67e0-191">Para quitar una extensión, ejecute el siguiente comando con el módulo de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a67e0-191">To remove an extension, run the following command with the Azure PowerShell module.</span></span> <span data-ttu-id="a67e0-192">Reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="a67e0-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="a67e0-193">También se puede quitar una extensión mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a67e0-193">An extension can also be removed using the Azure portal.</span></span> <span data-ttu-id="a67e0-194">Para ello:</span><span class="sxs-lookup"><span data-stu-id="a67e0-194">To do so:</span></span>

1. <span data-ttu-id="a67e0-195">Seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a67e0-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="a67e0-196">Seleccione **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="a67e0-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="a67e0-197">Elija la extensión deseada.</span><span class="sxs-lookup"><span data-stu-id="a67e0-197">Choose the desired extension.</span></span>
4. <span data-ttu-id="a67e0-198">Seleccione **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="a67e0-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="a67e0-199">Referencia de extensiones de máquina virtual comunes</span><span class="sxs-lookup"><span data-stu-id="a67e0-199">Common VM extensions reference</span></span>
| <span data-ttu-id="a67e0-200">Nombre de la extensión</span><span class="sxs-lookup"><span data-stu-id="a67e0-200">Extension name</span></span> | <span data-ttu-id="a67e0-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="a67e0-201">Description</span></span> | <span data-ttu-id="a67e0-202">Más información</span><span class="sxs-lookup"><span data-stu-id="a67e0-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a67e0-203">Extensión de la secuencia de comandos personalizada para Windows</span><span class="sxs-lookup"><span data-stu-id="a67e0-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="a67e0-204">Ejecución de scripts en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="a67e0-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="a67e0-205">Extensión de la secuencia de comandos personalizada para Windows</span><span class="sxs-lookup"><span data-stu-id="a67e0-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="a67e0-206">Extensión de DSC para Windows</span><span class="sxs-lookup"><span data-stu-id="a67e0-206">DSC Extension for Windows</span></span> |<span data-ttu-id="a67e0-207">Extensión DSC (configuración de estado deseado) de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a67e0-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="a67e0-208">Extensión DSC para Windows</span><span class="sxs-lookup"><span data-stu-id="a67e0-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="a67e0-209">Extensión de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="a67e0-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="a67e0-210">Administración de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="a67e0-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="a67e0-211">Extensión de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="a67e0-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="a67e0-212">Extensión de acceso a máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="a67e0-212">Azure VM Access Extension</span></span> |<span data-ttu-id="a67e0-213">Administración de usuarios y credenciales</span><span class="sxs-lookup"><span data-stu-id="a67e0-213">Manage users and credentials</span></span> |[<span data-ttu-id="a67e0-214">Extensión de acceso a máquina virtual para Linux</span><span class="sxs-lookup"><span data-stu-id="a67e0-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |

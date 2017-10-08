---
title: "máquinas de aaaOnboarding para la administración mediante el DSC de automatización de Azure | Documentos de Microsoft"
description: "¿Cómo toosetup los equipos para la administración con DSC de automatización de Azure"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="a2498-103">Incorporación de máquinas para administrarlas con DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="a2498-104">¿Por qué administrar máquinas con DSC de Automatización de Azure?</span><span class="sxs-lookup"><span data-stu-id="a2498-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="a2498-105">Al igual que [Configuración de estado deseado de PowerShell](https://technet.microsoft.com/library/dn249912.aspx), Configuración de estado deseado de Automatización de Azure es un servicio de administración de configuración, sencillo pero eficaz, para los nodos de DSC (máquinas físicas y virtuales) en cualquier centro de datos local o en la nube.</span><span class="sxs-lookup"><span data-stu-id="a2498-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="a2498-106">Permite la escalabilidad en miles de máquinas de forma rápida y sencilla desde una ubicación central y segura.</span><span class="sxs-lookup"><span data-stu-id="a2498-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="a2498-107">Puede incorporar fácilmente máquinas, asignar configuraciones declarativas de ellos así como ver informes que muestra cada equipo del estado de toohello deseado de cumplimiento especificado.</span><span class="sxs-lookup"><span data-stu-id="a2498-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="a2498-108">capa de administración de Hello DSC de automatización de Azure es tooDSC qué nivel de administración de la automatización de Azure de hello tooPowerShell de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="a2498-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="a2498-109">En otras palabras, en hello igual que automatización de Azure le ayuda a administrar los scripts de PowerShell, también le ayuda a administrar las configuraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="a2498-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="a2498-110">toolearn más información acerca de las ventajas de hello del uso de DSC de automatización de Azure, consulte [información general de DSC de automatización de Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2498-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="a2498-111">DSC de automatización de Azure puede ser usado toomanage una variedad de máquinas:</span><span class="sxs-lookup"><span data-stu-id="a2498-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="a2498-112">Azure Virtual Machines (clásico)</span><span class="sxs-lookup"><span data-stu-id="a2498-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="a2498-113">Máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-113">Azure virtual machines</span></span>
* <span data-ttu-id="a2498-114">Máquinas virtuales de Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="a2498-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="a2498-115">Máquinas físicas y virtuales con Windows locales o en una nube que no sea Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="a2498-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="a2498-116">Máquinas físicas y virtuales con Linux locales, en Azure o en una nube que no sea Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="a2498-117">Además, si no estás listo toomanage configuración de la máquina de nube de hello, DSC de automatización de Azure también puede utilizarse como un punto de conexión solo informe.</span><span class="sxs-lookup"><span data-stu-id="a2498-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="a2498-118">Esto le permite tooset (push) de configuración deseada a través de DSC local y ver detalles informes enriquecidos sobre la conformidad de nodo con hello deseado estado en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2498-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="a2498-119">Hola las secciones siguientes describen cómo se puede incorporar cada tipo de máquina tooAzure DSC de automatización.</span><span class="sxs-lookup"><span data-stu-id="a2498-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="a2498-120">Azure Virtual Machines (clásico)</span><span class="sxs-lookup"><span data-stu-id="a2498-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="a2498-121">Con DSC de automatización de Azure, puede incorporadas fácilmente máquinas virtuales de Azure (clásico) para la administración de configuración con el portal de Azure de Hola o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2498-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="a2498-122">Bajo el paraguas de Hola y sin que un administrador tenga tooremote en hello VM, Hola extensión de configuración de estado deseado de Azure VM registra Hola VM con el DSC de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2498-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="a2498-123">Puesto que Hola extensión de configuración de estado deseado de VM de Azure se ejecuta de forma asincrónica, pasos tootrack su progreso o solucionar problemas se proporcionan en hello [ **incorporación de la máquina virtual de Azure de solución de problemas de** ](#troubleshooting-azure-virtual-machine-onboarding)sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="a2498-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a2498-124">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2498-124">Azure portal</span></span>

<span data-ttu-id="a2498-125">Hola [portal de Azure](http://portal.azure.com/), haga clic en **examinar** -> **máquinas virtuales (clásicas)**.</span><span class="sxs-lookup"><span data-stu-id="a2498-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="a2498-126">Seleccione Hola VM de Windows que desee tooonboard.</span><span class="sxs-lookup"><span data-stu-id="a2498-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="a2498-127">En la hoja de la máquina virtual Hola panel, haga clic en **toda la configuración de** -> **extensiones** -> **agregar**  ->   **DSC de automatización de Azure** -> **crear**.</span><span class="sxs-lookup"><span data-stu-id="a2498-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="a2498-128">Escriba hello [valores del Administrador de configuración Local de DSC de PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necesarios para el caso de uso, clave de registro de la cuenta de automatización y dirección URL de registro y, opcionalmente, un toohello de tooassign de configuración de nodo VM.</span><span class="sxs-lookup"><span data-stu-id="a2498-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="a2498-129">dirección URL de registro de hello toofind y clave para la máquina hello tooonboard de cuenta de automatización de hello, vea hello [ **proteger el registro** ](#secure-registration) sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="a2498-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="a2498-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2498-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="a2498-131">Máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-131">Azure virtual machines</span></span>

<span data-ttu-id="a2498-132">DSC de automatización de Azure permite incorporadas fácilmente máquinas virtuales de Azure para la administración de configuración, utilizando Hola portal de Azure, plantillas del Administrador de recursos de Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2498-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="a2498-133">Bajo el paraguas de Hola y sin que un administrador tenga tooremote en hello VM, Hola extensión de configuración de estado deseado de Azure VM registra Hola VM con el DSC de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2498-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="a2498-134">Puesto que Hola extensión de configuración de estado deseado de VM de Azure se ejecuta de forma asincrónica, pasos tootrack su progreso o solucionar problemas se proporcionan en hello [ **incorporación de la máquina virtual de Azure de solución de problemas de** ](#troubleshooting-azure-virtual-machine-onboarding)sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="a2498-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a2498-135">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2498-135">Azure portal</span></span>

<span data-ttu-id="a2498-136">Hola [portal de Azure](https://portal.azure.com/), navegue toohello cuenta de automatización de Azure donde desee tooonboard las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a2498-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="a2498-137">En el panel de la cuenta de automatización de hello, haga clic en **nodos** -> **agregar Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="a2498-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="a2498-138">En **seleccionar máquinas virtuales tooonboard**, seleccione uno o más Azure virtual máquinas tooonboard.</span><span class="sxs-lookup"><span data-stu-id="a2498-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="a2498-139">En **configurar datos de registro**, escriba Hola [valores del Administrador de configuración Local de DSC de PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necesarios para el caso de uso y, opcionalmente, un toohello de tooassign de configuración de nodo máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a2498-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="a2498-140">Plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a2498-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="a2498-141">Se pueden implementar máquinas virtuales de Azure e incorporado tooAzure DSC de automatización a través de plantillas del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2498-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="a2498-142">Vea [configurar una máquina virtual a través de la extensión de DSC y DSC de automatización de Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) para una plantilla de ejemplo que onboards un tooAzure VM DSC de automatización existente.</span><span class="sxs-lookup"><span data-stu-id="a2498-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="a2498-143">toofind Hola clave y el registro de dirección URL de registro tomada como entrada en esta plantilla, vea hello [ **proteger el registro** ](#secure-registration) sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="a2498-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="a2498-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2498-144">PowerShell</span></span>

<span data-ttu-id="a2498-145">Hola [AzureRmAutomationDscNode Register](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet puede ser tooonboard usa máquinas virtuales Hola portal de Azure a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2498-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="a2498-146">Máquinas virtuales de Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="a2498-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="a2498-147">Puede incorporadas fácilmente máquinas virtuales de Amazon Web Services para la administración de configuración de DSC de automatización de Azure con hello AWS DSC Toolkit.</span><span class="sxs-lookup"><span data-stu-id="a2498-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="a2498-148">Puede aprender más sobre el Kit de herramientas de hello [aquí](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="a2498-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="a2498-149">Máquinas físicas y virtuales con Windows locales o en una nube que no sea Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="a2498-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="a2498-150">Máquinas de Windows locales y máquinas de Windows en las nubes distintas de Azure (como Amazon Web Services) también pueden ser incorporadas tooAzure DSC de automatización, siempre y cuando tienen acceso de salida toohello internet, a través de unos pocos pasos sencillos:</span><span class="sxs-lookup"><span data-stu-id="a2498-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="a2498-151">Crear seguro Hola de versión más reciente de [WMF 5](http://aka.ms/wmf5latest) está instalado en equipos de hello desea tooonboard tooAzure DSC de automatización.</span><span class="sxs-lookup"><span data-stu-id="a2498-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="a2498-152">Siga las instrucciones de Hola de sección [ **generar DSC metaconfiguraciones** ](#generating-dsc-metaconfigurations) a continuación toogenerate una carpeta que contenga Hola necesarios metaconfiguraciones de DSC.</span><span class="sxs-lookup"><span data-stu-id="a2498-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="a2498-153">Aplicar de forma remota máquinas de toohello de metaconfiguración Hola DSC de PowerShell que desee tooonboard.</span><span class="sxs-lookup"><span data-stu-id="a2498-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="a2498-154">**máquina de Hello este comando se ejecuta desde debe tener la versión más reciente de Hola de [WMF 5](http://aka.ms/wmf5latest) instalado**:</span><span class="sxs-lookup"><span data-stu-id="a2498-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="a2498-155">Si no se puede aplicar Hola DSC de PowerShell metaconfiguraciones de forma remota, copie la carpeta de metaconfiguraciones de hello en el paso 2 en cada máquina tooonboard.</span><span class="sxs-lookup"><span data-stu-id="a2498-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="a2498-156">A continuación, llame a **Set-DscLocalConfigurationManager** localmente en cada máquina tooonboard.</span><span class="sxs-lookup"><span data-stu-id="a2498-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="a2498-157">Uso de hello portal de Azure o cmdlets, compruebe que Hola máquinas tooonboard ahora aparecen como nodos registrado en la cuenta de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2498-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="a2498-158">Máquinas físicas y virtuales con Linux locales, en Azure o en una nube que no sea Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="a2498-159">Los equipos Linux locales, máquinas de Linux en Azure, y máquinas de Linux en nubes de distintas de Azure también pueden ser incorporadas tooAzure DSC de automatización, siempre y cuando tienen acceso de salida toohello internet, a través de unos pocos pasos sencillos:</span><span class="sxs-lookup"><span data-stu-id="a2498-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="a2498-160">Crear seguro Hola de versión más reciente de [configuración de estado deseado de PowerShell para Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) está instalado en equipos de hello desea tooonboard tooAzure DSC de automatización.</span><span class="sxs-lookup"><span data-stu-id="a2498-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="a2498-161">Si hello [valores predeterminados del Administrador de configuración Local de DSC de PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) coincide con el caso de uso, y desea tooonboard máquinas como lo **ambos** la extracción y tooAzure DSC de automatización de informes:</span><span class="sxs-lookup"><span data-stu-id="a2498-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="a2498-162">En cada tooAzure de tooonboard de máquina de Linux DSC de automatización, use tooonboard Register.py con hello tiene como valor predeterminado en el Administrador de configuración Local de DSC de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a2498-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="a2498-163">toofind Hola registro clave y el registro de dirección URL para la cuenta de automatización, vea hello [ **proteger el registro** ](#secure-registration) sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="a2498-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="a2498-164">Si hello tiene como valor predeterminado en Administrador de configuración Local de DSC de PowerShell **hacer** **no** coincide con el caso de uso, o quiere tooonboard equipos de forma que solo tooAzure DSC de automatización de informes, pero no de extracción configuración o módulos de PowerShell de él, siga los pasos 3 a 6.</span><span class="sxs-lookup"><span data-stu-id="a2498-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="a2498-165">En caso contrario, continúe directamente toostep 6.</span><span class="sxs-lookup"><span data-stu-id="a2498-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="a2498-166">Siga las instrucciones de Hola Hola [ **generar DSC metaconfiguraciones** ](#generating-dsc-metaconfigurations) sección toogenerate una carpeta que contiene metaconfiguraciones de DSC de Hola que sea necesitado.</span><span class="sxs-lookup"><span data-stu-id="a2498-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="a2498-167">Aplicar de forma remota máquinas de toohello de metaconfiguración Hola DSC de PowerShell que desee tooonboard:</span><span class="sxs-lookup"><span data-stu-id="a2498-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="a2498-168">máquina de Hello este comando se ejecuta desde debe tener la versión más reciente de Hola de [WMF 5](http://aka.ms/wmf5latest) instalado.</span><span class="sxs-lookup"><span data-stu-id="a2498-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="a2498-169">Si no se puede aplicar hello metaconfiguraciones de DSC de PowerShell de forma remota, para cada tooonboard de máquina Linux, copie máquina de hello metaconfiguración correspondiente toothat de carpeta de hello en el paso 5 en el equipo de Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="a2498-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="a2498-170">A continuación, llame a `SetDscLocalConfigurationManager.py` localmente en cada equipo Linux desea tooonboard tooAzure DSC de automatización:</span><span class="sxs-lookup"><span data-stu-id="a2498-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="a2498-171">Uso de hello portal de Azure o cmdlets, compruebe que Hola máquinas tooonboard ahora aparecen como nodos registrado en la cuenta de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2498-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="a2498-172">Generación de metaconfiguraciones de DSC</span><span class="sxs-lookup"><span data-stu-id="a2498-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="a2498-173">toogenerically incorporar cualquier máquina tooAzure DSC de automatización, un [metaconfiguración de DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) puede ser generado que, cuando aplica, indica el agente de hello DSC en hello máquina toopull desde o tooAzure DSC de automatización de informes.</span><span class="sxs-lookup"><span data-stu-id="a2498-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="a2498-174">DSC metaconfiguraciones de DSC de automatización de Azure se pueden generar utilizando una configuración de DSC de PowerShell o cmdlets de PowerShell de automatización de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2498-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="a2498-175">Metaconfiguraciones de DSC contienen Hola secretos necesitados tooonboard una cuenta de automatización para la administración de máquina tooan.</span><span class="sxs-lookup"><span data-stu-id="a2498-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="a2498-176">Asegúrese de tooproperly seguro proteger cualquier metaconfiguraciones DSC que creas o eliminarlos tras su uso.</span><span class="sxs-lookup"><span data-stu-id="a2498-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="a2498-177">Uso de una configuración de DSC</span><span class="sxs-lookup"><span data-stu-id="a2498-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="a2498-178">Abra Hola PowerShell ISE como administrador en un equipo en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="a2498-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="a2498-179">máquina de Hello debe tener la versión más reciente de Hola de [WMF 5](http://aka.ms/wmf5latest) instalado.</span><span class="sxs-lookup"><span data-stu-id="a2498-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="a2498-180">Copie Hola siguiente secuencia de comandos localmente.</span><span class="sxs-lookup"><span data-stu-id="a2498-180">Copy hello following script locally.</span></span> <span data-ttu-id="a2498-181">Este script contiene una configuración de DSC de PowerShell para crear metaconfiguraciones y un tookick comando desactivar la creación de hello metaconfiguración.</span><span class="sxs-lookup"><span data-stu-id="a2498-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="a2498-182">Rellene la clave de registro de hello y la dirección URL para la cuenta de automatización, así como los nombres de Hola de hello máquinas tooonboard.</span><span class="sxs-lookup"><span data-stu-id="a2498-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="a2498-183">Todos los demás parámetros son opcionales.</span><span class="sxs-lookup"><span data-stu-id="a2498-183">All other parameters are optional.</span></span> <span data-ttu-id="a2498-184">toofind Hola registro clave y el registro de dirección URL para la cuenta de automatización, vea hello [ **proteger el registro** ](#secure-registration) sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="a2498-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="a2498-185">Si desea Hola máquinas tooreport DSC estado información tooAzure DSC de automatización, pero no de extracción configuración o módulos de PowerShell, establezca hello **ReportOnly** tootrue de parámetro.</span><span class="sxs-lookup"><span data-stu-id="a2498-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="a2498-186">Ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2498-186">Run hello script.</span></span> <span data-ttu-id="a2498-187">Ahora debería tener una carpeta denominada **DscMetaConfigs** en el directorio de trabajo, que contiene hello metaconfiguraciones de DSC de PowerShell para hello máquinas tooonboard (como administrador):</span><span class="sxs-lookup"><span data-stu-id="a2498-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="a2498-188">Uso de cmdlets de automatización de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="a2498-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="a2498-189">Si los valores predeterminados de administrador de configuración Local de DSC de PowerShell de hello coincide con el caso de uso, y desea tooonboard máquinas tal que se extraiga de y tooAzure DSC de automatización de informes, Hola cmdlets de automatización de Azure proporcionan un método simplificado de generar Hola DSC metaconfiguraciones necesitado:</span><span class="sxs-lookup"><span data-stu-id="a2498-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="a2498-190">Abra la consola de PowerShell de Hola o PowerShell ISE como administrador en un equipo en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="a2498-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="a2498-191">Conectar con el Administrador de recursos de tooAzure **AzureRmAccount agregar**</span><span class="sxs-lookup"><span data-stu-id="a2498-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="a2498-192">Descargue metaconfiguraciones de DSC de PowerShell de Hola para máquinas Hola desea tooonboard de hello automatización cuenta toowhich que desea que los nodos de tooonboard:</span><span class="sxs-lookup"><span data-stu-id="a2498-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="a2498-193">Ahora debería tener una carpeta denominada ***DscMetaConfigs***, que contiene hello metaconfiguraciones de DSC de PowerShell para hello máquinas tooonboard (como administrador):</span><span class="sxs-lookup"><span data-stu-id="a2498-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="a2498-194">Registro seguro</span><span class="sxs-lookup"><span data-stu-id="a2498-194">Secure registration</span></span>

<span data-ttu-id="a2498-195">Máquinas pueden incorporar de manera segura tooan cuenta de automatización de Azure a través del protocolo de registro de WMF 5 DSC hello, que permite a un nodo tooauthenticate tooa V2 extracción de DSC de PowerShell o informes servidor DSC (incluida la DSC de automatización de Azure).</span><span class="sxs-lookup"><span data-stu-id="a2498-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="a2498-196">nodo Hola registra el servidor toohello en un **dirección URL de registro**, autenticación mediante un **clave de registro**.</span><span class="sxs-lookup"><span data-stu-id="a2498-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="a2498-197">Durante el registro, nodo de hello DSC y servidor de extracción de DSC/informes negocian un certificado único para este toouse de nodo de registro posterior a la del servidor de toohello autenticación.</span><span class="sxs-lookup"><span data-stu-id="a2498-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="a2498-198">Este proceso impide que los nodos incorporados se suplanten entre sí, como por ejemplo si un nodo está afectado y se comporta de forma malintencionada.</span><span class="sxs-lookup"><span data-stu-id="a2498-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="a2498-199">Después del registro, clave de registro de hello no se utiliza para la autenticación de nuevo y se elimina del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2498-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="a2498-200">Puede obtener información de hello necesaria para el protocolo de registro de hello DSC de hello **administrar claves** hoja en el portal de vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2498-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="a2498-201">Abra esta hoja haciendo clic en el icono de llave hello en hello **Essentials** panel para hello cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="a2498-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="a2498-202">Dirección URL de registro es el campo de dirección URL de hello en la hoja de administrar claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2498-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="a2498-203">Clave de registro es Hola clave de acceso principal o clave de acceso secundaria en la hoja de administrar claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2498-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="a2498-204">Se puede usar cualquiera de las dos.</span><span class="sxs-lookup"><span data-stu-id="a2498-204">Either key can be used.</span></span>

<span data-ttu-id="a2498-205">Para lograr una mayor seguridad, pueden volver a generar las claves de acceso principal y secundaria de Hola de una cuenta de automatización en cualquier momento (en hello **administrar claves** hoja) registros de nodo futuras de tooprevent mediante claves anteriores.</span><span class="sxs-lookup"><span data-stu-id="a2498-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="a2498-206">Solución de problemas de incorporación de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="a2498-207">DSC de Automatización de Azure permite incorporar fácilmente máquinas virtuales de Azure con Windows para la administración de configuraciones.</span><span class="sxs-lookup"><span data-stu-id="a2498-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="a2498-208">Bajo el paraguas de hello, Hola extensión de configuración de estado deseado de Azure VM es tooregister usado hello VM con el DSC de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2498-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="a2498-209">Puesto que Hola extensión de configuración de estado deseado de VM de Azure se ejecuta de forma asincrónica, seguimiento de su progreso y solucionar problemas de su ejecución pueden ser importantes.</span><span class="sxs-lookup"><span data-stu-id="a2498-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="a2498-210">Cualquier método de incorporación una tooAzure de VM en Windows Azure DSC de automatización que usa la extensión de la configuración de estado deseado de Azure VM Hola podría tardar hasta hora tooan Hola nodo tooshow seguridad como está registrado en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2498-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="a2498-211">Esto es debido a la instalación de toohello de Windows Management Framework 5.0 en hello VM por extensión de DSC de VM de Azure de hello, que es necesario tooonboard Hola VM tooAzure DSC de automatización.</span><span class="sxs-lookup"><span data-stu-id="a2498-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="a2498-212">tootroubleshoot o la vista estado de Hola de extensión de la configuración de estado deseado de Azure VM, en el portal de Azure de Hola Hola vaya toohello VM está incorporado, a continuación, haga clic -> **toda la configuración de** -> **extensiones**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="a2498-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="a2498-213">Para obtener más detalles, puede hacer clic en **Ver estado detallado**.</span><span class="sxs-lookup"><span data-stu-id="a2498-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="a2498-214">Expiración y repetición del registro del certificado</span><span class="sxs-lookup"><span data-stu-id="a2498-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="a2498-215">Después de registrar una máquina como un nodo de DSC de DSC de automatización de Azure, hay una serie de motivos por qué puede que necesite tooreregister ese nodo Hola futura:</span><span class="sxs-lookup"><span data-stu-id="a2498-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="a2498-216">Tras el registro, cada nodo negocia automáticamente un certificado único para la autenticación que expira después de un año.</span><span class="sxs-lookup"><span data-stu-id="a2498-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="a2498-217">Actualmente, Hola protocolo de registro de DSC de PowerShell no puede renovar certificados automáticamente cuando expirarán, por lo que tiene nodos de hello tooreregister después de la hora de un año.</span><span class="sxs-lookup"><span data-stu-id="a2498-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="a2498-218">Antes de volver a registrar, asegúrese de que cada nodo ejecute Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="a2498-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="a2498-219">Si expira el certificado de autenticación de un nodo y no se registra el nodo de hello, nodo de hello será no se puede toocommunicate con automatización de Azure y se marcará como "No responde".</span><span class="sxs-lookup"><span data-stu-id="a2498-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="a2498-220">Volver a registrar realiza 90 días o menor de tiempo de expiración del certificado de hello, o en cualquier momento después de la fecha de expiración del certificado de hello, dará como resultado un nuevo certificado que se va a generar y usar.</span><span class="sxs-lookup"><span data-stu-id="a2498-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="a2498-221">toochange cualquier [valores del Administrador de configuración Local de DSC de PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) que se establecieron durante el registro inicial del nodo de hello, como ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="a2498-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="a2498-222">Actualmente, estos valores de agente DSC solo pueden cambiarse mediante un nuevo registro.</span><span class="sxs-lookup"><span data-stu-id="a2498-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="a2498-223">una excepción de Hello es Hola configuración de nodo asignada toohello nodo, esto puede cambiarse en el DSC de automatización de Azure directamente.</span><span class="sxs-lookup"><span data-stu-id="a2498-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="a2498-224">Volver a registrar puede realizarse en hello igual registró nodo Hola inicialmente, mediante cualquiera de los métodos de incorporación de hello descrita en este documento.</span><span class="sxs-lookup"><span data-stu-id="a2498-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="a2498-225">No es necesario toounregister un nodo de DSC de automatización de Azure antes de volver a registrarlo.</span><span class="sxs-lookup"><span data-stu-id="a2498-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="a2498-226">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="a2498-226">Related Articles</span></span>

* [<span data-ttu-id="a2498-227">Información general de DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="a2498-228">Cmdlets de DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="a2498-229">Precios de DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="a2498-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

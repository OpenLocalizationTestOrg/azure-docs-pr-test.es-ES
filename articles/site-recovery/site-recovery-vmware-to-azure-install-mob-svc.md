---
title: "aaaInstall Mobility Service (VMware o tooAzure físico) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall Hola tooprotect de agente del servicio de movilidad sus equipos locales."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="c9746-103">Instalar servicio de movilidad (VMware o tooAzure físico)</span><span class="sxs-lookup"><span data-stu-id="c9746-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="c9746-104">Servicio de movilidad de Azure Site Recovery captura escrituras de datos en un equipo y, a continuación, reenvía el servidor de procesos de toohello.</span><span class="sxs-lookup"><span data-stu-id="c9746-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="c9746-105">Implementar el servicio de movilidad tooevery equipo (VM de VMware o servidor físico) que desea tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c9746-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="c9746-106">Puede implementar servidores de toohello de servicio de movilidad que desea tooprotect usando Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="c9746-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="c9746-107">Instalación de Mobility Service mediante herramientas de implementación herramientas de implementación de software como System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="c9746-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="c9746-108">Instalación de Mobility Service mediante Azure Automation y la configuración de estado deseado (DSC de Automatización)</span><span class="sxs-lookup"><span data-stu-id="c9746-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="c9746-109">Instalar manualmente el servicio de movilidad mediante interfaz gráfica de usuario de hello (GUI)</span><span class="sxs-lookup"><span data-stu-id="c9746-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="c9746-110">Instalación manual de Mobility Service mediante la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="c9746-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="c9746-111">Instalación de Mobility Service mediante la instalación de inserción de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c9746-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="c9746-112">A partir de la versión 9.7.0.0, en máquinas virtuales (VM) de Windows hello Mobility Service instalador también instala hello más reciente disponible [agente de máquina virtual de Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="c9746-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="c9746-113">Cuando se produce un error en un equipo a través de tooAzure, equipo de hello cumple instalación del agente Hola requisitos previo para utilizar cualquier extensión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9746-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9746-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c9746-114">Prerequisites</span></span>
<span data-ttu-id="c9746-115">Complete estos pasos de requisitos previos antes de instalar manualmente Mobility Service en el servidor:</span><span class="sxs-lookup"><span data-stu-id="c9746-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="c9746-116">Inicie sesión en el servidor de configuración de tooyour y, a continuación, abra una ventana del símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="c9746-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="c9746-117">Cambie la carpeta bin de hello directorio toohello y, a continuación, cree un archivo de frase de contraseña:</span><span class="sxs-lookup"><span data-stu-id="c9746-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="c9746-118">Almacene el archivo de frase de contraseña de hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="c9746-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="c9746-119">Utilice el archivo hello durante la instalación del servicio de movilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9746-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="c9746-120">Instaladores de servicio de movilidad para todos los sistemas operativos compatibles están en la carpeta %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9746-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="c9746-121">Instalador de Mobility Service para la asignación de sistemas operativos</span><span class="sxs-lookup"><span data-stu-id="c9746-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="c9746-122">Nombre de plantilla de archivo de instalador</span><span class="sxs-lookup"><span data-stu-id="c9746-122">Installer file template name</span></span>| <span data-ttu-id="c9746-123">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="c9746-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="c9746-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="c9746-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="c9746-125">Windows Server 2008 R2 SP1 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="c9746-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="c9746-126">Windows Server 2012 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="c9746-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="c9746-127">Windows Server 2012 R2 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="c9746-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="c9746-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c9746-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="c9746-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (solo 64 bits)</span><span class="sxs-lookup"><span data-stu-id="c9746-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="c9746-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (solo 64 bits)</span><span class="sxs-lookup"><span data-stu-id="c9746-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="c9746-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c9746-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="c9746-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (solo 64-bit)</span><span class="sxs-lookup"><span data-stu-id="c9746-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="c9746-133">CentOS 7.0, 7.1, 7.2 (solo 64-bit)</span><span class="sxs-lookup"><span data-stu-id="c9746-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="c9746-134">CentOs 7.3 (solo en la migración)</span><span class="sxs-lookup"><span data-stu-id="c9746-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="c9746-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c9746-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="c9746-136">SUSE Linux Enterprise Server 11 SP3 (solo 64 bits)</span><span class="sxs-lookup"><span data-stu-id="c9746-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="c9746-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c9746-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="c9746-138">SUSE Linux Enterprise Server 11 SP4 (solo 64-bit)</span><span class="sxs-lookup"><span data-stu-id="c9746-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="c9746-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c9746-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="c9746-140">Oracle Enterprise Linux 6.4, 6.5 (solo 64 bits)</span><span class="sxs-lookup"><span data-stu-id="c9746-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="c9746-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c9746-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="c9746-142">Ubuntu Linux 14.04 (solo 64-bit)</span><span class="sxs-lookup"><span data-stu-id="c9746-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="c9746-143">Instalar manualmente el servicio de movilidad mediante GUI Hola</span><span class="sxs-lookup"><span data-stu-id="c9746-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="c9746-144">Si usas un **servidor de configuración** tooreplicate **máquinas virtuales de IaaS de Azure** desde una tooanother de suscripción o la región de Azure, a continuación, **usar Hola de instalación basada en línea de comandos**  (método)</span><span class="sxs-lookup"><span data-stu-id="c9746-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="c9746-145">Instalación manual de Mobility Service mediante la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="c9746-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="c9746-146">Instalación de la línea de comandos en un equipo Windows</span><span class="sxs-lookup"><span data-stu-id="c9746-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="c9746-147">Instalación de la línea de comandos en un equipo Linux</span><span class="sxs-lookup"><span data-stu-id="c9746-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="c9746-148">Instalación de Mobility Service mediante la instalación de inserción de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c9746-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="c9746-149">toodo una instalación de inserción del servicio de movilidad mediante el uso de Site Recovery, todos los equipos de destino deben cumplir Hola siguiendo los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="c9746-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="c9746-150">Después de instalar el servicio de movilidad, Hola portal de Azure, seleccione hello **replicar** toostart botón proteger estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c9746-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="c9746-151">Desinstalación de Mobility Service en un equipo de Windows Server</span><span class="sxs-lookup"><span data-stu-id="c9746-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="c9746-152">Utilice uno de hello siguiendo métodos toouninstall Mobility Service en un equipo con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c9746-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="c9746-153">Desinstalar mediante la GUI de Hola</span><span class="sxs-lookup"><span data-stu-id="c9746-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="c9746-154">En el Panel de Control, seleccione **Programas**.</span><span class="sxs-lookup"><span data-stu-id="c9746-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="c9746-155">Seleccione **Microsoft Azure Site Recovery Mobility Service/Servidor de destino maestro** y, a continuación, haga clic en**Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="c9746-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="c9746-156">Desinstalación en un símbolo del sistema</span><span class="sxs-lookup"><span data-stu-id="c9746-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="c9746-157">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="c9746-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="c9746-158">toouninstall servicio de movilidad, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c9746-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="c9746-159">Desinstalación de Mobility Service en equipos Linux</span><span class="sxs-lookup"><span data-stu-id="c9746-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="c9746-160">En el servidor Linux, inicie sesión como un usuario **raíz**.</span><span class="sxs-lookup"><span data-stu-id="c9746-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="c9746-161">En un terminal, vaya demasiado/usuario/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="c9746-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="c9746-162">toouninstall servicio de movilidad, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c9746-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```

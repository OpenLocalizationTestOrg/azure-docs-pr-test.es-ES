---
title: "aaaReset Hola contraseña o la configuración de escritorio remoto en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooreset una contraseña de cuenta o servicios de escritorio remoto en una VM de Windows crean con hello clásico implementación modelo Hola portal de Azure o Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="56456-103">Cómo servicios de escritorio remoto de hello tooreset ni su contraseña de inicio de sesión en una máquina virtual de Windows creado con el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="56456-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="56456-104">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="56456-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="56456-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="56456-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="56456-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="56456-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="56456-107">También puede [realizar estos pasos para las máquinas virtuales creadas con el modelo de implementación del Administrador de recursos de hello](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="56456-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="56456-108">Si no se puede conectar la máquina virtual de Windows tooa (VM), puede restablecer la contraseña de administrador local de Hola o restablecer la configuración de servicios de escritorio remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="56456-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="56456-109">Puede usar cualquier extensión de acceso a máquinas virtuales de portal o hello Azure hello en la contraseña de Azure PowerShell tooreset Hola.</span><span class="sxs-lookup"><span data-stu-id="56456-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="56456-110">Configuración de formas tooreset o las credenciales</span><span class="sxs-lookup"><span data-stu-id="56456-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="56456-111">Puede restablecer los servicios y las credenciales de Escritorio remoto de varias maneras diferentes, dependiendo de sus necesidades:</span><span class="sxs-lookup"><span data-stu-id="56456-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="56456-112">Restablecer mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="56456-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="56456-113">Restablecimiento mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="56456-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="56456-114">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="56456-114">Azure portal</span></span>
<span data-ttu-id="56456-115">Puede usar hello [portal de Azure](https://portal.azure.com) tooreset Hola servicios de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="56456-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="56456-116">menús tooexpand Hola del portal, haga clic en hello tres barras en la esquina superior izquierda de hello y, a continuación, haga clic en **máquinas virtuales (clásicas)**:</span><span class="sxs-lookup"><span data-stu-id="56456-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Busque la máquina virtual de Azure.](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="56456-118">Seleccione la máquina virtual de Windows y, a continuación, haga clic en **restablecer remoto...** . hello siguiente aparece cuadro de diálogo Configuración de escritorio remoto de Hola tooreset:</span><span class="sxs-lookup"><span data-stu-id="56456-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Página Restablecer configuración de RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="56456-120">También puede restablecer Hola nombre de usuario y la contraseña de cuenta de administrador local de Hola.</span><span class="sxs-lookup"><span data-stu-id="56456-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="56456-121">En la máquina virtual, haga clic en **Soporte y solución de problemas** > **Restablecer contraseña**.</span><span class="sxs-lookup"><span data-stu-id="56456-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="56456-122">se muestra la hoja de restablecimiento de contraseña de Hello:</span><span class="sxs-lookup"><span data-stu-id="56456-122">hello password reset blade is displayed:</span></span>

![Página Restablecimiento de contraseña](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="56456-124">Después de escribir Hola nuevo nombre de usuario y contraseña, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="56456-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="56456-125">Extensión VMAccess y PowerShell</span><span class="sxs-lookup"><span data-stu-id="56456-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="56456-126">Asegúrese de hello seguro que VM Agent esté instalado en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="56456-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="56456-127">Hola extensión VMAccess no necesita toobe instalado para poder usar, como Hola agente de máquina virtual está disponible.</span><span class="sxs-lookup"><span data-stu-id="56456-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="56456-128">Compruebe que Hola que ya está instalado el agente de máquina virtual usando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="56456-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="56456-129">(Reemplace "myCloudService" y "myVM" hello nombres de servicio en la nube y la máquina virtual, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="56456-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="56456-130">Para saber qué nombres son, ejecute `Get-AzureVM` sin ningún parámetro).</span><span class="sxs-lookup"><span data-stu-id="56456-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="56456-131">Si hello **escritura host** comando muestra **True**, Hola está instalado el agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56456-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="56456-132">Si muestra **False**, consulte las instrucciones de Hola y un toohello vínculo Descargar Hola [agente de máquina virtual y extensiones: parte 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) entrada de blog de Azure.</span><span class="sxs-lookup"><span data-stu-id="56456-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="56456-133">Si ha creado la máquina virtual de Hola mediante el portal de hello, compruebe si `$vm.GetInstance().ProvisionGuestAgent` devuelve **True**.</span><span class="sxs-lookup"><span data-stu-id="56456-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="56456-134">De lo contrario, puede configurarlo con este comando:</span><span class="sxs-lookup"><span data-stu-id="56456-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="56456-135">Este comando impide Hola siguiente error si estás ejecutando hello **Set-AzureVMExtension** comando en pasos de hello: "Aprovisionar el agente invitado debe habilitarse en el objeto de máquina virtual de hello antes de establecer la extensión de acceso de VM de IaaS."</span><span class="sxs-lookup"><span data-stu-id="56456-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="56456-136">**Restablecer la contraseña de cuenta de administrador local de Hola**</span><span class="sxs-lookup"><span data-stu-id="56456-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="56456-137">Crear una credencial de inicio de sesión con nombre de cuenta de administrador local actual hello y una contraseña nueva y, a continuación, ejecute hello `Set-AzureVMAccessExtension` como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="56456-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="56456-138">Si escribe un nombre diferente de la cuenta actual de hello, Hola extensión VMAccess cambia el nombre de cuenta de administrador local de hello, asigna la cuenta de hello contraseña toothat y emite un cierre de sesión de escritorio remoto. Si se deshabilita la cuenta de administrador local de hello, Hola extensión VMAccess lo habilita.</span><span class="sxs-lookup"><span data-stu-id="56456-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="56456-139">Estos comandos también restablecen la configuración del servicio de escritorio remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="56456-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="56456-140">**Restablecer la configuración de servicios de escritorio remoto de Hola**</span><span class="sxs-lookup"><span data-stu-id="56456-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="56456-141">tooreset Hola servicio configuración de escritorio remoto, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="56456-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="56456-142">Hola extensión VMAccess ejecuta dos comandos en la máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="56456-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="56456-143">Este comando habilita a grupo Firewall de Windows integrado Hola que permite el tráfico entrante de escritorio remoto, que usa el puerto TCP 3389.</span><span class="sxs-lookup"><span data-stu-id="56456-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="56456-144">Este comando establece hello fDenyTSConnections del Registro valor too0, lo que permite conexiones de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="56456-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56456-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56456-145">Next steps</span></span>
<span data-ttu-id="56456-146">Si Hola extensión de acceso de la máquina virtual de Azure no responde y contraseña de hello tooreset no se puede, puede [restablecimiento Hola local contraseña de Windows sin conexión](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56456-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="56456-147">Este método es un proceso más avanzado y requiere tooconnect Hola disco duro de hello problemático VM tooanother máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56456-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="56456-148">Siga los pasos de hello primero se documentan en este artículo y solo intentar método de restablecimiento de contraseña sin conexión hello como último recurso.</span><span class="sxs-lookup"><span data-stu-id="56456-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="56456-149">Características y extensiones de las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="56456-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="56456-150">Conectar tooan máquina virtual de Azure con RDP o SSH</span><span class="sxs-lookup"><span data-stu-id="56456-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="56456-151">Solucionar problemas de escritorio remoto conexiones tooa basados en Windows Azure máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56456-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


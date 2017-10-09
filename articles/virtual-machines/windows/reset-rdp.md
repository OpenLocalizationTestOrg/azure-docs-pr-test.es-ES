---
title: "aaaReset Hola contraseña o la configuración de escritorio remoto en una máquina virtual de Windows | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooreset una contraseña de cuenta o servicios de escritorio remoto en una VM de Windows con Hola portal de Azure o Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="9751c-103">¿Cómo tooreset Hola servicios de escritorio remoto o su contraseña de inicio de sesión en una máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="9751c-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="9751c-104">Si no se puede conectar la máquina virtual de Windows tooa (VM), puede restablecer la contraseña de administrador local de Hola o restablecer la configuración de servicios de escritorio remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="9751c-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="9751c-105">Puede usar cualquier extensión de acceso a máquinas virtuales de portal o hello Azure hello en la contraseña de Azure PowerShell tooreset Hola.</span><span class="sxs-lookup"><span data-stu-id="9751c-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="9751c-106">Si usa PowerShell, asegúrese de que dispone de hello [módulo más reciente de PowerShell instalado y configurado](/powershell/azure/overview) y han iniciado sesión en tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9751c-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="9751c-107">También puede [realizar estos pasos para las máquinas virtuales creadas con el modelo de implementación clásica de hello](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="9751c-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="9751c-108">Configuración de formas tooreset o las credenciales</span><span class="sxs-lookup"><span data-stu-id="9751c-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="9751c-109">Puede restablecer los servicios y las credenciales de Escritorio remoto de varias maneras diferentes, dependiendo de sus necesidades:</span><span class="sxs-lookup"><span data-stu-id="9751c-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="9751c-110">Restablecer mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9751c-110">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="9751c-111">Restablecimiento mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9751c-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="9751c-112">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9751c-112">Azure portal</span></span>
<span data-ttu-id="9751c-113">menús tooexpand Hola del portal, haga clic en hello tres barras en la esquina superior izquierda de hello y, a continuación, haga clic en **máquinas virtuales**:</span><span class="sxs-lookup"><span data-stu-id="9751c-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![Busque la máquina virtual de Azure.](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="9751c-115">**Restablecer la contraseña de cuenta de administrador local de Hola**</span><span class="sxs-lookup"><span data-stu-id="9751c-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="9751c-116">Seleccione la máquina virtual Windows, haga clic en **Soporte y solución de problemas** > **Restablecer contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9751c-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="9751c-117">se muestra la hoja de restablecimiento de contraseña de Hello:</span><span class="sxs-lookup"><span data-stu-id="9751c-117">hello password reset blade is displayed:</span></span>

![Página Restablecimiento de contraseña](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="9751c-119">Escriba el nombre de usuario de hello y una contraseña nueva, a continuación, haga clic en **actualización**.</span><span class="sxs-lookup"><span data-stu-id="9751c-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="9751c-120">Intente conectarse de nuevo tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9751c-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="9751c-121">**Restablecer la configuración de servicios de escritorio remoto de Hola**</span><span class="sxs-lookup"><span data-stu-id="9751c-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="9751c-122">Seleccione la máquina virtual Windows, haga clic en **Soporte y solución de problemas** > **Restablecer contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9751c-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="9751c-123">se muestra la hoja de restablecimiento de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="9751c-123">hello password reset blade is displayed.</span></span> 

![Restablecer configuración de RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="9751c-125">Seleccione **configuración del restablecimiento solo** desde el menú desplegable de hello, a continuación, haga clic en **actualización**.</span><span class="sxs-lookup"><span data-stu-id="9751c-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="9751c-126">Intente conectarse de nuevo tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9751c-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="9751c-127">Extensión VMAccess y PowerShell</span><span class="sxs-lookup"><span data-stu-id="9751c-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="9751c-128">Asegúrese de que dispone de hello [módulo más reciente de PowerShell instalado y configurado](/powershell/azure/overview) y han iniciado sesión en tooyour suscripción de Azure con hello `Login-AzureRmAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9751c-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="9751c-129">**Restablecer la contraseña de cuenta de administrador local de Hola**</span><span class="sxs-lookup"><span data-stu-id="9751c-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="9751c-130">Restablecimiento de hello administrador contraseña nombre de usuario o con hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9751c-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="9751c-131">Cree sus credenciales de cuenta de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="9751c-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="9751c-132">Si escribe un nombre diferente de la cuenta de administrador local actual de hello en su máquina virtual, Hola extensión VMAccess cambia el nombre de cuenta de administrador local de hello, asigna la cuenta de toothat contraseña especificada y emite un evento de cierre de sesión de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="9751c-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="9751c-133">Si se deshabilita la cuenta de administrador local de hello en su máquina virtual, Hola extensión VMAccess lo habilita.</span><span class="sxs-lookup"><span data-stu-id="9751c-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="9751c-134">Después de las actualizaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup` credenciales toohello especificadas.</span><span class="sxs-lookup"><span data-stu-id="9751c-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="9751c-135">**Restablecer la configuración de servicios de escritorio remoto de Hola**</span><span class="sxs-lookup"><span data-stu-id="9751c-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="9751c-136">Restablecer el acceso remoto tooyour VM con hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9751c-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="9751c-137">Hello en el ejemplo siguiente se restablece extensión de acceso de hello denominada `myVMAccess` en máquina virtual denominada hello `myVM` en hello `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="9751c-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="9751c-138">En cualquier momento, una VM puede tener un solo agente de acceso a VM.</span><span class="sxs-lookup"><span data-stu-id="9751c-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="9751c-139">propiedades de agente de acceso VM de tooset Hola Hola correctamente, `-ForceRerun` opción puede utilizarse.</span><span class="sxs-lookup"><span data-stu-id="9751c-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="9751c-140">Cuando se usa `-ForceRerun`, asegúrese de que toouse Hola el mismo nombre para el agente de acceso de máquina virtual de hello tal y como se usan en los comandos anteriores.</span><span class="sxs-lookup"><span data-stu-id="9751c-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="9751c-141">Si todavía no se puede conectar remotamente tooyour virtual machine, vea más tootry de pasos en [solucionar problemas de escritorio remoto conexiones tooa basados en Windows Azure máquina virtual](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9751c-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9751c-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9751c-142">Next steps</span></span>
<span data-ttu-id="9751c-143">Si Hola extensión de acceso de la máquina virtual de Azure no responde y contraseña de hello tooreset no se puede, puede [restablecimiento Hola local contraseña de Windows sin conexión](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9751c-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9751c-144">Este método es un proceso más avanzado y requiere tooconnect Hola disco duro de hello problemático VM tooanother máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9751c-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="9751c-145">Siga los pasos de hello primero se documentan en este artículo y solo intentar método de restablecimiento de contraseña sin conexión hello como último recurso.</span><span class="sxs-lookup"><span data-stu-id="9751c-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="9751c-146">Características y extensiones de las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="9751c-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="9751c-147">Conectar tooan máquina virtual de Azure con RDP o SSH</span><span class="sxs-lookup"><span data-stu-id="9751c-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="9751c-148">Solucionar problemas de escritorio remoto conexiones tooa basados en Windows Azure máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9751c-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


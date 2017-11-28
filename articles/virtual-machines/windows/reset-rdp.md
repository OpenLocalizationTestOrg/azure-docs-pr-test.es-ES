---
title: "Restablecimiento de la contraseña o la configuración de Escritorio remoto en una VM Windows | Microsoft Docs"
description: "Aprenda a restablecer la contraseña de una cuenta o los servicios de Escritorio remoto en una máquina virtual Windows mediante Azure Portal o Azure PowerShell."
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
ms.openlocfilehash: 2e002e3f336422b8fa1eceece889cd083e355a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="1f193-103">Restablecimiento del servicio Escritorio remoto o la contraseña de inicio de sesión en una VM con Windows</span><span class="sxs-lookup"><span data-stu-id="1f193-103">How to reset the Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="1f193-104">Si no puede conectarse a una máquina virtual Windows, puede restablecer la contraseña de administrador local o la configuración de servicio de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="1f193-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="1f193-105">Puede usar el Portal de Azure o la extensión de acceso de máquina virtual en Azure PowerShell para restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="1f193-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span> <span data-ttu-id="1f193-106">Si usa Azure PowerShell, asegúrese de tener [instalado y configurado el módulo de PowerShell más reciente](/powershell/azure/overview) y haber iniciado sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1f193-106">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription.</span></span> <span data-ttu-id="1f193-107">También puede [realizar estos pasos para máquinas virtuales creadas con el modelo de implementación clásica](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="1f193-107">You can also [perform these steps for VMs created with the Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="1f193-108">Métodos para restablecer la configuración o las credenciales</span><span class="sxs-lookup"><span data-stu-id="1f193-108">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="1f193-109">Puede restablecer los servicios y las credenciales de Escritorio remoto de varias maneras diferentes, dependiendo de sus necesidades:</span><span class="sxs-lookup"><span data-stu-id="1f193-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="1f193-110">Restablecimiento mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1f193-110">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="1f193-111">Restablecimiento mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f193-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="1f193-112">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1f193-112">Azure portal</span></span>
<span data-ttu-id="1f193-113">Para expandir los menús del portal, haga clic en las tres barras en la esquina superior izquierda y, a continuación, en **Máquinas virtuales**:</span><span class="sxs-lookup"><span data-stu-id="1f193-113">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span></span>

![Busque la máquina virtual de Azure.](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="1f193-115">**Restablecer la contraseña de cuenta de administración local**</span><span class="sxs-lookup"><span data-stu-id="1f193-115">**Reset the local administrator account password**</span></span>

<span data-ttu-id="1f193-116">Seleccione la máquina virtual Windows, haga clic en **Soporte y solución de problemas** > **Restablecer contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1f193-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="1f193-117">Se mostrará la hoja de restablecimiento de contraseña:</span><span class="sxs-lookup"><span data-stu-id="1f193-117">The password reset blade is displayed:</span></span>

![Página Restablecimiento de contraseña](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="1f193-119">Escriba el nombre de usuario y una nueva contraseña nueva; después, haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="1f193-119">Enter the username and a new password, then click **Update**.</span></span> <span data-ttu-id="1f193-120">Trate de conectarse de nuevo a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f193-120">Try connecting to your VM again.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="1f193-121">**Restablecer la configuración de servicio de Escritorio remoto**</span><span class="sxs-lookup"><span data-stu-id="1f193-121">**Reset the Remote Desktop service configuration**</span></span>

<span data-ttu-id="1f193-122">Seleccione la máquina virtual Windows, haga clic en **Soporte y solución de problemas** > **Restablecer contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1f193-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="1f193-123">Se mostrará la hoja de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="1f193-123">The password reset blade is displayed.</span></span> 

![Restablecer configuración de RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="1f193-125">Seleccione **Restablecer solo configuración** en el menú desplegable y, a continuación, haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="1f193-125">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span></span> <span data-ttu-id="1f193-126">Trate de conectarse de nuevo a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f193-126">Try connecting to your VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="1f193-127">Extensión VMAccess y PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f193-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="1f193-128">Asegúrese de tener [instalado y configurado el módulo de PowerShell más reciente](/powershell/azure/overview) y haber iniciado sesión en su suscripción de Azure con el cmdlet `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="1f193-128">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription with the `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="1f193-129">**Restablecer la contraseña de cuenta de administración local**</span><span class="sxs-lookup"><span data-stu-id="1f193-129">**Reset the local administrator account password**</span></span>
<span data-ttu-id="1f193-130">Restablezca la contraseña de administrador o el nombre de usuario con el comando de PowerShell [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension).</span><span class="sxs-lookup"><span data-stu-id="1f193-130">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="1f193-131">Cree sus credenciales de cuenta de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="1f193-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="1f193-132">Si escribe un nombre distinto al de la cuenta de administrador local actual en la máquina virtual, la siguiente extensión VMAccess cambia el nombre de la cuenta de administrador local, asigna la contraseña especificada a esa cuenta y emite un evento de cierre de sesión con Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="1f193-132">If you type a different name than the current local administrator account on your VM, the VMAccess extension renames the local administrator account, assigns your specified password to that account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="1f193-133">Si la cuenta de administrador local en la máquina virtual está deshabilitada, la extensión VMAccess la habilita.</span><span class="sxs-lookup"><span data-stu-id="1f193-133">If the local administrator account on your VM is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="1f193-134">En el ejemplo siguiente se actualiza la máquina virtual llamada `myVM` en el grupo de recursos `myResourceGroup` a las credenciales especificadas.</span><span class="sxs-lookup"><span data-stu-id="1f193-134">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to the credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="1f193-135">**Restablecer la configuración de servicio de Escritorio remoto**</span><span class="sxs-lookup"><span data-stu-id="1f193-135">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="1f193-136">Restablezca el acceso remoto a la máquina virtual con el cmdlet de PowerShell [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension).</span><span class="sxs-lookup"><span data-stu-id="1f193-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="1f193-137">En el ejemplo siguiente se habilita se restablece la extensión de acceso llamada `myVMAccess` en la máquina virtual denominada `myVM` en el grupo de recursos `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="1f193-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="1f193-138">En cualquier momento, una VM puede tener un solo agente de acceso a VM.</span><span class="sxs-lookup"><span data-stu-id="1f193-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="1f193-139">Para establecer las propiedades del agente de acceso de la máquina virtual correctamente, puede usarse la opción `-ForceRerun`.</span><span class="sxs-lookup"><span data-stu-id="1f193-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span></span> <span data-ttu-id="1f193-140">Al usar `-ForceRerun`, procure usar el mismo nombre para el agente de acceso de máquina virtual establecido en los comandos anteriores.</span><span class="sxs-lookup"><span data-stu-id="1f193-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="1f193-141">Si sigue sin poder conectarse remotamente a la máquina virtual, consulte más pasos que puede tratar de realizar en [Solución de problemas de conexiones del Escritorio remoto a una máquina virtual de Azure con Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f193-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="1f193-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1f193-142">Next steps</span></span>
<span data-ttu-id="1f193-143">Si la extensión de acceso de la máquina virtual de Azure no responde y no puede restablecer la contraseña, puede [restablecer la contraseña de Windows local sin conexión](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f193-143">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1f193-144">Este método es un proceso más avanzado y requiere que se conecte el disco duro virtual de la máquina virtual problemática a otra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f193-144">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="1f193-145">Primero siga los pasos descritos en este artículo e intente solamente el método de restablecimiento de contraseña sin conexión como último recurso.</span><span class="sxs-lookup"><span data-stu-id="1f193-145">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="1f193-146">Características y extensiones de las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="1f193-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="1f193-147">Conexión a una máquina virtual de Azure con RDP o SSH</span><span class="sxs-lookup"><span data-stu-id="1f193-147">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="1f193-148">Solucionar problemas de conexiones de Escritorio remoto a una máquina virtual de Azure basada en Windows</span><span class="sxs-lookup"><span data-stu-id="1f193-148">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>¿Cómo tooreset Hola servicios de escritorio remoto o su contraseña de inicio de sesión en una máquina virtual de Windows
Si no se puede conectar la máquina virtual de Windows tooa (VM), puede restablecer la contraseña de administrador local de Hola o restablecer la configuración de servicios de escritorio remoto de Hola. Puede usar cualquier extensión de acceso a máquinas virtuales de portal o hello Azure hello en la contraseña de Azure PowerShell tooreset Hola. Si usa PowerShell, asegúrese de que dispone de hello [módulo más reciente de PowerShell instalado y configurado](/powershell/azure/overview) y han iniciado sesión en tooyour suscripción de Azure. También puede [realizar estos pasos para las máquinas virtuales creadas con el modelo de implementación clásica de hello](reset-rdp.md).

## <a name="ways-tooreset-configuration-or-credentials"></a>Configuración de formas tooreset o las credenciales
Puede restablecer los servicios y las credenciales de Escritorio remoto de varias maneras diferentes, dependiendo de sus necesidades:

- [Restablecer mediante Hola portal de Azure](#azure-portal)
- [Restablecimiento mediante Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure Portal
menús tooexpand Hola del portal, haga clic en hello tres barras en la esquina superior izquierda de hello y, a continuación, haga clic en **máquinas virtuales**:

![Busque la máquina virtual de Azure.](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**Restablecer la contraseña de cuenta de administrador local de Hola**

Seleccione la máquina virtual Windows, haga clic en **Soporte y solución de problemas** > **Restablecer contraseña**. se muestra la hoja de restablecimiento de contraseña de Hello:

![Página Restablecimiento de contraseña](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Escriba el nombre de usuario de hello y una contraseña nueva, a continuación, haga clic en **actualización**. Intente conectarse de nuevo tooyour máquina virtual.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Restablecer la configuración de servicios de escritorio remoto de Hola**

Seleccione la máquina virtual Windows, haga clic en **Soporte y solución de problemas** > **Restablecer contraseña**. se muestra la hoja de restablecimiento de contraseña de Hola. 

![Restablecer configuración de RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

Seleccione **configuración del restablecimiento solo** desde el menú desplegable de hello, a continuación, haga clic en **actualización**. Intente conectarse de nuevo tooyour máquina virtual.


## <a name="vmaccess-extension-and-powershell"></a>Extensión VMAccess y PowerShell
Asegúrese de que dispone de hello [módulo más reciente de PowerShell instalado y configurado](/powershell/azure/overview) y han iniciado sesión en tooyour suscripción de Azure con hello `Login-AzureRmAccount` cmdlet.

### <a name="reset-hello-local-administrator-account-password"></a>**Restablecer la contraseña de cuenta de administrador local de Hola**
Restablecimiento de hello administrador contraseña nombre de usuario o con hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet de PowerShell. Cree sus credenciales de cuenta de la manera siguiente:

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> Si escribe un nombre diferente de la cuenta de administrador local actual de hello en su máquina virtual, Hola extensión VMAccess cambia el nombre de cuenta de administrador local de hello, asigna la cuenta de toothat contraseña especificada y emite un evento de cierre de sesión de escritorio remoto. Si se deshabilita la cuenta de administrador local de hello en su máquina virtual, Hola extensión VMAccess lo habilita.

Después de las actualizaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup` credenciales toohello especificadas.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Restablecer la configuración de servicios de escritorio remoto de Hola**
Restablecer el acceso remoto tooyour VM con hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet de PowerShell. Hello en el ejemplo siguiente se restablece extensión de acceso de hello denominada `myVMAccess` en máquina virtual denominada hello `myVM` en hello `myResourceGroup` grupo de recursos:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> En cualquier momento, una VM puede tener un solo agente de acceso a VM. propiedades de agente de acceso VM de tooset Hola Hola correctamente, `-ForceRerun` opción puede utilizarse. Cuando se usa `-ForceRerun`, asegúrese de que toouse Hola el mismo nombre para el agente de acceso de máquina virtual de hello tal y como se usan en los comandos anteriores.

Si todavía no se puede conectar remotamente tooyour virtual machine, vea más tootry de pasos en [solucionar problemas de escritorio remoto conexiones tooa basados en Windows Azure máquina virtual](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Pasos siguientes
Si Hola extensión de acceso de la máquina virtual de Azure no responde y contraseña de hello tooreset no se puede, puede [restablecimiento Hola local contraseña de Windows sin conexión](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Este método es un proceso más avanzado y requiere tooconnect Hola disco duro de hello problemático VM tooanother máquina virtual. Siga los pasos de hello primero se documentan en este artículo y solo intentar método de restablecimiento de contraseña sin conexión hello como último recurso.

[Características y extensiones de las máquinas virtuales de Azure](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Conectar tooan máquina virtual de Azure con RDP o SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Solucionar problemas de escritorio remoto conexiones tooa basados en Windows Azure máquina virtual](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


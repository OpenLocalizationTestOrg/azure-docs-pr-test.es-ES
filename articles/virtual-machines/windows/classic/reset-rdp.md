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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Cómo servicios de escritorio remoto de hello tooreset ni su contraseña de inicio de sesión en una máquina virtual de Windows creado con el modelo de implementación clásica de Hola
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. También puede [realizar estos pasos para las máquinas virtuales creadas con el modelo de implementación del Administrador de recursos de hello](../reset-rdp.md).

Si no se puede conectar la máquina virtual de Windows tooa (VM), puede restablecer la contraseña de administrador local de Hola o restablecer la configuración de servicios de escritorio remoto de Hola. Puede usar cualquier extensión de acceso a máquinas virtuales de portal o hello Azure hello en la contraseña de Azure PowerShell tooreset Hola.

## <a name="ways-tooreset-configuration-or-credentials"></a>Configuración de formas tooreset o las credenciales
Puede restablecer los servicios y las credenciales de Escritorio remoto de varias maneras diferentes, dependiendo de sus necesidades:

- [Restablecer mediante Hola portal de Azure](#azure-portal)
- [Restablecimiento mediante Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure Portal
Puede usar hello [portal de Azure](https://portal.azure.com) tooreset Hola servicios de escritorio remoto. menús tooexpand Hola del portal, haga clic en hello tres barras en la esquina superior izquierda de hello y, a continuación, haga clic en **máquinas virtuales (clásicas)**:

![Busque la máquina virtual de Azure.](./media/reset-rdp/Portal-Select-Classic-VM.png)

Seleccione la máquina virtual de Windows y, a continuación, haga clic en **restablecer remoto...** . hello siguiente aparece cuadro de diálogo Configuración de escritorio remoto de Hola tooreset:

![Página Restablecer configuración de RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

También puede restablecer Hola nombre de usuario y la contraseña de cuenta de administrador local de Hola. En la máquina virtual, haga clic en **Soporte y solución de problemas** > **Restablecer contraseña**. se muestra la hoja de restablecimiento de contraseña de Hello:

![Página Restablecimiento de contraseña](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Después de escribir Hola nuevo nombre de usuario y contraseña, haga clic en **guardar**.

## <a name="vmaccess-extension-and-powershell"></a>Extensión VMAccess y PowerShell
Asegúrese de hello seguro que VM Agent esté instalado en la máquina virtual de Hola. Hola extensión VMAccess no necesita toobe instalado para poder usar, como Hola agente de máquina virtual está disponible. Compruebe que Hola que ya está instalado el agente de máquina virtual usando el siguiente comando de Hola. (Reemplace "myCloudService" y "myVM" hello nombres de servicio en la nube y la máquina virtual, respectivamente. Para saber qué nombres son, ejecute `Get-AzureVM` sin ningún parámetro).

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Si hello **escritura host** comando muestra **True**, Hola está instalado el agente de máquina virtual. Si muestra **False**, consulte las instrucciones de Hola y un toohello vínculo Descargar Hola [agente de máquina virtual y extensiones: parte 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) entrada de blog de Azure.

Si ha creado la máquina virtual de Hola mediante el portal de hello, compruebe si `$vm.GetInstance().ProvisionGuestAgent` devuelve **True**. De lo contrario, puede configurarlo con este comando:

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

Este comando impide Hola siguiente error si estás ejecutando hello **Set-AzureVMExtension** comando en pasos de hello: "Aprovisionar el agente invitado debe habilitarse en el objeto de máquina virtual de hello antes de establecer la extensión de acceso de VM de IaaS."

### <a name="reset-hello-local-administrator-account-password"></a>**Restablecer la contraseña de cuenta de administrador local de Hola**
Crear una credencial de inicio de sesión con nombre de cuenta de administrador local actual hello y una contraseña nueva y, a continuación, ejecute hello `Set-AzureVMAccessExtension` como se indica a continuación.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Si escribe un nombre diferente de la cuenta actual de hello, Hola extensión VMAccess cambia el nombre de cuenta de administrador local de hello, asigna la cuenta de hello contraseña toothat y emite un cierre de sesión de escritorio remoto. Si se deshabilita la cuenta de administrador local de hello, Hola extensión VMAccess lo habilita.

Estos comandos también restablecen la configuración del servicio de escritorio remoto de Hola.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Restablecer la configuración de servicios de escritorio remoto de Hola**
tooreset Hola servicio configuración de escritorio remoto, ejecute el siguiente comando de hello:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Hola extensión VMAccess ejecuta dos comandos en la máquina virtual de hello:

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

Este comando habilita a grupo Firewall de Windows integrado Hola que permite el tráfico entrante de escritorio remoto, que usa el puerto TCP 3389.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

Este comando establece hello fDenyTSConnections del Registro valor too0, lo que permite conexiones de escritorio remoto.

## <a name="next-steps"></a>Pasos siguientes
Si Hola extensión de acceso de la máquina virtual de Azure no responde y contraseña de hello tooreset no se puede, puede [restablecimiento Hola local contraseña de Windows sin conexión](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Este método es un proceso más avanzado y requiere tooconnect Hola disco duro de hello problemático VM tooanother máquina virtual. Siga los pasos de hello primero se documentan en este artículo y solo intentar método de restablecimiento de contraseña sin conexión hello como último recurso.

[Características y extensiones de las máquinas virtuales de Azure](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Conectar tooan máquina virtual de Azure con RDP o SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Solucionar problemas de escritorio remoto conexiones tooa basados en Windows Azure máquina virtual](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


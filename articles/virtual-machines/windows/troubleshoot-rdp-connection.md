---
title: aaaCannot conectarse con RDP tooa VM de Windows en Azure | Documentos de Microsoft
description: "Solucionar problemas cuando no se puede conectar la máquina virtual de Windows tooyour en Azure mediante Escritorio remoto"
keywords: "Error de escritorio remoto, error de conexión a Escritorio remoto, no se puede conectar tooVM, solución de problemas de escritorio remoto"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>Solucionar problemas de conexiones de escritorio remoto tooan máquina virtual de Azure
Hola protocolo de escritorio remoto (RDP) conexión tooyour basados en Windows Azure máquina virtual (VM) puede producir un error por diversas razones, dejando tooaccess no se puede la máquina virtual. problema de Hello puede ser con hello servicios de escritorio remoto en hello VM, la conexión de red de Hola o el cliente de escritorio remoto de hello en el equipo host. En este artículo le guía a través de algunas Hola problemas más comunes que métodos tooresolve RDP conexión. 

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>Pasos rápidos para solucionar problemas
Después de cada paso de la solución de problemas, intente volver a conectarse toohello VM:

1. Restablezca la configuración de Escritorio remoto.
2. Compruebe las reglas de grupo de seguridad de red/puntos de conexión de Cloud Services.
3. Revise los registros de la consola de máquina virtual.
4. Restablecer hello NIC para VM Hola.
5. Hola de comprobación de mantenimiento de recursos de máquina virtual.
6. Restablezca la contraseña de la máquina virtual.
7. Reinicie la máquina virtual.
8. Vuelva a implementar la máquina virtual.

Si necesita instrucciones más detalladas y explicaciones, siga leyendo. Compruebe que el equipo de red local, como enrutadores y firewalls, no están bloqueando el puerto TCP 3389 saliente, como se indicó en [los escenarios de solución de problemas de RDP detallados](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!TIP]
> Si hello **conectar** botón de la máquina virtual aparece en gris horizontal en el portal de Hola y no es tooAzure conectado a través de un [Express Route](../../expressroute/expressroute-introduction.md) o [VPN de sitio a sitio](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) conexión, que necesita toocreate y asignar la máquina virtual una IP pública resolver antes de puedan utilizar RDP. Aquí puede leer más sobre [direcciones IP públicas en Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).


## <a name="ways-tootroubleshoot-rdp-issues"></a>Problemas de RDP de formas tootroubleshoot
Puede solucionar el problema de máquinas virtuales creadas mediante el modelo de implementación del Administrador de recursos de hello mediante uno de los siguientes métodos de hello:

* [Portal de Azure](#using-the-azure-portal) : great si necesita tooquickly restablece credenciales de usuario o configuración de RDP hello y no haya Hola instaladas herramientas de Azure.
* [Azure PowerShell](#using-azure-powershell) : si está familiarizado con un símbolo del sistema de PowerShell, rápidamente restablecimiento Hola RDP configuración o credenciales de usuario con los cmdlets de PowerShell de Azure de Hola.

También puede consultar los pasos para solucionar problemas de máquinas virtuales creadas mediante hello [modelo de implementación clásica](#troubleshoot-vms-created-using-the-classic-deployment-model).

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Solucionar problemas mediante Hola portal de Azure
Después de cada paso de la solución de problemas, intente conectarse de nuevo tooyour máquina virtual. Si sigue sin poder conectarse, pruebe el paso siguiente Hola.

1. **Restablezca la conexión RDP**. Este paso para solucionar problemas restablece la configuración de RDP de hello cuando las conexiones remotas están deshabilitadas o las reglas de Firewall de Windows están bloqueando RDP, por ejemplo.
   
    Seleccione la máquina virtual en hello portal de Azure. Desplácese hacia abajo en hello configuración panel toohello **soporte técnico y solución de problemas** sección cerca de la parte inferior de la lista de Hola. Haga clic en hello **de restablecimiento de contraseña** botón. Conjunto hello **modo** demasiado**Restablecer configuración solo** y, a continuación, haga clic en hello **actualización** botón:
   
    ![Restablecer configuración de RDP Hola Hola portal de Azure](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **Compruebe las reglas del grupo de seguridad de red**. Use [comprobar flujo IP](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm si una regla en un grupo de seguridad de red está bloqueando el tráfico tooor desde una máquina virtual. También puede revisar el grupo de seguridad eficaz reglas tooensure de entrada "Permitir" NSG regla existe y se establece una prioridad para el puerto RDP (valor predeterminado 3389). Para obtener más información, consulte [flujo del tráfico con reglas de seguridad efectivo tootroubleshoot VM](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

3. **Revise los diagnósticos de arranque de la máquina virtual**. Este paso para solucionar problemas revisa Hola VM consola registros toodetermine si Hola VM está informando de un problema. No todas las máquinas virtuales tienen diagnósticos de arranque habilitados, por lo que este paso para solucionar problemas puede ser opcional.
   
    Pasos de solución de problemas específicos son más allá del ámbito de Hola de este artículo, pero pueden indicar un problema más amplio que está afectando a la conectividad RDP. Para obtener más información acerca de cómo revisar los registros de la consola de Hola y captura de pantalla de máquina virtual, consulte [el diagnóstico de arranque para máquinas virtuales](boot-diagnostics.md).

4. **Restablecimiento de hello NIC para VM de hello**. Para obtener más información, consulte [cómo tooreset NIC para VM de Windows Azure](reset-network-interface.md).
5. **Comprobar Hola mantenimiento de recursos de máquina virtual**. Este paso para solucionar problemas comprueba que no hay ningún problema conocido con hello plataforma Windows Azure que afecte a conectividad toohello máquina virtual.
   
    Seleccione la máquina virtual en hello portal de Azure. Desplácese hacia abajo en hello configuración panel toohello **soporte técnico y solución de problemas** sección cerca de la parte inferior de la lista de Hola. Haga clic en hello **estado de los recursos** botón. Una máquina virtual correcta se notifica como **Disponible**:
   
    ![Comprobar estado de recursos de máquina virtual en hello portal de Azure](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **Restablezca las credenciales de usuario**. Este paso para solucionar problemas restablece la contraseña de hello en una cuenta de administrador local cuando no está seguro o ha olvidado credenciales Hola.
   
    Seleccione la máquina virtual en hello portal de Azure. Desplácese hacia abajo en hello configuración panel toohello **soporte técnico y solución de problemas** sección cerca de la parte inferior de la lista de Hola. Haga clic en hello **de restablecimiento de contraseña** botón. Asegúrese de hello seguro **modo** se establece demasiado**de restablecimiento de contraseña** y, a continuación, escriba el nombre de usuario y una contraseña nueva. Por último, haga clic en hello **actualización** botón:
   
    ![Restablecer credenciales de usuario de Hola Hola portal de Azure](./media/troubleshoot-rdp-connection/reset-password.png)
7. **Reinicie la máquina virtual**. Este paso de solución de problemas puede corregir cualquier problema subyacente tiene Hola propia máquina virtual.
   
    Seleccione la máquina virtual en Hola portal de Azure y haga clic en hello **Introducción** ficha. Haga clic en hello **reiniciar** botón:
   
    ![Reiniciar VM Hola Hola portal de Azure](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **Vuelva a implementar la máquina virtual**. Este paso para solucionar problemas vuelve a implementar el host de máquina virtual tooanother dentro de Azure toocorrect cualquier problema de plataforma o conexión de red subyacente.
   
    Seleccione la máquina virtual en hello portal de Azure. Desplácese hacia abajo en hello configuración panel toohello **soporte técnico y solución de problemas** sección cerca de la parte inferior de la lista de Hola. Haga clic en hello **volver a implementar** botón y, a continuación, haga clic en **volver a implementar**:
   
    ![Volver a implementar Hola VM Hola portal de Azure](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    Una vez finalizada esta operación, datos de disco efímero están dinámicas y perdidas direcciones IP que están asociadas con hello VM se actualizan.

Si sigue teniendo problemas con RDP, puede [abrir una solicitud de soporte técnico](https://azure.microsoft.com/support/options/) o leer [más pasos y conceptos detallados de solución de problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-using-azure-powershell"></a>Solución de problemas mediante Azure PowerShell
Si no lo ha hecho ya, [instalar y configurar Hola más reciente de PowerShell de Azure](/powershell/azure/overview).

Hello en los ejemplos siguientes utilizan variables como `myResourceGroup`, `myVM`, y `myVMAccessExtension`. Reemplace estos nombres de variables y las ubicaciones por sus propios valores.

> [!NOTE]
> Restablecer las credenciales de usuario de Hola y configuración de RDP hello mediante hello [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet de PowerShell. Hola, en los ejemplos siguientes `myVMAccessExtension` es un nombre que especifique como parte del proceso de Hola. Si ha trabajado previamente con hello VMAccessAgent, puede obtener nombre de Hola de extensión existente de Hola mediante `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` toocheck propiedades de Hola de hello máquina virtual. nombre de hello tooview, busque sección Hola "Extensions" de la salida de hello.

Después de cada paso de la solución de problemas, intente conectarse de nuevo tooyour máquina virtual. Si sigue sin poder conectarse, pruebe el paso siguiente Hola.

1. **Restablezca la conexión RDP**. Este paso para solucionar problemas restablece la configuración de RDP de hello cuando las conexiones remotas están deshabilitadas o las reglas de Firewall de Windows están bloqueando RDP, por ejemplo.
   
    Hola seguimiento en el ejemplo se restablece la conexión RDP de hello en una máquina virtual denominada `myVM` en hello `WestUS` ubicación y en el grupo de recursos de hello llamado `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **Compruebe las reglas del grupo de seguridad de red**. Este paso para la solución comprueba que dispones de una regla en el tráfico RDP toopermit de grupo de seguridad de red. puerto predeterminado de Hola para RDP es el puerto TCP 3389. Un tráfico de RDP toopermit de regla no se crean automáticamente al crear la máquina virtual.
   
    En primer lugar, asigne todos los datos de configuración de hello para el grupo de seguridad de red toohello `$rules` variable. Hello en el ejemplo siguiente se obtiene información sobre Hola grupo de seguridad de red denominado `myNetworkSecurityGroup` en grupo de recursos de hello llamado `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    Ahora, ver las reglas de Hola que están configuradas para este grupo de seguridad de red. Compruebe que existe una regla tooallow el puerto TCP 3389 para las conexiones entrantes como se indica a continuación:
   
    ```powershell
    $rules.SecurityRules
    ```
   
    Hello en el ejemplo siguiente se muestra una regla de seguridad válido que permita el tráfico de RDP. Puede ver que `Protocol`, `DestinationPortRange`, `Access` y `Direction` están configurados correctamente:
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    Si no dispone de una regla que permita el tráfico RDP, [cree una regla de grupo de seguridad de red](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Permita el puerto TCP 3389.
3. **Restablezca las credenciales de usuario**. Este paso para solucionar problemas restablece la contraseña de hello en la cuenta de administrador local de Hola que especifique cuando no está seguro de, o ha olvidado, las credenciales de Hola.
   
    En primer lugar, especifique Hola nombre de usuario y una contraseña nueva mediante la asignación de credenciales toohello `$cred` variable como se indica a continuación:
   
    ```powershell
    $cred=Get-Credential
    ```
   
    Ahora, actualice las credenciales de hello en su máquina virtual. Hello en el ejemplo siguiente se actualiza las credenciales de hello en una máquina virtual denominada `myVM` en hello `WestUS` ubicación y en el grupo de recursos de hello llamado `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **Reinicie la máquina virtual**. Este paso de solución de problemas puede corregir cualquier problema subyacente tiene Hola propia máquina virtual.
   
    Después de reinicios del ejemplo de Hola Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **Vuelva a implementar la máquina virtual**. Este paso para solucionar problemas vuelve a implementar el host de máquina virtual tooanother dentro de Azure toocorrect cualquier problema de plataforma o conexión de red subyacente.
   
    Después de nuevas implementaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` en hello `WestUS` ubicación y en el grupo de recursos de hello llamado `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

Si sigue teniendo problemas con RDP, puede [abrir una solicitud de soporte técnico](https://azure.microsoft.com/support/options/) o leer [más pasos y conceptos detallados de solución de problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Solucionar problemas de máquinas virtuales creadas mediante el modelo de implementación de hello clásico
Después de cada paso de la solución de problemas, intente volver a conectarse toohello máquina virtual.

1. **Restablezca la conexión RDP**. Este paso para solucionar problemas restablece la configuración de RDP de hello cuando las conexiones remotas están deshabilitadas o las reglas de Firewall de Windows están bloqueando RDP, por ejemplo.
   
    Seleccione la máquina virtual en hello portal de Azure. Haga clic en hello **... Más** , a continuación, haga clic en **restablecer el acceso remoto**:
   
    ![Restablecer configuración de RDP Hola Hola portal de Azure](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Compruebe los puntos de conexión de Cloud Services**. Este paso para la solución comprueba que dispones de puntos de conexión en el tráfico RDP de toopermit de servicios en la nube. puerto predeterminado de Hola para RDP es el puerto TCP 3389. Un tráfico de RDP toopermit de regla no se crean automáticamente al crear la máquina virtual.
   
   Seleccione la máquina virtual en hello portal de Azure. Haga clic en hello **extremos** botón extremos de hello tooview configurados actualmente para la máquina virtual. Compruebe que hay puntos de conexión que permiten el tráfico RDP en el puerto TCP 3389.
   
   Hola siguiente ejemplo muestra los puntos de conexión válidos que permitan el tráfico RDP:
   
   ![Comprobar los extremos de servicios en la nube de hello portal de Azure](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   Si no tiene un punto de conexión que permita el tráfico RDP, [cree un punto de conexión de Cloud Services](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Permitir TCP tooprivate puerto 3389.
3. **Revise los diagnósticos de arranque de la máquina virtual**. Este paso para solucionar problemas revisa Hola VM consola registros toodetermine si Hola VM está informando de un problema. No todas las máquinas virtuales tienen diagnósticos de arranque habilitados, por lo que este paso para solucionar problemas puede ser opcional.
   
    Pasos de solución de problemas específicos son más allá del ámbito de Hola de este artículo, pero pueden indicar un problema más amplio que está afectando a la conectividad RDP. Para obtener más información acerca de cómo revisar los registros de la consola de Hola y captura de pantalla de máquina virtual, consulte [el diagnóstico de arranque para máquinas virtuales](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).
4. **Comprobar Hola mantenimiento de recursos de máquina virtual**. Este paso para solucionar problemas comprueba que no hay ningún problema conocido con hello plataforma Windows Azure que afecte a conectividad toohello máquina virtual.
   
    Seleccione la máquina virtual en hello portal de Azure. Desplácese hacia abajo en hello configuración panel toohello **soporte técnico y solución de problemas** sección cerca de la parte inferior de la lista de Hola. Haga clic en hello **estado de los recursos** botón. Una máquina virtual correcta se notifica como **Disponible**:
   
    ![Comprobar estado de recursos de máquina virtual en hello portal de Azure](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **Restablezca las credenciales de usuario**. Este paso para solucionar problemas restablece la contraseña de hello en la cuenta de administrador local de Hola que se especifica cuando no está seguro o ha olvidado credenciales Hola.
   
    Seleccione la máquina virtual en hello portal de Azure. Desplácese hacia abajo en hello configuración panel toohello **soporte técnico y solución de problemas** sección cerca de la parte inferior de la lista de Hola. Haga clic en hello **de restablecimiento de contraseña** botón. Escriba su nombre de usuario y una nueva contraseña. Por último, haga clic en hello **guardar** botón:
   
    ![Restablecer credenciales de usuario de Hola Hola portal de Azure](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **Reinicie la máquina virtual**. Este paso de solución de problemas puede corregir cualquier problema subyacente tiene Hola propia máquina virtual.
   
    Seleccione la máquina virtual en Hola portal de Azure y haga clic en hello **Introducción** ficha. Haga clic en hello **reiniciar** botón:
   
    ![Reiniciar VM Hola Hola portal de Azure](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

Si sigue teniendo problemas con RDP, puede [abrir una solicitud de soporte técnico](https://azure.microsoft.com/support/options/) o leer [más pasos y conceptos detallados de solución de problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-specific-rdp-errors"></a>Solución de errores específicos de RDP
Puede encontrar un mensaje de error específico al tratar de tooconnect tooyour máquina virtual a través de RDP. siguiente Hola es mensajes de error más comunes de saludo:

* [se desconectó la sesión remota de Hello porque no hay ningún tooprovide disponible servidores de licencias de escritorio remoto una licencia](troubleshoot-specific-rdp-errors.md#rdplicense).
* [Escritorio remoto no puede encontrar Hola "nombre" del equipo](troubleshoot-specific-rdp-errors.md#rdpname).
* [Se ha producido un error de autenticación. Hello autoridad de seguridad Local no se puede establecer contacto con](troubleshoot-specific-rdp-errors.md#rdpauth).
* [Error de Seguridad de Windows: Las credenciales no funcionaron](troubleshoot-specific-rdp-errors.md#wincred).
* [Este equipo no puede conectar el equipo remoto toohello](troubleshoot-specific-rdp-errors.md#rdpconnect).

## <a name="additional-resources"></a>Recursos adicionales
Si ninguno de estos errores se produjeron y sigue sin poder conectarse toohello máquina virtual mediante Escritorio remoto, lea Hola detallada [guía para escritorio remoto para solucionar problemas](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Para solucionar problemas de pasos al obtener acceso a aplicaciones que se ejecutan en una máquina virtual, consulte [aplicación tooan solucionar access que ejecuta en una VM de Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Si tiene problemas con el Shell seguro (SSH) tooconnect tooa VM de Linux en Azure, consulte [solucionar problemas de SSH conexiones tooa VM de Linux en Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


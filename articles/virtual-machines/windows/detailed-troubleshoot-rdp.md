---
title: solucionar problemas de Azure de escritorio remoto aaaDetailed | Documentos de Microsoft
description: "Revise los pasos de solución de problemas detallados para los errores de escritorio remotos donde no máquinas virtuales de Windows tooa en Azure"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "no se puede conectar tooremote escritorio, solucionar problemas de escritorio remoto, no se puede conectar a Escritorio remoto, los errores de escritorio remotos, la solución de problemas de escritorio de forma remota, problemas de escritorio remoto"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>Pasos detallados de solución de problemas de conexión a Escritorio remoto emite tooWindows máquinas virtuales en Azure
Este artículo proporciona pasos de solución de problemas detalladas toodiagnose y corregir errores complejos de escritorio remoto para máquinas virtuales Azure basadas en Windows.

> [!IMPORTANT]
> tooeliminate Hola los errores más comunes de escritorio remoto, asegúrese de que tooread [artículo de solución de problemas básicos de Hola para escritorio remoto](troubleshoot-rdp-connection.md) antes de continuar.

Puede encontrar un escritorio remoto trata el mensaje de error que no se parece a cualquiera de los mensajes de error específicos de Hola en [Hola guía para solucionar problemas de escritorio remoto básica](troubleshoot-rdp-connection.md). Siga estos toodetermine pasos ¿por qué cliente de escritorio remoto (RDP) de hello es servicio RDP de toohello de tooconnect no se puede en hello VM de Azure.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [hello Azure de MSDN y Hola foros de desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, también puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Get Support**. Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte técnico de Microsoft Azure](https://azure.microsoft.com/support/faq/).

## <a name="components-of-a-remote-desktop-connection"></a>Componentes de una conexión de Escritorio remoto
Hola de los componentes siguientes está implicado en una conexión RDP:

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

Antes de continuar, puede ser útil toomentally revisar lo que ha cambiado desde Hola última correcta escritorio remoto conexión toohello máquina virtual. Por ejemplo:

* Hola dirección IP pública de hello VM o hello servicio en la nube que contiene Hola VM (también denominado dirección IP virtual de hello [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) ha cambiado. Hola RDP error podría deberse a que la memoria caché del cliente DNS aún Hola *dirección IP antigua* registrado para el nombre DNS de Hola. Vaciar la memoria caché del cliente DNS e intente conectarse Hola VM de nuevo. O bien, intente conectarse directamente con hello nueva VIP.
* Está utilizando una aplicación de otro fabricante toomanage las conexiones de escritorio remoto en lugar de usar conexión de hello generado por hello portal de Azure. Compruebe que configuración de la aplicación hello incluye Hola TCP por el puerto correcto Hola tráfico de escritorio remoto. Puede comprobar este puerto para una máquina virtual clásica en hello [portal de Azure](https://portal.azure.com), haciendo clic en configuración de la máquina virtual de hello > puntos de conexión.

## <a name="preliminary-steps"></a>Pasos previos
Antes de continuar toohello solución de problemas detallada,

* Comprobar estado de Hola de máquina virtual de Hola Hola portal de Azure para cualquier problema obvio.
* Siga hello [pasos de corrección rápida para errores RDP comunes de solución de problemas básicos hello](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).

Intente conectarse de nuevo toohello máquina virtual mediante Escritorio remoto después de realizar estos pasos.

## <a name="detailed-troubleshooting-steps"></a>Pasos de la solución de problemas detallada
cliente de escritorio remoto de Hello no puede ser capaz de tooreach de servicio de escritorio remoto de hello en hello Azure VM due tooissues en hello siguientes orígenes:

* [Equipo cliente de Escritorio remoto](#source-1-remote-desktop-client-computer)
* [Dispositivo perimetral de intranet de la organización](#source-2-organization-intranet-edge-device)
* [Extremo de servicio en la nube y lista de control de acceso (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Grupos de seguridad de red](#source-4-network-security-groups)
* [Máquina virtual de Azure basada en Windows](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>Causa 1: equipo cliente de Escritorio remoto
Compruebe que el equipo puede crear el escritorio remoto conexiones tooanother local, el equipo basado en Windows.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

Si no es posible, busque Hola después de configuración en el equipo:

* Una configuración del firewall local que bloquea el tráfico de Escritorio remoto
* Software de proxy de cliente instalado localmente que impide las conexiones a Escritorio remoto
* Software de supervisión de red instalado localmente que impide las conexiones a Escritorio remoto
* Otro tipo de software de seguridad, por ejemplo, para supervisar el tráfico o para permitir o impedir ciertos tipos de tráfico, que imposibilita las conexiones a Escritorio remoto

En todos estos casos, temporalmente deshabilite software Hola e intente tooconnect tooan equipo de local a través de escritorio remoto. Si puede averiguar causa real Hola de este modo, trabajar con las conexiones de escritorio remoto red administrador toocorrect Hola software configuración tooallow.

## <a name="source-2-organization-intranet-edge-device"></a>Causa 2: dispositivo perimetral de intranet de la organización
Compruebe que un equipo conectado directamente toohello que Internet puede hacer que las conexiones de escritorio remoto tooyour máquina virtual de Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

Si no tiene un equipo que esté conectado directamente toohello Internet, cree y pruebe con una nueva máquina virtual de Azure en un servicio de nube o de grupo de recursos. Para más información, consulte [Creación de una máquina virtual Windows en Azure](../virtual-machines-windows-hero-tutorial.md). Puede eliminar la máquina virtual de Hola y grupo de recursos de Hola o servicio en la nube hello, después de probar Hola.

Si puede crear una conexión a Escritorio remoto con un equipo conectado directamente toohello Internet, compruebe si el dispositivo de borde de intranet de organización para:

* Un firewall interno bloqueo toohello de las conexiones HTTPS Internet.
* Un servidor proxy que impide las conexiones a Escritorio remoto
* Software de detección de intrusiones o supervisión de red en ejecución en los dispositivos de la red perimetral que impide las conexiones a Escritorio remoto

Trabajar con la configuración de Hola de toocorrect de administrador de red de su organización intranet borde dispositivo tooallow escritorio remoto basado en HTTPS conexiones toohello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Causa 3: extremo de servicio en la nube y ACL
Para las máquinas virtuales que se crean mediante el modelo de implementación clásica de hello, compruebe que otra máquina virtual de Azure que está en hello mismo servicio en la nube o red virtual puede hacer que las conexiones de escritorio remoto tooyour máquina virtual de Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> Para las máquinas virtuales creadas en el Administrador de recursos, omita demasiado[origen 4: grupos de seguridad de red](#source-4-network-security-groups).

Si no tiene otra máquina virtual en Hola mismo servicio en la nube o red virtual, cree uno. Siga los pasos de hello en [crear una máquina virtual ejecuta Windows en Azure](../virtual-machines-windows-hero-tutorial.md). Eliminar la máquina virtual de prueba de hello una vez completada la prueba de Hola.

Si se puede conectar a través de escritorio remoto tooa virtual machine Hola mismo nube de servicio o de red virtual, busque esta configuración:

* configuración de extremo de Hello para el tráfico de escritorio remoto en el destino de hello VM: Hola privada el puerto TCP del extremo de hello debe coincidir con el puerto TCP de hello en qué Hola está escuchando el servicio de escritorio remoto de la máquina virtual (el valor predeterminado es 3389).
* Hola ACL para punto de conexión del tráfico de escritorio remoto de hello en destino Hola VM: las ACL permiten toospecify permitirá o denegará el tráfico entrante de hello basado en Internet de su dirección IP de origen. ACL mal configuradas pueden impedir que el punto de conexión de entrada escritorio remoto tráfico toohello. Compruebe su tooensure de ACL que se permite el tráfico entrante desde las direcciones IP públicas de su servidor proxy u otro servidor de borde. Para obtener más información, vea [qué es una lista de control de acceso (ACL) de red](../../virtual-network/virtual-networks-acl.md)

Si el punto de conexión de hello es el origen de Hola de problema de hello, toocheck quitar punto de conexión actual de Hola y crear uno nuevo, elija un puerto aleatorio en hello intervalo 49152 – 65535 para el número de puerto externo Hola. Para obtener más información, consulte [cómo tooset la máquina virtual de los puntos de conexión tooa](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="source-4-network-security-groups"></a>Causa 4: grupos de seguridad de red
Los grupos de seguridad de red permiten un control pormenorizado del tráfico entrante y saliente permitido. Puede crear reglas que abarquen subredes y servicios en la nube en una red virtual de Azure.

Use [comprobar flujo IP](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm si una regla en un grupo de seguridad de red está bloqueando el tráfico tooor desde una máquina virtual. También puede revisar el grupo de seguridad eficaz reglas tooensure de entrada "Permitir" NSG regla existe y se establece una prioridad para el puerto RDP (valor predeterminado 3389). Para obtener más información, consulte [flujo del tráfico con reglas de seguridad efectivo tootroubleshoot VM](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

## <a name="source-5-windows-based-azure-vm"></a>Causa 5: máquina virtual de Azure basada en Windows
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Siga las instrucciones de hello en [este artículo](reset-rdp.md). En este artículo se restablece servicios de escritorio remoto de hello en la máquina virtual de hello:

* Habilitar la regla predeterminada de Firewall de Windows de "Escritorio remoto" hello (puerto TCP 3389).
* Habilite las conexiones de escritorio remoto estableciendo hello HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections del Registro valor too0.

Vuelva a intentar la conexión de Hola desde su equipo nuevo. Si es que aún no se puede tooconnect a través de escritorio remoto, compruebe los siguientes posibles problemas de hello:

* Hola servicio Escritorio remoto no está ejecutando en el destino de hello máquina virtual.
* Hola servicio Escritorio remoto no está escuchando en el puerto TCP 3389.
* El firewall de Windows u otro firewall local tiene una regla de salida que impide el tráfico de Escritorio remoto.
* La detección de intrusiones o software que se ejecuta en la máquina virtual de Azure Hola de supervisión de red impide las conexiones de escritorio remoto.

Para las máquinas virtuales creadas con el modelo de implementación clásica de hello, puede usar un toohello de sesión de PowerShell de Azure remoto máquina virtual de Azure. En primer lugar, debe tooinstall un certificado de servicio de nube de hospedaje de la máquina virtual Hola. Vaya demasiado[tooAzure configurar Secure Remote PowerShell Access máquinas virtuales](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) y descargar hello **InstallWinRMCertAzureVM.ps1** equipo local de tooyour de archivo de script.

A continuación, instale Azure PowerShell si todavía no lo ha hecho. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

A continuación, abra un símbolo del sistema de PowerShell de Azure y cambie Hola actual toohello ubicación de carpeta de hello **InstallWinRMCertAzureVM.ps1** archivo de script. toorun un script de PowerShell de Azure, debe establecer la directiva de ejecución correcta de Hola. Ejecute hello **Get-ExecutionPolicy** comando toodetermine su nivel actual de directiva. Para obtener información acerca de cómo establecer el nivel adecuado de hello, consulte [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).

A continuación, rellene su nombre de suscripción de Azure, nombre del servicio de nube de Hola y el nombre de máquina virtual (quitando Hola < y > caracteres) y, a continuación, ejecute estos comandos.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

Puede obtener nombre de la suscripción correcta de Hola de hello *SubscriptionName* propiedad de pantalla de Hola de hello **Get-AzureSubscription** comando. Puede obtener el nombre del servicio de nube de hello para la máquina virtual de Hola de hello *ServiceName* columna de presentación de Hola de hello **Get-AzureVM** comando.

Compruebe si tiene un nuevo certificado Hola. Abra un complemento de certificados para el usuario actual de Hola y mire en hello **Authorities\Certificates de certificación de raíz de confianza** carpeta. Debería ver un certificado con nombre DNS de hello del servicio en la nube en hello emitido toocolumn (ejemplo: cloudservice4testing.cloudapp.net).

A continuación, inicie una sesión remota de Azure PowerShell mediante el uso de estos comandos.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

Después de escribir las credenciales de administrador válida, debería ver algo similar toohello después de símbolo del sistema de PowerShell de Azure:

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

Hola primera parte de este mensaje es el nombre del servicio en la nube que contiene el destino de Hola de máquina virtual, que podría ser diferente de "cloudservice4testing.cloudapp.net". Ahora puede emitir comandos de PowerShell de Azure para esta nube problemas del servicio tooinvestigate Hola mencionados y corregir la configuración de Hola.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>toomanually corregir los servicios de escritorio remoto hello escucha el puerto TCP
En el símbolo de sesión de PowerShell de Azure remoto hello, ejecute este comando.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Hola propiedad PortNumber muestra el número de puerto actual de Hola. Si es necesario, cambie el valor de predeterminado tooits atrás de número de puerto de escritorio remoto del hello (3389) mediante este comando.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Comprobar si el puerto de Hola se ha too3389 modificadas mediante este comando.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Salga de la sesión remota de PowerShell de Azure de hello mediante este comando.

```powershell
Exit-PSSession
```

Comprobar que ese punto de conexión de escritorio remoto para máquina virtual de Azure hello hello también utiliza el puerto TCP 3398 como su puerto interno. Reinicie hello Azure VM e inténtelo de nuevo la conexión a Escritorio remoto hello.

## <a name="additional-resources"></a>Recursos adicionales
[¿Cómo tooreset una contraseña u Hola escritorio remoto de servicios de máquinas virtuales de Windows](reset-rdp.md)

[¿Cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview)

[Solucionar problemas de Shell seguro (SSH) conexiones tooa basados en Linux máquina virtual de Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Solucionar problemas de acceso tooan aplicación que se ejecuta en una máquina virtual de Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


---
title: aaaPrepare una tooAzure tooupload de VHD de Windows | Documentos de Microsoft
description: "¿Cómo tooprepare un VHD de Windows o VHDX antes de cargar tooAzure"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Preparar una tooAzure tooupload Windows VHD o VHDX
Antes de cargar una máquina virtual de Windows (VM) desde local tooMicrosoft Azure, debe preparar Hola disco de duro virtual (VHD o VHDX). Azure admite solo máquinas virtuales de generación 1 que están en formato de archivo de disco duro virtual de Hola y tienen un disco de tamaño fijo. Hola tamaño máximo permitido para hello VHD 1.023 GB. Puede convertir una generación 1 máquina virtual de hello VHDX tooVHD de sistema de archivos y de expansión dinámica en disco toofixed tamaño. Sin embargo, no puede cambiar la generación de una máquina virtual. Para obtener más información, consulte [¿Debería crear una máquina virtual de generación 1 o 2 en Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)

Para obtener más información sobre la directiva de soporte de hello para la máquina virtual de Azure, consulte [soporte de software de servidor de Microsoft para las máquinas virtuales de Microsoft Azure](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> instrucciones de Hello en este artículo aplican toohello versión de 64 bits de Windows Server 2008 R2 y posterior sistema operativo de Windows server. Para obtener información sobre cómo ejecutar la versión de 32 bits del sistema operativo en Azure, consulte [Soporte para sistemas operativos de 32 bits en máquinas virtuales de Azure](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Convertir tooVHD de disco virtual de Hola y disco de tamaño fijo 
Si necesita tooconvert su toohello de disco virtual requiere el formato de Azure, use uno de los métodos de hello en esta sección. Realizar una copia de hello VM antes de ejecutar el proceso de conversión de disco virtual de Hola y asegúrese de que ese Hola que VHD de Windows funciona correctamente en el servidor local de Hola. Resuelva los errores dentro de hello propia máquina virtual antes de que intente tooconvert o cargar tooAzure.

Después de convertir el disco de hello, cree una máquina virtual que usa Hola convertir disco. Inicie e inicie sesión en toohello VM toofinish preparar Hola VM para la carga.

### <a name="convert-disk-using-hyper-v-manager"></a>Conversión del disco mediante el Administrador de Hyper-V
1. Abra el Administrador de Hyper-V y seleccione el equipo local en hello izquierda. En el menú de Hola por encima de la lista de equipos de hello, haga clic en **acción** > **editar disco**.
2. En hello **localizar disco duro Virtual** pantalla, busque y seleccione el disco virtual.
3. En hello **elegir acción** pantalla y, a continuación, seleccione **convertir** y **siguiente**.
4. Si necesita tooconvert vhdx, seleccione **VHD** y, a continuación, haga clic en **siguiente**
5. Si necesita tooconvert desde un disco de expansión dinámica, seleccione **tamaño fijo** y, a continuación, haga clic en **siguiente**
6. Busque y seleccione un ruta de acceso toosave Hola nuevo archivo VHD.
7. Haga clic en **Finalizar**

>[!NOTE]
>comandos de Hello en este artículo se deben ejecutar en una sesión de PowerShell con privilegios elevados.

### <a name="convert-disk-by-using-powershell"></a>Conversión de disco con PowerShell
Puede convertir un disco virtual mediante el uso de hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) comando en Windows PowerShell. Seleccione **Ejecutar como administrador** al iniciar PowerShell. 

Hello comando de ejemplo siguiente se convierte de VHDX tooVHD y de un expansión dinámica toofixed tamaño del disco:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
En este comando, reemplace el valor de Hola de "-ruta de acceso" hello ruta de acceso toohello disco duro virtual que desea que el valor de hello y tooconvert para "-DestinationPath" con la nueva ruta de acceso de Hola y el nombre del programa Hola a convertir el disco.

### <a name="convert-from-vmware-vmdk-disk-format"></a>Conversión del formato de disco VMDK de VMware
Si tiene una imagen de máquina virtual de Windows en hello [formato de archivo VMDK](https://en.wikipedia.org/wiki/VMDK), convertir tooa VHD mediante el uso de hello [Microsoft VM Converter](https://www.microsoft.com/download/details.aspx?id=42497). Para obtener más información, vea el artículo de blog de hello [cómo tooConvert un disco duro virtual de VMware VMDK tooHyper-V](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Establecimiento de configuraciones de Windows para Azure

En hello máquina virtual que tiene previsto tooupload tooAzure, ejecutar todos los comandos en los siguientes Hola pasos desde una [ventana de símbolo del sistema con privilegios elevados](https://technet.microsoft.com/library/cc947813.aspx):

1. Quite cualquier ruta estática persistente en la tabla de enrutamiento de hello:
   
   * tabla de rutas de hello tooview, ejecute `route print` en línea de comandos de Hola.
   * Comprobar hello **rutas de persistencia** secciones. Si hay una ruta persistente, use [ruta delete](https://technet.microsoft.com/library/cc739598.apx) tooremove lo.
2. Quitar del proxy WinHTTP hello:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Establecer una directiva de SAN de hello disco demasiado[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    En la ventana de símbolo del sistema abierta hello, escriba Hola siguientes comandos:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Establecer tiempo de hora Universal coordinada (UTC) para Windows y Hola tipo de inicio del servicio de hora de Windows (w32time) Hola demasiado**automáticamente**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Establecer Hola power perfil toohello **de alto rendimiento**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Compruebe los servicios de Windows hello
Asegúrese de que cada uno de hello después de servicios de Windows se establece toohello **valores predeterminados de Windows**. Estos son los números mínimo de hello de servicios que deben estar configurados toomake ese Hola VM tenga conectividad. configuración de inicio en hello tooreset, ejecute hello siguientes comandos:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Actualización de la configuración del Registro de Escritorio remoto
Asegúrese de que ese Hola después de configuración están configurados correctamente para la conexión a Escritorio remoto:

>[!Note] 
>Puede recibir un mensaje de error al ejecutar hello **Set-ItemProperty-ruta de acceso ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal servicios - nombre &lt;nombre de objeto&gt; &lt;valor&gt;** en estos pasos. mensajes de bienvenida del error pueden omitirse. Significa que sólo ese dominio hello no inserta esa configuración a través de un objeto de directiva de grupo.
>
>

1. Protocolo de escritorio remoto (RDP) está habilitado:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Hola puerto RDP está configurado correctamente (puerto 3389 predeterminado):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    Cuando se implementa una máquina virtual, se crean las reglas predeterminadas de hello en el puerto 3389. Si desea que el número de puerto de toochange hello, hacerlo una vez implementada Hola VM en Azure.

3. Hola se escuchan en todas las interfaces de red:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Configurar el modo de autenticación a nivel de red de Hola para las conexiones RDP de hello:
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Establecer el valor keep-alive hello:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Vuelva a conectarse:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Hola limitar el número de conexiones simultáneas:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. Si hay cualquier los certificados autofirmados acumular el agente de escucha de toohello RDP, quitarlos:
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Se trata de toomake seguro de que puede conectarse al principio de hello al implementar Hola máquina virtual. También puede ver esto en una fase posterior después de hello que máquina virtual se implementa en Azure si es necesario.

9. Si Hola VM va a formar parte de un dominio, compruebe que todos Hola después configuración toomake seguro de que la configuración anterior de hello no se revierte. las directivas de Hola que deben comprobarse son siguiente hello:
    
    - RDP está habilitado:

         Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\ Componentes\Servicios de Escritorio remoto\Host de sesión de Escritorio remoto\Conexiones:
         
         **Permitir a los usuarios tooconnect remotamente mediante Escritorio remoto**

    - Directiva de grupo de NLA:

        Configuración\Plantillas administrativas\Componentes\Servicios de Escritorio remoto\Host de sesión de Escritorio remoto\Seguridad: 
        
        **Exigir la autenticación de usuarios para conexiones remotas con Autenticación a nivel de red**
    
    - Configuración de conexión persistente:

        Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\ Componentes Windows\Servicios de Escritorio remoto\Host de sesión de Escritorio remoto\Conexiones: 
        
        **Configurar el intervalo de conexión persistente**

    - Vuelva a conectar la configuración:

        Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\ Componentes Windows\Servicios de Escritorio remoto\Host de sesión de Escritorio remoto\Conexiones: 
        
        **Reconexión automática**

    - Limitar el número de Hola de configuración de conexiones:

        Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\ Componentes Windows\Servicios de Escritorio remoto\Host de sesión de Escritorio remoto\Conexiones: 
        
        **Limitar el número de conexiones**

## <a name="configure-windows-firewall-rules"></a>Configuración de reglas de firewall de Windows
1. Activar Firewall de Windows en los perfiles de hello tres (dominio, estándar y público):

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Ejecutar el siguiente comando de PowerShell tooallow WinRM a través de perfiles de firewall de hello tres (dominio, privado y público) de Hola y habilitar Hola servicio remota de PowerShell:
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Habilitar Hola siguiendo el tráfico de RDP de Hola de tooallow de reglas de firewall 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Habilitar la regla de uso compartido de impresoras y Hola archivo para que hello VM puede responder comando ping de tooa dentro de hello red Virtual:

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Si Hola VM va a formar parte de un dominio, compruebe Hola después configuración toomake seguro de que la configuración anterior de hello no se revierte. las directivas de Hello AD que deben comprobarse son siguiente hello:

    - Habilitar perfiles de Firewall de Windows hello

        Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\Red\Conexión de red\Firewall de Windows\Perfil de dominio\Firewall de Windows: **Proteger todas las conexiones de red**

       Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\Red\Conexión de red\Firewall de Windows\Perfil estándar\Firewall de Windows: **Proteger todas las conexiones de red**

    - Habilitar RDP 

        Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\Red\Conexión de red\Firewall de Windows\Perfil de dominio\Firewall de Windows: **Permitir las excepciones de Escritorio remoto de entrada**

        Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\Red\Conexión de red\Firewall de Windows\Perfil estándar\Firewall de Windows: **Permitir las excepciones de Escritorio remoto de entrada**

    - Habilitar ICMP-V4

        Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\Red\Conexión de red\Firewall de Windows\Perfil de dominio\Firewall de Windows: **Permitir las excepciones ICMP**

        Configuración del equipo\Directivas\Configuración de Windows\Plantillas administrativas\Red\Conexión de red\Firewall de Windows\Perfil estándar\Firewall de Windows: **Permitir las excepciones ICMP**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>Comprobación de que la que máquina virtual es correcta, está segura y es accesible con RDP 
1. disco de hello seguro toomake es correcto y coherente, ejecute una operación de comprobación de disco en el próximo reinicio de máquina virtual de hello:

    ```PowerShell
    Chkdsk /f
    ```
    Asegúrese de que el informe de hello muestra un disco limpio y en buen estado.

2. Establecer configuración de datos de configuración de arranque (BCD) de Hola. 

    > [!Note]
    > Asegúrese de ejecutar estos comandos en una ventana CMD con privilegios elevados y **no** en PowerShell:
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Comprobar que ese repositorio de este último de administración de Windows hello es coherente. tooperform, Hola ejecución siguiente comando:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Si se daña el repositorio de hello, consulte [WMI: repositorio está dañado, o no](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Asegúrese de que cualquier otra aplicación no está usando el puerto 3389 Hola. Este puerto se usa para hello servicio RDP en Azure. Puede ejecutar **netstat - anob** toosee qué puertos se utilizan en hello VM:

    ```PowerShell
    netstat -anob
    ```

5. Si hello VHD de Windows que desea que tooupload es un controlador de dominio, siga estos pasos:

    A. Siga [estos pasos adicionales](https://support.microsoft.com/kb/2904015) disco de hello tooprepare.

    B. Asegúrese de que conoce contraseña de DSRM hello en caso de tener toostart Hola VM en DSRM en algún momento. Puede que desee toorefer toothis vincular hello tooset [contraseña de DSRM](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Asegúrese de que la contraseña y la cuenta de administrador integrada Hola se conocen tooyou. Puede desea contraseña de administrador local actual de tooreset hello y asegúrese de que puede usar esta cuenta toosign en tooWindows a través de hello conexión RDP. Este permiso de acceso se controla mediante el objeto de directiva de grupo "Permitir el registro a través de servicios de escritorio remoto" Hola. Puede ver este objeto en el Editor de directivas de grupo Local de hello en:

    Configuración del equipo\Configuración de Windows\Configuración de seguridad\Directivas locales\Asignación de derechos de usuario

7. Compruebe toomake seguro de que no está bloqueando el acceso RDP a través de RDP ni de red de hello las directivas de hello después de AD:

    - Equipo de toothis de acceso de configuración de equipo\Configuración de Windows\Configuración seguridad\Directivas locales\Asignación derechos Assignment\Deny de equipo desde la red de Hola

    - Configuración del equipo\Configuración de Windows\Configuración de seguridad\Directivas locales\Asignación de derechos de usuario\Denegar inicio de sesión a través de Servicios de Escritorio remoto


8. Reinicio Hola VM toomake seguro de que Windows todavía funciona correctamente puede tener acceso mediante el uso de la conexión RDP de Hola. En este momento, puede desee toocreate una máquina virtual en su Hola de seguro local del toomake de Hyper-V que está iniciando completamente la máquina virtual y, a continuación, probar si es accesible de RDP.

9. Quite los filtros adicionales de la Interfaz de controlador de transporte, como el software que analiza los paquetes TCP o los firewalls adicionales. También puede ver esto en una fase posterior después de hello que máquina virtual se implementa en Azure si es necesario.

10. Desinstale cualquier otro software de terceros y controlador de componentes de toophysical relacionados o cualquier otra tecnología de virtualización.

### <a name="install-windows-updates"></a>Instalación de actualizaciones de Windows
configuración de Hello ideal es demasiado**tiene el nivel de revisión de Hola de máquina de hello en hello más reciente**. Si esto no es posible, asegúrese de que ese Hola siguiendo las actualizaciones están instaladas:

|                       |                   |           |                                       Versión del archivo mínima x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Componente               | Binary            | Windows 7 y Windows Server 2008 R2 | Windows 8 y Windows Server 2012             | Windows 8.1 y Windows Server 2012 R2 | Windows 10 y Windows Server 2016 RS1 | Windows 10 RS2             |
| Almacenamiento                 | disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | ntfs.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | Msdsm.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | Mpio.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| Red                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | http.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| Núcleo                    | ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| Servicios de Escritorio remoto | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | termsrv.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| Seguridad                | TooWannaCrypt vencimiento | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Cuando sysprep toouse<a id="step23"></a>    

Sysprep es un proceso que pueda ejecutar en una instalación de windows que se restablecerá la instalación de hello del sistema de Hola y proporcionará un "hello rápida", eliminando todos los datos personales y restablezca varios componentes. Normalmente hace esto si desea toocreate una plantilla desde la que puede implementar varias otras máquinas virtuales que tienen una configuración específica. Esto se conoce como **imagen generalizada**.

En su lugar, si desea que sólo toocreate una máquina virtual desde un disco, no tienes toouse sysprep. En esta situación, puede crear simplemente Hola VM de lo que se conoce como un **imagen especializada**.

Para obtener más información acerca de cómo toocreate una máquina virtual desde un disco especializado, vea:

- [Creación de una máquina virtual a partir de un disco especializado](create-vm-specialized.md)
- [Create a VM from a specialized VHD disk](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/) (Creación de una máquina virtual a partir de un disco duro virtual especializado)

Si desea que toocreate una imagen generalizada, deberá toorun sysprep. Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx). 

No todos los roles o aplicaciones instalados en un equipo basado en Windows admiten esta generalización. Por lo que antes de que se ejecute este procedimiento, consulte toohello siguiente artículo toomake seguro de que ese rol Hola de ese equipo es compatible con sysprep. Para obtener más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Compatibilidad de Sysprep con los roles de servidor).

### <a name="steps-toogeneralize-a-vhd"></a>Pasos toogeneralize un disco duro virtual

>[!NOTE]
> Después de ejecutar sysprep.exe como Hola especificado de pasos, desactive la opción Hola VM y no se vuelve a activar hasta que cree una imagen de ella en Azure.

1. Inicie sesión en toohello VM de Windows.
2. Ejecute **Símbolo del sistema** como administrador. 
3. Cambie el directorio de Hola a: **%windir%\system32\sysprep**y, a continuación, ejecute **sysprep.exe**.
3. Hola **herramienta de preparación del sistema** cuadro de diálogo, seleccione **sistema Out-of-Box experiencia inmediata (OOBE)**y asegúrese de que ese hello **generalizar** casilla está activada.

    ![Herramienta de preparación del sistema](media/prepare-for-upload-vhd-image/syspre.png)
4. En **Opciones de apagado**, seleccione **Apagar**.
5. Haga clic en **Aceptar**.
6. Cuando Sysprep finalice, cierre Hola máquina virtual. No utilice **reiniciar** tooshut hacia abajo Hola máquina virtual.
7. Ahora hello VHD es listo toobe cargado. Para obtener más información acerca de cómo toocreate una máquina virtual desde un disco generalizado, consulte [cargar un disco duro virtual generalizado y utilizar toocreate un nuevas máquinas virtuales en Azure](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Realice las configuraciones recomendadas
Hola después de la configuración no afectan a la carga del disco duro virtual. Sin embargo, se recomienda firmemente que los configure.

* Instalar hello [Azure VM Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). A continuación, puede habilitar las extensiones de máquina virtual. las extensiones de VM de Hello implementan la mayor parte de funcionalidad crítica de Hola que podría desee toouse con las máquinas virtuales como el restablecimiento de contraseñas, configuración de RDP y así sucesivamente. Para más información, consulte:

    - [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/) (Agente de VM y extensiones: parte 1)
    - [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) (Agente de VM y extensiones: parte 2)
* registro de volcado de memoria de Hello puede ser útil para solucionar problemas de bloqueo de Windows. Habilitar la recopilación de registro de hello volcado de memoria:
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    Si recibe errores durante alguno de los procedimientos de hello los pasos de este artículo, esto significa que las claves del registro de hello ya existe. En esta situación, utilice Hola siguientes comandos en su lugar:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Después de crea Hola VM en Azure, se recomienda colocar el archivo de paginación de hello en el rendimiento de tooimprove de volumen de "Unidad Temporal" Hola. Puede configurar esto como se muestra a continuación:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
Si no hay ningún disco de datos que está adjunto toohello VM, letra de unidad del volumen de la unidad Temporal de hello suele ser "D." Esta designación podría ser diferente, dependiendo del número de Hola de unidades de disco disponibles y la configuración de Hola que realice.

## <a name="next-steps"></a>Pasos siguientes
* [Cargar un tooAzure de imagen de máquina virtual de Windows para las implementaciones del Administrador de recursos](upload-generalized-managed.md)


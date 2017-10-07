---
title: aaaConnect remotamente el dispositivo de StorSimple tooyour | Documentos de Microsoft
description: "Explica cómo tooconfigure el dispositivo para la administración remota y cómo tooconnect tooWindows PowerShell para StorSimple a través de HTTP o HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Conectar dispositivo de la serie 8000 de StorSimple tooyour de forma remota

## <a name="overview"></a>Información general
Puede usar el dispositivo de StorSimple de tooyour de tooconnect de comunicación remota de Windows PowerShell. Cuando se conecta de este modo, no verá un menú. (Verá un menú solo si usa la consola serie de hello en hello dispositivo tooconnect). Con la comunicación remota de Windows PowerShell, conecte tooa espacio de ejecución específica. También puede especificar el idioma para mostrar hello. 

Para obtener más información acerca del uso de Windows PowerShell remoting toomanage el dispositivo, vaya demasiado[usar Windows PowerShell para StorSimple tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).

Este tutorial le explica cómo tooconfigure el dispositivo para la administración remota y, a continuación, cómo tooconnect tooWindows PowerShell para StorSimple. Puede usar tooconnect HTTP o HTTPS a través de comunicación remota de Windows PowerShell. Sin embargo, cuando decida cómo tooconnect tooWindows PowerShell para StorSimple, tenga en cuenta los siguiente hello: 

* Conexión directa toohello consola serie del dispositivo es segura, pero conexión toohello de consola serie a través de conmutadores de red no lo es. Tenga cuidado de riesgos de seguridad de hello cuando se conecte la consola serie del dispositivo toohello a través de conmutadores de red. 
* Conexión a través de una sesión HTTP puede ofrecer más seguridad que la conexión a través de la consola serie de Hola a través de red de Hola. Aunque esto no es el método más seguro de hello, es aceptable en redes de confianza. 
* Conexión a través de una sesión HTTPS con un certificado autofirmado es más segura de Hola y Hola opción recomendada.

Puede conectarse remotamente toohello interfaz de Windows PowerShell. Sin embargo, el dispositivo de StorSimple de tooyour de acceso remoto a través de la interfaz de Windows PowerShell de hello no está habilitado de forma predeterminada. Se necesita tooenable administración remota en el dispositivo de hello en primer lugar y, a continuación, en Hola a cliente que sea tooaccess usa el dispositivo.

pasos de Hello descritos en este artículo se han ejecutado en un sistema host que ejecute Windows Server 2012 R2.

## <a name="connect-through-http"></a>Conectarse a través de HTTP
Conexión tooWindows PowerShell para StorSimple a través de una sesión HTTP ofrece más seguridad que la conexión a través de la consola de serie de hello de dispositivo StorSimple. Aunque esto no es el método más seguro de hello, es aceptable en redes de confianza.

Puede usar Hola portal de Azure clásico o administración remota de hello consola serie tooconfigure. Seleccione una de hello procedimientos siguientes:

* [Utilizar la administración remota de Azure tooenable portal clásico de Hola a través de HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

Después de habilitar la administración remota, use Hola siguiendo el procedimiento tooprepare Hola del cliente para una conexión remota.

* [Preparar el cliente de Hola para conexión remota](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a>Utilizar la administración remota de Azure tooenable portal clásico de Hola a través de HTTP
Realizar Hola siguiendo los pasos en la administración remota de hello Azure tooenable portal clásico a través de HTTP.

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a>administración remota de tooenable a través de hello portal de Azure clásico
1. Acceda a **Dispositivos** > **Configurar** para el dispositivo.
2. Desplácese hacia abajo toohello **administración remota** sección.
3. Establecer **habilitar la administración remota** demasiado**Sí**.
4. Ahora puede elegir tooconnect mediante HTTP. (el valor predeterminado de hello es tooconnect a través de HTTPS). Asegúrese de que se selecciona HTTP.
   
   > [!NOTE]
   > La conexión a través de HTTP solo es aceptable en redes de confianza.
   > 
   > 
5. Haga clic en **guardar** final Hola de página Hola.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTP
Realizar Hola pasos Hola administración de dispositivos consola serie tooenable remoto.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>administración remota de tooenable a través de la consola serie del dispositivo Hola
1. En el menú de la consola serie de hello, seleccione la opción 1. Para obtener más información acerca del uso de consola serie de hello en dispositivo hello, vaya demasiado[conectar tooWindows PowerShell para StorSimple a través de la consola serie del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. En el símbolo del sistema de hello, escriba:`Enable-HcsRemoteManagement –AllowHttp`
3. Se le notificará acerca de las vulnerabilidades de seguridad de Hola de usar HTTP tooconnect toohello dispositivo. Cuando se le solicite, confirme escribiendo **S**.
4. Compruebe que está habilitado HTTP escribiendo: `Get-HcsSystem`
5. Compruebe que hello **RemoteManagementMode** campo muestra **HttpsAndHttpEnabled**.hello después de la ilustración se muestra esta configuración en PuTTY.
   
     ![Serie HTTPS y HTTP habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>Preparar el cliente de Hola para conexión remota
Realizar Hola siguiendo los pasos en la administración remota de hello cliente tooenable.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>cliente de hello tooprepare para conexión remota
1. Iniciar una sesión de Windows PowerShell como administrador.
2. Escriba Hola siguiente dirección IP de comando tooadd Hola de lista de hosts de confianza del cliente de toohello de hello StorSimple dispositivo: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Reemplace <*device_ip*> con la dirección IP de Hola de su dispositivo, por ejemplo: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Escriba Hola después comando toosave hello las credenciales del dispositivo en una variable: 
   
    ```
    $cred = Get-Credential
    ```
    
4. En el cuadro de diálogo de Hola que aparece:
   
   1. Escriba el nombre de usuario de hello en este formato: *device_ip\SSAdmin*.
   2. Escriba la contraseña del Administrador de dispositivos de Hola que se estableció al dispositivo de Hola se configuró con el Asistente para la instalación de Hola. es la contraseña predeterminada de Hello *Password1*.
5. Iniciar una sesión de Windows PowerShell en el dispositivo de hello, escriba este comando:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate una sesión de Windows PowerShell para su uso con el dispositivo virtual StorSimple de hello, anexar hello `–Port` parámetro y especifique el puerto público de Hola que configuró en la comunicación remota de dispositivo Virtual StorSimple.
   > 
   > 
   
     En este punto, debe tener un dispositivo de toohello de sesión de Windows PowerShell remoto activo.
   
    ![Conexión remota de PowerShell mediante HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Conectarse a través de HTTPS
Conexión tooWindows PowerShell para StorSimple a través de una sesión HTTPS es más segura de hello y método de conexión de forma remota dispositivos de Microsoft Azure StorSimple tooyour recomendado. Hola procedimientos siguientes explica cómo tooset seguridad Hola serie consola y los equipos cliente para que puedan utilizar HTTPS tooconnect tooWindows PowerShell para StorSimple.

Puede usar Hola portal de Azure clásico o administración remota de hello consola serie tooconfigure. Seleccione una de hello procedimientos siguientes:

* [Utilizar la administración remota de Azure tooenable portal clásico de Hola a través de HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

Después de habilitar la administración remota, use Hola después de host de hello tooprepare de procedimientos para una administración remota y conecte toohello dispositivo desde el host remoto Hola.

* [Preparar el host de hello para la administración remota](#prepare-the-host-for-remote-management)
* [Conecte el dispositivo de toohello desde el host remoto hello](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a>Utilizar la administración remota de Azure tooenable portal clásico de Hola a través de HTTPS
Realizar Hola siguiendo los pasos en la administración remota de hello Azure tooenable portal clásico a través de HTTPS.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a>tooenable la administración remota a través de HTTPS de hello portal de Azure clásico
1. Acceda a **Dispositivos** > **Configurar** para el dispositivo.
2. Desplácese hacia abajo toohello **administración remota** sección.
3. Establecer **habilitar la administración remota** demasiado**Sí**.
4. Ahora puede elegir tooconnect mediante HTTPS. (el valor predeterminado de hello es tooconnect a través de HTTPS). Asegúrese de que se ha seleccionado HTTPS. 
5. Haga clic en **Descargar certificado de administración remota**. Especifique una ubicación toosave este archivo. Necesitará tooinstall este certificado en el equipo cliente o host Hola que va a usar tooconnect toohello dispositivo.
6. Haga clic en **guardar** final Hola de página Hola.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Utilizar la administración remota de tooenable de consola serie de Hola a través de HTTPS
Realizar Hola pasos Hola administración de dispositivos consola serie tooenable remoto.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>administración remota de tooenable a través de la consola serie del dispositivo Hola
1. En el menú de la consola serie de hello, seleccione la opción 1. Para obtener más información acerca del uso de consola serie de hello en dispositivo hello, vaya demasiado[conectar tooWindows PowerShell para StorSimple a través de la consola serie del dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. En el símbolo del sistema de hello, escriba: 
   
     `Enable-HcsRemoteManagement`
   
    Esto debe habilitar HTTPS en el dispositivo.
3. Compruebe que se ha habilitado HTTPS escribiendo: 
   
     `Get-HcsSystem`
   
    Asegúrese de que ese hello **RemoteManagementMode** campo muestra **HttpsEnabled**.hello después de la ilustración se muestra esta configuración en PuTTY.
   
     ![Serie HTTPS habilitada](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. De salida de hello de `Get-HcsSystem`, copie Hola de número de serie del dispositivo de Hola y guardarlo para su uso posterior.
   
   > [!NOTE]
   > número de serie de Hello asigna toohello nombre CN de certificado de Hola.
   > 
   > 
5. Obtenga un certificado de administración remota, escriba: 
   
     `Get-HcsRemoteManagementCert`
   
    Aparecerá un siguiente toohello similar de certificado.
   
    ![Obtener certificado de administración remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Copiar información de hello en el certificado de Hola de **---BEGIN CERTIFICATE---** demasiado**---END CERTIFICATE---** en un editor de texto como Bloc de notas y guárdelo como un archivo .cer. (Copiará este host remoto de archivo tooyour al preparar los host de Hola.)
   
   > [!NOTE]
   > toogenerate un nuevo certificado, utilice hello `Set-HcsRemoteManagementCert` cmdlet.
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a>Preparar el host de hello para la administración remota
equipo de host de hello tooprepare para una conexión remota que utiliza una sesión HTTPS, lleve a cabo Hola procedimientos siguientes:

* [Archivo de importación hello .cer en almacén raíz de Hola de hello cliente o host remoto](#to-import-the-certificate-on-the-remote-host).
* [Agregar archivo hosts toohello de números de serie de dispositivo de hello en el host remoto](#to-add-device-serial-numbers-to-the-remote-host).

A continuación se describe cada uno de estos procedimientos.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>certificado de hello tooimport en host remoto hello
1. Haga clic en el archivo .cer de hello y seleccione **instalar certificado**. Esto iniciará Hola Asistente para importación de certificados.
   
    ![Asistente para importación de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Para **Ubicación de almacén**, seleccione **Equipo local** y, después, haga clic en **Siguiente**.
3. Seleccione **colocar todos los certificados en hello después almacén**y, a continuación, haga clic en **examinar**. Navegar por el almacén raíz de toohello del host remoto y, a continuación, haga clic en **siguiente**.
   
    ![Asistente para importación de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Haga clic en **Finalizar** Aparece un mensaje que indica que la importación de hello fue correcta.
   
    ![Asistente para importación de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>host remoto del toohello tooadd dispositivo números de serie
1. Inicie el Bloc de notas como administrador y, a continuación, abra el archivo de hosts de hello ubicado en \Windows\System32\Drivers\etc.
2. Agregar Hola siguiente archivo de hosts de tres entradas tooyour: **dirección IP de DATA 0**, **dirección IP fija del controlador 0**, y **dirección IP fija del controlador 1**.
3. Escriba el número de serie del dispositivo Hola que guardó anteriormente. Asigne esta dirección IP de toohello como se muestra en hello después de la imagen. Para el controlador 0 y 1, anexe **Controller0** y **Controller1** final Hola Hola del número de serie (nombre CN).
   
    ![Agregar nombre CN toohosts archivo](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Guardar el archivo de hosts de Hola.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Conecte el dispositivo de toohello desde el host remoto hello
Usar Windows PowerShell y SSL tooenter una sesión de SSAdmin en el dispositivo desde un cliente o host remoto. sesión de SSAdmin Hola asigna toooption 1 Hola [consola serie](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menú del dispositivo.

Realizar Hola siguiendo el procedimiento en el equipo Hola del que desea que la conexión remota de Windows PowerShell de toomake Hola.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>tooenter una sesión de SSAdmin en dispositivo hello mediante Windows PowerShell y SSL
1. Iniciar una sesión de Windows PowerShell como administrador.
2. Agregar hosts de confianza del cliente de hello dispositivo IP dirección toohello, escriba:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Donde <*device_ip*> Hola dirección de IP del dispositivo; por ejemplo: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Cree una nueva credencial, escriba: 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Donde <*dirección IP del dispositivo de destino*> Hola dirección de IP de DATA 0 de su dispositivo; por ejemplo, **10.126.173.90** como se muestra en hello delante de la imagen del archivo de hosts de Hola. Además, proporcione la contraseña de administrador de hello para el dispositivo.
4. Cree una sesión, escriba:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Para el parámetro - ComputerName de hello en cmdlet hello, proporcionar Hola <*número de serie del dispositivo de destino*>. Se ha asignado este número de serie toohello dirección IP de DATA 0 en el archivo de hosts de hello en el host remoto; Por ejemplo, **SHX0991003G44MT** como se muestra en hello después de la imagen.
5. Escriba: 
   
     `Enter-PSSession $session`
6. Necesitará toowait unos minutos y, a continuación, podrá dispositivo tooyour conectado a través de HTTPS a través de SSL. Verá un mensaje que indica que está conectado tooyour dispositivo.
   
    ![Conexión remota de PowerShell mediante HTTP y SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre [mediante Windows PowerShell tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).


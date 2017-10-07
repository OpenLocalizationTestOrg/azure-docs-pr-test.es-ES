---
title: dispositivo de StorSimple 8000 tootroubleshoot herramienta aaaDiagnostics | Documentos de Microsoft
description: "Describe los modos de dispositivo de StorSimple de Hola y explica cómo toouse Windows PowerShell para StorSimple toochange Hola modo del dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>Usar Hola herramienta de diagnóstico de StorSimple tootroubleshoot 8000 series problemas del dispositivo

## <a name="overview"></a>Información general

Hola herramienta de diagnóstico de StorSimple diagnostica problemas relacionados toosystem, rendimiento, red y estado del componente de hardware para un dispositivo de StorSimple. herramienta de diagnóstico de Hola se puede usar en distintos escenarios. Estos escenarios incluyen la planeación de la carga de trabajo, implementar un dispositivo de StorSimple, evaluar el entorno de red de Hola y determinar el rendimiento de Hola de un dispositivo operativo. En este artículo se proporciona información general de la herramienta de diagnóstico de Hola y describe cómo se puede utilizar la herramienta Hola con un dispositivo de StorSimple.

herramienta de diagnóstico de Hello sirve principalmente para dispositivos de StorSimple 8000 series locales (8100 y 8600).

## <a name="run-diagnostics-tool"></a>Ejecución de la herramienta de diagnóstico

Esta herramienta se puede ejecutar mediante la interfaz de Windows PowerShell de hello de dispositivo StorSimple. Hay dos maneras de tooaccess Hola interfaz local del dispositivo:

* [Consola serie del dispositivo use PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
* [Acceso remoto a herramienta de Hola a través de hello Windows PowerShell para StorSimple](storsimple-remote-connect.md).

En este artículo, se supone que se ha conectado toohello consola serie del dispositivo mediante PuTTY.

#### <a name="toorun-hello-diagnostics-tool"></a>herramienta de diagnóstico de hello toorun

Una vez que se ha conectado toohello de interfaz de Windows PowerShell del dispositivo de hello, realizar Hola siguiendo los pasos toorun Hola cmdlet.
1. Inicie sesión en la consola serie del dispositivo toohello siguiendo los pasos de hello en [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).

2. Escriba el siguiente comando de hello:

    `Invoke-HcsDiagnostics`

    Si no se especifica el parámetro de ámbito de hello, Hola cmdlet ejecuta todas las pruebas de diagnóstico de Hola. Estas pruebas incluyen el sistema, el estado de los componentes de hardware, la red y el rendimiento. 
    
    toorun solo una prueba concreta, especifique el parámetro de ámbito de Hola. Por ejemplo, toorun solo Hola prueba de red, tipo

    `Invoke-HcsDiagnostics -Scope Network`

3. Seleccione y copie la salida de hello de hello PuTTY ventana en un archivo de texto para su posterior análisis.

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>Herramienta de diagnóstico de escenarios toouse Hola

Utilice Hola diagnósticos herramienta tootroubleshoot Hola red, el rendimiento, el sistema y hardware mantenimiento del sistema de Hola. Algunos posibles escenarios son:

* **Dispositivo sin conexión**: su dispositivo de StorSimple de la serie 8000 está desconectado. Sin embargo, desde la interfaz de Windows PowerShell de hello, parece que ambos controladores Hola están activados y ejecutándose.
    * También puede utilizar esta herramienta toothen determinar el estado de la red de Hola.
         
         > [!NOTE]
         > No utilice esta configuración de red y el rendimiento de tooassess de herramienta en un dispositivo antes de registro de hello (o la configuración mediante el Asistente para la instalación). Una dirección IP válida se asigna toohello dispositivo durante el registro y el Asistente para la instalación. Puede ejecutar este cmdlet en un dispositivo que no esté registrado para conocer el estado del hardware y del sistema. Utilice el parámetro de ámbito de hello, por ejemplo:
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **Problemas del dispositivo persistente** -están experimentando problemas de dispositivo que parezcan toopersist. Por ejemplo, error en el registro. Puede también tratarse de problemas del dispositivo después de hello dispositivo registrado correctamente y en funcionamiento durante un tiempo.
    * En este caso, puede usar esta herramienta para la solución de problemas preliminar antes de registrar una solicitud de servicio con el soporte técnico de Microsoft. Le recomendamos que ejecute esta salida de hello de herramienta y la captura de esta herramienta. A continuación, puede proporcionar esta salida tooSupport tooexpedite solución de problemas.
    * Si existe algún error en el componente de hardware o el clúster, debe registrar una solicitud de soporte técnico.

* **Rendimiento bajo del dispositivo**: el dispositivo de StorSimple es lento.
    * En este caso, ejecute este cmdlet con tooperformance de conjunto de parámetros de ámbito. Analizar la salida de hello. Obtener en la nube hello las latencias de lectura y escritura. Hola uso notificado latencias como máximo destino factible, factor en cierta sobrecarga para el procesamiento de datos interno de hello y, a continuación, implementar las cargas de trabajo de hello en el sistema de Hola. Para obtener más información, consulte demasiado[usar Hola red prueba tootroubleshoot dispositivo rendimiento](#network-test).


## <a name="diagnostics-test-and-sample-outputs"></a>Salidas de ejemplo y prueba de diagnóstico

### <a name="hardware-test"></a>Prueba de hardware

Esta prueba determina el estado de Hola de componentes de hardware de hello, el firmware USM Hola y el firmware de disco de hello ejecutando en el sistema.

* componentes de hardware de Hello notificados son los componentes de esa prueba Hola errores o no están presentes en el sistema de Hola.
* versiones de firmware de disco y el firmware USM Hola se notifican para hello controlador 0, 1 de controlador y componentes comparten en el sistema. Para obtener una lista completa de los componentes de hardware, vaya a:

    * [Componentes de la caja principal](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [Componentes de la caja EBOD](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> Si prueba de hardware de hello informa de componentes con errores, [iniciar sesión en una solicitud de servicio con Microsoft Support](storsimple-contact-microsoft-support.md).

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>La salida de ejemplo de la prueba de hardware se ejecuta en un dispositivo 8100

Esta es una salida de ejemplo de un dispositivo de StorSimple 8100. En el dispositivo de modelo de hello 8100, Hola alojamiento de EBOD no está presente. Por lo tanto, no se notifican los componentes del controlador EBOD Hola.

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>Prueba del sistema

Esta prueba notifica información del sistema hello, hello las actualizaciones disponibles, información de clúster de Hola e información del servicio de hello para el dispositivo.

* información del sistema Hola incluye modelo hello, número de serie del dispositivo, zona horaria, el estado del controlador y versión de detallado del software de hello ejecutando en el sistema de Hola. Hola toounderstand distintos parámetros del sistema se notifican como salida de hello, vaya demasiado[interpretar la información del sistema](#appendix-interpreting-system-information).

* disponibilidad de la actualización de Hello informa de si los modos normal y el mantenimiento de hello están disponibles y sus nombres de paquete asociado. Si `RegularUpdates` y `MaintenanceModeUpdates` son `false`, esto indica que no hay disponibles actualizaciones de Hola. El dispositivo está actualizado.
* información de clúster de Hello contiene información de hello en diversos componentes lógicos de todos los grupos de clúster HCS hello y sus Estados respectivos. Si ve un grupo de clúster sin conexión en esta sección del informe de hello, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md).
* información de servicio de Hello incluye nombres de Hola y Estados del programa Hola a todos los HCS y servicios de elementos de configuración que se ejecutan en el dispositivo. Esta información es útil para hello Microsoft Support para solucionar el problema con un dispositivo Hola.

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>Salida de ejemplo de la prueba del sistema ejecutada en un dispositivo 8100

Este es un resultado de ejemplo de Hola sistema serie de pruebas en un dispositivo 8100.

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>Prueba de red

Esta prueba valida Hola estado de interfaces de red de hello, puertos, DNS y NTP conectividad con el servidor, SSL certificado, las credenciales de cuenta de almacenamiento, servidores de actualización de toohello de conectividad y conectividad de proxy web en el dispositivo StorSimple.

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>Salida de ejemplo de la prueba de red solo cuando está habilitado DATA0

Este es un resultado de ejemplo de dispositivo 8100 Hola. Puede ver en la salida de hello que:
* Solo las interfaces de red DATA 0 y DATA 1 están habilitadas y configuradas.
* 2-5 de datos no están habilitados en el portal de Hola.
* configuración del servidor DNS Hello es válida y Hola dispositivo puede conectarse a través del servidor DNS de Hola.
* Hola conectividad con el servidor NTP también es correcto.
* Los puertos 80 y 443 están abiertos. Sin embargo, el puerto 9354 está bloqueado. En función de hello [requisitos de sistema de red](storsimple-system-requirements.md), necesita tooopen este puerto para la comunicación de bus de servicio de Hola.
* certificación de Hello SSL es válido.
* puede conectar el dispositivo de Hello toohello cuenta de almacenamiento: _myss8000storageacct_.
* servidores de tooUpdate de conectividad de Hello es válido.
* proxy de Hello web no está configurado en este dispositivo.

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>Salida de ejemplo de la prueba de red cuando se habilitan DATA0 y DATA1

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>Prueba de rendimiento

Esta prueba informes de rendimiento de hello en la nube a través de las latencias de lectura y escritura de hello en la nube para el dispositivo. Esta herramienta puede ser tooestablish usa una línea de base de rendimiento en la nube de Hola que se puede lograr con StorSimple. Hola herramienta informes Hola máximo rendimiento (escenario de mejor caso para las latencias de lectura y escritura) que puede obtener la conexión.

Como herramienta de hello notifica un rendimiento máximo alcanzable hello, podemos usar Hola notifique las latencias de lectura y escritura como destinos al implementar hello las cargas de trabajo.

prueba de Hello simula tamaños de blob de hello asociados con los tipos de otro volumen de hello en dispositivo Hola. Los niveles normales y las copias de seguridad de volúmenes anclados localmente usan un tamaño de blob de 64 KB. Los volúmenes en capas con la opción de archivado marcada usan un tamaño de datos de blob de 512 KB. Si el dispositivo tiene configurado volúmenes anclados localmente y en niveles, solo Hola prueba too64 KB blob correspondiente se ejecuta el tamaño de los datos.

toouse esta herramienta, realizar Hola pasos:

1.  En primer lugar, cree una mezcla de volúmenes en capas y volúmenes anclados localmente con la opción de archivado marcada. Esta acción garantiza que esa herramienta Hola ejecuta pruebas de Hola de 64 KB y 512 KB tamaños de blob.

2. Ejecute el cmdlet de hello después de haber creado y configurado los volúmenes de Hola. Escriba:

    `Invoke-HcsDiagnostics -Scope Performance`

3. Tome nota de las latencias de lectura y escritura de hello notificados por herramienta Hola. Esta prueba puede tardar varios toorun minutos antes de notificar los resultados de Hola.

4. Si las latencias de conexión de hello son todos en hello intervalo esperado, hello latencias notificadas por hello herramienta pueden utilizarse como destino factible máximo al implementar las cargas de trabajo de Hola. Estime cierta sobrecarga en el procesamiento de datos interno.

    Si las latencias de lectura y escritura de hello notifican por la herramienta de diagnóstico de hello son altas:

    1. Configurar el análisis de almacenamiento para los servicios blob y analizar Hola salida toounderstand Hola latencias de hello cuenta de almacenamiento de Azure. Para obtener instrucciones detalladas, consulte demasiado[habilitar y configurar el análisis de almacenamiento](../storage/common/storage-enable-and-view-metrics.md). Si esas latencias también son números toohello alta y comparable que recibió de hello herramienta de diagnóstico de StorSimple, a continuación, deberá toolog una solicitud de servicio con el almacenamiento de Azure.

    2. Si se están quedando sin las latencias de cuenta de almacenamiento de hello, póngase en contacto con su tooinvestigate de administrador de red emite alguna latencia en la red.

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>Salida de ejemplo de una prueba de rendimiento ejecutada en un dispositivo 8100

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>Apéndice: interpretación de la información del sistema

Aquí es una tabla que describe qué Hola diversos parámetros de Windows PowerShell en información del sistema Hola se asignan a. 

| Parámetro de PowerShell    | Descripción  |
|-------------------------|------------------|
| Id. de instancia             | Cada controlador lleva asociado un identificador único o un GUID.|
| Nombre                    | nombre descriptivo de Hello de dispositivo de hello conforme a la configuración a través del portal de Azure de Hola durante la implementación de dispositivo. nombre descriptivo de Hello predeterminado es el número de serie del dispositivo de Hola. |
| Modelo                   | modelo de Hola de su dispositivo de la serie StorSimple 8000. modelo de Hello puede ser 8100 o 8600.|
| SerialNumber            | número de serie del dispositivo de Hola se asigna en el generador de Hola y 15 caracteres. Por ejemplo, 8600-SHX0991003G44HT indica:<br> 8600: es el modelo de dispositivo de Hola.<br>¿SHX – fabricación Hola sitio.<br> 0991003: indica un producto específico. <br> Últimos 5 dígitos son G44HT-Hola incrementa toocreate números de serie exclusivos. Es posible que no sea un conjunto secuencial.|
| TimeZone                | Hola dispositivo la zona de horaria que esté establecida en hello portal de Azure durante la implementación de dispositivo.|
| CurrentController       | controlador de Hola que son de interfaz de Windows PowerShell de hello toothrough conectados del dispositivo StorSimple.|
| ActiveController        | controlador de Hola que está activa en el dispositivo y controla todas las operaciones de red y disco de Hola. Puede ser el Controlador 0 o el Controlador 1.  |
| Controller0Status       | estado de saludo del controlador 0 en el dispositivo. estado del controlador Hola puede ser normal, en modo de recuperación, o es inaccesible.|
| Controller1Status       | estado de saludo del controlador 1 en el dispositivo.  estado del controlador Hola puede ser normal, en modo de recuperación, o es inaccesible.|
| SystemMode              | Hola estado general del dispositivo StorSimple. estado del dispositivo Hola puede ser normal, mantenimiento, o dado de baja (corresponde toodeactivated Hola portal de Azure).|
| FriendlySoftwareVersion | Hola descriptivo cadena correspondiente versión de software de dispositivo de toohello. Para un sistema que se ejecuta Update 4, versión de software descriptivo Hola sería StorSimple 8000 Series Update 4.0.|
| HcsSoftwareVersion      | versión de software de Hello HCS ejecutando en su dispositivo. Por ejemplo, hello tooStorSimple correspondiente de una versión de software HCS 8000 Series Update 4.0 es 6.3.9600.17820. |
| ApiVersion              | versión de software de Hola de API de Windows PowerShell del dispositivo HCS Hola Hola.|
| VhdVersion              | versión de software de Hola de imagen de fábrica de Hola que hello de dispositivo se distribuyó con. Si restablece los valores predeterminados del dispositivo toofactory, a continuación, se ejecuta esta versión de software.|
| OSVersion               | versión de software de Hola de sistema operativo Hola Windows Server que ejecuta en el dispositivo de Hola. dispositivo de StorSimple de Hola se basa en Windows Server 2012 R2 que corresponde too6.3.9600 Hola.|
| CisAgentVersion         | versión de Hola para su agente de elementos de configuración que se ejecuta en el dispositivo StorSimple. Este agente ayuda a comunicarse con el servicio de StorSimple Manager Hola ejecuta en Azure.|
| MdsAgentVersion         | Hola versión correspondiente toohello Mds agente se ejecuta en el dispositivo StorSimple. Este agente mueve datos toohello supervisión y diagnóstico de servicio (MDS).|
| Lsisas2Version          | Hola controladores de toohello LSI correspondientes de la versión en el dispositivo StorSimple.|
| Capacity                | capacidad total de Hello de dispositivo de hello en bytes.|
| RemoteManagementMode    | Indica si el dispositivo de hello puede administrarse de manera remota a través de la interfaz de Windows PowerShell. |
| FipsMode                | Indica si se habilita el modo de Estados Unidos información procesamiento estándar Federal (FIPS) de hello en el dispositivo. estándar de Hello FIPS 140 define los algoritmos criptográficos aprobados para su uso por los sistemas de equipo de Gobierno Federal nos para la protección de Hola de los datos confidenciales. Para dispositivos que ejecutan Update 4 o posterior, el modo FIPS está habilitado de forma predeterminada. |

## <a name="next-steps"></a>Pasos siguientes

* Obtenga información acerca de hello [sintaxis del cmdlet Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).

* Más información acerca de cómo demasiado[solucionar problemas de implementación](storsimple-troubleshoot-deployment.md) en el dispositivo StorSimple.

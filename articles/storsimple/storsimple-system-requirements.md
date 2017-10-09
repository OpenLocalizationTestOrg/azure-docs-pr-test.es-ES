---
title: requisitos del sistema aaaStorSimple | Documentos de Microsoft
description: "Describe los requisitos de software, redes y alta disponibilidad y procedimientos recomendados para una solución Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2b6ca34a-d758-48e7-ab1e-4fdd80cf48d4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: alkohli
ms.openlocfilehash: ec0bb5ad2f2d4c9901da2d95147dd9daa178f6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-software-high-availability-and-networking-requirements"></a>Software de StorSimple, alta disponibilidad y requisitos de red
## <a name="overview"></a>Información general
Página principal de tooMicrosoft StorSimple de Azure. Este artículo describen los requisitos de sistema importantes y prácticas recomendadas para el dispositivo StorSimple y para los clientes de almacenamiento de hello obtiene acceso a dispositivo de Hola. Se recomienda que revise cuidadosamente información Hola antes de implementar el sistema de StorSimple y, a continuación, hacen referencia tooit según sea necesario durante la implementación y las operaciones subsiguientes.

los requisitos de sistema de Hello incluyen:

* **Requisitos de software para los clientes de almacenamiento** -describe Hola admitida los sistemas operativos y los requisitos adicionales para estos sistemas operativos.
* **Requisitos de red para el dispositivo StorSimple hello** -proporciona información acerca de los puertos de hello ese toobe necesidad abierto en el firewall tooallow para el tráfico de iSCSI, de nube o de administración.
* **Requisitos de alta disponibilidad para StorSimple** : describe los requisitos de alta disponibilidad y las prácticas recomendadas del equipo host y del dispositivo StorSimple. 

## <a name="software-requirements-for-storage-clients"></a>Requisitos de software para clientes de almacenamiento
Hola según los requisitos de software es para los clientes de almacenamiento de Hola que tienen acceso a su dispositivo de StorSimple.

| Sistemas operativos compatibles | Versión requerida | Requisitos/notas adicionales |
| --- | --- | --- |
| Windows Server |2008R2 SP1, 2012, 2012R2, 2016 |Se admiten volúmenes iSCSI de StorSimple para su uso en solo Hola siguientes tipos de disco de Windows:<ul><li>Volumen simple en disco básico</li><li>Volumen simple y reflejado en disco dinámico</li></ul>Se admiten solo Hola iniciadores de software iSCSI está presentes de forma nativa en el sistema operativo de Hola. No se admiten los iniciadores iSCSI de hardware.<br></br>El aprovisionamiento fino de Windows Server 2012 y 2016 y las características de ODX se admiten si se usa un volumen iSCSI de StorSimple.<br><br>StorSimple puede crear volúmenes con aprovisionamiento fino y totalmente aprovisionados. No puede crear volúmenes de aprovisionamiento parcial.<br><br>El proceso de volver a formatear un volumen con aprovisionamiento fino puede tardar mucho tiempo en completarse. Se recomienda eliminar volumen hello y, a continuación, crear uno nuevo en lugar de volver a formatear. Sin embargo, si aún así prefiere tooreformat un volumen:<ul><li>Ejecute hello siguiente comando antes de retrasos de recuperación de espacio de hello formatear tooavoid: <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Una vez completada la formato hello, siguiente Hola de uso de comandos de toore Habilitar recuperación de espacio:<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>Aplique la revisión de Windows Server 2012 Hola tal y como se describe en [KB 2878635](https://support.microsoft.com/kb/2870270) tooyour equipo con Windows Server.</li></ul></li></ul></ul> Si está configurando StorSimple Snapshot Manager o el adaptador de StorSimple para SharePoint, vaya demasiado[requisitos de Software para los componentes opcionales](#software-requirements-for-optional-components). |
| VMWare ESX |5.5 y 6.0 |Admitido con VMware vSphere como cliente iSCSI La característica VAAI-block se admite con VMware vSphere en dispositivos de StorSimple. |
| Linux RHEL/CentOS |5, 6 y 7 |Compatibilidad con clientes iSCSI de Linux con versiones del iniciador Open-iSCSI 5, 6 y 7. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> IBM AIX no es compatible actualmente con StorSimple.
> 
> 

## <a name="software-requirements-for-optional-components"></a>requisitos de software para ver los componentes opcionales
Hola según los requisitos de software es para hello StorSimple componentes opcionales (Administrador de instantáneas StorSimple y el adaptador de StorSimple para SharePoint).

| Componente | Plataforma de host | Requisitos/notas adicionales |
| --- | --- | --- |
| StorSimple Snapshot Manager |Windows Server 2008 R2 SP1, 2012, 2012 R2 |El uso de Snapshot Manager de StorSimple en Windows Server es necesario para realizar la copia de seguridad y restauración de los discos dinámicos reflejados y para realizar copias de seguridad coherentes con la aplicación.<br> StorSimple Snapshot Manager solo se admite en Windows Server 2008 R2 SP1 (64 bits), Windows 2012 R2 y Windows Server 2012.<ul><li>Si usa Windows Server 2012, debe instalar .NET 3.5 o 4.5 antes de instalar StorSimple Snapshot Manager.</li><li>Si usa Windows Server 2008 R2 SP1, debe instalar Windows Management Framework 3.0 antes de instalar StorSimple Snapshot Manager.</li></ul> |
| Adaptador de StorSimple para SharePoint |Windows Server 2008 R2 SP1, 2012, 2012 R2 |<ul><li>El adaptador de StorSimple para SharePoint solo se admite en SharePoint 2010 y SharePoint 2013.</li><li>RBS requiere SQL Server Enterprise Edition, versión 2008 R2 o 2012.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>Requisitos de red para el dispositivo StorSimple
El dispositivo StorSimple es un dispositivo bloqueado. Sin embargo, hay puertos toobe abierto en su tooallow de firewall para tráfico de administración, en la nube e iSCSI. Hello tabla siguiente enumeran los puertos de Hola que necesitan toobe abierto en el firewall. En esta tabla, *en* o *entrada* hace referencia dirección toohello desde el que las solicitudes de cliente entrantes, tener acceso a su dispositivo. *Out* o *saliente* hace referencia en el que el dispositivo StorSimple envía datos externamente, más allá de la implementación de Hola de dirección de toohello: por ejemplo, saliente toohello de Internet.

| Nº de puerto<sup>1,2</sup> | Dentro o fuera | Ámbito de puerto | Obligatorio | Notas |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |Fuera |WAN |No |<ul><li>Puerto de salida se usa para las actualizaciones de tooretrieve de acceso a Internet.</li><li>proxy web de salida de Hello es configurable por el usuario.</li><li>tooallow actualizaciones del sistema, este puerto también debe estar abierto para hello IP fijas del controlador.</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |Fuera |WAN |Sí |<ul><li>Puerto de salida se usa para tener acceso a datos en la nube de Hola.</li><li>proxy web de salida de Hello es configurable por el usuario.</li><li>tooallow actualizaciones del sistema, este puerto también debe estar abierto para hello IP fijas del controlador.</li><li>Este puerto también se utiliza en ambos controladores de hello para la recolección.</li></ul> |
| UDP 53 (DNS) |Fuera |WAN |En algunos casos; consulte las notas. |Este puerto es necesario solo si está utilizando un servidor DNS basado en Internet. |
| UDP 123 (NTP) |Fuera |WAN |En algunos casos; consulte las notas. |Este puerto solo es necesario si está utilizando un servidor DNS basado en Internet. |
| TCP 9354 |Fuera |WAN |Sí |puerto de salida de Hello usa hello toocommunicate de dispositivo de StorSimple con hello el servicio StorSimple Manager. |
| 3260 (iSCSI) |En el |LAN |No |Este puerto es usado tooaccess datos a través de iSCSI. |
| 5985 |En el |LAN |No |Puerto de entrada se usa por el Administrador de instantáneas StorSimple toocommunicate Hola de dispositivos de StorSimple.<br>Este puerto también se utiliza cuando se conecta remotamente tooWindows PowerShell para StorSimple a través de HTTP. |
| 5986 |En el |LAN |No |Este puerto se usa cuando se conecta remotamente tooWindows PowerShell para StorSimple a través de HTTPS. |

<sup>1</sup> ningún puerto de entrada necesario toobe abierto en Hola Internet pública.

<sup>2</sup> si varios puertos usan una configuración de puerta de enlace, el orden del tráfico enrutado de salida de hello se determinará según se describe en el orden de hello puerto enrutamiento [enrutamiento del puerto](#routing-metric), más adelante.

<sup>3</sup> controlador Hola IP fijo en el dispositivo de StorSimple debe ser enrutable y pueda tooconnect toohello Internet directamente o a través de hello configura proxy web. direcciones IP de Hello fijada se utilizan para dar servicio a dispositivos de hello actualizaciones toohello. Si los controladores de dispositivo de hello no pueden conectar toohello IP fijas de Internet a través de hello, no será capaz de tooupdate el dispositivo StorSimple.

> [!IMPORTANT]
> Asegúrese de que firewall de hello no modificar o descifrar todo el tráfico SSL entre el dispositivo de StorSimple de Hola y Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Patrones de URL para reglas de firewall
Los administradores de red a menudo pueden configurar firewall avanzada reglas basadas en Hola Hola de toofilter de patrones de dirección URL de entrada y de Hola el tráfico saliente. El dispositivo de StorSimple y el servicio StorSimple Manager Hola dependen de otras aplicaciones de Microsoft como Service Bus de Azure, Azure Active Directory Access Control, cuentas de almacenamiento y servidores de Microsoft Update. patrones de dirección URL de Hello asociadas a estas aplicaciones pueden ser tooconfigure usa reglas de firewall. Es importante toounderstand que pueden cambiar los patrones de dirección URL de hello asociadas a estas aplicaciones. Esto a su vez necesitarán toomonitor de administrador de red de Hola y actualizar las reglas de firewall para StorSimple como y cuando sea necesario.

Se recomienda que establezca las reglas de firewall para el tráfico saliente, basándose en las direcciones IP fijas de StorSimple, de forma generosa en la mayoría de los casos. Sin embargo, puede utilizar información de hello debajo tooset avanzadas reglas de firewall que son entornos seguros toocreate necesarios.

> [!NOTE]
> siempre se debe establecer el dispositivo de Hello (origen) de direcciones IP tooall interfaces de red de hello habilitado. destino de Hello direcciones IP deben establecerse demasiado[intervalos IP del centro de datos Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

#### <a name="url-patterns-for-azure-portal"></a>Patrones de dirección URL del Portal de Azure
| Patrón de URL | Componente o funcionalidad | Direcciones IP del dispositivo |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Servicio StorSimple Manager<br>Access Control Service<br>Bus de servicio |Interfaces de red habilitadas para la nube |
| `https://*.backup.windowsazure.com` |Registro de dispositivos |Solo DATA 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revocación de certificados |Interfaces de red habilitadas para la nube |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Supervisión y cuentas de Almacenamiento de Azure |Interfaces de red habilitadas para la nube |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Servidores de Microsoft Update<br> |Solo direcciones IP fijas del controlador |
| `http://*.deploy.akamaitechnologies.com` |CDN de Akamai |Solo direcciones IP fijas del controlador |
| `https://*.partners.extranet.microsoft.com/*` |Paquete de soporte |Interfaces de red habilitadas para la nube |

#### <a name="url-patterns-for-azure-government-portal"></a>Patrones de dirección URL para el Portal de Azure Government
| Patrón de URL | Componente o funcionalidad | Direcciones IP del dispositivo |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*` |Servicio StorSimple Manager<br>Access Control Service<br>Bus de servicio |Interfaces de red habilitadas para la nube |
| `https://*.backup.windowsazure.us` |Registro de dispositivos |Solo DATA 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revocación de certificados |Interfaces de red habilitadas para la nube |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Supervisión y cuentas de Almacenamiento de Azure |Interfaces de red habilitadas para la nube |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Servidores de Microsoft Update<br> |Solo direcciones IP fijas del controlador |
| `http://*.deploy.akamaitechnologies.com` |CDN de Akamai |Solo direcciones IP fijas del controlador |
| `https://*.partners.extranet.microsoft.com/*` |Paquete de soporte |Interfaces de red habilitadas para la nube |

### <a name="routing-metric"></a>Métrica de enrutamiento
Una métrica de enrutamiento está asociada con interfaces de Hola y puerta de enlace de Hola que enrutar Hola datos toohello especificado redes. Métrica de enrutamiento se usa por hello enrutamiento protocolo toocalculate Hola mejor ruta de acceso tooa dado de destino, si aprende varias rutas de acceso existen toohello mismo destino. Hola inferior Hola enrutamiento métrica, Hola Hola preferencia mayor.

Hola contexto de StorSimple, si hay varias interfaces de red y puertas de enlace había configurada toochannel tráfico, métrica de enrutamiento de hello entrará en orden relativo play toodetermine hello en qué Hola obtener utilizará interfaces. no se puede cambiar la métrica de enrutamiento de Hola por usuario de Hola. Sin embargo, puede usar hello `Get-HcsRoutingTable` cmdlet tooprint tabla de enrutamiento de hello (y las métricas) en el dispositivo StorSimple. Para más información sobre el cmdlet Get-HcsRoutingTable, consulte [Solución de problemas de implementación de dispositivos de StorSimple](storsimple-troubleshoot-deployment.md).

Hola algoritmos de métrica de enrutamiento es diferente según la versión del software Hola ejecutando en el dispositivo StorSimple.

**Las versiones anterior tooUpdate 1**

Esto incluye la versión anterior tooUpdate 1 como Hola GA, 0.1, 0.2 o 0.3 de versiones de software. orden de Hello en función de la métrica de enrutamiento es el siguiente:

   *Última interfaz de red de 10 GbE configurada &gt; Otra interfaz de red de 10 GbE &gt; Última interfaz de red de 1 GbE configurada &gt; Otra interfaz de red de 1 GbE*

**Versiones a partir de actualizaciones 1 y 2 de tooUpdate anterior**

Esto incluye las versiones de software, como 1, 1.1 o 1.2. orden de Hello en función de la métrica de enrutamiento se decide como sigue:

   *DATA 0 &gt; Última interfaz de red de 10 GbE configurada &gt; Otra interfaz de red de 10 GbE &gt; Última interfaz de red de 1 GbE configurada &gt; Otra interfaz de red de 1 GbE*

   En Update 1, métrica de enrutamiento de Hola de DATA 0 se realiza hello más baja; por lo tanto, todo el tráfico en la nube de la Hola se enruta a través de DATA 0. Tome nota de esto si hay más de una interfaz de red habilitada para la nube en el dispositivo de StorSimple.

**Versiones a partir de Update 2**

Actualización 2 tiene varias mejoras relacionadas con las redes y métrica de enrutamiento de hello ha cambiado. comportamiento de Hello puede explicarse como sigue.

* Un conjunto de valores predeterminados se han asignado toonetwork interfaces.     
* Considere la posibilidad de una tabla de ejemplo que se muestra a continuación con valores asignados toohello diversas interfaces de red cuando están habilitadas en la nube o deshabilitados en la nube, pero con una puerta de enlace configurada. Nota los valores de hello asignados aquí son solo los valores de ejemplo.

    | Interfaz de red | Habilitada para la nube | Deshabilitada para la nube con puerta de enlace |
    |-----|---------------|---------------------------|
    | Data 0  | 1            | -                        |
    | Data 1  | 2            | 20 |                       |
    | Data 2  | 3            | 30                       |
    | Data 3  | 4            | 40                       |
    | Data 4  | 5            | 50                       |
    | Data 5  | 6            | 60                       |


* orden de Hello en el que el tráfico de hello en la nube se enrutará a través de interfaces de red de hello es:
  
    *Data 0 &gt; Data 1 &gt; Date 2 &gt; Data 3 &gt; Data 4 &gt; Data 5*
  
    Esto puede explicarse por el siguiente ejemplo de Hola.
  
    Consideremos un dispositivo de StorSimple con dos interfaces de red habilitadas para la nube, Data 0 y Data 5. De Data 1 a Data 4 la interfaz estará deshabilitada para la nube pero con una puerta de enlace configurada. orden de Hello en el que se enrutará el tráfico para este dispositivo puede ser:
  
    *Data 0 (1) &gt; Data 5 (6) &gt; Data 1 (20) &gt; Data 2 (30) &gt; Data 3 (40) &gt; Data 4 (50)*
  
    *donde los números de hello entre paréntesis indican las métricas de enrutamiento respectivas Hola.*
  
    Si se produce un error en Data 0, tráfico de nube de hello obtener enrutará a través de Data 5. Dado que una puerta de enlace está configurado en todos los demás red, si se toofail de Data 0 y Data 5, tráfico de la nube de hello pasará a través de datos 1.
* Si se produce un error en una interfaz de red habilitada para la nube, entonces no será 3 reintentos con un 30 segunda retraso tooconnect toohello interfaz. Si se produce un error en todos los reintentos de hello, tráfico de hello es toohello enrutado siguiente habilitada para la nube interfaz disponible según lo determinado por la tabla de enrutamiento de Hola. Si todos Hola habilitada para la nube producirá un error en interfaces de red, se producirá un error de dispositivo de hello sobre toohello otro controlador (no necesita reiniciar en este caso).
* Si se produce un error de la IP virtual de una interfaz de red habilitada para iSCSI, se producirán 3 reintentos con un retraso de 2 segundos. Este comportamiento ha permanecido Hola igual de versiones anteriores de Hola. Si se produce un error en todas las interfaces de red de iSCSI de hello, se producirá una conmutación por error de controlador (acompañado por un reinicio).
* También se genera una alerta en el dispositivo de StorSimple cuando hay un error en la IP virtual. Para obtener más información, consulte demasiado[referencia rápida de alerta](storsimple-manage-alerts.md).
* En términos de reintentos, iSCSI tendrá prioridad sobre la nube.
  
    Considere el siguiente ejemplo de Hola: StorSimple un dispositivo tiene dos interfaces de red habilitadas, Data 0 y 1 de datos. Data 0 está habilitada para la nube mientras que Data 1 está habilitada para la nube y para iSCSI. Ninguna otra interfaz de red de este dispositivo está habilitada para la nube ni para iSCSI.
  
    Si se produce un error de datos 1, dado es la interfaz de red de iSCSI última hello, esto producirá un tooData de conmutación por error del controlador 1 hello en otro controlador.

### <a name="networking-best-practices"></a>Prácticas recomendadas de redes
Además toohello sobre requisitos de red, para un rendimiento óptimo hello de la solución StorSimple, tenga en cuenta toohello seguir las prácticas recomendadas:

* Asegúrese de que el dispositivo StorSimple tenga un ancho de banda de 40 Mbps (o más) disponible en todo momento. No se debe compartir este ancho de banda (o asignación debe garantizarse mediante el uso de Hola de las directivas de QoS) con otras aplicaciones.
* Asegúrese de que hay conectividad de red toohello Internet en todo momento. Esporádicos o poco confiables Internet conexiones toohello dispositivos, no incluidos conectividad a Internet sea, dará como resultado una configuración no admitida.
* Aislar el tráfico de iSCSI y la nube de hello mediante interfaces de red en el dispositivo para el acceso iSCSI y nube dedicadas. Para obtener más información, vea cómo demasiado[modificar interfaces de red](storsimple-modify-device-config.md#modify-network-interfaces) en el dispositivo StorSimple.
* No utilice una configuración de Protocolo de control de adición de enlaces (LACP) para las interfaces de red. Se trata de una configuración no admitida.

## <a name="high-availability-requirements-for-storsimple"></a>Requisitos de alta disponibilidad para StorSimple
plataforma de hardware de Hola que se incluye con la solución de StorSimple de hello tiene características de disponibilidad y confiabilidad que proporcionan los cimientos para una infraestructura de almacenamiento de alta disponibilidad, tolerancia en el centro de datos. Sin embargo, deben cumplirse los requisitos y las prácticas recomendadas que deben obedecer toohelp garantizan la disponibilidad de hello de la solución StorSimple. Antes de implementar StorSimple, revise atentamente Hola siguiendo los requisitos y procedimientos recomendados para el dispositivo de StorSimple de Hola y equipos host conectados.

Para obtener más información sobre la supervisión y mantenimiento de componentes de hardware de hello de dispositivo StorSimple, vaya demasiado[utilizar componentes de hardware de toomonitor de servicio de administrador de StorSimple de Hola y estado](storsimple-monitor-hardware-status.md) y [StorSimple sustitución de componentes de hardware](storsimple-hardware-component-replacement.md).

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>Requisitos de alta disponibilidad y procedimientos para el dispositivo StorSimple
Hola de revisión siguiente información cuidadosamente alta disponibilidad de Hola de tooensure del dispositivo StorSimple.

#### <a name="pcms"></a>PCM
Los dispositivos de StorSimple incluyen módulos de alimentación y refrigeración (PCM) redundantes intercambiables en caliente. Cada PCM tiene suficiente servicio tooprovide de capacidad todo chasis de Hola. alta disponibilidad tooensure, ambos PCM debe instalarse.

* Conectar su disponibilidad PCM toodifferent power orígenes tooprovide si se produce un error en una fuente de alimentación.
* Si se produce un error en un PCM, solicite su sustitución inmediatamente.
* Quite el PCM con error solo cuando tiene reemplazo hello y tooinstall listo.
* No quite los PCM simultáneamente. módulo PCM en Hello incluye el módulo de batería de reserva de Hola. La eliminación de hello PCM dará como resultado un apagado sin protección de batería y no se guardará el estado del dispositivo Hola. Para obtener más información acerca de la batería de hello, vaya demasiado[módulo de batería de reserva de mantener hello](storsimple-battery-replacement.md#maintain-the-backup-battery-module).

#### <a name="controller-modules"></a>Módulos de controlador
Los dispositivos StorSimple incluyen módulos de controlador intercambiables en caliente. módulos de controlador de Hello funcionan en modo activo/pasivo. En un momento dado, un módulo de controlador está activo y proporcionando servicio, mientras Hola otro módulo de controlador es pasivo. módulo del controlador pasivo Hola está encendida y empieza a funcionar si el módulo del controlador activo de hello falla o se quitan. Cada módulo de controlador tiene suficiente servicio tooprovide de capacidad todo chasis de Hola. Dos módulos de controlador deben estar instalado tooensure alta disponibilidad.

* Asegúrese de que ambos módulos de controlador estén instalados en todo momento.
* Si se produce un error en un módulo de controlador, solicite su sustitución inmediatamente.
* Quitar un módulo de controlador con error solo cuando tenga el recambio de Hola y son tooinstall listo. Si quita un módulo durante períodos prolongados afectará flujo de aire hello y, por tanto, Hola refrigeración del sistema de Hola.
* Asegúrese de módulos de controlador de tooboth de conexiones de red de hello son idénticos, y hello interfaces de red conectadas tienen una configuración de red idéntica.
* Si un módulo de controlador falla o necesita sustitución, asegúrese de que ese Hola otro módulo de controlador está en un estado activo antes de reemplazar el módulo de controlador con error de Hola. tooverify que un controlador está activo, vaya demasiado[controlador activo de identificación hello en el dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* No quite los dos módulos de controlador en hello mismo tiempo. Si una conmutación por error de controlador está en curso, no apague el módulo de controlador en espera de Hola o quitarlos del chasis de Hola.
* Después de una conmutación por error del controlador, espere al menos cinco minutos antes de quitar cualquier módulo del controlador.

#### <a name="network-interfaces"></a>Interfaces de red
Los módulos del controlador del dispositivo StorSimple tienen cada uno cuatro interfaces de red Ethernet de 1 Gigabit y dos de 10 Gigabits.

* Asegúrese de que módulos de controlador de tooboth de conexiones de red de hello son idénticos e interfaces de red de Hola que interfaces de módulo de controlador de hello están conectado toohave una configuración de red idéntica.
* Cuando sea posible, implemente las conexiones de red en disponibilidad del servicio de diferentes conmutadores tooensure en caso de hello de un error de dispositivo de red.
* Antes de desconectar un solo Hola o restante de la última Hola interfaz habilitada para iSCSI (con direcciones IP asignadas), deshabilitar primero la interfaz de hello y, a continuación, desconecte los cables de Hola. Si interfaz Hola se desconecta en primer lugar, hará que Hola controlador activo toofail sobre toohello el controlador pasivo. Si el controlador pasivo hello tiene también sus interfaces correspondientes desconectadas, ambos controladores Hola se reiniciarán varias veces antes de establecerse en un controlador.
* Conectar al menos dos redes de toohello de interfaces de datos de cada módulo de controlador.
* Si ha habilitado la interfaces de hello dos de 10 GbE, impleméntelas en diferentes conmutadores.
* Cuando sea posible, use MPIO en tooensure de servidores que los servidores de hello pueden tolerar un vínculo, red o errores de interfaz.

Para obtener más información sobre el dispositivo para alta disponibilidad y rendimiento de la red, vaya demasiado[instalar el dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) o [instalar su dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

#### <a name="ssds-and-hdds"></a>SSD y unidades de disco duro
Los dispositivos StorSimple incluyen discos de estado sólido (SSD) y unidades de disco duro (HDD) que están protegidos con espacios reflejados. Uso de espacios reflejados garantiza que ese dispositivo hello es Error de hello tootolerate capaz de uno o varios SSD o HDD.

* Asegúrese de que estén instalados todos los módulos SSD y de disco duro.
* Si se produce un error en un PCM o en un disco duro, solicite su sustitución inmediatamente.
* Si una SDD o HDD se produce un error o es necesario sustituirla, asegúrese de que quita solo Hola SSD o HDD que requiera la sustitución.
* No quite más de un SSD o HDD del sistema de Hola en cualquier momento en el tiempo.
  Es posible que un error de 2 o más discos de cierto tipo (disco duro, SSD) o errores consecutivos dentro de un período de tiempo breve provoquen un fallo de funcionamiento en el sistema y una posible pérdida de datos. Si esto ocurre, [póngase en contacto con el servicio de soporte técnico de Microsoft](storsimple-contact-microsoft-support.md) para obtener ayuda.
* Durante la sustitución, supervise hello **estado del Hardware** en hello **mantenimiento** página para unidades de hello en hello SSD y HDD. Un estado de la marca de verificación verde indica que los discos de Hola correcto o bueno, mientras que una exclamación roja indica un error de SSD o HDD.
* Se recomienda configurar instantáneas en la nube para todos los volúmenes que necesita tooprotect en el caso de un error del sistema.

#### <a name="ebod-enclosure"></a>Receptáculo EBOD
Modelo de dispositivo de StorSimple 8600 incluye un alojamiento extendido grupo de discos (EBOD) en el alojamiento principal de suma toohello. Un EBOD contiene controladores EBOD y unidades de disco duro (HDD) que están protegidas mediante espacios reflejados. Uso de espacios reflejados garantiza que ese dispositivo hello es Error de hello tootolerate capaz de uno o más unidades de disco duro. Hola alojamiento de EBOD está conectado toohello alojamiento principal mediante cables SAS redundantes.

* Asegúrese de que los dos módulos de controlador de alojamiento EBOD, cables SAS y todas las unidades de disco duro de Hola se instalan en todo momento.
* Si se produce un error en un módulo de controlador de receptáculo EBOD, solicite su sustitución inmediatamente.
* Si se produce un error en un módulo de controlador de alojamiento EBOD, asegúrese de que ese Hola otro módulo de controlador está activo antes de reemplazar el módulo con error Hola. tooverify que un controlador está activo, vaya demasiado[controlador activo de identificación hello en el dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Durante una sustitución del módulo de controlador EBOD, supervise continuamente Hola estado del componente de hello en el servicio StorSimple Manager Hola accediendo **mantenimiento** > **estado del Hardware**.
* Si un cable SAS se produce un error o es necesario sustituirla (Microsoft Support debe estar implicado toomake esta decisión), asegúrese de que elimina solo cable SAS de Hola que requiera la sustitución.
* No simultáneamente quitar dos cables SAS de sistema de Hola en cualquier momento en el tiempo.

### <a name="high-availability-recommendations-for-your-host-computers"></a>Recomendaciones de alta disponibilidad para los equipos host
Revise cuidadosamente estos mejores prácticas tooensure Hola alta disponibilidad del dispositivo de StorSimple de tooyour conectado de hosts.

* Configure StorSimple con [configuraciones de clúster de servidor de archivos de dos nodos][1]. Mediante la eliminación de puntos únicos de fallo e integrar redundancia en el lado del host de hello, toda la solución Hola se convierte en la alta disponibilidad.
* Usar disponibles continuamente (CA) recursos compartidos disponibles con Windows Server 2012 (SMB 3.0) para alta disponibilidad durante la conmutación por error de controladores de almacenamiento de Hola. Para obtener información adicional para configurar clústeres de servidores de archivos y recursos compartidos disponibles continuamente con Windows Server 2012, consulte toothis [demostración en vídeo](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares).

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga más información acerca de los límites de StorSimple](storsimple-limits.md).
* [Obtenga información acerca de cómo toodeploy su solución de StorSimple](storsimple-deployment-walkthrough-u2.md).

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx

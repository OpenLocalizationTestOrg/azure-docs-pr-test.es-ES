---
title: "configuración de dispositivo de StorSimple de hello aaaModify | Documentos de Microsoft"
description: "Describe cómo toouse Hola tooreconfigure de servicio de administrador de StorSimple a un dispositivo de StorSimple que ya se ha implementado."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: bb679264-8d46-429c-9ef7-630dc3b4a423
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: v-sharos
ms.openlocfilehash: 10a54c191260bf1baba58d28cdbfa0ed72217f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomodify-your-storsimple-device-configuration"></a>Usar la configuración del dispositivo StorSimple de toomodify de servicio de StorSimple Manager Hola
## <a name="overview"></a>Información general
Hola portal de Azure clásico **configurar** página contiene todos los parámetros de dispositivo de Hola que puede volver a configurar en un dispositivo de StorSimple que se administra mediante un servicio de StorSimple Manager. Este tutorial le explica cómo puede usar hello **configurar** hello tooperform de página después de las tareas de nivel de dispositivo:

* Modificar la configuración del dispositivo 
* Modificar la configuración del tiempo 
* Modificar la configuración de DNS 
* Modificar las interfaces de red
* Intercambiar o volver a asignar direcciones IP

## <a name="modify-device-settings"></a>Modificar la configuración del dispositivo
configuración del dispositivo de Hello incluye el nombre descriptivo de hello de dispositivo de hello y una descripción de dispositivo de Hola.

> [!NOTE] 
> No se puede modificar el nombre de dispositivo de Hola Hola portal de Azure clásico. Cambio de nombre de hello de dispositivo no es compatible.

Un dispositivo de StorSimple que está conectado toohello el servicio StorSimple Manager se le asigna un nombre predeterminado. nombre de Hello predeterminado normalmente refleja el número de serie de hello de dispositivo de Hola. Por ejemplo, un nombre de dispositivo predeterminado que tiene 15 caracteres, como 8600-SHX0991003G44HT, indica a continuación hello:

* **8600** : modelo del dispositivo indica Hola.
* **SHX** : sitio de producción de hello indica.
* **0991003** : indica un producto específico.
* **G44HT**: hello últimos 5 dígitos son números de serie exclusivos toocreate incrementado. Es posible que esto no sea un conjunto secuencial.

También puede especificar una descripción para el dispositivo. Descripción de un dispositivo normalmente ayuda a identificar propietario hello y la ubicación física de hello de dispositivo de Hola. campo de descripción de Hello debe contener menos de 256 caracteres.

## <a name="modify-time-settings"></a>Modificar la configuración del tiempo
El dispositivo debe sincronizar la hora en orden tooauthenticate con su proveedor de servicios de almacenamiento en la nube. Seleccione la zona horaria de la lista desplegable de Hola y especifique los servidores de protocolo de tiempo de red (NTP) tootwo. el servidor NTP principal Hello es necesario y se especifica al usar Windows PowerShell para StorSimple tooconfigure, el dispositivo. Puede especificar de forma predeterminada Hola Windows Server **time.windows.com** como el servidor NTP. Puede ver Hola principal configuración del servidor NTP a través del portal de Azure clásico hello, pero debe usar toochange de interfaz de Windows PowerShell de Hola.

configuración del servidor NTP secundario Hello es opcional. Puede usar tooconfigure portal clásico de hello un servidor NTP secundario. 

Al configurar el servidor NTP hello, asegúrese de que su red permite toopass de tráfico NTP Hola desde su toohello de centro de datos Internet. Al especificar un servidor NTP público, debe asegurarse de que los firewalls de red y otros dispositivos de seguridad son tooallow configurado NTP tráfico tootravel tooand de hello fuera de la red. Si no se permite el tráfico NTP bidireccional, debe usar un servidor NTP interno (esta función la proporciona un controlador de dominio de Windows). Si el dispositivo no puede sincronizar la hora, no puede ser capaz de toocommunicate con el proveedor de almacenamiento en la nube.

una lista de servidores NTP públicos, vaya toohello toosee [NTP servidores Web](http://support.ntp.org/bin/view/Servers/WebHome). 

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>¿Qué ocurre si el dispositivo de Hola se implementa en una zona horaria diferente?
Si el dispositivo de Hola se implementa en una zona horaria diferente, cambiará Hola zona horaria del dispositivo. Dado que todas las directivas de copia de seguridad de hello usa la zona horaria del dispositivo hello, directivas de copia de seguridad de Hola se ajustarán automáticamente a la nueva zona de horaria Hola. No se requiere ninguna intervención del usuario.

## <a name="modify-dns-settings"></a>Modificar la configuración de DNS
Un servidor DNS se usa cuando el dispositivo intenta toocommunicate con su proveedor de servicios de almacenamiento en la nube. Para lograr alta disponibilidad, son necesario tooconfigure ambos Hola principal y Hola los servidores DNS secundarios durante la implementación inicial de dispositivos de Hola. servidor DNS principal a tooreconfigure hello, deberá toouse interfaz de Windows PowerShell de hello en el dispositivo StorSimple.

servidor DNS secundario a toomodify hello, puede usar hello portal de Azure clásico.

## <a name="modify-network-interfaces"></a>Modificar las interfaces de red
El dispositivo tiene seis interfaces de red de dispositivo, cuatro de las cuales son de 1 GbE y dos de 10 GbE. Estas interfaces están etiquetadas mediante DATA 0 – DATA 5. DATA 0, DATA 1, DATA 4 y DATA 5 son de 1 GbE, mientras que DATA 2 y DATA 3 son interfaces de red de 10 GbE.

Configurar **configuración de la interfaz de red** para cada uno de hello interfaces toobe usa. tooensure alta disponibilidad, se recomienda tener al menos dos interfaces iSCSI y dos interfaces habilitadas para la nube en su dispositivo. Es recomendable, pero no obligatorio, deshabilitar las interfaces no usadas.

Al configurar cualquiera de las interfaces de red de hello, debe configurar una dirección IP virtual (VIP).

DATA 0 es compatible con la nube de manera predeterminada. Al configurar DATA 0, también son tooconfigure requiere dos direcciones IP fijas, una para cada controlador. Estas direcciones IP fijas pueden ser tooaccess usa controladores de dispositivo de hello directamente y son útiles cuando se instalan actualizaciones en el dispositivo de Hola o cuando tiene acceso a controladores de hello para el propósito de Hola de solución de problemas.

En StorSimple 8000 Series Update 1, métrica de enrutamiento de Hola de DATA 0 se establece toohello más baja; por lo tanto, si el dispositivo está ejecutando StorSimple 8000 Series Update 1, todo el tráfico de hello en la nube se enrutará a través de DATA 0. Tome nota de esto si hay más de una interfaz de red compatible con la nube en el dispositivo StorSimple.

> [!NOTE]
> Hola direcciones IP para el controlador de hello fijas se usan para atender toohello dispositivo de hello las actualizaciones. Por lo tanto, Hola IP fija debe ser enrutables y deben poder tooconnect toohello Internet.
> 
> 

Para cada interfaz de red, se muestra Hola parámetros siguientes:

* **Velocidad** : no es un parámetro configurable por el usuario. DATA 0, DATA 1, DATA 4 y DATA 5 son siempre de 1 GbE, mientras que DATA 2 y DATA 3 son interfaces de 10 GbE.
  
  > [!NOTE]
  > La velocidad y el dúplex siempre se negocian automáticamente. Las tramas gigantes no son compatibles.
  > 
  > 
* **Estado de interfaz** : una interfaz se puede habilitar o deshabilitar. Si está habilitada, dispositivo Hola tratará de interfaz de hello toouse. Se recomienda que solo las interfaces que son redes conectadas toohello y utilizaron esté habilitada. Deshabilite las interfaces que no esté usando.
* **Tipo de interfaz** : este parámetro permite tooisolate el tráfico iSCSI del tráfico de almacenamiento en la nube. Este parámetro puede ser uno de hello siguientes:
  
  * **En la nube habilitada** : cuando está habilitada, Hola dispositivo va a usar esta interfaz toocommunicate con la nube de Hola.
  * **habilitado para iSCSI** : cuando está habilitada, Hola dispositivo va a usar esta interfaz toocommunicate con host iSCSI de Hola.
    
    Es recomendable aislar el tráfico iSCSI del tráfico de almacenamiento en la nube. Tenga en cuenta si el host está dentro de hello misma subred que el dispositivo, no es necesario tooassign una puerta de enlace; Sin embargo, si el host está en una subred diferente que el dispositivo, deberá tooassign una puerta de enlace.
* **Dirección IP** : esta puede ser IPv4, IPv6 o ambas. Hola IPv4 y familias de direcciones IPv6 se admiten para las interfaces de red de dispositivo Hola. Si usa IPv4, especifique una dirección IP de 32 bits (*xxx.xxx.xxx.xxx*) en notación punto-decimal. Cuando use IPv6, solo tiene que proporcionar un prefijo de 4 dígitos y se generará automáticamente una dirección de 128 bits para la interfaz de red del dispositivo en función de ese prefijo.
* **Subred** : Esto hace referencia a la máscara de subred toohello y se configura mediante la interfaz de Windows PowerShell de Hola.
* **Puerta de enlace** : se trata de puerta de enlace predeterminada de Hola que se debe usar esta interfaz cuando intenta toocommunicate a los nodos que no están dentro de hello mismo espacio de direcciones IP (subred). Hello puerta de enlace predeterminada debe ser Hola mismo espacio de direcciones (subred) como dirección IP de la interfaz de hello, según lo determinado por la máscara de subred de Hola.
* **Dirección IP fija** : este campo solo está disponible al configurar Hola DATA 0 interfaz. Para operaciones como actualizaciones o solución de problemas de hello de dispositivo, puede que necesite tooconnect toohello directamente del controlador del dispositivo. Hola dirección IP fija puede ser utilizados tooaccess Hola activo y el controlador pasivo hello en el dispositivo.

Puede volver a configurar el controlador 0 y 1 a través del portal de Azure clásico de Hola.

> [!NOTE]
> * tooensure el funcionamiento correcto, compruebe la velocidad de la interfaz de Hola y dúplex en el conmutador de Hola que está conectado cada interfaz de dispositivo. Las interfaces de conmutador deben negociar con o configurarse para Gigabit Ethernet (1000 Mbps) y ser de dúplex completo. Las interfaces que funcionan a velocidades menores o en un semidúplex darán como resultado problemas de rendimiento.
> * toominimize interrupciones y tiempo de inactividad, recomendamos habilitar portfast en cada uno de conmutador de hello puertos que Hola iSCSI de interfaz de red del dispositivo se conectará a. Esto garantizará que la conectividad de red se puede establecer rápidamente en caso de hello de una conmutación por error.
> 
> 

## <a name="swap-or-reassign-ips"></a>Intercambiar o volver a asignar direcciones IP
Actualmente, si alguna interfaz de red en el controlador de hello tiene asignado una VIP que está en uso (por hello mismo dispositivo u otro dispositivo de red de hello), se producirá un error de controlador de hello sobre. Por lo tanto, tiene toofollow Hola apropiado procedimiento si intercambia a VIP para la interfaz de red del dispositivo de hello, puesto que creará una situación de IP duplicada.

Realizar Hola siguiendo los pasos tooswap o reasignar a VIP de Hola para cualquiera de las interfaces de red de hello:

#### <a name="tooreassign-ips"></a>tooreassign direcciones IP
1. Dirección IP de hello clara para ambas interfaces.
2. Después de que se borran direcciones IP de hello, asignar nuevas direcciones IP de hello toohello respectivas interfaces.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[configurar MPIO para el dispositivo StorSimple](storsimple-configure-mpio-windows-server.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).


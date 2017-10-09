---
title: "configuración de dispositivo de aaaModify hello StorSimple 8000 series | Documentos de Microsoft"
description: "Describe cómo toouse Hola tooreconfigure de servicio de administrador de dispositivos de StorSimple a un dispositivo de StorSimple que ya se ha implementado."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a>Usar la configuración del dispositivo StorSimple de toomodify de servicio del Administrador de dispositivos de StorSimple de Hola

## <a name="overview"></a>Información general

Hola portal de Azure **configuración de dispositivo** sección Hola **configuración** hoja contiene todos los parámetros de dispositivo de Hola que puede volver a configurar en un dispositivo de StorSimple que está administrado por un administrador de dispositivos de StorSimple servicio. Este tutorial le explica cómo puede usar hello **configuración** Hola de tooperform hoja siguiente las tareas de nivel de dispositivo:

* Modificar el nombre descriptivo del dispositivo
* Modificar la configuración de hora del dispositivo
* Asignar un DNS secundario
* Modificar las interfaces de red
* Intercambiar o volver a asignar direcciones IP

## <a name="modify-device-friendly-name"></a>Modificar el nombre descriptivo del dispositivo

Puede usar nombre de dispositivo de hello toochange portal Azure hello y asígnele un nombre descriptivo único de su elección. Hola de uso **configuración General** hoja en el nombre descriptivo del dispositivo de hello de dispositivo toomodify. nombre descriptivo de Hello puede contener cualquier carácter y puede tener un máximo de 64 caracteres.

> [!NOTE] 
> Sólo puede modificar el nombre de dispositivo de Hola Hola portal de Azure antes de que finalice el programa de instalación de dispositivo de Hola. Una vez completada la configuración mínima del dispositivo de hello, no se puede cambiar el nombre de dispositivo de Hola.

![Nombre del dispositivo en Configuración general](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

Un dispositivo de StorSimple que está conectado toohello servicio de administrador de dispositivos de StorSimple se asigna un nombre predeterminado. nombre de Hello predeterminado normalmente refleja el número de serie de hello de dispositivo de Hola. Por ejemplo, un nombre de dispositivo predeterminado que tiene 15 caracteres, como 8600-SHX0991003G44HT, indica a continuación hello:

* **8600** : modelo del dispositivo indica Hola.
* **SHX** : sitio de producción de hello indica.
* **0991003** : indica un producto específico.
* **G44HT**: hello últimos 5 dígitos son números de serie exclusivos toocreate incrementado. Es posible que esto no sea un conjunto secuencial.

## <a name="modify-device-description"></a>Modificar la descripción del dispositivo

Hola de uso **configuración General** hoja en la descripción del dispositivo toomodify hello de dispositivo.

![Descripción del dispositivo en Configuración general](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

Descripción de un dispositivo normalmente ayuda a identificar propietario hello y la ubicación física de hello de dispositivo de Hola. campo de descripción de Hello debe contener menos de 256 caracteres.

## <a name="modify-time-settings"></a>Modificar la configuración del tiempo

El dispositivo debe sincronizar la hora en orden tooauthenticate con su proveedor de servicios de almacenamiento en la nube. Hola de uso **configuración General** hoja en la configuración de hora del dispositivo de hello de dispositivo toomodify.

![Descripción del dispositivo en Configuración general](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 Seleccione la zona horaria de la lista desplegable de Hola. Puede especificar los servidores de protocolo de tiempo de red (NTP) tootwo:

 - **Servidor NTP principal** -configuración de hello es necesario y se especifica al usar Windows PowerShell para StorSimple tooconfigure, el dispositivo. Puede especificar de forma predeterminada Hola Windows Server **time.windows.com** como el servidor NTP. Puede ver Hola principal configuración del servidor NTP a través de hello portal de Azure, pero debe usar toochange de interfaz de Windows PowerShell de Hola. Hola de uso `Set-HcsNTPClientServerAddress` toomodify de servidor NTP principal cmdlet Hola de su dispositivo. Para obtener más información, vaya toosynxtax cmdlet [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx).

- **El servidor NTP secundario** -Hola configuración es opcional. Puede usar Hola portal tooconfigure un servidor NTP secundario.

Al configurar el servidor NTP hello, asegúrese de que su red permite toopass de tráfico NTP Hola desde su toohello de centro de datos Internet. Al especificar un servidor NTP público, debe asegurarse de que los firewalls de red y otros dispositivos de seguridad son tooallow configurado NTP tráfico tootravel tooand de hello fuera de la red. Si no se permite el tráfico NTP bidireccional, debe usar un servidor NTP interno (esta función la proporciona un controlador de dominio de Windows). Si el dispositivo no puede sincronizar la hora, no puede ser capaz de toocommunicate con el proveedor de almacenamiento en la nube.

una lista de servidores NTP públicos, vaya toohello toosee [NTP servidores Web](http://support.ntp.org/bin/view/Servers/WebHome).

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>¿Qué ocurre si el dispositivo de Hola se implementa en una zona horaria diferente?

Si el dispositivo de Hola se implementa en una zona horaria diferente, cambiará Hola zona horaria del dispositivo. Dado que todas las directivas de copia de seguridad de hello usa la zona horaria del dispositivo hello, directivas de copia de seguridad de Hola se ajustarán automáticamente a la nueva zona de horaria Hola. No se requiere ninguna intervención del usuario.

## <a name="modify-dns-settings"></a>Modificar la configuración de DNS

Un servidor DNS se usa cuando el dispositivo intenta toocommunicate con su proveedor de servicios de almacenamiento en la nube. Hola de uso **configuración de red** hoja en el dispositivo tooview y modificar la configuración de DNS de hello configurado. 

![Configuración de DNS en Configuración de red](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

Para lograr alta disponibilidad, son necesario tooconfigure ambos Hola principal y Hola los servidores DNS secundarios durante la implementación inicial de dispositivos de Hola.

**Servidor DNS principal** -usar hello Windows PowerShell para StorSimple toofirst especificar servidor DNS principal de Hola durante la instalación inicial de Hola. Puede configurar el servidor DNS principal de hello sólo a través de la interfaz de Windows PowerShell de Hola. Hola de uso `Set-HcsDNSClientServerAddress` cmdlet toomodify Hola servidor DNS principal de su dispositivo. Para obtener más información, visite toosynxtax obtener [Set-HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.

**Servidor DNS secundario** -toomodify Hola servidor DNS secundario, use hello `Set-HcsDNSClientServerAddress` cmdlet en la interfaz de Windows PowerShell de hello de dispositivo de Hola o **configuración de red** hoja del dispositivo de StorSimple en hello Azure Portal.

servidor DNS toomodify Hola secundario en el portal de Azure, realice Hola pasos.

1. Servicio de administrador de dispositivos de StorSimple de tooyour go. En la lista Hola de dispositivos, seleccione y haga clic en el dispositivo.

2. Hola **configuración** hoja, vaya demasiado**configuración del dispositivo > red**. Esto abrirá hello **configuración de red** hoja. Haga clic en el icono de **Configuración DNS**. Modificar Hola secundaria DNS dirección IP del servidor.

    ![Modificación de la dirección IP del servidor DNS secundario](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. En la barra de comandos de hello, haga clic en **guardar** y cuando se le solicite confirmación, haga clic en **Aceptar**.

    ![Guardado y confirmación de los cambios](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a>Modificar las interfaces de red

El dispositivo tiene seis interfaces de red de dispositivo, cuatro de las cuales son de 1 GbE y dos de 10 GbE. Estas interfaces están etiquetadas mediante DATA 0 – DATA 5. DATA 0, DATA 1, DATA 4 y DATA 5 son de 1 GbE, mientras que DATA 2 y DATA 3 son interfaces de red de 10 GbE.

Hola de uso **configuración de red** hoja tooconfigure cada de hello interfaces toobe usa.

![Configuración de las interfaces de red mediante Configuración de red](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

tooensure alta disponibilidad, se recomienda tener al menos dos interfaces iSCSI y dos interfaces habilitadas para la nube en su dispositivo. Es recomendable, pero no obligatorio, deshabilitar las interfaces no usadas.

Para cada interfaz de red, se muestra Hola parámetros siguientes:

* **Velocidad** : no es un parámetro configurable por el usuario. DATA 0, DATA 1, DATA 4 y DATA 5 son siempre de 1 GbE, mientras que DATA 2 y DATA 3 son interfaces de 10 GbE.
  
  > [!NOTE]
  > La velocidad y el dúplex siempre se negocian automáticamente. Las tramas gigantes no son compatibles.
  
* **Estado de interfaz** : una interfaz se puede habilitar o deshabilitar. Si está habilitada, dispositivo Hola tratará de interfaz de hello toouse. Se recomienda que solo las interfaces que son redes conectadas toohello y utilizaron esté habilitada. Deshabilite las interfaces que no esté usando.
* **Tipo de interfaz** : este parámetro permite tooisolate el tráfico iSCSI del tráfico de almacenamiento en la nube. Este parámetro puede ser uno de hello siguientes:
  
  * **En la nube habilitada** : cuando está habilitada, Hola dispositivo va a usar esta interfaz toocommunicate con la nube de Hola.
  * **habilitado para iSCSI** : cuando está habilitada, Hola dispositivo va a usar esta interfaz toocommunicate con host iSCSI de Hola.
    
    Es recomendable aislar el tráfico iSCSI del tráfico de almacenamiento en la nube. Tenga en cuenta si el host está dentro de hello misma subred que el dispositivo, no es necesario tooassign una puerta de enlace; Sin embargo, si el host está en una subred diferente que el dispositivo, deberá tooassign una puerta de enlace.
* **Dirección IP** : al configurar cualquiera de las interfaces de red de hello, debe configurar una dirección IP virtual (VIP). Puede ser IPv4, IPv6 o ambas. Hola IPv4 y familias de direcciones IPv6 se admiten para las interfaces de red de dispositivo Hola. Si usa IPv4, especifique una dirección IP de 32 bits (*xxx.xxx.xxx.xxx*) en notación punto-decimal. Cuando use IPv6, solo tiene que proporcionar un prefijo de 4 dígitos y se generará automáticamente una dirección de 128 bits para la interfaz de red del dispositivo en función de ese prefijo.
* **Subred** : Esto hace referencia a la máscara de subred toohello y se configura mediante la interfaz de Windows PowerShell de Hola.
* **Puerta de enlace** : se trata de puerta de enlace predeterminada de Hola que se debe usar esta interfaz cuando intenta toocommunicate a los nodos que no están dentro de hello mismo espacio de direcciones IP (subred). Hello puerta de enlace predeterminada debe ser Hola mismo espacio de direcciones (subred) como dirección IP de la interfaz de hello, según lo determinado por la máscara de subred de Hola.
* **Dirección IP fija** : este campo solo está disponible al configurar Hola DATA 0 interfaz. Para operaciones como actualizaciones o solución de problemas de hello de dispositivo, puede que necesite tooconnect toohello directamente del controlador del dispositivo. Hola dirección IP fija puede ser utilizados tooaccess Hola activo y el controlador pasivo hello en el dispositivo.

> [!NOTE]
> * tooensure el funcionamiento correcto, compruebe la velocidad de la interfaz de Hola y dúplex en el conmutador de Hola que está conectado cada interfaz de dispositivo. Las interfaces de conmutador deben negociar con o configurarse para Gigabit Ethernet (1000 Mbps) y ser de dúplex completo. Las interfaces que funcionan a velocidades menores o en un semidúplex darán como resultado problemas de rendimiento.
> * toominimize interrupciones y tiempo de inactividad, recomendamos habilitar portfast en cada uno de conmutador de hello puertos que Hola iSCSI de interfaz de red del dispositivo se conectará a. Esto garantizará que la conectividad de red se puede establecer rápidamente en caso de hello de una conmutación por error.

### <a name="configure-data-0"></a>Configuración de DATA 0

DATA 0 es compatible con la nube de manera predeterminada. Al configurar DATA 0, también son tooconfigure requiere dos direcciones IP fijas, una para cada controlador. Estas direcciones IP fijas pueden ser tooaccess usa controladores de dispositivo de hello directamente y son útiles cuando se instalan actualizaciones en el dispositivo de Hola o cuando tiene acceso a controladores de hello para el propósito de Hola de solución de problemas.

Puede volver a configurar Hola fijo controladores IP a través de la hoja de hello datos 0 la configuración.

![Configuración de la interfaz de red: DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> Hola direcciones IP para el controlador de hello fijas se usan para atender toohello dispositivo de hello las actualizaciones. Por lo tanto, Hola IP fija debe ser enrutables y deben poder tooconnect toohello Internet.

### <a name="configure-data-1---data-5"></a>Configuración de DATA 1 a DATA5

Para los datos 1 - interfaces de red 5 de datos, puede configurar todas las configuraciones de red de hello tal y como se muestra en la siguiente captura de pantalla de hello:

![Configuración de las interfaces de red de DATA 1 a DATA 5](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a>Intercambiar o volver a asignar direcciones IP

Actualmente, si alguna interfaz de red en el controlador de hello tiene asignado una VIP que está en uso (por hello mismo dispositivo u otro dispositivo de red de hello), se producirá un error de controlador de hello sobre. Si intercambia o reasigna direcciones IP virtuales para una interfaz de red de dispositivo, debe seguir un procedimiento adecuado ya que podría crear una situación de IP duplicada.

Realizar Hola siguiendo los pasos tooswap o reasignar a VIP de Hola para cualquiera de las interfaces de red de hello:

#### <a name="tooreassign-ips"></a>tooreassign direcciones IP

1. Dirección IP de hello clara para ambas interfaces.
2. Después de que se borran direcciones IP de hello, asignar nuevas direcciones IP de hello toohello respectivas interfaces.

## <a name="next-steps"></a>Pasos siguientes

* Obtenga información acerca de cómo demasiado[configurar MPIO para el dispositivo StorSimple](storsimple-8000-configure-mpio-windows-server.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).


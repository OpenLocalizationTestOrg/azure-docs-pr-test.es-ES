---
title: dispositivo de Microsoft Azure StorSimple 8600 aaaInstall | Documentos de Microsoft
description: "Describe cómo toounpack, montaje en bastidor y cable del dispositivo de StorSimple 8600 antes de implementar y configurar el software de Hola."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>Desempaquetar, montar en bastidor y colocar los cables del dispositivo StorSimple 8600.
## <a name="overview"></a>Información general
Su Microsoft Azure StorSimple 8600 es un dispositivo de receptáculo dual que consta de un receptáculo principal y EBOD. Este tutorial le explica cómo toounpack y montaje en bastidor, cable Hola el hardware del dispositivo StorSimple 8600 antes de configurar el software de StorSimple Hola.

## <a name="unpack-your-storsimple-8600-device"></a>Desempaquete el dispositivo StorSimple 8600
Hello pasos siguientes proporcionan claras y obtener instrucciones detalladas sobre cómo toounpack el dispositivo de almacenamiento de StorSimple 8600. Este dispositivo se incluye en dos cajas, uno para el alojamiento principal de hello y otro para Hola alojamiento de EBOD. Después, estas dos cajas se colocan en un una sola caja.

### <a name="prepare-toounpack-your-device"></a>Preparar el dispositivo de toounpack
Antes de desempaquetar el dispositivo, revise Hola siguiente información.

![Icono Advertencia](./media/storsimple-safety/IC740879.png)![icono de peso elevado](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png)**ADVERTENCIA**

1. Asegúrese de que dispone de dos personas toomanage disponibles Hola peso dispositivo Hola si se manipule de forma manual. Un alojamiento totalmente configurado puede pesar seguridad too32 kg (70 lbs).
2. Cuadro de Hola se coloca en una superficie plana y nivelada.

A continuación, completar Hola siguiendo los pasos toounpack el dispositivo.

#### <a name="toounpack-your-device"></a>toounpack el dispositivo
1. Inspeccionar cuadro hello y la espuma de embalaje de hello en busca de golpes, cortes, daños por agua o cualquier otro daño evidente. Si la caja de Hola o el embalaje está muy dañado, no abra cuadro Hola. Por favor, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) toohelp evaluar si el dispositivo de hello está en buenas condiciones de funcionamiento.
2. Abrir cuadro externa de hello y, a continuación, retire dos cuadros de hello correspondiente alojamientos EBOD y tooprimary. Ahora puede desempaquetar hello principal y alojamientos de EBOD. Hola figura siguiente muestra la vista de hello desempaquetado de uno de los contenedores de Hola.
   
    ![Desempaquetar el dispositivo de almacenamiento](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **Vista del dispositivo de almacenamiento desempaquetado**
   
   | Etiqueta | Descripción |
   | --- | --- |
   |   1 |Caja de embalaje |
   |   2 |Cables SAS (en la bandeja de cables y accesorios) |
   |   3 |Espuma inferior |
   |   4 |Dispositivo |
   |   5 |Espuma superior |
   |   6 |Caja de accesorios |
3. Después de desempaquetar cuadros Hola dos, asegúrese de que dispone de:
   
   * 1 alojamiento principal (alojamiento principal de Hola y el alojamiento de EBOD están en dos cajas separadas)
   * 1 receptáculos EBOD
   * 4 cables de alimentación, 2 en cada caja
   * 2 cables SAS (alojamiento de tooEBOD del alojamiento principal de Hola de tooconnect)
   * 1 cable Ethernet cruzado
   * 2 cables de consola serie
   * 1 convertidor serie a USB para el acceso en serie
   * 4 adaptadores QSFP a SFP+ para su uso con interfaces de red de 10 GbE
   * 2 kits de montaje (4 rieles laterales con hardware de montaje, 2 para el alojamiento principal de Hola y el alojamiento de EBOD), bastidor 1 en cada caja
   * Documentación de introducción
     
     Si no recibió alguno de los elementos de hello mencionados anteriormente, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md).  

paso siguiente Hello es toorack montar el dispositivo.

## <a name="rack-mount-your-storsimple-8600-device"></a>Montaje en bastidor del dispositivo StorSimple 8600
Siga hello tooinstall de pasos siguiente dispositivo de almacenamiento de StorSimple 8600 en un bastidor estándar de 19 pulgadas con puestos frontal y trasero. Este dispositivo se suministra con dos receptáculos: un receptáculo principal y un EBOD. Ambos necesitan toobe montados en bastidor.

instalación de Hello consta de varios pasos, cada uno de los cuales se explica en hello procedimientos siguientes.

> [!IMPORTANT]
> Los dispositivos StorSimple deben estar montados en un bastidor para funcionar correctamente.
> 
> 

### <a name="site-preparation"></a>Preparación del sitio
contenedores de Hello deben instalarse en un bastidor estándar de 19 pulgadas con puestos frontal y trasero. Usar hello siguiendo el procedimiento tooprepare para la instalación del bastidor.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>sitio de hello tooprepare para la instalación del bastidor
1. Asegúrese de que ese hello es principal y son los alojamientos de EBOD descansen de manera segura en una superficie de trabajo plana, estable y nivelada (o similar).
2. Comprobar ese sitio Hola donde piensa tooset seguridad tiene CA estándar energía desde una fuente independiente o una unidad de distribución de energía (PDU) de bastidor con un sistema de alimentación ininterrumpida (SAI).
3. Asegúrese de que esa ranura de uno 4U (2 X 2U) está disponible en bastidor de hello en el que piensa alojamientos de hello toomount.

![Icono Advertencia](./media/storsimple-safety/IC740879.png)![icono de peso elevado](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png)**ADVERTENCIA**

 Asegúrese de que dispone de peso de dos personas disponibles toomanage Hola si se manipule el programa de instalación de dispositivo de Hola de forma manual. Un alojamiento totalmente configurado puede pesar seguridad too32 kg (70 lbs).

### <a name="rack-prerequisites"></a>Requisitos previos del bastidor
Hola alojamientos están diseñados para la instalación en un bastidor de 19 pulgadas estándar CAB con:

* Profundidad mínima de 27,84 pulgadas de bastidor registrar toopost
* Peso máximo de 32 kg para el dispositivo de Hola
* Contrapresión máxima de 5 pascales (medidor de agua de 0,5 mm)

### <a name="rack-mounting-rail-kit"></a>Kit de guías de montaje en bastidor
Un conjunto de raíles de montaje se proporcionarán para su uso con el gabinete de bastidor de 19 pulgadas de Hola. raíles de Hello han sido probado peso máximo del alojamiento de toohandle Hola. Estos raíles también permitirán la instalación de varios alojamientos sin perder espacio dentro del bastidor de Hola. Instale primero el alojamiento de EBOD Hola.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>Hola tooinstall alojamiento de EBOD en los raíles de Hola
1. Realice este paso únicamente si las guías internas no están instaladas en el dispositivo. Por lo general, raíles interna de Hola se instalan en fábrica Hola. Si raíles no están instalados, instale los lados de hello deslizantes izquierda y derecha raíl toohello del chasis del alojamiento de Hola. Estas se instalan mediante seis tornillos métricos en cada lado. toohelp con orientación, ferroviario Hola diapositivas están marcadas **LH – Front** y **RH – Front**, y el final de Hola que se sujeta hacia la parte trasera de hello del alojamiento de hello más tiene un extremo cónico.
   
    ![Adjuntar carriles deslizantes tooenclosure chasis](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **Adjuntar raíl diapositivas toohello lados del alojamiento de Hola**
   
   | Etiqueta | Descripción |
   | --- | --- |
   |  1 |Tornillos de cabeza de botón M 3 x 4 |
   |  2 |Guías de chasis |
2. Adjuntar izquierdo hello y columna derecha ensamblados toohello rack miembros verticales del gabinete. Hola soportes están marcados con **LH**, **RH**, y **esta cara hacia arriba** tooguide a través de la orientación correcta.
3. Localice los pasadores de raíl de hello en hello frontal y trasera del ensamblado del raíl Hola. Extender Hola raíl toofit entre cada envío de bastidor de Hola e inserte los PIN de Hola orificios del miembro vertical de post frontal y trasero del bastidor de Hola. Asegúrese de que el ensamblado del raíl Hola está nivelado.
4. Proteger Hola bastidor de toohello ensamblado raíl miembros verticales por medio de dos de los tornillos métricos de hello proporcionados. Use un tornillo en la parte frontal de hello y otro en la parte trasera de Hola.
5. Repita estos pasos para hello otro ensamblado del raíl.
   
     ![Adjuntar carriles deslizantes toorack cab](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Adjuntar raíl ensamblados toohello rack**
   
   | Etiqueta | Descripción |
   | --- | --- |
   |   1 |Tornillo de fijación |
   |   2 |Tornillo del poste del bastidor delantero de orificio cuadrado |
   |   3 |Pasadores de ubicación de la guía delantera izquierda |
   |   4 |Tornillo de fijación |
   |   5 |Pasadores de ubicación de la guía trasera izquierda |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Montar el alojamiento de EBOD hello en bastidor Hola
Con los raíles del bastidor de Hola que acaba de instalar, realizar Hola después de alojamiento de EBOD pasos toomount hello en bastidor Hola.

#### <a name="toomount-hello-ebod-enclosure"></a>Hola toomount alojamiento de EBOD
1. Con un Ayudante, levante el alojamiento de Hola y alinéelo con los raíles del bastidor Hola.
2. Inserte con cuidado el alojamiento de hello en los raíles de hello y, a continuación, empújelo por completo en bastidor Hola cab.
   
    ![Insertando dispositivo en bastidor Hola](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Montar el alojamiento de hello en bastidor de Hola**
3. Quitar Hola izquierda y topes de aletas frontal derecho extrayendo los límites de hello libres. topes de aletas Hola simplemente acoplados a pestañas Hola.
4. Asegure el alojamiento de hello en bastidor hello mediante la instalación de un tornillo de cabeza Phillips proporcionado a través de cada brida, izquierda y derecha.
5. Instale los topes de bridas de hello presionándolos en su posición y ajustándolos en su lugar.
   
     ![Instalación de los topes de las bridas](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Instalando topes de aletas Hola**
   
   | Etiqueta | Descripción |
   | --- | --- |
   |   1 |Tornillo de fijación del receptáculo |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Montar el alojamiento principal de hello en bastidor Hola
Cuando haya terminado de montar el alojamiento de EBOD hello, necesitará alojamiento principal de hello toomount siguiente Hola los mismos pasos.

> [!NOTE]
> * Es posible toohave varias ranuras vacías en hello en bastidor entre el alojamiento principal de Hola y el alojamiento de EBOD Hola.
> * Utilice Hola proporciona 2m SAS cable tooconnect Hola alojamiento principal toohello alojamiento de EBOD.
> * No hay ninguna restricción en la posición relativa de Hola de unidad de hello unidad principal toohello EBOD. Por lo tanto, se puede colocar alojamiento principal de hello en ranura superior de Hola y el alojamiento de EBOD de hello debajo, o viceversa.
> 
> 

paso siguiente Hello es toocable del dispositivo para alimentación, red y acceso serie.

## <a name="cable-your-storsimple-8600-device"></a>Instalación de cables del dispositivo StorSimple 8600
Hello procedimientos siguientes explican cómo toocable su dispositivo 8600 de StorSimple para alimentación, red y conexiones en serie.

### <a name="prerequisites"></a>Requisitos previos
Antes de comenzar toocable el dispositivo, necesitará:

* El alojamiento principal y alojamiento de EBOD hello, completamente desempaquetados.
* 4 cables de alimentación (2 cada hello principal y alojamiento de EBOD Hola) que acompañan al dispositivo
* 2 cables SAS suministrados con hello tooconnect de dispositivo Hola alojamiento principal de toohello de alojamiento EBOD
* Acceso too2 distribución unidades de energía (PDU) (recomendado)
* Cables de red
* Cables serie suministrados
* Convertidor serie-USB con controlador de hello apropiado instalado en su PC (si es necesario)
* Se proporcionan 4 adaptadores QSFP a SFP+ para su uso con interfaces de red de 10 GbE.
* [Hardware compatible con interfaces de red de hello 10 GbE en el dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>SAS y cables de alimentación
El dispositivo cuenta con una caja principal y una caja EBOD. Para ello, Hola unidades toobe cableado conjuntamente para alimentación y conectividad Serial Attached SCSI (SAS).

Al configurar este dispositivo para hello primera vez, realice los pasos de Hola para cableado de SAS y los pasos de hello, a continuación, completa para el cableado de alimentación.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>Cables de red
El dispositivo tiene una configuración activo-espera: en un momento dado, un módulo de controlador está activo y procesa todas las operaciones de disco y red mientras Hola otro módulo de controlador está en modo de espera. Si se produce un error de controlador, controlador en espera de Hola se activa inmediatamente y continúa todas las operaciones de disco y redes de Hola.

toosupport esta conmutación por error de controlador redundante, necesita toocable el dispositivo de red como se muestra en hello pasos.

#### <a name="toocable-for-network-connection"></a>toocable para conexión de red
1. El dispositivo tiene seis interfaces de red en cada controlador: cuatro puertos Ethernet de 1 Gbps y dos de 10 Gbps. Consulte toohello siguiente puertos de datos de ilustración tooidentify Hola de hello backplane de su dispositivo.
   
     ![Panel posterior del dispositivo 8600](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Parte posterior del dispositivo con hello los puertos de datos**
   
   | Etiqueta | Description |
   | --- | --- |
   |   0,1,4,5 |Interfaces de red de 1 GbE |
   |   2,3 |Interfaces de red de 10 GbE |
   |   6 |Puertos serie |
2. Vea Hola siguiente diagrama para el cableado de red. (configuración de red mínimas de Hola se indica con líneas azules sólidas. Para obtener un alto rendimiento y disponibilidad, la configuración adicional requerida se muestra mediante líneas de puntos).

![Colocación del cable de red del dispositivo 4U](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**Cables de red del dispositivo**

| Etiqueta | Descripción |
| --- | --- |
| Encontrará |LAN con acceso a Internet |
| B |Controlador 0 |
| C |PCM 0 |
| D |Controlador 1 |
| E |PCM 1 |
| F |Controlador EBOD 0 |
| G |Controlador EBOD 1 |
| H,I |Hosts (por ejemplo, servidores de archivos) |
| 0-5 |Interfaces de red |
| 6 |Receptáculo principal |
| 7 |Receptáculo EBOD |

Cuando cablear el dispositivo de hello, requiere configuración mínima de hello:

* Al menos dos interfaces de red conectadas en cada controlador con una para el acceso a la nube y otra para iSCSI. Hola DATA 0 puerto automáticamente está habilitado y configurado a través de la consola de serie de hello de dispositivo de Hola. Aparte de DATA 0, otro puerto de datos también debe toobe configurado a través de hello portal de Azure clásico. En este caso, conectar DATA 0 puerto toohello LAN (red con acceso a Internet) principal. Hello otros datos pueden ser puertos conectado segmento de tooSAN/iSCSI LAN (VLAN) de red de hello, según el rol de hello prevista.
* Interfaces idénticas en cada controlador conectado toohello mismo red tooensure disponibilidad si se produce una conmutación por error del controlador. Por ejemplo, si elige tooconnect DATA 0 y DATA 3 para uno de los controladores de hello, necesita hello tooconnect correspondiente DATA 0 y DATA 3 en Hola otro controlador.

Tenga en cuenta lo siguiente para alta disponibilidad y rendimiento:

* Cuando sea posible, configure un par de interfaz de red para el acceso a la nube (1 GbE) y otro par para iSCSI (se recomiendan 10 GbE) en cada controlador.
* Cuando sea posible, conéctese interfaces de red desde cada tootwo diferentes conmutadores tooensure la disponibilidad del controlador con un error de interruptor. ilustración de Hola Hola dos 10 interfaces de red GbE, DATA 2 y 3 de datos, desde cada controlador conectado tootwo diferentes conmutadores. Para obtener más información, consulte toohello **interfaces de red** en hello [requisitos de alta disponibilidad para el dispositivo StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Si utiliza transceptores SFP + con las interfaces de red 10 GbE, use Hola proporciona QSFP-SFP + adaptadores. Para obtener más información, consulte demasiado[hardware compatible Hola 10 GbE interfaces de red en el dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Cableado del puerto serie
Realizar Hola siguiendo los pasos toocable el puerto serie.

#### <a name="toocable-for-serial-connection"></a>toocable conexión serie
1. El dispositivo tiene un puerto serie en cada controlador que se identifica mediante un icono de una llave inglesa. puertos serie de toolocate hello, consulte toohello ilustración que muestra los puertos de datos de hello en hello parte posterior del dispositivo.
2. Identificar controlador activo de hello en el plano posterior del dispositivo. Un LED azul que parpadea indica que el controlador de hello está activo.
3. Use Hola proporciona el cable serie (si es necesario, convertidor Hola USB-serie para su portátil) y conecte la consola o equipo (con el dispositivo de emulación de terminales toohello) toohello puerto serie del controlador activo Hola.
4. Instalar a controladores serie-USB de hello (incluidos con el dispositivo de Hola) en el equipo.
5. Configure la conexión serie hello, como sigue:
   
   * 115.200 baudios
   * Bits de datos: 8
   * Bit de parada: 1
   * Sin paridad
   * Control de flujo establecido demasiado**ninguno**
6. Compruebe que Hola conexión funciona, presione ENTRAR en la consola de Hola. Debería aparecer un menú de consola serie.

> [!NOTE]
> **Administración de KVM:** al dispositivo de hello está instalado en un centro de datos remoto o en una sala de informática con acceso limitado, garantizar que controladores de hello las conexiones serie tooboth estén siempre conectado tooa interruptor de consola serie o equipo similar. Esto permite el control remoto de fuera de banda y las operaciones de soporte si hay interrupciones de red o errores inesperados.
> 
> 

Se ha completado el cableado del dispositivo para alimentación, acceso a la red, y connection.hello serie siguiente paso es un software de hello tooconfigure en el dispositivo.

## <a name="next-steps"></a>Pasos siguientes
Ya estás listo demasiado[implementar y configurar el dispositivo de StorSimple local](storsimple-deployment-walkthrough-u2.md).


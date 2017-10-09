---
title: aaaMonitor el dispositivo de la serie StorSimple 8000 | Documentos de Microsoft
description: "Describe cómo toouse Hola Administrador de dispositivos de StorSimple service toomonitor uso, el rendimiento de E/S y la utilización de la capacidad."
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
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>Usar toomonitor de servicio del Administrador de dispositivos de StorSimple de hello en el dispositivo de StorSimple
## <a name="overview"></a>Información general
Puede usar dispositivos específicos de hello Administrador de dispositivos de StorSimple servicio toomonitor dentro de la solución StorSimple. Puede crear gráficos personalizados basados en rendimiento, utilización de la capacidad, rendimiento de la red y las métricas de rendimiento del dispositivo de E/S y anclar esos paneles toohello. Para obtener más información, consulte demasiado[personalizar el panel del portal](/articles/azure-portal/azure-portal-dashboards.md).

información de supervisión de hello tooview para un dispositivo específico, Hola portal de Azure, seleccione servicio de administrador de dispositivos de StorSimple de Hola. En lista de Hola de dispositivos, seleccione el dispositivo y, a continuación, vaya demasiado**Monitor**. A continuación, puede ver hello **capacidad**, **uso**, y **rendimiento** gráficos del dispositivo seleccionado Hola.

## <a name="capacity"></a>Capacity
**Capacidad** pistas Hola aprovisionado el espacio de hello queda en el dispositivo de Hola. capacidad restante de Hello, a continuación, se muestra como anclado localmente o en niveles.

Hola aprovisionado y la capacidad restante adicional se divide en volúmenes anclados localmente y en niveles. Para cada volumen, capacidad aprovisionada de Hola y Hola capacidad en el dispositivo de hello restante se muestra.

![Capacidad de E/S](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>Uso
**Uso de** cantidad de toohello relacionadas de las métricas de pistas de espacio de almacenamiento de datos que se utiliza para volúmenes de hello, contenedores de volúmenes o el dispositivo. Puede crear informes basados en la utilización de la capacidad de Hola de su almacenamiento principal, el almacenamiento en la nube o el almacenamiento del dispositivo. La utilización de la capacidad se puede medir para un volumen específico, un contenedor de volúmenes específico o todos los contenedores de volúmenes.
De forma predeterminada, se informa del uso de Hola durante las últimas 24 horas. Puede modificar la duración de Hola Hola gráfico toochange sobre qué Hola se informa del uso mediante la selección de:
* Últimas 24 horas
* Últimos 7 días
* Últimos 30 días
* Últimos 90 días
* Últimos año


Hola principal y en la nube, almacenamiento local usa se pueden describir como sigue:

### <a name="primary-storage-usage"></a>Uso del almacenamiento principal
Estos gráficos muestran la cantidad de Hola de los datos escritos tooStorSimple volúmenes antes de hello datos desduplicados y comprimidos. Puede ver Hola almacenamiento principal usada por todos los volúmenes en un contenedor de volumen o un único volumen. almacenamiento principal de Hello usado más es desglosado por principal almacenamiento en capas utilizado y principal utiliza almacenamiento anclado localmente.

Hello gráficos siguientes muestran almacenamiento principal de hello usado para un dispositivo de StorSimple antes y después de que se tomó una instantánea en la nube. Puesto que éste es simplemente los datos de volumen, una instantánea en la nube no debería cambiar almacenamiento principal de Hola. Como puede ver, el gráfico de hello no muestra ninguna diferencia en hello en capas o anclado localmente almacenamiento principal usado como resultado de tomar una instantánea de nube. instantánea en la nube Hola iniciado a aproximadamente 11:50 p.m. en dicho dispositivo.

![Uso de la capacidad principal después de la instantánea en la nube](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

Si ejecuta ahora E/S en el dispositivo de StorSimple de tooyour de hello host conectado, verá un aumento en el almacenamiento en capas principal o principal localmente anclado a la función de almacenamiento utilizado en los volúmenes (en niveles o anclado localmente) escribir datos de Hola a. Aquí son gráficos de uso de almacenamiento principal de Hola para un dispositivo de StorSimple. En este dispositivo, host de StorSimple Hola iniciado que sirve al escribe a aproximadamente 2:30 p.m. en un volumen en capas en el dispositivo de Hola. Puede ver el pico de hello en correspondiente E/S toohello ejecutando en el host de Hola Hola escritura bytes/s.

![Rendimiento cuando se ejecuta E/S en volúmenes en capas](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

Si observa hello en capas almacenamiento principal consumido, que ha pasado a, mientras que el uso de hello principal anclado localmente permanece sin cambios que no haya ninguna escritura sirve volúmenes toohello anclado localmente en el dispositivo de Hola.

![Uso de la capacidad principal cuando se ejecuta E/S en volúmenes en capas](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

Si está ejecutando la actualización 3 o posterior, puede desglosar utilización de capacidad de almacenamiento principal de Hola por un volumen individual, todos los volúmenes, todos los volúmenes en capas y todos los volúmenes anclados localmente tal y como se muestra a continuación. Dividir por todos los localmente volúmenes anclados le permitirá tooquickly determinar la cantidad de capa de hello local se ha consumido.

![Uso de la capacidad principal de todos los volúmenes en capas](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![Utilización de la capacidad principal de todos los volúmenes anclados localmente](./media/storsimple-8000-monitor-device/monitor-usage4.png)

Además puede haga clic en cada uno de los volúmenes de hello en lista de Hola y ver uso correspondiente Hola.

![Utilización de la capacidad principal de todos los volúmenes anclados localmente](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>Uso de almacenamiento en la nube
Estos gráficos muestran la cantidad de Hola de almacenamiento en nube utiliza. Estos datos están desduplicados y comprimidos. Esta cantidad incluye instantáneas en la nube que podrían contener datos que no se reflejan en ningún volumen principal y que se mantienen con fines de retención necesaria o heredada. Puede comparar Hola principal y el consumo de almacenamiento de en la nube cifras tooget clasificar una idea Hola de reducción de datos, aunque el número de hello no serán exacto.

Hello gráficos siguientes muestran utilización del almacenamiento de nube Hola de un dispositivo de StorSimple cuando se tomó una instantánea en la nube.

* instantánea en la nube Hola iniciado en aproximadamente 11:50 a.m. en ese dispositivo y puede ver que antes de la instantánea en la nube hello, se ha producido ningún almacenamiento en nube utiliza. 
* Una vez instantánea en la nube Hola completado, utilización del almacenamiento de nube Hola captura backup 0,89 GB. 
* Durante la instantánea en la nube hello en curso, hay también un pico correspondiente en hello E/S de dispositivo toocloud.

    ![Uso del almacenamiento en la nube antes de la instantánea de nube](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![Uso del almacenamiento en la nube después de la instantánea de nube](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![E/S de dispositivo toocloud durante una instantánea en la nube](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>Uso del almacenamiento local
Estos gráficos muestran el uso total de hello de dispositivo de hello, que será mayor que el uso de almacenamiento principal porque incluye capa lineal de hello SSD. Este nivel contiene una cantidad de datos que también existe en hello otras capas del dispositivo. capacidad de Hello en la capa de hello SSD lineal se recorre para que cuando llegan nuevos datos, los datos antiguos de hello están capa HDD toohello movida (en ese momento se está desduplicado y comprimido) y posteriormente toohello en la nube.

Con el tiempo, almacenamiento principal local y usa almacenamiento usado aumentará muy probablemente juntos hasta que los datos de hello comienzan toobe niveles toohello en la nube. En ese momento, almacenamiento local de hello usa probablemente empezará tooplateau, pero el almacenamiento principal de hello usado aumenta a medida que se escriben los datos más.

Hello gráficos siguientes muestran almacenamiento principal de hello usado para un dispositivo de StorSimple cuando se tomó una instantánea en la nube. instantánea en la nube Hola se inició a las 11:50 a.m. y almacenamiento local de hello inicia disminuyendo en ese momento. almacenamiento local de Hello usa ha fallado desde GB 1.445 too1.09 GB. Esto indica que probablemente hello datos sin comprimir en la capa de SSD lineal Hola se desduplicados, comprimidos y movidos capa HDD de Hola. Tenga en cuenta que si el dispositivo de hello ya tiene una gran cantidad de datos de hello SSD y niveles de unidad de disco duro, puede que no vea esta reducción. En este ejemplo, el dispositivo de hello tiene una pequeña cantidad de datos.

![Uso del almacenamiento local después de la instantánea de nube](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>Rendimiento
**Rendimiento** pistas métricas relacionadas con el número de toohello de lectura y escribir operaciones entre cualquier iSCSI Hola interfaces de iniciador en servidor de host de Hola y dispositivos de Hola o dispositivo de Hola y nube Hola. Este rendimiento se puede medir para un volumen específico, un contenedor de volúmenes específico o todos los contenedores de volúmenes. Rendimiento también incluye el uso de CPU y el rendimiento de red para hello diversas interfaces de red en el dispositivo.

### <a name="io-performance-for-initiator-toodevice"></a>Rendimiento de E/S de iniciador toodevice
gráfico de Hello siguiente muestra hello E/S de dispositivo de tooyour de iniciador de Hola para todos los volúmenes de Hola para un dispositivo de producción. las métricas de Hello trazadas son leer y escriben bytes por segundo. También se puede representar la E/S de lectura, escritura y pendiente, o las latencias de lectura y escritura.

![Rendimiento de E/S de iniciador toodevice](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>Rendimiento de E/S de dispositivo toocloud
Para hello mismo dispositivo, las operaciones de E/S de Hola se trazan para los datos de hello de dispositivo de la nube toohello Hola de Hola a todos los contenedores de volúmenes. En este dispositivo, Hola datos solo en nivel lineal de Hola y nada ha derramado toohello en la nube. No hay ninguna operación de lectura y escritura que se producen desde dispositivo toohello la nube. Por lo tanto, picos de hello en el gráfico de hello están en un intervalo de 5 minutos que corresponde a la que se comprueba latido Hola entre dispositivos de Hola y el servicio de Hola de frecuencia de toohello.

Para hello se tomó mismo dispositivo, una instantánea en la nube para datos de volumen inicial a las 11:50 a.m.. Esto producía datos fluyen desde el dispositivo de la nube toohello Hola. Escrituras se sirven toohello en la nube durante este proceso. gráfico de E/S de Hello muestra un pico en el tiempo Hola Bytes de escritura/s de toohello correspondiente cuando se tomó la instantánea de Hola.

![E/S de dispositivo toocloud durante una instantánea en la nube](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>Rendimiento de la red para las interfaces de red del dispositivo
**Rendimiento de la red** cantidad de toohello relacionadas de las métricas de pistas de datos se transfiere de hello interfaces de iniciador iSCSI en el servidor de host de Hola y el dispositivo de Hola y entre dispositivos de Hola y de nube de Hola. Puede supervisar estas métricas para cada una de las interfaces de red de iSCSI de hello en el dispositivo.

Hola siguientes gráficos muestran el rendimiento de red de Hola para hello Data 0, 1 1 red GbE en el dispositivo, lo cual era ambos nube habilitada (predeterminado) y habilitada para iSCSI. En este dispositivo en 14 de junio aproximadamente 9 p.m., los datos se en niveles en hello en la nube (no hay ninguna nube que se realicen las instantáneas en que tiempo qué puntos tootiering que se va a Hola datos toomove del mecanismo de hello en nube de Hola) que dio como resultado E/S servirlo toohello en la nube. No hay un pico correspondiente en el gráfico de rendimiento de red de Hola para hello mismo tiempo y la mayoría del tráfico de red de hello es toohello saliente en la nube.

![Rendimiento de la red para Data 0](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

Si miramos gráfico de rendimiento de interfaz de hello Data 1, interfaz que solo estaba habilitada para iSCSI de la red de otro 1 GbE, no hubo prácticamente ningún tráfico de red durante este proceso.

![Rendimiento de la red para Data 1](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>Uso de CPU para el dispositivo
**El uso de CPU** pistas métricas relacionadas con la CPU de toohello utilizado en el dispositivo. Hello siguiente gráfico muestra estadísticas de uso de CPU de Hola para un dispositivo en producción.

![Uso de CPU para el dispositivo](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar el panel del dispositivo de servicio de administrador de dispositivos de StorSimple de hello](storsimple-device-dashboard.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-manager-service-administration.md).


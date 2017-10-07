---
title: aaaMonitor el dispositivo StorSimple | Documentos de Microsoft
description: "Describe cómo toouse Hola toomonitor E/S rendimiento del servicio StorSimple Manager, utilización de la capacidad, rendimiento de la red y el rendimiento del dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>Usar hello StorSimple Manager servicio toomonitor el dispositivo de StorSimple
## <a name="overview"></a>Información general
Puede usar dispositivos específicos de hello StorSimple Manager servicio toomonitor dentro de la solución StorSimple. Puede crear gráficos personalizados basados en el rendimiento de E/S, la utilización de la capacidad, la capacidad de proceso de la red y las métricas de rendimiento del dispositivo. 

Hola de tooview información para un dispositivo específico, Hola portal de Azure clásico, el servicio StorSimple Manager seleccione Hola de supervisión. Haga clic en hello **Monitor** ficha y, a continuación, seleccionar en lista de Hola de dispositivos. Hola **Monitor** página contiene Hola siguiente información.

## <a name="io-performance"></a>Rendimiento de E/S
**Rendimiento de E/S** pistas métricas relacionadas con el número de toohello de lectura y escribir operaciones entre cualquier iSCSI Hola interfaces de iniciador en servidor de host de Hola y dispositivos de Hola o dispositivo de Hola y nube Hola. Este rendimiento se puede medir para un volumen específico, un contenedor de volúmenes específico o todos los contenedores de volúmenes.

gráfico de Hello siguiente muestra hello E/S de dispositivo de tooyour de iniciador de Hola para todos los volúmenes de Hola para un dispositivo de producción. las métricas de Hello trazadas se leen y escriben bytes por segundo, leen y escribir las operaciones de E/S por segundo y leerán y escribir las latencias.

![Rendimiento de E/S de iniciador toodevice](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Para hello mismo dispositivo, las operaciones de E/S de Hola se trazan para los datos de hello de dispositivo de la nube toohello Hola de Hola a todos los contenedores de volúmenes. En este dispositivo, Hola datos solo en nivel lineal de Hola y nada ha derramado toohello en la nube. No hay ninguna operación de lectura y escritura que se producen desde dispositivo toohello la nube. Por lo tanto, picos de hello en el gráfico de hello están en un intervalo de 5 minutos que corresponde a la que se comprueba latido Hola entre dispositivos de Hola y el servicio de Hola de frecuencia de toohello. 

![Rendimiento de E/S de dispositivo toocloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Para hello se tomó mismo dispositivo, una instantánea en la nube para datos de volumen a partir de 2:00 pm. Esto producía datos fluyen desde el dispositivo de la nube toohello Hola. Lecturas y escrituras se sirven toohello en la nube durante este proceso. Hello E/S gráfico muestra un pico en hello diversas métricas correspondiente tiempo toohello cuando se tomó la instantánea de Hola. 

![Rendimiento de E/S de dispositivo toocloud después de la instantánea en la nube](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Uso de la capacidad
**Utilización de la capacidad** cantidad de toohello relacionadas de las métricas de pistas de espacio de almacenamiento de datos que se utiliza para volúmenes de hello, contenedores de volúmenes o el dispositivo. Puede crear informes basados en la utilización de la capacidad de Hola de su almacenamiento principal, el almacenamiento en la nube o el almacenamiento del dispositivo. La utilización de la capacidad se puede medir para un volumen específico, un contenedor de volúmenes específico o todos los contenedores de volúmenes.

Hola principal, la nube y la capacidad de almacenamiento del dispositivo se pueden describir como sigue:

### <a name="primary-storage-capacity-utilization"></a>Uso de la capacidad del almacenamiento principal
Estos gráficos muestran la cantidad de Hola de los datos escritos tooStorSimple volúmenes antes de hello datos desduplicados y comprimidos. Puede ver el uso del almacenamiento principal de Hola por todos los volúmenes o un único volumen.

Al ver gráficos de utilización de capacidad de volumen de hello almacenamiento principal para todos los volúmenes frente a cada uno de los volúmenes individuales de Hola y suma los datos principal de hello en ambos de estos casos, puede haber una discrepancia entre dos números de Hola. Hola todos los datos principales en todos los volúmenes no pueden coincidir toohello la suma total de datos principal de saludo de volúmenes individuales Hola. Esto puede deberse tooone de siguientes hello:

* **Datos de instantáneas incluidos para todos los volúmenes**: Se produce este comportamiento solo si está ejecutando la versión anterior a Update 3. datos principales de Hola que se muestra para todos los volúmenes de hello están la suma de Hola de Hola de datos principal para cada volumen y los datos de instantánea de Hola. se muestra para un volumen determinado de datos principal de Hello corresponde cantidad de hello tooonly de datos que se asignan en el volumen de hello (y no incluyen datos de instantánea de volumen correspondiente de hello).
  
    Esto también puede explicarse por hello siguiente ecuación:
  
    *Datos primarios (todos los volúmenes) = Suma de (datos principales (volumen i) + tamaño de los datos de instantánea (volumen i))*
  
    *WHERE, datos principal (volumen i) = tamaño de datos principal asignados toovolume*
  
    Si se eliminan las instantáneas de Hola a través del servicio hello, eliminación de Hola se hace de forma asincrónica en segundo plano de Hola. Puede tardar algún tiempo Hola volumen toobe de tamaño de datos actualizado después de la eliminación de instantánea de Hola. 
  
    Si ejecuta Update 3 o posterior, datos de instantánea de hello no se incluyen en los datos de volumen de saludo. Y uso principal de Hola se calcula como sigue:
  
    *Datos primarios (todos los volúmenes) = Suma de (datos principales (volumen i)
  
    *WHERE, datos principal (volumen i) = tamaño de datos principal asignados toovolume*
* **Volúmenes con la supervisión deshabilitado incluidos en todos los volúmenes**: si tiene volúmenes en el dispositivo para el que la supervisión se ha desactivado, Hola datos de supervisión de estos volúmenes individuales no estará disponible en los gráficos de Hola. Sin embargo, los datos de Hola para todos los volúmenes en el gráfico de hello incluyen volúmenes de hello para el que la supervisión se ha desactivado. 
* **Eliminar volúmenes con copias de seguridad asociadas en vivo incluidos para todos los volúmenes**: si se eliminan los volúmenes que contienen datos de instantánea pero instantáneas Hola asociado todavía existen, es posible que vea un error de coincidencia.
* **Se incluyen los volúmenes eliminados de todos los volúmenes**: es posible que en algunos casos existan volúmenes anteriores aunque se eliminasen. no se ve el efecto de Hola de eliminación y dispositivo Hola puede mostrar menor capacidad disponible. Debe toocontact Microsoft Support tooremove estos volúmenes.

Hello gráficos siguientes muestran utilización de capacidad de almacenamiento principal de Hola de un dispositivo de StorSimple antes y después de que se tomó una instantánea en la nube. Puesto que éste es simplemente los datos de volumen, una instantánea en la nube no debería cambiar almacenamiento principal de Hola. Como puede ver, el gráfico de hello no muestra ninguna diferencia en el uso de la capacidad principal de hello como resultado de tomar una instantánea de nube. instantánea en la nube Hola iniciado a aproximadamente 2:00 p.m. en dicho dispositivo.

![Uso de la capacidad principal antes de instantánea en la nube](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Uso de la capacidad principal después de la instantánea en la nube](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Si está ejecutando Update 2 o versiones posteriores, puede desglosar utilización de capacidad de almacenamiento principal de Hola por un volumen individual, todos los volúmenes, todos los volúmenes en capas y todos los volúmenes anclados localmente tal y como se muestra a continuación. Dividir por todos los localmente volúmenes anclados le permitirá tooquickly determinar la cantidad de capa de hello local se ha consumido.

![Utilización de la capacidad principal de todos los volúmenes anclados localmente](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Uso de la capacidad de almacenamiento en la nube
Estos gráficos muestran la cantidad de Hola de almacenamiento en nube utiliza. Estos datos están desduplicados y comprimidos. Esta cantidad incluye instantáneas en la nube que podrían contener datos que no se reflejan en ningún volumen principal y que se mantienen con fines de retención necesaria o heredada. Puede comparar Hola principal y el consumo de almacenamiento de en la nube cifras tooget clasificar una idea Hola de reducción de datos, aunque el número de hello no serán exacto. Hello gráficos siguientes muestran utilización de capacidad de almacenamiento de hello en la nube de un dispositivo de StorSimple antes y después de que se tomó una instantánea en la nube. Hello instantánea en la nube se inició a aproximadamente 2:00 p.m. en ese dispositivo y se puede ver la utilización de la capacidad de hello en la nube captura en hello mismo tiempo, aumentar desde MB 5,73 too4.04 GB.

![Uso de la capacidad en la nube antes de la instantánea en la nube](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Uso de la capacidad en la nube después de la instantánea en la nube](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Uso de la capacidad de almacenamiento del dispositivo
Estos gráficos muestran el uso total de hello de dispositivo de hello, que será mayor que el uso de almacenamiento principal porque incluye capa lineal de hello SSD. Este nivel contiene una cantidad de datos que también existe en hello otras capas del dispositivo. capacidad de Hello en la capa de hello SSD lineal se recorre para que cuando llegan nuevos datos, los datos antiguos de hello están capa HDD toohello movida (en ese momento se está desduplicado y comprimido) y posteriormente toohello en la nube.

Con el tiempo, utilización de la capacidad principal y la utilización de la capacidad de dispositivo aumentará muy probablemente juntos hasta que los datos de hello comienzan toobe niveles toohello en la nube. En ese momento, utilización de la capacidad de hello dispositivo probablemente empezará tooplateau, pero utilización de la capacidad principal de hello aumenta a medida que se escriben más datos.

Hello gráficos siguientes muestran utilización de capacidad de almacenamiento principal de Hola de un dispositivo de StorSimple antes y después de que se tomó una instantánea en la nube. instantánea en la nube Hola se inició a las 2:00 p.m. y utilización de la capacidad de hello dispositivo inicia disminuyendo en ese momento. utilización de la capacidad de almacenamiento de Hello dispositivo ha empeorado desde GB 11.58 too7.48 GB. Esto indica que probablemente hello datos sin comprimir en la capa de SSD lineal Hola se desduplicados, comprimidos y movidos capa HDD de Hola. Tenga en cuenta que si el dispositivo de hello ya tiene una gran cantidad de datos de hello SSD y niveles de unidad de disco duro, puede que no vea esta reducción. En este ejemplo, el dispositivo de hello tiene una pequeña cantidad de datos.

![Uso de la capacidad del dispositivo antes de la instantánea en la nube](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Uso de la capacidad del dispositivo después de la instantánea en la nube](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Capacidad de proceso de la red
**Rendimiento de la red** cantidad de toohello relacionadas de las métricas de pistas de datos se transfiere de hello interfaces de iniciador iSCSI en el servidor de host de Hola y el dispositivo de Hola y entre dispositivos de Hola y de nube de Hola. Puede supervisar estas métricas para cada una de las interfaces de red de iSCSI de hello en el dispositivo.

Hola siguientes gráficos muestran el rendimiento de red de hello hello Data 0 y 4 de datos, las interfaces de red de 1 GbE en el dispositivo. En este caso, Data 0 estaba habilitada para la nube mientras que Data 4 estaba habilitada para iSCSI. Puede ver ambos Hola entrantes y Hola el tráfico saliente para el dispositivo StorSimple. línea plana de Hello en gráfico de Hola a partir de 3:24 pm es poseer toohello hechos se recopilar datos solo cada 5 minutos y debe omitirse. 

![Rendimiento de la red para Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Rendimiento de la red para Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Rendimiento del dispositivo
**El rendimiento del dispositivo** pistas métricas relacionadas con toohello rendimiento del dispositivo. Hello siguiente gráfico muestra estadísticas de uso de CPU de Hola para un dispositivo en producción.

![Uso de CPU para el dispositivo](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar el panel de dispositivo de servicio de StorSimple Manager de hello](storsimple-device-dashboard.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).


---
title: dispositivo de la serie StorSimple 8000 aaaUse resumen | Documentos de Microsoft
description: "Describe el dispositivo del servicio de administrador de dispositivos de StorSimple de hello resumen y cómo toouse se tooview las métricas de almacenamiento y los iniciadores y buscar Hola número de serie y IQN."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>Usar dispositivos de hello resumen en el servicio de administrador de dispositivos de StorSimple

## <a name="overview"></a>Información general
hoja de resumen de dispositivo de StorSimple de Hello le ofrece una visión general de la información de un dispositivo de StorSimple específico, en cambio toohello servicio hoja de resumen, que proporciona información sobre todos los dispositivos de Hola que se incluyen en la solución de StorSimple de Microsoft Azure.

hoja de resumen de dispositivo de Hello proporciona una vista resumida de un dispositivo de la serie 8000 de StorSimple que está registrado con un determinado StorSimple Administrador de dispositivos, resaltar los problemas de dispositivos que necesitan la atención del administrador del sistema. Este tutorial presenta la hoja de resumen de dispositivo de hello, explica la función y el contenido de Hola y describe las tareas de Hola que puede realizar desde esta hoja.

hoja de resumen de dispositivo de Hello muestra hello siguiente información:

![Hoja de resumen del dispositivo](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>Barra de comandos de administración

En la hoja de dispositivo de StorSimple de hello, verá opciones de Hola para administrar el dispositivo StorSimple. Verá los comandos de administración de Hola a lo largo de la parte superior de Hola de hoja de Hola y en el lado izquierdo de Hola. Use estos recursos compartidos de tooadd de opciones o volúmenes, o actualizar o conmutar por error el dispositivo.

![Barra de comandos de administración](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>Essentials

área de essentials Hola captura una parte de las propiedades importantes de hello como, estado de hello, modelo, IQN de destino y versión del software de Hola. 

![Información esencial de dispositivos](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>Supervisión

* Hola **alertas** mosaico proporciona una instantánea de todas las alertas activas de hello para el dispositivo, agrupado por gravedad.

    ![Icono Alertas](./media/storsimple-8000-device-dashboard/device-summary4.png)

    Haga clic en Hola mosaico tooopen Hola **alertas** hoja y, a continuación, haga clic en un usuario individual alerta tooview más detalles acerca de ella, las incluidas acciones recomendadas. También puede desactivar alerta Hola si se ha resuelto el problema de Hola.

    ![Hacer clic en el icono Alertas](./media/storsimple-8000-device-dashboard/device-summary10.png)

* Hola **estado** icono proporciona información sobre el estado del componente de hardware de Hola para un dispositivo, incluidos el estado del dispositivo de Hola. estado del dispositivo Hola puede ser sin conexión, en línea, desactivado o listo tooset up.

    ![Icono Estado y mantenimiento](./media/storsimple-8000-device-dashboard/device-summary5.png)

* Hola **volúmenes** mosaico proporciona un resumen del número de Hola de volúmenes en el dispositivo agrupados por estado.

    ![Icono Volúmenes](./media/storsimple-8000-device-dashboard/device-summary6.png)

    Haga clic en Hola mosaico tooopen Hola **volúmenes** lista hoja y, a continuación, haga clic en un volumen individual tooview o modificar sus propiedades.
    
    ![Hacer clic en el icono Volúmenes](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    Para obtener más información, vea cómo demasiado[administrar volúmenes](storsimple-8000-manage-volumes-u2.md).

* Hola **uso** gráfico, puede ver el almacenamiento principal de hello usado por el dispositivo y el almacenamiento en nube Hola consumen durante Hola últimos 7 días, predeterminado Hola período de tiempo.

     ![Icono de Uso](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     toochoose una escala de tiempo diferente, utilice hello **editar** opción en la esquina superior derecha de hello del gráfico de Hola.

     ![Editar gráfico de uso](./media/storsimple-8000-device-dashboard/device-summary12.png)

     En este gráfico, puede ver las métricas de almacenamiento principal total (cantidad de Hola de los datos escritos por dispositivo de tooyour de hosts) de Hola y Hola total consumido por el dispositivo durante un período de tiempo de almacenamiento en nube.
  
     En este contexto, *almacenamiento principal* hace referencia toohello cantidad total de los datos escritos por el host de Hola y puede dividirse por tipo de volumen: *principal en niveles de almacenamiento* incluye tanto almacenadas localmente los datos y los datos en la nube toohello en capas. El *almacenamiento principal anclado localmente* incluye solo los datos almacenados localmente. *Almacenamiento en nube*, en Hola otra parte, es una medida de la cantidad total de Hola de los datos almacenados en la nube de Hola. Este almacenamiento incluye las copias de seguridad y los datos en niveles. datos de Hello almacenados en la nube de hello es desduplicados y comprimidos, mientras que el almacenamiento principal indica la cantidad de Hola de almacenamiento usado antes de hello datos desduplicados y comprimidos. (Puede comparar estos tooget de dos números una idea del tipo de compresión de hello). Ambos principal y almacenamiento, Hola importes se basan en hello seguimiento frecuencia que configures en la nube. Por ejemplo, si elige una frecuencia de una semana, Hola gráfico muestra datos para cada día en hello semana anterior.

     cantidad de hello toosee de almacenamiento en nube consumida durante el tiempo, seleccione hello **almacenamiento de nube usa** opción. toosee Hola total de almacenamiento que se ha escrito por host hello, seleccione hello **principal en niveles de almacenamiento usa** y **LOCALMENTE ANCLADO almacenamiento principal CONSUMIDO** opciones. 
     Para obtener más información, consulte [uso Hola toomonitor de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-monitor-device.md).


* Hola **capacidad** mosaico muestra hello almacenamiento principal aprovisionado y permanece en Hola dispositivo toohello relativa almacenamiento total disponible para Hola igual. **Aprovisionar** hace referencia toohello cantidad de almacenamiento que está preparado y asignado para su uso, **restante** hace referencia toohello restante capacidad que se puede aprovisionar a través de este dispositivo. 

    ![Icono de Uso](./media/storsimple-8000-device-dashboard/device-summary8.png)

    Haga clic en este tooview icono cómo se aprovisiona la capacidad de Hola a través de volúmenes anclados localmente y en niveles. Hola **niveles restantes** capacidad es Hola capacidad disponible que se puede aprovisionar incluidos en la nube, mientras hello **restantes Local** es capacidad de hello restante en discos de hello adjunta toothis dispositivo.

    ![Hacer clic en el gráfico de uso](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>Pasos siguientes
* Obtener más información sobre hello [hoja de resumen de servicio de StorSimple](storsimple-8000-service-dashboard.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).


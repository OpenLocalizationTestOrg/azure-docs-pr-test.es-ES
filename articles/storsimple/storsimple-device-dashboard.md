---
title: panel de dispositivos de StorSimple Manager aaaUse Hola | Documentos de Microsoft
description: "Describe el panel del dispositivo del servicio StorSimple Manager hello y cómo toouse se tooview las métricas de almacenamiento y los iniciadores y buscar Hola número de serie y IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>Usar el panel de dispositivo de hello en el servicio StorSimple Manager  

## <a name="overview"></a>Información general
panel de dispositivo de StorSimple Manager Hola proporciona una información general de un dispositivo de StorSimple específico, en cambio toohello service panel, que proporciona información acerca de todos los dispositivos de hello incluidos en la solución de StorSimple de Microsoft Azure.

![Página de Panel del dispositivo](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

panel de Hello contiene Hola siguiente información:

* **Área del gráfico** : puede ver las métricas de almacenamiento relevantes de hello en hello gráfico área Hola parte superior del panel de Hola. En este gráfico, puede ver las métricas de almacenamiento principal total (cantidad de Hola de los datos escritos por dispositivo de tooyour de hosts) de Hola y Hola total consumido por el dispositivo durante un período de tiempo de almacenamiento en nube.
  
     En este contexto, *almacenamiento principal* hace referencia toohello cantidad total de los datos escritos por el host de Hola y puede dividirse por tipo de volumen: *principal en niveles de almacenamiento* incluye tanto almacenadas localmente los datos y los datos en la nube toohello en niveles; *principal anclado localmente almacenamiento* incluye solo los datos almacenados localmente. *Almacenamiento en nube*, en Hola otra parte, es una medida de la cantidad total de Hola de los datos almacenados en la nube de Hola. Esto incluye las copias de seguridad y los datos en niveles. Tenga en cuenta que los datos almacenados en la nube de hello están desduplicados y comprimidos, mientras que el almacenamiento principal indica la cantidad de Hola de almacenamiento usado antes de hello datos desduplicados y comprimidos. (Puede comparar estos tooget de dos números una idea del tipo de compresión de hello). Ambos principal y almacenamiento, Hola importes se basará en hello seguimiento frecuencia que configures en la nube. Por ejemplo, si elige una frecuencia de una semana, gráfico de hello mostrará datos para cada día en hello semana anterior.
  
     Puede configurar el gráfico de hello como sigue:
  
  * cantidad de hello toosee de almacenamiento en nube consumida durante el tiempo, seleccione hello **almacenamiento de nube usa** opción. toosee Hola total de almacenamiento que se ha escrito por host hello, seleccione hello **principal en niveles de almacenamiento usa** y **LOCALMENTE ANCLADO almacenamiento principal CONSUMIDO** opciones. En la ilustración hello, ambas opciones están seleccionadas; por lo tanto, el gráfico de hello muestra las cantidades de almacenamiento principal y en la nube. Tenga en cuenta que cualquier almacenamiento principal utiliza anterior tooinstalling Update 2 se representa mediante hello **principal en niveles de almacenamiento usa** línea.
  * Utilice Hola menú desplegable situado en la esquina superior derecha de Hola de hello gráfico toospecify un período de tiempo de 1 semana, 1 mes, 3 meses o 1 año. Tenga en cuenta que Hola gráfico de nivel superior se actualiza solo una vez al día y, por tanto, reflejará Hola totales del día anterior.
    
    Para obtener más información, consulte [uso Hola toomonitor de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-monitor-device.md).
* **Información general del uso** : Hola **información general del uso** área, puede ver el importe de Hola de almacenamiento aprovisionado y la capacidad de almacenamiento máximo de hello para el dispositivo utilizado por cantidad de Hola de almacenamiento principal. Al comparar estos cantidad máxima de uso números toohello de almacenamiento que está disponible, puede ver de un vistazo si necesita almacenamiento adicional de tooobtain. Tenga en cuenta que esta información general se actualiza cada 15 minutos y, debido a la diferencia de hello en la frecuencia de actualización, puede mostrar un número diferente a los que se muestran en hello área del gráfico anterior, que se actualiza diariamente. Para obtener más información, consulte [uso Hola toomonitor de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-monitor-device.md).
* **Alertas** : hello **alertas** área contiene un resumen de alertas de hello para el dispositivo. Las alertas se agrupan por gravedad y se proporciona un recuento del número de Hola de alertas en cada nivel de gravedad. Al hacer clic en la alerta de hello gravedad abre una vista concreta de hello alertas pestaña tooshow que solo Hola alertas de ese nivel de gravedad para este dispositivo.
* **Trabajos** : hello **trabajos** muestra área Hola resultado de la actividad de trabajo reciente. Puede garantizar que Hola sistema funciona según lo esperado, o puede notificarle que necesita acción correctiva tootake. toosee más información acerca de los trabajos completados recientemente, haga clic en **trabajos correctos en hello últimas 24 horas**.
* Hola **vista rápida** área Hola derecha del panel de hello proporciona información útil, como el modelo del dispositivo, número de serie, estado, descripción y número de volúmenes.

También puede configurar la conmutación por error y ver los iniciadores en el panel del dispositivo Hola.

Hola tareas comunes que se pueden realizar en esta página son:

* Ver iniciadores conectados
* Buscar el número de serie del dispositivo de Hola
* Buscar el IQN de destino del dispositivo Hola

## <a name="view-connected-initiators"></a>Ver iniciadores conectados
Puede ver los iniciadores de iSCSI de Hola que están conectados tooyour dispositivo haciendo clic en hello **ver iniciadores conectados** vínculo proporcionado en hello **vista rápida** área del panel del dispositivo. Esta página proporciona una lista tabular de los iniciadores de Hola que se han conectado correctamente el dispositivo de tooyour. Para cada iniciador, podrá ver:

* Hola iSCSI nombre completo (IQN) de hello conectado el iniciador.
* nombre de Hello del registro de control de acceso de hello (ACR) que permite este iniciador conectado.
* dirección IP de Hola de hello conectado iniciador.
* Hello interfaces de red que iniciador hello es tooon conectado el dispositivo de almacenamiento. Estas pueden variar de DATA 0 tooDATA 5.
* Todos los volúmenes de Hola Hola iniciador conectado se permite tooaccess según la configuración actual de ACR toohello.

Si ve iniciadores inesperados en esta lista o no se ve Hola que espera, revise la configuración de ACR. Un máximo de 512 iniciadores puede conectar el dispositivo de tooyour.

## <a name="find-hello-device-serial-number"></a>Buscar el número de serie del dispositivo de Hola
Puede que tenga el número de serie del dispositivo de hello al configurar E/S de múltiples rutas (MPIO) de Microsoft en el dispositivo de Hola. Realizar Hola siguiendo el número de serie del dispositivo de pasos toofind Hola.

#### <a name="toofind-hello-device-serial-number"></a>número de serie del dispositivo de toofind Hola
1. Navegue demasiado**dispositivos** > **panel**.
2. En panel derecho de Hola de panel de hello, busque hello **vista rápida** área.
3. Desplácese hacia abajo y busque el número de serie de Hola.

## <a name="find-hello-device-target-iqn"></a>Buscar el IQN de destino del dispositivo Hola
Puede que necesite IQN de destino del dispositivo hello cuando configure Hola protocolo de autenticación por desafío mutuo (CHAP) en el dispositivo StorSimple. Realizar Hola siguiendo los pasos IQN de destino de dispositivo de hello toofind.

### <a name="toofind-hello-device-target-iqn"></a>IQN de destino del dispositivo toofind Hola
1. Navegue demasiado**dispositivos** > **panel**.
2. En panel derecho de Hola de panel de hello, busque hello **vista rápida** área.
3. Desplácese hacia abajo y busque el IQN de destino de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información sobre hello [panel de servicio de StorSimple Manager](storsimple-service-dashboard.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).


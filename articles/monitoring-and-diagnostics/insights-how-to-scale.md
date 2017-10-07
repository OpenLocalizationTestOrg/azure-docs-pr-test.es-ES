---
title: "número de instancias de aaaScale manualmente o con el escalado automático con el Portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale los servicios de Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>Escalación del recuento de instancias de forma manual o automática
Hola [Portal de Azure](https://portal.azure.com/), puede establecer manualmente el número de instancias de Hola de su servicio, o puede establecer parámetros toohave ajusta automáticamente según la demanda. Esto es que normalmente se conoce tooas *escalar horizontalmente* o *escalar en*.

Antes de escalado basado en recuento de instancias, considere la posibilidad de que se ajuste de escala se ve afectado por **tarifa** recuento tooinstance de adición. Diferentes niveles de precios pueden tener un número diferente núcleos y la memoria y por lo que tendrán un mejor rendimiento para hello mismo número de instancias (que es *escalar verticalmente* o *reducir*). Este artículo trata específicamente sobre *Reducir horizontalmente* y *Escalar horizontalmente*.

Puede escalar en el portal de Hola y también puede usar hello [API de REST](https://msdn.microsoft.com/library/azure/dn931953.aspx) o [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust escalar de forma manual o automática.

> [!NOTE]
> Este artículo se describe cómo toocreate una configuración en el portal de hello en de escalado automático [http://portal.azure.com](http://portal.azure.com). Configuración de escalado automático creada en este portal no puede ser editado portal clásico de hello ([http://manage.windowsazure.com](http://manage.windowsazure.com)).
> 
> 

## <a name="scaling-manually"></a>Escalado manual
1. Hola [Portal de Azure](https://portal.azure.com/), haga clic en **examinar**, a continuación, desplácese recursos toohello desea tooscale, como un **plan de servicio de aplicaciones**.
2. Haga clic en **Configuración > Escalar horizontalmente (plan de App Service).**
3. En parte superior de Hola de hello **escala** hoja puede ver un historial de acciones de escalado automático del servicio de Hola.
   
    ![Hoja Escala](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > Solo aparecerán en este gráfico las acciones que se lleven a cabo mediante el escalado automático. Si ajustar manualmente el recuento de instancias de hello, cambio de hello no se reflejará en este gráfico.
   > 
   > 
4. Puede ajustar manualmente el número de hello **instancias** con el control deslizante.
5. Haga clic en hello **guardar** command y estará escalar toothat número de instancias de casi inmediatamente.

## <a name="scaling-based-on-a-pre-set-metric"></a>Escalado según una métrica preestablecida
Si desea que el número de Hola de instancias tooautomatically ajustar en función de una métrica, seleccione Hola métrica que desee en hello **escalar** lista desplegable. Por ejemplo, para un **plan de App Service** puede escalar por **Porcentaje de CPU**.

1. Cuando se selecciona una métrica obtendrá un control deslizante, o número de Hola de tooenter de cuadros de texto de instancias que desee tooscale entre:
   
    ![Hoja Escala con Porcentaje de la CPU](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    Escalado automático nunca tendrá el servicio por debajo o por encima de los límites de Hola que establezca, con independencia de su carga.
2. En segundo lugar, elija intervalo de destino de Hola de métrica de Hola. Por ejemplo, si ha elegido **porcentaje de CPU**, puede establecer un objetivo para hello promedio de CPU en todas las instancias de hello en el servicio. Una escalada ocurrirá cuando Hola promedio de CPU supera el máximo de Hola que defina, del mismo modo, se realizará una escala en cada vez que la CPU promedio Hola cae por debajo de hello mínimo.
3. Haga clic en hello **guardar** comando. Escalado automático comprobará cada pocos toomake de minutos que se encuentra en el intervalo de la instancia de Hola y de destino para la métrica. Cuando el servicio recibe tráfico adicional, obtendrá más instancias sin hacer nada.

## <a name="scale-based-on-other-metrics"></a>Escalación según otras métricas
Puede escalar en función de las métricas que no sea de valores preestablecidos de Hola que aparecen en hello **escalar** de lista desplegable y puede incluso tiene un conjunto complejo de escalado horizontal y escalar en las reglas.

### <a name="adding-or-changing-a-rule"></a>Incorporación o cambio de una regla
1. Elija hello **reglas de programación y rendimiento** en hello **escalar** desplegable: ![reglas de rendimiento](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. Si previamente ha escalado automático, en verá una vista de reglas precisas de Hola que tenía.
3. tooscale según Hola de métrica haga clic en otro **Agregar regla** fila. También puede hacer clic en uno de hello toochange de filas existentes de métrica de Hola que tenía anteriormente métrica toohello desea tooscale por.
   ![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)
4. Ahora debe tooselect la métrica que desee tooscale por. Cuando elija una métrica existe tooconsider un par de cosas:
   
   * Hola *recursos* procede métrica Hola. Normalmente, esto se puede Hola igual que los recursos de hello escalará. Sin embargo, si desea tooscale por profundidad de Hola de una cola de almacenamiento, recursos de hello es cola de Hola que desee tooscale por.
   * Hola *nombre de la métrica* propio.
   * Hola *tiempo agregación* de métrica de Hola. Así es cómo los datos de hello combinar sobre hello *duración*.
5. Después de elegir la métrica elija Hola umbral de métrica de hello y de operador Hola. Por ejemplo, podría decir **Mayor que** **80 %**.
6. A continuación, elija la acción de Hola que desea tootake. Hay un par de diferentes tipos de acciones:
   
   * Aumentar o disminuir en: Esto agregará o quitará hello **valor** número de instancias define
   * Aumentar o reducir el porcentaje: esta operación cambiará el recuento de instancias de Hola por porcentaje. Por ejemplo, podría poner 25 en hello **valor** campo, y si actualmente tiene 8 instancias, se agregaría 2.
   * Aumentar o disminuir demasiado: este modo, establecerá Hola instancia recuento toohello **valor** defina.
7. Por último, puede elegir de enfriamiento - cuánto tiempo debe esperar esta regla después de hello anterior escala acción tooscale nuevo.
8. Después de configurar la regla, haga clic en **Aceptar**.
9. Una vez haya configurado todas las reglas de Hola que desea, puede seguro hello toohit **guardar** comando.

### <a name="scaling-with-multiple-steps"></a>Escalación con varios pasos
ejemplos de Hello anteriores son bastante básicos. Sin embargo, si desea toobe más agresiva acerca de cómo escalar hacia arriba (o hacia abajo), puede incluso agregar escala varias reglas para hello misma métrica. Por ejemplo, puede definir dos reglas de escalado en el porcentaje de CPU:

1. Escalar horizontalmente por 1 instancia si el porcentaje de CPU es superior al 60 %
2. Escalar horizontalmente por 3 instancias si el porcentaje de CPU es superior al 85 %

![Varias reglas de escalado](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

Con esta regla adicional, si la carga excede del 85 % antes de una acción de escalado, obtendrá dos instancias adicionales en lugar de una.

## <a name="scale-based-on-a-schedule"></a>Escalación según una programación
De forma predeterminada, al crear una regla de escala se aplicará siempre una regla de escalado. Puede ver que, al hacer clic en el encabezado de perfil de hello:

![Perfil](./media/insights-how-to-scale/Insights_Profile.png)

Sin embargo, puede que desee toohave más agresiva si se escalan durante el día de hello, o una semana de hello, que de fin de semana de Hola. Incluso puede apagar el servicio completamente fuera de horas de trabajo.

1. toodo, en perfil de hello tiene, seleccione **periodicidad** en lugar de **siempre,** y elija Hola el tiempo que desea que Hola perfil tooapply.
2. Por ejemplo, toohave un perfil que se aplica durante la semana de hello, Hola **días** desactive la opción desplegable **el sábado** y **el domingo**.
3. un perfil que se aplica durante Hola Hola durante el día, establezca toohave **hora de inicio** toohello hora del día en que desea toostart en.
   
    ![Periodicidad predeterminada](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. Haga clic en **Aceptar**.
5. A continuación, deberá perfil de hello tooadd que desea tooapply en otras ocasiones. Haga clic en hello **Agregar perfil** fila.
    ![No laborable](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. Ponga un nombre a su nuevo segundo perfil; por ejemplo, podría llamarlo **No laborable**.
7. A continuación, seleccione **periodicidad** nuevo y elija el intervalo de recuento de instancia Hola desea durante este tiempo.
8. Como con hello perfil predeterminado, seleccione hello **días** desea este tooapply de perfil y se hello **hora de inicio** durante el día de Hola.
   
   > [!NOTE]
   > Escalado automático usa las reglas de ahorro de horario de verano de Hola para que sea **zona horaria** seleccione. Sin embargo, durante el horario de verano desplazamiento de UTC de hello mostrará el desplazamiento de zona horaria base hello, desplazamiento de hello UTC de ahorro de verano no.
   > 
   > 
9. Haga clic en **Aceptar**.
10. Ahora, deberá tooadd lo que las reglas desea tooapply durante el segundo perfil. Haga clic en **Agregar regla**, y, a continuación, podría crear Hola misma regla tiene durante el perfil predeterminado de Hola.
    
    ![Agregar regla toooff trabajo](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. Ser seguro toocreate tanto una regla de escalado horizontal y escalado en, o bien durante Hola recuento de instancias de perfil Hola se solo aumentar (o disminuir).
12. Finalmente, haga clic en **Guardar**.

## <a name="next-steps"></a>Pasos siguientes
* [Supervisar las métricas de servicio](insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.
* [Habilitar la supervisión y diagnóstico](insights-how-to-use-diagnostics.md) toocollect detallada las métricas de alta frecuencia en su servicio.
* [Reciba notificaciones de alerta](insights-receive-alert-notifications.md) cada vez que se produzcan eventos de operaciones o las métricas traspasen un umbral.
* [Supervisar el rendimiento de la aplicación](../application-insights/app-insights-azure-web-apps.md) si desea toounderstand exactamente cómo se está realizando el código en la nube de Hola.
* [Ver eventos y registros de actividad](insights-debugging-with-events.md) toolearn todo lo que se ha producido en el servicio.
* [Supervise la disponibilidad y la capacidad de respuesta de cualquier página web](../application-insights/app-insights-monitor-web-app-availability.md) con Application Insights, para poder averiguar si su página está inactiva.


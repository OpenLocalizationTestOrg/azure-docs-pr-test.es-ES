---
title: "aaaSet alertas de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Reciba notificaciones acerca de tiempos de respuesta lentos, excepciones y otros cambios de rendimiento o uso de la aplicación web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Definición de alertas en Application Insights
[Azure Application Insights] [ start] puede avisarle toochanges en las métricas de rendimiento o el uso de la aplicación web. 

Visión de la aplicación supervisa la aplicación activa en un [amplia variedad de plataformas] [ platforms] toohelp diagnosticar problemas de rendimiento y conocer los patrones de uso.

Hay tres tipos de alertas:

* **Alertas de métricas** le avisan cuando una métrica cruza un valor de umbral durante un período determinado: por ejemplo, tiempos de respuesta, recuentos de excepciones, uso de la CPU o vistas de página. 
* [**Pruebas Web** ] [ availability] saber si el sitio no está disponible en hello internet o responde lentamente. [Más información][availability].
* [**Diagnósticos proactivos** ](app-insights-proactive-diagnostics.md) se configuran automáticamente toonotify acerca de los patrones de rendimiento inusual.

Nos centraremos en las alertas de métricas en este artículo.

## <a name="set-a-metric-alert"></a>Establecimiento de una alerta de métrica
Hoja de reglas de alerta de hello abierto y, a continuación, use Hola agregan botón. 

![En la hoja de reglas de alerta de hello, elija Agregar alerta. Establecer la aplicación como Hola toomeasure de recursos, proporcione un nombre de alerta de Hola y elija una métrica.](./media/app-insights-alerts/01-set-metric.png)

* Configurar otras propiedades de recursos de hello antes de Hola. **Elija recurso hello "(componentes)"** si desea que las alertas de tooset las métricas de rendimiento o el uso.
* nombre de Hola que se asigne toohello alerta debe ser único en el grupo de recursos de hello (no solo la aplicación).
* Ser unidades de hello toonote cuidado en el que se le pide el valor del umbral de tooenter Hola.
* Si se activa la casilla de Hola "Propietarios de correo electrónico...", las alertas se envían por tooeveryone de correo electrónico que tenga el grupo de recursos de toothis de acceso. tooexpand este conjunto de usuarios, agréguelos toohello [grupo de recursos o suscripción](app-insights-resources-roles-access-control.md) (no Hola recursos).
* Si especifica "Correos electrónicos adicionales", las alertas se envían toothose individuos o grupos (si no ha activado el cuadro de "email propietarios..." hello). 
* Establecer un [webhook dirección](../monitoring-and-diagnostics/insights-webhooks-alerts.md) si ha configurado una aplicación web que responde tooalerts. Se llama cuando se activa la alerta de Hola y cuando se ha resuelto. (Pero tenga en cuenta que, en la actualidad, los parámetros de consulta no se pasan como propiedades de webhook).
* Puede deshabilitar o habilitar Hola alerta: consulte botones de hello en parte superior de Hola de hoja de Hola.

*No se ve botón alerta de hello agregar.* 

* ¿Está usando una cuenta de organización? Puede establecer alertas si tiene propietario o colaborador acceso toothis recurso de la aplicación. Eche un vistazo en la hoja de Control de acceso de Hola. [Más información sobre el control de acceso][roles].

> [!NOTE]
> En la hoja de alertas de hello, verá que ya hay un conjunto de alerta de: [diagnósticos proactivos](app-insights-proactive-failure-diagnostics.md). alerta automática de Hello supervisa un determinado porcentaje de errores de solicitud métrica. A menos que decida alerta automático de toodisable hello, no es necesario tooset su propio alerta de tasa de error de solicitud. 
> 
> 

## <a name="see-your-alerts"></a>Visualización de alertas
Recibirá un correo electrónico cuando un alerta cambia el estado entre inactivo y activo. 

estado actual de Hola de cada alerta se muestra en la hoja de hello las reglas de alerta.

Hay un resumen de la actividad reciente de las alertas de hello desplegable:

![Lista desplegable de alertas](./media/app-insights-alerts/010-alert-drop.png)

Hola el historial de cambios de estado es Hola registro de actividad:

![En la hoja de información general de hello, haga clic en configuración, los registros de auditoría](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Funcionamiento de las alertas
* Una alerta tiene tres estados: "Nunca activada", "Activada" y "Resuelta". Activado significa Hola condición especificada sea true, cuando estaba se evaluó por última vez.
* Se genera una notificación cuando una alerta cambia de estado. (Si la condición de alerta de hello ya era true cuando se creó la alerta de hello, podría no obtener una notificación hasta que sale false condición Hola.)
* Cada notificación genera un correo electrónico si se activa el cuadro de mensajes de correo electrónico de Hola o proporcionan direcciones de correo electrónico. También puede buscar en la lista desplegable de hello las notificaciones.
* Una alerta se evalúa cada vez que llega una métrica, pero no en caso contrario.
* evaluación de Hello agrega métrica Hola sobre Hola anterior período y a continuación, compara el estado nuevo de toohello umbral toodetermine Hola.
* período de Hola que elija especifica sobre el que se agregan las métricas de intervalo de saludo. No se ve afectada la frecuencia con hello alerta se evalúa: que depende de la frecuencia de Hola de llegada de métricas.
* Si no llega ningún dato para una métrica concreta durante algún tiempo, intervalo de hello tiene distintos efectos en la evaluación de alertas y en los gráficos de hello en el Explorador de métrica. En el Explorador de métrica, si no se ve ningún dato durante más tiempo que el intervalo de muestreo del gráfico de hello, gráfico de hello muestra un valor de 0. Pero una alerta basada en hello misma métrica no se vuelven a evaluar y Hola sigue siendo de estado de la alerta sin cambios. 
  
    Cuando los datos llegan finalmente, gráfico de hello salta valor distinto de cero de tooa atrás. alerta de Hello evalúa basados en datos de hello disponibles para el período de hello especificado. Si Hola nuevo punto de datos es Hola solo uno disponible en el período de hello, Hola agregado se basa solo en punto de datos.
* Una alerta puede parpadear con frecuencia entre los estados de alerta y correcto, incluso si se establece un período largo. Esto puede ocurrir si el valor de métrica de hello sitúa cerca umbral Hola. No hay ninguna inclinación de umbral de hello: Hola tooalert de transición se produce en hello mismo valor que toohealthy de transición de Hola.

## <a name="what-are-good-alerts-tooset"></a>¿Qué alertas buena tooset?
Depende de la aplicación. toostart con, es preferible no tooset demasiados métricas. Dedique algún tiempo examinando los gráficos de métricas mientras se ejecuta la aplicación, tooget una idea de cómo se comportará normalmente. Esta práctica ayuda a encontrar maneras tooimprove su rendimiento. A continuación, configurar tootell de alertas se cuando salen de las métricas de hello fuera de zona normal de Hola. 

Las alertas más populares son:

* Las [métricas del explorador][client], especialmente los **tiempos de carga de página del explorador**, son buenas para aplicaciones web. Si la página tiene muchos scripts, debe buscar **excepciones del explorador**. En orden tooget estas métricas y alertas, tiene tooset [supervisión de la página web][client].
* **Tiempo de respuesta de servidor** para servidor hello de aplicaciones web. Así como configurar las alertas, esté atento en esta métrica toosee si desproporcionadamente varía con velocidad de solicitudes alta: variación podría indicar que la aplicación se está quedando sin recursos. 
* **Excepciones de servidor** -toosee usarlas, tiene algunas toodo [el programa de instalación adicional](app-insights-asp-net-exceptions.md).

No olvide que [los diagnósticos de tasa de errores proactiva](app-insights-proactive-failure-diagnostics.md) automáticamente Hola frecuencia del monitor en el que la aplicación responde toorequests con códigos de error. 

## <a name="automation"></a>Automation
* [Usar PowerShell tooautomate configurar alertas](app-insights-powershell-alerts.md)
* [Use webhooks tooautomate responde tooalerts](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Otras referencias
* [Pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md)
* [Use PowerShell to set alerts in Application Insights (Uso de PowerShell para definir alertas en Application Insights)](app-insights-powershell-alerts.md)
* [Proactive diagnostics](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md


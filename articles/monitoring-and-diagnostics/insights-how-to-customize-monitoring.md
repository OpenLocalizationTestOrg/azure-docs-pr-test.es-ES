---
title: "aaaOverview de métricas en Microsoft Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo supervisar toocustomize gráficos en Azure."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Información general sobre las métricas en Microsoft Azure
Todos los servicios de Azure realizar un seguimiento de las métricas clave que le permiten el uso de los servicios, rendimiento, disponibilidad y estado de hello toomonitor. Puede ver estas métricas en hello portal de Azure, y también puede usar hello [API de REST](https://msdn.microsoft.com/library/azure/dn931930.aspx) o [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess Hola conjunto completo de métricas mediante programación.

Para algunos servicios, puede que necesite tooturn en diagnósticos en orden toosee todas las métricas. En otros casos, como máquinas virtuales, obtendrá un conjunto básico de las métricas, pero necesita tooenable Hola métricas de alta frecuencia de todo el conjunto. Vea [habilitar la supervisión y diagnóstico](insights-how-to-use-diagnostics.md) toolearn más.

## <a name="using-monitoring-charts"></a>Uso de gráficos de supervisión
Puede representar cualquiera de las métricas de hello usarlas durante cualquier período de tiempo que elija.

1. Hola [Portal de Azure](https://portal.azure.com/), haga clic en **examinar**, y, a continuación, un recurso está interesado en la supervisión.
2. Hola **supervisión** sección contiene las métricas más importantes de Hola para cada recurso de Azure. Por ejemplo, una aplicación web tiene **Solicitudes y errores** donde, como máquina virtual, tendría **Porcentaje de CPU** y **Lectura y escritura de disco**: ![modo Supervisión](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. Al hacer clic en cualquier gráfico mostrará que Hola **métrica** hoja. En la hoja de hello, además toohello gráfico, es una tabla que muestra las agregaciones de métricas de hello (por ejemplo, promedio, mínimo y máximo, de intervalo de tiempo de hello eligió). A continuación que es Hola reglas de alerta para el recurso de Hola.
    ![Cuadro de métricas](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. líneas de hello toocustomize que aparecen, haga clic en hello **editar** situado en el gráfico de hello, o bien, Hola **Editar gráfico** comando hoja de métricas de Hola.
5. En la hoja de hello Editar consulta puede hacer tres cosas:
   
   * Cambiar el intervalo de tiempo de Hola
   * Cambiar la apariencia de hello entre barras y líneas
   * Elegir otras métricas ![Editar consulta](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. Cambiar el intervalo de tiempo de hello es tan fácil como seleccionar un intervalo diferente (como **última hora**) y haga clic en **guardar** final Hola de hoja de Hola. También puede elegir **personalizado**, que le permite toochoose cualquier período de tiempo sobre Hola últimas 2 semanas. Por ejemplo, puede ver Hola todo dos semanas o, simplemente 1 hora de ayer. Escriba en tooenter de cuadro de texto hello otra hora.
    ![Intervalo de tiempo personalizado](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Debajo de intervalo de tiempo de hello, subir de canal elija cualquier número de tooshow de métricas en el gráfico de Hola.
8. Al hacer clic en Guardar, los cambios se guardarán para ese recurso concreto. Por ejemplo, si tiene dos máquinas virtuales y cambiar un gráfico en uno, no afectará Hola otro.

## <a name="creating-side-by-side-charts"></a>Creación de gráficos paralelos
Con la personalización eficaz de hello en el portal de hello puede agregar tantos gráficos como desee.

1. Hola **...**  menú situado en la parte superior de Hola de hoja de hello haga clic en **agregar iconos**:  
    ![Adición de menú](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. A continuación, se puede seleccionar un gráfico de hello **galería** en hello derecha de la pantalla: ![Galería](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Si no ve la métrica de Hola que desee, siempre puede agregar uno de hello preestablecido métricas, y **editar** Hola métrica del gráfico tooshow Hola que necesita.

## <a name="monitoring-usage-quotas"></a>Supervisión de las cuotas de uso
La mayoría de las métricas muestran tendencias a lo largo del tiempo, pero determinados datos, como las cuotas de uso, suponen información puntual con un umbral.

También puede ver las cuotas de uso en la hoja de Hola para los recursos que tienen cuotas:

![Uso](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Al igual que con las métricas, puede usar hello [API de REST](https://msdn.microsoft.com/library/azure/dn931963.aspx) o [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess Hola conjunto completo de las cuotas de uso mediante programación.

## <a name="next-steps"></a>Pasos siguientes
* [Reciba notificaciones de alerta](insights-receive-alert-notifications.md) cada vez que una métrica traspase un umbral.
* [Habilitar la supervisión y diagnóstico](insights-how-to-use-diagnostics.md) toocollect detallada las métricas de alta frecuencia en su servicio.
* [Escalar el número de instancias automáticamente](insights-how-to-scale.md) toomake que el servicio esté disponible y capacidad de respuesta.
* [Supervisar el rendimiento de la aplicación](../application-insights/app-insights-azure-web-apps.md) si desea toounderstand exactamente cómo se está realizando el código en la nube de Hola.
* Use [Application Insights para las aplicaciones de JavaScript y páginas web](../application-insights/app-insights-web-track-usage.md) tooget análisis de cliente acerca de los exploradores de Hola que visitar una página web.
* [Supervise la disponibilidad y la capacidad de respuesta de cualquier página web](../application-insights/app-insights-monitor-web-app-availability.md) con Application Insights, para poder averiguar si su página está inactiva.


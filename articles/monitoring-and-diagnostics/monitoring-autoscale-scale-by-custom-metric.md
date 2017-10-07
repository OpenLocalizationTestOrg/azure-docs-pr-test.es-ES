---
title: "aaaGet iniciada con escalado automático por métrica personalizada en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale el recurso por métrica personalizado en Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Introducción al escalado automático mediante métricas personalizadas en Azure
Este artículo se describe cómo tooscale el recurso por una métrica personalizada en el portal de Azure.

Azure Autoescala de Monitor aplica solo tooVirtual conjuntos de escala de máquina (VMSS), servicios en la nube, planes de servicio de aplicaciones y entornos del servicio de aplicación. 

# <a name="lets-get-started"></a>Introducción
En este artículo se presupone que tiene una aplicación web con Application Insights configurado. Si aún no la tiene, puede [configurar Application Insights para el sitio web ASP.NET][1].

- Abra [Azure Portal][2].
- Haga clic en el icono de Monitor de Azure en el panel de navegación izquierdo de Hola.
  ![Inicio de Azure Monitor][3]
- Haga clic en configuración tooview todos los recursos de Hola para que automáticamente la escala es aplicable, junto con su estado actual de escalado automático de escalado automático ![detectar Autoescala en el monitor de Azure][4]
- Abrir la hoja de 'Escalado automático' en el Monitor de Azure y seleccione un recurso que desee tooscale
> Nota: estos pasos Hola usan un plan de servicio de aplicación asociado a una aplicación web que tiene detalles de aplicaciones configurados.
- En la hoja de configuración de la escala de hello para el recurso de hello, tenga en cuenta que el recuento de instancias actual de hello es 1. Haga clic en "Enable autoscale" (Habilitar escalado automático).
  ![Configuración de escalado para la nueva aplicación web][5]
- Proporcione un nombre para la configuración de escala de Hola y Hola, haga clic en "Agregar una regla de". Observe las opciones de regla de escala de Hola que se abre como un panel de contexto en hello del lado derecho. De forma predeterminada, Establece la instancia de recuento en 1 si Hola CPU percetage del recurso de hello supera el 70% de hello opción tooscale. Origen de métricas de Hola de cambio en la parte superior de hello demasiado "Application Insights", seleccione Hola recursos de información de aplicación en lista desplegable de 'Resource' hello y métrica de hello, a continuación, seleccione personalizada basada en la que desea tooscale.
  ![Escalar por métrica personalizada][6]
- Paso de toohello similar anterior, agregar una regla de escala que se escale en y reduzca el recuento de escala de hello en 1 si la métrica personalizada hello está por debajo del umbral.
  ![Escala en función de la CPU][7]
- Establecer hello para la instancia de límites. Por ejemplo, si desea tooscale entre 2 y 5 instancias según las fluctuaciones de métrica personalizada hello, establezca 'mínimo"demasiado '2', 'máximo' demasiado '5' y 'default' demasiado '2'
> Nota: en caso de que hay un problema al leer las métricas de recursos de Hola y capacidad actual de hello está por debajo de la capacidad predeterminada de hello, a continuación, disponibilidad de hello tooensure del recurso de hello, escalado automático se espera el valor predeterminado de toohello. Si la capacidad actual de hello ya es mayor que la capacidad predeterminada, escalado automático no se ajusta en.
- Haga clic en "Guardar".

¡Enhorabuena! Es ahora correctamente una vez creado el tooauto de configuración de escala escalar la aplicación web en función de una métrica personalizada.

> Nota: hello mismos pasos son aplicable tooget a trabajar con un rol de servicio VMSS o en la nube.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png

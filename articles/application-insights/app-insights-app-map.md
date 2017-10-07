---
title: "aaaApplication mapa de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Una presentación visual de las dependencias de hello entre componentes de aplicación, con la etiqueta con los KPI y las alertas."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Mapa de aplicación en Application Insights
En [Azure Application Insights](app-insights-overview.md), asignación de aplicación no es un aspecto visual de las relaciones de dependencia de Hola de los componentes de aplicación. Cada componente muestra KPI como toohelp de carga, el rendimiento, errores y alertas, detectar cualquier componente que se produce un error o problema de rendimiento. Puede hacer clic en a través de cualquier componente toomore obtener diagnósticos, tales como eventos de Application Insights. Si su aplicación usa los servicios de Azure, también puede hacer clic a través de diagnósticos de tooAzure, como las recomendaciones del Asistente de la base de datos de SQL.

Al igual que otros gráficos, puede anclar un toohello de asignación de aplicación panel de Azure, donde es totalmente funcional. 

## <a name="open-hello-application-map"></a>Asignación de la aplicación hello abierto
Hola abrir mapa de hoja de información general de hello para la aplicación:

![abrir el mapa de aplicación](./media/app-insights-app-map/01.png)

![mapa de aplicación](./media/app-insights-app-map/02.png)

mapa de Hello muestra:

* Pruebas de disponibilidad
* Componente de cliente (que se supervisan con hello SDK de JavaScript)
* Componente del lado servidor
* Dependencias de los componentes de cliente y servidor de Hola

Puede expandir y contraer los grupos de vínculos de dependencia:

![contraer](./media/app-insights-app-map/03.png)

Si tiene un gran número de dependencias de un tipo (SQL, HTTP, etc.), aparecen agrupadas. 

![dependencias agrupadas](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>Detección de problemas
Cada nodo tiene indicadores de rendimiento pertinentes, como las velocidades de carga y rendimiento, error de Hola para ese componente. 

Los iconos de advertencia resaltan los posibles problemas. Una advertencia naranja significa que hay errores en las solicitudes, las vistas de página o las llamadas de dependencia. Rojo significa un porcentaje de error superior al 5 %. Si desea tooadjust estos umbrales, abra Opciones.

![iconos de error](./media/app-insights-app-map/04.png)

También se muestran las alertas activas: 

![alertas activas](./media/app-insights-app-map/05.png)

Si usa SQL Azure, hay un icono que se muestra cuando hay recomendaciones sobre cómo mejorar el rendimiento. 

![recomendación de Azure](./media/app-insights-app-map/06.png)

Haga clic en cualquier icono tooget más detalles:

![recomendación de Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>Recorrido por los diagnósticos mediante clic
Cada uno de los nodos de hello en el mapa de hello ofrece destino click-through para diagnósticos. Opciones de Hello varían según el tipo hello del nodo de Hola.

![opciones de servidor](./media/app-insights-app-map/09.png)

Para los componentes que se hospedan en Azure, las opciones de hello incluyen toothem de vínculos directos.

## <a name="filters-and-time-range"></a>Filtros e intervalo de tiempo
De forma predeterminada, mapa de hello resume todos los datos de hello disponibles para hello elegido el intervalo de tiempo. Pero puede filtrar nombres de las operaciones determinadas tooinclude o dependencias.

* Nombre de la operación: incluye vistas de página y tipos de solicitud del lado servidor. Con esta opción, Hola mapa muestra Hola KPI en el nodo de cliente/servidor hello para las operaciones de hello seleccionado solo. Muestra las dependencias de hello llamadas en el contexto de Hola de esas operaciones específicas.
* Nombre de base de dependencia: Esto incluye dependencias de explorador de AJAX de Hola y de servidor. Si informe de telemetría de dependencia personalizada con hello TrackDependency API, también aparecen aquí. Puede seleccionar tooshow de dependencias de hello en el mapa de Hola. Actualmente esta selección no filtra las solicitudes del servidor de Hola o vistas de página del lado cliente de Hola.

![Establecer filtros](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>Guardado de los filtros
filtros de hello toosave ha aplicado, Hola pin filtra vista en una [panel](app-insights-dashboards.md).

![Toodashboard de PIN](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>Panel de errores
Al hacer clic en un nodo del mapa de hello, un panel de error se muestra en el lado derecho de hello resumir los errores de ese nodo. Los errores se agrupan en primer lugar por identificador de operación y, luego, por identificador de problema.

![Panel de errores](./media/app-insights-app-map/error-pane.png)

Al hacer clic en un error, le toohello instancia más reciente de ese error.

## <a name="resource-health"></a>Estado de los recursos
Para algunos tipos de recursos, estado de los recursos se muestra en la parte superior de hello del panel de errores de Hola. Por ejemplo, al hacer clic en un nodo de SQL se mostrará de estado de base de datos de Hola y las alertas que se ha activado.

![Estado de los recursos](./media/app-insights-app-map/resource-health.png)

Puede hacer clic en hello recurso nombre tooview estándar información general sobre las métricas para ese recurso.

## <a name="end-to-end-system-app-maps"></a>Mapas de la aplicación del sistema completo

*Se requiere la versión 2.3 o posterior del SDK*

Si la aplicación tiene varios componentes: por ejemplo, un servicio back-end además toohello web app -, a continuación, se puede mostrar usarlas en mapa de una aplicación integrada.

![Establecer filtros](./media/app-insights-app-map/multi-component-app-map.png)

asignación de aplicación Hola busca los nodos de servidor siguiendo las llamadas de la dependencia HTTP entre los servidores con hello que Application Insights SDK instalado. Se supone que cada recurso de Application Insights toocontain un servidor.

### <a name="multi-role-app-map-preview"></a>Mapa de aplicación de varios roles (versión preliminar)

característica de asignación de aplicación de varios roles de vista previa de Hello le permite toouse Hola aplicación asigna con varios servidores de envío de datos toohello mismo recurso de Application Insights / clave de instrumentación. Servidores de asignación de hello están segmentados por propiedad de cloud_RoleName hello en los elementos de telemetría. Establecer *asignación de la aplicación de varios roles* demasiado*en* de Hola tooenable de hoja de las vistas previas, esta configuración.

Este enfoque puede ser deseable en una aplicación de servicios de micro o en otros escenarios donde desea toocorrelate eventos a través de varios servidores dentro de un único recurso de Application Insights.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>Comentarios
Proporcione sus comentarios a través de la opción de comentarios de portal de Hola.

![Imagen MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>Pasos siguientes

* [Portal de Azure](https://portal.azure.com)

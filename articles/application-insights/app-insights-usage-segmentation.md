---
title: "análisis de aaaUser, sesiones y eventos en Azure Application Insights | Documentos de Microsoft"
description: "Este artículo trata sobre el análisis de los usuarios de su aplicación web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Análisis de usuarios, sesiones y eventos en Application Insights

Descubra cuándo los usuarios utilizan la aplicación web, en qué páginas que están más interesados, en qué ubicación se encuentran dichos usuarios, y los sistemas operativos y exploradores que emplean. Analice la telemetría de uso y de negocio con [Azure Application Insights](app-insights-overview.md).

## <a name="get-started"></a>Primeros pasos

Si aún no ve los datos en los usuarios de hello, sesiones o las hojas de eventos en el portal de Application Insights hello, [Obtenga información acerca de cómo tooget a trabajar con herramientas de uso de hello](app-insights-usage-overview.md).

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>herramienta de segmentación de los usuarios, sesiones y eventos Hola

Tres de usar hojas de uso de Hola Hola mismo telemetría herramienta de tooslice y dividir los datos desde la aplicación web desde tres perspectivas. Mediante el filtrado y dividir los datos de hello, se puede descubrir información acerca del uso de relativa Hola de distintas páginas y características.

* **Herramienta de usuarios**: averigüe cuántas personas usan la aplicación y sus características.  Los usuarios se cuentan mediante el uso de identificadores anónimos almacenados en las cookies del explorador. Una sola persona que usa distintos exploradores o máquinas se contarán como más de un usuario.
* **Herramienta de sesiones**: la cantidad de sesiones de actividad de usuario que han incluido determinadas páginas y características de la aplicación. Una sesión se cuenta después de media hora de inactividad del usuario, o después de 24 horas de uso continuas.
* **Herramienta de eventos**: la frecuencia con la que se usan ciertas páginas y características de la aplicación. Una vista de página se cuenta cuando un explorador carga una página de la aplicación, siempre que se haya [instrumentado](app-insights-javascript.md). 

    Un evento personalizado representa una ocurrencia de algo que sucede en la aplicación, a menudo una interacción del usuario como un botón, haga clic en u Hola realización de alguna tarea. Inserte código en su aplicación demasiado[generar eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).

![Herramienta de uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Consulta de determinados usuarios 

Explorar distintos grupos de usuarios mediante el ajuste de opciones de consulta de hello en parte superior de Hola de herramienta de Hola a los usuarios: 

* que usaron: elija eventos personalizados y vistas de página. 
* Durante: elija un intervalo de tiempo. 
* Por: Elija cómo toobucket Hola datos, por un período de tiempo o por otra propiedad como explorador o una ciudad. 
* Dividir por: Elija una propiedad por los datos de hello toosplit o segmento. 
* Agregar filtros: Limitar Hola consultar toocertain a los usuarios, sesiones o eventos en función de sus propiedades, como el explorador o una ciudad. 
 
## <a name="saving-and-sharing-reports"></a>Guardado e intercambio de informes 
Puede guardar los informes de los usuarios, ya sea tooyou privada solo en la sección de Mis informes de hello, o comparten con todos los demás con toothis de acceso a recursos de Application Insights de hello sección informes compartidos.  
 
Al guardar un informe o editar sus propiedades, elija toosave "Intervalo de tiempo relativa actual" un informe le continuamente actualiza datos, volviendo a un período de tiempo.  
 
Elegir un informe con un conjunto fijo de datos de toosave "Intervalo de tiempo absoluto actual". Tenga en cuenta que solo se almacenan datos de Application Insights durante 90 días, por lo que se guardó si han pasado más de 90 días desde un informe con un intervalo de tiempo absoluto, informe de Hola se mostrará vacío. 
 
## <a name="example-instances"></a>Instancias de ejemplo

Hola sección de instancias en el ejemplo muestra información sobre una serie de eventos que coinciden con la consulta actual de Hola, sesiones o usuarios individuales. Teniendo en cuenta y explorar los comportamientos de Hola de individuos, en tooaggregates de suma, pueden proporcionar información sobre cómo se utiliza realmente la aplicación. 
 
## <a name="insights"></a>Información detallada 

barra lateral de visión de Hello muestra grandes clústeres de los usuarios que comparten propiedades comunes. Estos grupos pueden descubrir tendencias sorprendentes sobre cómo se usa la aplicación. Por ejemplo, si procede de 40% de todas las de uso de saludo de la aplicación de personas que usan una sola función.  


## <a name="next-steps"></a>Pasos siguientes
- uso de tooenable experimenta, empezar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [página vistas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si ya envía eventos personalizados o las vistas de página, explorar Hola uso herramientas toolearn cómo los usuarios utilizar el servicio.
    - [Embudos](usage-funnels.md)
    - [Retención](app-insights-usage-retention.md)
    - [Flujos de usuario](app-insights-usage-flows.md)
    - [Libros](app-insights-usage-workbooks.md)
    - [Adición de contexto de usuario](app-insights-usage-send-user-context.md)


---
title: aaaExploring HockeyApp datos en Azure Application Insights | Documentos de Microsoft
description: "Analice el uso y el rendimiento de la aplicación de Azure con Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>Exploración de datos de HockeyApp en Application Insights
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) recomienda Hola plataforma para la supervisión de aplicaciones de escritorio y móviles en vivo. De HockeyApp, puede enviar personalizado y realice un seguimiento telemetría toomonitor uso y ayudar a un diagnóstico más detallado (en los datos de bloqueo de suma toogetting). Puede consultar esta secuencia de telemetría con hello eficaz [análisis](app-insights-analytics.md) característica de [Azure Application Insights](app-insights-overview.md). Además, puede [exportar Hola personalizado y telemetría de seguimiento](app-insights-export-telemetry.md). tooenable estas características, configurar un puente que retransmite HockeyApp datos personalizados tooApplication visión.

## <a name="hello-hockeyapp-bridge-app"></a>aplicación de puente de HockeyApp Hello
Hola HockeyApp puente aplicación es Hola principal característica que permite tooaccess la telemetría de seguimiento en Application Insights a través de hello análisis y HockeyApp personalizado y las características de exportación continua. Custom y seguimiento de los eventos recopilados por HockeyApp después de la creación de hello de hello HockeyApp puente aplicación será accesibles desde estas características. Veamos cómo tooset una de estas aplicaciones de puente.

En HockeyApp, abra Configuración de cuenta, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens)(Tokens de API). Cree un token o use uno existente. se requieren permisos mínimo de Hello son "solo lectura". Realizar una copia de hello API símbolo (token).

![Obtener un token de API de HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

Portal de Microsoft Azure Hola abierto y [crear un recurso de Application Insights](app-insights-create-new-resource.md). Establecer tipo de aplicación demasiado "Aplicación de puente de HockeyApp":

![Nuevo recurso de Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

No es necesario tooset un nombre: Esto se establecerá automáticamente de nombre de HockeyApp Hola.

Hola HockeyApp puente campos aparecen. 

![Especifique los campos de puente](./media/app-insights-hockeyapp-bridge-app/03.png)

Escriba hello HockeyApp token que se ha indicado anteriormente. Esta acción rellena el menú de lista desplegable de "HockeyApp aplicación" hello con todas las aplicaciones de HockeyApp. Seleccione Hola uno desea toouse y el resto de hello completa de campos de Hola. 

Abra el nuevo recurso de Hola. 

Tenga en cuenta que los datos de hello tardan un tiempo toostart que fluyen.

![Recurso de Application Insights en espera de datos](./media/app-insights-hockeyapp-bridge-app/04.png)

¡Ya está! Custom y seguimiento de los datos recopilados en la aplicación instrumentada HockeyApp a partir de este punto están ahora también tooyou disponible en hello análisis y exportar continua características de Application Insights.

Revisemos brevemente cada uno de estos tooyou ahora disponible de características.

## <a name="analytics"></a>Análisis
Análisis es una herramienta eficaz para realizar consultas de los datos, lo que le toodiagnose de ad hoc y analizar la telemetría y descubra rápidamente los patrones y las causas raíz.

![Análisis](./media/app-insights-hockeyapp-bridge-app/05.png)

* [Aprenda más acerca de Analytics](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>Exportación continua
Exportación continua permite tooexport los datos en un contenedor de almacenamiento de blobs de Azure. Esto es muy útil si necesita tookeep los datos durante más tiempo que el período de retención de hello ofrece actualmente de Application Insights. Puede mantener los datos de hello en almacenamiento de blobs, procesarlo en una base de datos de SQL o la solución de almacenamiento de datos preferidos.

[Aprenda más acerca de la exportación continua](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Pasos siguientes
* [Aplicar datos de análisis de tooyour](app-insights-analytics-tour.md)


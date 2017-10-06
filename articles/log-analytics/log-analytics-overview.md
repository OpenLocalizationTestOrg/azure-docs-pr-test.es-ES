---
title: "¿aaaWhat es el análisis de registros de Operations Management Suite (OMS)? | Microsoft Docs"
description: "Log Analytics es un servicio de Operations Management Suite (OMS) que le ayuda a recopilar y analizar los datos operativos generados por los recursos en los entornos locales o de nube.  Este artículo proporciona una breve descripción de los diferentes componentes de Hola de análisis de registros y el contenido de toodetailed de vínculos."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>¿Qué es Log Analytics?
Análisis de registros es un servicio en [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) que supervisa su toomaintain de entornos de nube y locales su disponibilidad y el rendimiento.  Recopila los datos generados por los recursos en los entornos de nube y locales y de otros análisis de tooprovide herramientas supervisión a través de varios orígenes.  Este artículo se proporciona una breve explicación del valor de Hola que análisis de registros proporciona una visión general de cómo funciona, y vínculos toomore detallada contenido por lo que ya puede adentrarse aún más.

## <a name="is-log-analytics-for-you"></a>¿Es Log Analytics adecuado en su caso?
Si no dispone actualmente de ningún tipo de supervisión en su entorno de Azure, debe comenzar con [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md), que recopila y analiza los datos de supervisión de los recursos de Azure.  Análisis de registros pueden [recopilar datos de Azure Monitor](log-analytics-azure-storage.md) toocorrelate con otros datos y proporcionar análisis adicionales.

Si desea toomonitor su entorno local o si tiene la supervisión existente mediante servicios como System Center Operations Manager o el Monitor de Azure, análisis de registros puede agregar un valor significativo.  Esta solución recopila datos directamente de los agentes y también de estas otras herramientas en un único repositorio.  Las herramientas de análisis de Log Analytics, como búsquedas de registros, vistas y soluciones funcionan con todos los datos recopilados que proceden del análisis centralizado de todo el entorno.


## <a name="using-log-analytics"></a>Uso de Log Analytics
Análisis de registros puede tener acceso a través del portal de OMS de Hola o hello portal de Azure que se ejecutan en cualquier explorador y proporcionar a la configuración de acceso tooconfiguration y tooanalyze de varias herramientas y actuar en los datos recopilados.  Desde el portal de hello puede aprovechar [búsquedas de registro](log-analytics-log-searches.md) donde construir consultas tooanalyze recopilan datos, [paneles](log-analytics-dashboards.md) que se pueden personalizar mediante vistas gráficas de las búsquedas más valiosas, y [soluciones](log-analytics-add-solutions.md) que proporcionan herramientas de análisis y funcionalidad adicionales.

imagen de Hello siguiente es Hola portal de OMS qué panel de hello muestra que muestra información resumida de hello [soluciones](#add-functionality-with-management-solutions) que se instalan en el área de trabajo de Hola.  Puede hacer clic en cualquier toodrill mosaico aún más en datos de Hola para esa solución.

![Portal de OMS](media/log-analytics-overview/portal.png)

Análisis de registros incluyen una recuperación de tooquickly de lenguaje de consulta y consolidan los datos en el repositorio de Hola.  Puede crear y guardar [búsquedas de registros](log-analytics-log-searches.md) toodirectly analizar los datos en el portal de Hola o búsquedas de registros ejecutaron automáticamente toocreate una alerta si los resultados de Hola de consulta de hello indican una condición importante.

![Búsqueda de registros](media/log-analytics-overview/log-search.png)

tooget una vista gráfica rápida del estado de Hola de su entorno global, puede agregar visualizaciones de registros guardadas búsquedas tooyour [panel](log-analytics-dashboards.md).   

![Panel](media/log-analytics-overview/dashboard.png)

Datos de pedidos tooanalyze fuera de análisis de registros, puede exportar datos de Hola desde repositorio de OMS de Hola en herramientas como [Power BI](log-analytics-powerbi.md) o Excel.  También puede aprovechar hello [API de búsqueda de registros](log-analytics-log-search-api.md) toobuild soluciones personalizadas que aprovechan los datos de análisis de registros o toointegrate con otros sistemas.

## <a name="add-functionality-with-management-solutions"></a>Adición de funcionalidad con soluciones de administración
[Soluciones de administración de](log-analytics-add-solutions.md) agregar funcionalidad tooOMS, que proporcionan datos adicionales y herramientas de análisis tooLog análisis.  También pueden definir nuevos toobe de tipos de registro recopilado que se pueden analizar con búsquedas de registros o mediante la interfaz de usuario adicionales de solución de hello en el panel de Hola.  imagen de ejemplo de Hola siguiente muestra hello [solución de seguimiento de cambios](log-analytics-change-tracking.md)

![Solución de seguimiento de cambios](media/log-analytics-overview/change-tracking.png)

Existen soluciones disponibles para diversas funciones y continuamente se agregan otras nuevas.  Puede examinar fácilmente soluciones disponibles y [agregarlos área de trabajo OMS tooyour](log-analytics-add-solutions.md) desde la Galería de soluciones de Hola o Azure Marketplace.  Muchas soluciones se implementan automáticamente y comienzan a funcionar de inmediato, mientras que otras pueden requerir algo de configuración.

![Galería de soluciones](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Componentes de Log Analytics
En hello centro de análisis de registros es repositorio de OMS de Hola que se hospeda en hello nube de Azure.  Recopilar datos en el repositorio de Hola de orígenes conectados por configurar orígenes de datos y agregar suscripción de tooyour de soluciones.  Soluciones y los orígenes de datos creará diferentes tipos de registros que tienen su propio conjunto de propiedades, pero pueden seguir analizando juntos en el repositorio de consultas toohello.  Esto le permite hello toouse mismo toowork de herramientas y los métodos con distintos tipos de datos recopilado por diferentes orígenes.

![Repositorio de OMS](media/log-analytics-overview/overview.png)

Orígenes conectados son equipos de Hola y otros recursos que generan datos recopilados por el análisis de registro.  Esto puede incluir los agentes instalados en equipos [Windows](log-analytics-windows-agents.md) y [Linux](log-analytics-linux-agents.md) que se conectan directamente o agentes en un [grupo de administración de System Center Operations Manager conectado](log-analytics-om-agents.md).  Para los recursos de Azure, Log Analytics recopila datos de [Azure Monitor y Diagnósticos de Azure](log-analytics-azure-storage.md).

[Orígenes de datos](log-analytics-data-sources.md) sean Hola diferentes tipos de datos recopilados de cada origen conectado.  Esto incluye [eventos](log-analytics-data-sources-windows-events.md) y [los datos de rendimiento](log-analytics-data-sources-performance-counters.md) de [Windows](log-analytics-data-sources-windows-events.md) y agentes de Linux en suma toosources como [registros de IIS](log-analytics-data-sources-iis-logs.md)y [registros de texto personalizado](log-analytics-data-sources-custom-logs.md).  Configure cada origen de datos que se desea toocollect, y configuración de hello es origen conectado tooeach automáticamente entregado.

Si tiene requisitos personalizados, puede usar hello [API de recopilador de datos HTTP](log-analytics-data-collector-api.md) toowrite repositorio de toohello de datos desde un cliente de la API de REST.

## <a name="log-analytics-architecture"></a>Arquitectura de Log Analytics
requisitos de implementación de Hola de análisis de registros son mínimos, ya que los componentes de hello central se hospedan en hello nube de Azure.  Esto incluye el repositorio de hello en los servicios de toohello de suma que le permiten toocorrelate y analizar los datos recopilados.  portal de Hello son accesibles desde cualquier explorador así que no hay ningún requisito para el software de cliente.

Debe instalar agentes en equipos [Windows](log-analytics-windows-agents.md) y [Linux](log-analytics-linux-agents.md), pero no se requiere un agente adicional para los equipos que ya son miembros de un [grupo de administración de SCOM conectado](log-analytics-om-agents.md).  Agentes de SCOM continuará toocommunicate con los servidores de administración que reenvía su tooLog análisis de datos.  Aunque algunas soluciones requerirá toocommunicate agentes directamente con análisis de registros.  documentación de Hola para cada solución especificará sus requisitos de comunicación.

Cuando se [suscriba a Log Analytics](log-analytics-get-started.md), creará un área de trabajo de OMS.  Puede pensar en el área de trabajo de Hola como un único entorno de análisis de registros con su propio repositorio de datos, orígenes de datos y soluciones. Puede crear varias áreas de trabajo en su suscripción toosupport varios entornos, como de producción y pruebas.

![Arquitectura de Log Analytics](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>Pasos siguientes
* [Registrarse para obtener una cuenta gratuita de análisis de registros](log-analytics-get-started.md) tootest en su propio entorno.
* Hola de vista diferentes [orígenes de datos](log-analytics-data-sources.md) datos toocollect disponibles en el repositorio de OMS Hola.
* [Buscar Hola soluciones disponibles en la Galería de soluciones de hello](log-analytics-add-solutions.md) tooadd funcionalidad tooLog análisis.


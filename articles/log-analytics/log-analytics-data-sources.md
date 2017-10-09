---
title: "aaaConfigure orígenes de datos de análisis de registros de OMS | Documentos de Microsoft"
description: "Orígenes de datos definen los datos de Hola que recopila de análisis de registros de agentes y otros orígenes conectados.  Este artículo describe el concepto de hello del modo en que análisis de registros utiliza orígenes de datos, se explican los detalles de Hola de cómo tooconfigure y proporciona un resumen de hello distintos orígenes de datos disponibles."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Orígenes de datos en Log Analytics
Análisis de registros recopila datos de orígenes conectados, hello en el área de trabajo OMS y lo almacena en el repositorio de OMS.  datos de Hola que se recopilan en cada uno de ellos se define mediante Hola orígenes de datos que configure.  Datos en el repositorio OMS Hola se almacenan como un conjunto de registros.  Cada origen de datos crea registros de un tipo determinado, donde cada tipo tiene su propio conjunto de propiedades.

![Recopilación de datos de Log Analytics](./media/log-analytics-data-sources/overview.png)

Orígenes de datos son diferentes de las soluciones de OMS que también recopilar datos de orígenes conectados y crear registros en el repositorio de OMS Hola.  Soluciones se pueden agregar área de trabajo tooyour de hello Galería de soluciones y normalmente proporcionará las herramientas de análisis adicionales en el portal de OMS Hola.  

## <a name="summary-of-data-sources"></a>Resumen de orígenes de datos
orígenes de datos de Hola que están actualmente disponibles en el análisis de registros se muestran en hello en la tabla siguiente.  Cada uno tiene un vínculo tooa otro artículo proporciona detalles para ese origen de datos.

| Origen de datos | Tipo de evento | Descripción |
|:--- |:--- |:--- |
| [Registros personalizados](log-analytics-data-sources-custom-logs.md) |\<nombreDeRegistro\>_CL |Archivos de texto en agentes de Windows o Linux que contienen información de registro. |
| [Registros de eventos de Windows](log-analytics-data-sources-windows-events.md) |Evento |Los eventos se recopilan Hola registro de eventos en los equipos de Windows. |
| [Contadores de rendimiento de Windows](log-analytics-data-sources-performance-counters.md) |Perf |Contadores de rendimiento recopilados de equipos con Windows. |
| [Contadores de rendimiento de Linux](log-analytics-data-sources-performance-counters.md) |Perf |Contadores de rendimiento recopilados de equipos con Linux. |
| [Registros de IIS](log-analytics-data-sources-iis-logs.md) |W3CIISLog |Registros de Internet Information Services en el formato W3C. |
| [Syslog](log-analytics-data-sources-syslog.md) |syslog |Eventos de Syslog en equipos con Windows o Linux. |

## <a name="configuring-data-sources"></a>Configuración de orígenes de datos
Configurar orígenes de datos de hello **datos** menú análisis de registros **configuración**.  Cualquier configuración se entrega orígenes tooall conectado en el área de trabajo OMS.  Actualmente, no puede excluir ningún agente de esta configuración.

![Configurar eventos de Windows](./media/log-analytics-data-sources/configure-events.png)

1. En la consola de OMS hello, haga clic en hello **configuración** mosaico o hello **configuración** situado en la parte superior de Hola de pantalla de bienvenida.
2. Seleccione **Datos**.
3. Haga clic en tooconfigure de origen de datos de Hola.
4. Seguir la documentación de toohello de vínculo de Hola para cada origen de datos en hello por encima de la tabla para obtener más información sobre su configuración.

> [!NOTE]
> Actualmente, no puede configurar orígenes de datos de análisis de registros en hello portal de Azure.

## <a name="data-collection"></a>Colección de datos
Las configuraciones de origen de datos se entregan tooagents que están directamente conectado tooLog análisis dentro de unos minutos.  Hola especifica datos se recopilan desde el agente de Hola y entregan directamente tooLog análisis en el origen de datos de intervalos tooeach específico.  Consulte la documentación de Hola para cada origen de datos para estas características.

Para los agentes de System Center Operations Manager (SCOM) en un grupo de administración conectado, configuraciones de origen de datos se traducen en módulos de administración y entrega el grupo de administración de toohello cada 5 minutos de forma predeterminada.  agente de Hello descarga el módulo de administración de hello como cualquier otro y recopila Hola datos especificados. Función Hola Hola de origen de datos datos será envía tooa servidor de administración que reenvía Hola datos toohello análisis de registros o agente Hola enviará Hola datos tooLog análisis sin pasar por el servidor de administración de Hola. Consulte demasiado[detalles de recopilación de datos para características y soluciones OMS](log-analytics-add-solutions.md#data-collection-details) para obtener más información.  Puede leer acerca de los detalles de la conexión de SCOM y OMS y modificar la frecuencia de Hola que la configuración se entrega en [configurar la integración con System Center Operations Manager](log-analytics-om-agents.md).

Si el agente hello es tooconnect no se puede tooLog análisis u Operations Manager, seguirá toocollect datos que entregará cuando establece una conexión.  Se pueden perder datos si cantidad Hola de datos alcanza el tamaño máximo de caché de hello para el cliente de hello, o si Hola agente no es capaz de tooestablish una conexión dentro de 24 horas.

## <a name="log-analytics-records"></a>Registros de Log Analytics
Todos los datos recopilados por el análisis de registro se almacena en el repositorio OMS hello como registros.  Los registros que recopilan distintos orígenes de datos tendrán su propio conjunto de propiedades y se identificar por su propiedad **Type** .  Consulte la documentación de Hola para cada origen de datos y soluciones para obtener más información sobre cada tipo de registro.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [soluciones](log-analytics-add-solutions.md) que agregar funcionalidad tooLog análisis y recopilar datos en el repositorio de OMS Hola.
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.  
* Configurar [alertas](log-analytics-alerts.md) tooproactively avisarle de los datos críticos recopilados de los orígenes de datos y soluciones.

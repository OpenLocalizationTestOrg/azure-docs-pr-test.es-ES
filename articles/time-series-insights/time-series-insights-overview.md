---
title: "aaaOverview de visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "Introducción tooAzure una visión general de tiempo serie, un nuevo servicio de análisis de datos de series de tiempo y las soluciones de IoT"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>¿Qué es Azure Time Series Insights?

Azure visión de serie de tiempo es un servicio de nube administrado con componentes de visualización que hace más fácil tooingest, almacenarán, explorarán y analizar miles de millones de eventos al mismo tiempo, análisis y almacenamiento. Time Series Insights proporciona una vista global de los datos, lo que le permite validar las soluciones de IoT de forma rápida y evitar costosos tiempos de inactividad en dispositivos, además de ayudarle a detectar tendencias ocultas y anomalías, y realizar análisis de causas principales casi en tiempo real. Visión de la serie de tiempo recopila datos de serie temporal de agentes de evento (por ejemplo, los centros de IoT o concentradores de eventos), Hola de datos de índices y datos según una directiva de retención configurable se retira. Los usuarios consumen datos de Hola a través de una intuitiva UX o API de REST de consulta.

![Información general de Time Series Insight](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>Escenarios principales

* Supervisar y validar soluciones de IoT en minutos.
* Visualizar y analizar datos de IoT a escala.
* Análisis rápido de causas principales y detección de anomalías.
* Crear una vista global de múltiples dispositivos, plantas y datos.

## <a name="capabilities-and-benefits"></a>Funcionalidades y ventajas

* **Fácil tooget iniciado**: visión de serie de tiempo de Azure no requiere ninguna preparación de datos iniciales y es increíblemente rápida. Conectar toobillions de eventos en el centro de eventos o centro de IoT de Azure en minutos. Una vez conectado, visualizar e interactuar con datos del sensor de segundos tooquickly validar sus soluciones de IoT. Visión de la serie de tiempo es fácil toouse; puede interactuar con los datos sin escribir una sola línea de código.  No hay ninguna nueva toolearn de lenguaje; Visión de la serie de tiempo proporciona una superficie de consulta granular y texto sin formato para los usuarios avanzados y seleccione y haga clic en la exploración para todos.

* **Casi en tiempo real visión**: visión de la serie de tiempo puede introducir centenares de millones de eventos de sensor al día, con una latencia de un minuto, por lo que le permitirá reaccionar toochanges rápidamente. Time Series Insights ayuda a obtener información detallada sobre los datos de sensores, contribuyendo a detectar tendencias y anomalías rápido, llevar a cabo fácilmente análisis de causa principal complejos y evitar costosos tiempos de inactividad. Al habilitar la correlación entre entre los datos en tiempo real e históricos, visión de la serie de tiempo ayuda a desbloquear ocultas tendencias en los datos de Hola.

* **Crear soluciones personalizadas**: inserte los datos de Azure Time Series Insights en aplicaciones existentes o cree nuevas soluciones personalizadas con las API de REST de Time Series Insights. Crear y compartir personalizan vistas que se pueden compartir para que otros lo tooexplore sus descubrimientos.

* **Escalabilidad**: información de la serie de tiempo es diseñada toosupport IoT a escala. En la vista previa, es posible entrada de too100 1 millón abarcan millones de eventos al día, con un tiempo predeterminado de retención de 31 días. Puede visualizar y analizar flujos de datos activos casi en tiempo real, junto con grandes cantidades de datos históricos. Más adelante, la tasa de entrada y retención aumentará tooaccommodate una escala de empresa en constante evolución alguna vez.

## <a name="time-series-insights-glossary"></a>Glosario de Time Series Insights

* **Entorno**: un entorno es un recurso de Azure con funcionalidades de incorporación y almacenamiento.  Los clientes aprovisione entornos a través de hello portal de Azure con su capacidad requerida.
* **Origen de eventos**: un origen de eventos se deriva de un agente de eventos, como Azure Event Hubs.  Visión de la serie de tiempo se conecta directamente tooEvent orígenes, ingesta de flujo de datos de hello sin escribir ningún código. Actualmente, Time Series Insights es compatible tanto con Azure Event Hubs como con Azure IoT Hubs.
* **Datos de referencia**: información de la serie de tiempo proporciona a los usuarios datos de series de hello capacidad toojoin temporales con datos de referencia.  Los datos de referencia pueden incluir metadatos relacionados con dispositivos u otros datos estáticos que varíen con poca frecuencia. Visión de la serie de tiempo combina datos de referencia de hello con flujos de datos, lo que permite a los usuarios toovisualize y analizar estos datos en casi en tiempo real.

---
title: aaaAdd un entorno de Azure Insights de serie de tiempo de evento origen tooyour | Documentos de Microsoft
description: "En este tutorial, se conectará un entorno de visión de la serie de tiempo de tooyour de origen de eventos"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Crear un origen de eventos para el entorno de visión de la serie de tiempo mediante este portal como Hola

El origen de eventos de Time Series Insights se deriva de un agente de eventos, como Azure Event Hubs. Visión de la serie de tiempo se conecta directamente orígenes tooEvent, ingesta de flujo de datos de hello sin necesidad de toowrite a los usuarios una sola línea de código. Actualmente, Time Series Insights es compatible tanto con Azure Event Hubs como con Azure IoT Hubs. Hola futuras, se agregarán más orígenes de eventos.

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>Pasos tooadd un entorno de tooyour de origen de eventos

1.  Inicie sesión en toohello [este portal como](https://portal.azure.com).
2.  Haga clic en "Todos los recursos" en el menú izquierda Hola de este portal como Hola Hola.
3.  Seleccione el entorno de Time Series Insights.

  ![Crear origen de eventos de información de la serie de tiempo de Hola](media/add-event-source/getstarted-create-event-source-1.png)

4.  Seleccione "Orígenes de eventos", haga clic en "+Agregar".

  ![Crear origen de eventos de información de la serie de tiempo de hello - detalles](media/add-event-source/getstarted-create-event-source-2.png)

5.  Especifique el nombre de Hola Hola del origen de evento. Este nombre se asocia a todos los eventos procedentes de este origen de eventos y está disponible en el momento de la consulta.
6.  Seleccione un concentrador de eventos de lista de Hola de recursos de concentrador de eventos de suscripción actual de Hola. En caso contrario, elija la opción de importación "configuración del centro de eventos de proporcionar manualmente" toospecify un concentrador de eventos en otra suscripción. Los eventos se deben publicar en formato JSON.
7.  Seleccione la directiva que tiene permiso en el concentrador de eventos de Hola de lectura.
8.  Especifique el grupo de consumidores del centro de eventos.

  > [!IMPORTANT]
  > Asegúrese de que el grupo de consumidores no es utilizado por ningún otro servicio (como un trabajo de Stream Analytics u otro entorno de Time Series Insights). Si se usa el grupo de consumidores por otros servicios, lea la operación se ve afectada negativamente para este entorno y Hola otros servicios. Si usas "$Default" como grupo de consumidores de hello, puede provocar toopotential reutilización por otro lector.

9.  Haga clic en "Crear".

Después de la creación del origen de evento de hello, visión de la serie de tiempo se iniciará automáticamente la transmisión de datos en su entorno.

## <a name="next-steps"></a>Pasos siguientes

* [Enviar eventos](time-series-insights-send-events.md) toohello origen del evento
* Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)

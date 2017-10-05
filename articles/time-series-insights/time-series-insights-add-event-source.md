---
title: "Incorporación de un origen de eventos al entorno de Azure Time Series Insights | Microsoft Docs"
description: En este tutorial, se conecta un origen de eventos al entorno de Time Series Insights
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
ms.openlocfilehash: ffa2eaf3680e68ac14aabf49b6308caeb173fd43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-the-ibiza-portal"></a>Creación de un origen de eventos para el entorno de Time Series Insights mediante el portal Ibiza

El origen de eventos de Time Series Insights se deriva de un agente de eventos, como Azure Event Hubs. Time Series Insights se conecta directamente a los orígenes de eventos e ingiere el flujo de datos sin necesidad de que los usuarios escriban una sola línea de código. Actualmente, Time Series Insights es compatible tanto con Azure Event Hubs como con Azure IoT Hubs. En el futuro, se agregarán más orígenes de eventos.

## <a name="steps-to-add-an-event-source-to-your-environment"></a>Pasos para agregar un origen de eventos a su entorno

1.  Inicie sesión en el [portal Ibiza](https://portal.azure.com).
2.  Haga clic en "Todos los recursos" en el menú izquierdo del portal Ibiza.
3.  Seleccione el entorno de Time Series Insights.

  ![Creación del origen de eventos de Time Series Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  Seleccione "Orígenes de eventos", haga clic en "+Agregar".

  ![Creación del origen de eventos de Time Series Insights: detalles](media/add-event-source/getstarted-create-event-source-2.png)

5.  Especifique el nombre del origen de eventos. Este nombre se asocia a todos los eventos procedentes de este origen de eventos y está disponible en el momento de la consulta.
6.  Seleccione un centro de eventos en la lista de recursos de Event Hub de la suscripción actual. Otra opción es que elija la opción "Proporcionar configuración del centro de eventos de forma manual" para especificar un centro de eventos de otra suscripción. Los eventos se deben publicar en formato JSON.
7.  Seleccione una directiva con permiso de lectura en el centro de eventos.
8.  Especifique el grupo de consumidores del centro de eventos.

  > [!IMPORTANT]
  > Asegúrese de que el grupo de consumidores no es utilizado por ningún otro servicio (como un trabajo de Stream Analytics u otro entorno de Time Series Insights). Si otros servicios utilizan el grupo de consumidores, la operación de lectura se ve afectada negativamente en este entorno y en los otros servicios. Utilizar “$Default” como grupo de consumidores podría provocar que otros lectores lo reutilicen.

9.  Haga clic en "Crear".

Tras la creación del origen de eventos, Time Series Insights iniciará automáticamente la transmisión de datos al entorno.

## <a name="next-steps"></a>Pasos siguientes

* [Envío de eventos](time-series-insights-send-events.md) al origen de eventos
* Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)

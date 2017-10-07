---
title: "aaaCreate un entorno de visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "En este tutorial, obtendrá información sobre cómo toocreate entorno de la serie de tiempo, lo conecte el origen del evento tooan y está listo tooanalyze los datos del evento en minutos."
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Crear un nuevo entorno de visión de la serie de tiempo en hello portal de Azure

Un entorno de Time Series Insights es un recurso de Azure con funcionalidades de incorporación y almacenamiento. Los clientes proporcionar entornos a través de hello portal de Azure con capacidad de hello necesario.

## <a name="steps-toocreate-hello-environment"></a>Entorno de hello toocreate de pasos

Siga estos pasos toocreate su entorno:

1.  Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2.  Haga clic en hello más el signo ("+") en hello esquina superior izquierda.
3.  Busque "Información de Series de tiempo" en el cuadro de búsqueda de Hola.

  ![Crear entorno de visión de la serie de tiempo de Hola](media/get-started/getstarted-create-environment1.png)

4.  Seleccione "Time Series Insights" y haga clic en "Crear".

  ![Crear grupo de recursos de información de la serie de tiempo de Hola](media/get-started/getstarted-create-environment2.png)

5.  Especifique el nombre del entorno. Este nombre representa el entorno de hello en [explorer de la serie de tiempo](https://insights.timeseries.azure.com).
6.  Seleccione una suscripción. Elija una que contenga el origen de eventos. Visión de la serie de tiempo puede detectar automáticamente centro de IoT de Azure y recursos de concentrador de eventos existentes en Hola misma suscripción.
7.  Seleccione o cree un grupo de recursos. Un grupo de recursos es una colección de recursos de Azure que se usan juntos.
8.  Selección de una ubicación de hospedaje. centros de tooavoid mover datos a través de los datos, elija la ubicación que contiene el origen del evento.
9.  Seleccione un plan de tarifa.
10. Seleccione la capacidad. Puede cambiar la capacidad de un entorno después de su creación.
11. Cree el entorno. También puede anclar el panel de toohello de entorno para facilitar el acceso siempre que inicie sesión.

  ![Crear toodashboard de pin de hello visión de la serie de tiempo](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Pasos siguientes

* [Definir directivas de acceso de datos](time-series-insights-data-access.md) tooaccess su entorno en [Portal de visión de Series de tiempo](https://insights.timeseries.azure.com)
* [Creación de un origen de eventos](time-series-insights-add-event-source.md)
* [Enviar eventos](time-series-insights-send-events.md) toohello origen del evento

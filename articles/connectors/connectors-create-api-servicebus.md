---
title: "Conector de Service Bus de Azure de aaaLearn toouse hello en las aplicaciones lógicas | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conectar tooAzure toosend de Bus de servicio y recibir mensajes. Puede realizar acciones como envío tooqueue, tootopic de enviar, recibir de cola y recibir de suscripción."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a>Empezar a trabajar con el conector de Bus de servicio de Azure Hola
Conectar tooAzure toosend de Bus de servicio y recibir mensajes. Puede realizar acciones como envío tooqueue, tootopic de enviar, recibir de cola y recibir de suscripción.

toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica. Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooservice-bus"></a>Conectar tooService Bus
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate un servicio de toohello de conexión. Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>Uso de un desencadenador del Bus de servicio
Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica. [Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>Uso de una acción del Bus de servicio
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/servicebus/). 

## <a name="next-steps"></a>Pasos siguientes
[Crear una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).


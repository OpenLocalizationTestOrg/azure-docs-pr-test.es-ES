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
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="3f361-105">Empezar a trabajar con el conector de Bus de servicio de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="3f361-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="3f361-106">Conectar tooAzure toosend de Bus de servicio y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="3f361-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="3f361-107">Puede realizar acciones como envío tooqueue, tootopic de enviar, recibir de cola y recibir de suscripción.</span><span class="sxs-lookup"><span data-stu-id="3f361-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="3f361-108">toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3f361-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="3f361-109">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3f361-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="3f361-110">Conectar tooService Bus</span><span class="sxs-lookup"><span data-stu-id="3f361-110">Connect tooService Bus</span></span>
<span data-ttu-id="3f361-111">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate un servicio de toohello de conexión.</span><span class="sxs-lookup"><span data-stu-id="3f361-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="3f361-112">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="3f361-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="3f361-113">Uso de un desencadenador del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="3f361-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="3f361-114">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="3f361-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="3f361-115">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3f361-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="3f361-116">Uso de una acción del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="3f361-116">Use a Service Bus action</span></span>
<span data-ttu-id="3f361-117">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f361-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="3f361-118">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3f361-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="3f361-119">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="3f361-119">Connector-specific details</span></span>

<span data-ttu-id="3f361-120">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="3f361-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3f361-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f361-121">Next steps</span></span>
<span data-ttu-id="3f361-122">[Crear una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3f361-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>


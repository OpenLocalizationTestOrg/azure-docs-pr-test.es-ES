---
title: "aaaLearn toouse Hola conector de Salesforce en las aplicaciones lógicas | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Hola conector de Salesforce proporciona un toowork de API con objetos de Salesforce."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="7728c-104">Empezar a trabajar con el conector de Salesforce Hola</span><span class="sxs-lookup"><span data-stu-id="7728c-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="7728c-105">Hola conector de Salesforce proporciona un toowork de API con objetos de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7728c-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="7728c-106">toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="7728c-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="7728c-107">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7728c-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="7728c-108">Conecte el conector de tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="7728c-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="7728c-109">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="7728c-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="7728c-110">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="7728c-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="7728c-111">Crear un conector de tooSalesforce de conexión</span><span class="sxs-lookup"><span data-stu-id="7728c-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="7728c-112">Uso de un desencadenador del conector de Salesforce</span><span class="sxs-lookup"><span data-stu-id="7728c-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="7728c-113">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="7728c-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="7728c-114">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7728c-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="7728c-115">Agregar una condición</span><span class="sxs-lookup"><span data-stu-id="7728c-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="7728c-116">Uso de una acción del conector de Salesforce</span><span class="sxs-lookup"><span data-stu-id="7728c-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="7728c-117">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7728c-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="7728c-118">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7728c-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="7728c-119">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="7728c-119">Connector-specific details</span></span>

<span data-ttu-id="7728c-120">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="7728c-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7728c-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7728c-121">Next steps</span></span>
[<span data-ttu-id="7728c-122">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="7728c-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)


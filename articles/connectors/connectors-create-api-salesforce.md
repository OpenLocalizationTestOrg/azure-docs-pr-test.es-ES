---
title: "Información sobre cómo utilizar el conector de Salesforce en Logic Apps | Microsoft Docs"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. El conector de Salesforce proporciona una API para trabajar con objetos de Salesforce."
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
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="0deb2-104">Introducción al conector de Salesforce</span><span class="sxs-lookup"><span data-stu-id="0deb2-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="0deb2-105">El conector de Salesforce proporciona una API para trabajar con objetos de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0deb2-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="0deb2-106">Para poder usar [un conector](apis-list.md), primero debe crear una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="0deb2-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="0deb2-107">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0deb2-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="0deb2-108">Conexión con el conector de Salesforce</span><span class="sxs-lookup"><span data-stu-id="0deb2-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="0deb2-109">Para que la aplicación lógica pueda acceder a un servicio, primero debe crear una *conexión* con dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="0deb2-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="0deb2-110">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="0deb2-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="0deb2-111">Creación de una conexión con el conector de Salesforce</span><span class="sxs-lookup"><span data-stu-id="0deb2-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="0deb2-112">Uso de un desencadenador del conector de Salesforce</span><span class="sxs-lookup"><span data-stu-id="0deb2-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="0deb2-113">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="0deb2-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="0deb2-114">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0deb2-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="0deb2-115">Agregar una condición</span><span class="sxs-lookup"><span data-stu-id="0deb2-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="0deb2-116">Uso de una acción del conector de Salesforce</span><span class="sxs-lookup"><span data-stu-id="0deb2-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="0deb2-117">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="0deb2-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="0deb2-118">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0deb2-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="0deb2-119">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="0deb2-119">Connector-specific details</span></span>

<span data-ttu-id="0deb2-120">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="0deb2-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0deb2-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0deb2-121">Next steps</span></span>
[<span data-ttu-id="0deb2-122">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="0deb2-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

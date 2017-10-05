---
title: "Aprenda a utilizar el conector de SharePoint Online en las aplicaciones lógicas | Microsoft Docs"
description: "Cree aplicaciones lógicas con el conector de SharePoint Online para administrar listas en SharePoint."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e0ec3149-507a-409d-8e7b-d5fbded006ce
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 96fc1347604c0c6cc2c2463a5dbd83b560183a16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-online-connector"></a><span data-ttu-id="f7abf-103">Introducción al conector de SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f7abf-103">Get started with the SharePoint Online connector</span></span>
<span data-ttu-id="f7abf-104">Use el conector de SharePoint Online para administrar las listas de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f7abf-104">Use the SharePoint Online connector to manage SharePoint lists.</span></span>  

<span data-ttu-id="f7abf-105">Para poder usar [un conector](apis-list.md), primero debe crear una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="f7abf-105">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="f7abf-106">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7abf-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sharepoint-online"></a><span data-ttu-id="f7abf-107">Conexión a SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f7abf-107">Connect to SharePoint Online</span></span>
<span data-ttu-id="f7abf-108">Para que la aplicación lógica pueda acceder a un servicio, primero debe crear una *conexión* con dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="f7abf-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="f7abf-109">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="f7abf-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sharepoint-online"></a><span data-ttu-id="f7abf-110">Creación de una conexión a SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f7abf-110">Create a connection to SharePoint Online</span></span>
> [!INCLUDE [Steps to create a connection to SharePoint](../../includes/connectors-create-api-sharepointonline.md)]


## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="f7abf-111">Uso de un desencadenador de SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f7abf-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="f7abf-112">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="f7abf-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="f7abf-113">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f7abf-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]


## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="f7abf-114">Uso de una acción de SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f7abf-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="f7abf-115">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="f7abf-115">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="f7abf-116">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f7abf-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]


## <a name="connector-specific-details"></a><span data-ttu-id="f7abf-117">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="f7abf-117">Connector-specific details</span></span>

<span data-ttu-id="f7abf-118">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="f7abf-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7abf-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f7abf-119">Next Steps</span></span>
[<span data-ttu-id="f7abf-120">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="f7abf-120">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)


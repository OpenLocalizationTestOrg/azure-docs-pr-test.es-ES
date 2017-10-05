---
title: Conector de Trello en Azure Logic Apps | Microsoft Docs
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Trello le ofrece perspectiva sobre todos los proyectos, en el trabajo y en casa.  Es una manera fácil, gratis, flexible y visual de administrar los proyectos y organizar todo.  Conéctese a Trello para administrar los paneles, listas y tarjetas"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: fe7a4377-5c24-4f72-ab1a-6d9d23e8d895
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 526a14710f24ee4a4b61a11873aa6caa0b47dc10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-trello-connector"></a><span data-ttu-id="4f415-106">Introducción al conector Trello</span><span class="sxs-lookup"><span data-stu-id="4f415-106">Get started with the Trello connector</span></span>
<span data-ttu-id="4f415-107">Trello le ofrece perspectiva sobre todos los proyectos, en el trabajo y en casa.</span><span class="sxs-lookup"><span data-stu-id="4f415-107">Trello gives you perspective over all your projects, at work and at home.</span></span>  <span data-ttu-id="4f415-108">Es una manera fácil, gratis, flexible y visual de administrar los proyectos y organizar todo.</span><span class="sxs-lookup"><span data-stu-id="4f415-108">It is an easy, free, flexible, and visual way to manage your projects and organize anything.</span></span>  <span data-ttu-id="4f415-109">Conéctese a Trello para administrar los paneles, listas y tarjetas.</span><span class="sxs-lookup"><span data-stu-id="4f415-109">Connect to Trello to manage your boards, lists and cards.</span></span>

<span data-ttu-id="4f415-110">Para empezar, cree una aplicación lógica; consulte [Creación de su primer flujo de trabajo de aplicación lógica para automatizar los procesos entre aplicaciones de nube y servicios en la nube](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4f415-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-trello"></a><span data-ttu-id="4f415-111">Creación de una conexión a Trello</span><span class="sxs-lookup"><span data-stu-id="4f415-111">Create a connection to Trello</span></span>
<span data-ttu-id="4f415-112">Para crear aplicaciones lógicas con Trello, cree una **conexión** y especifique los detalles de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="4f415-112">To create Logic apps with Trello, first create a **connection**, and enter the details for the following properties:</span></span>

| <span data-ttu-id="4f415-113">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4f415-113">Property</span></span> | <span data-ttu-id="4f415-114">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="4f415-114">Required</span></span> | <span data-ttu-id="4f415-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="4f415-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f415-116">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="4f415-116">Token</span></span> |<span data-ttu-id="4f415-117">Sí</span><span class="sxs-lookup"><span data-stu-id="4f415-117">Yes</span></span> |<span data-ttu-id="4f415-118">Proporciona las credenciales de Trello</span><span class="sxs-lookup"><span data-stu-id="4f415-118">Provide Trello Credentials</span></span> |

<span data-ttu-id="4f415-119">Después de crear la conexión, puede usarla para ejecutar las acciones y escuchar los desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="4f415-119">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Trello](../../includes/connectors-create-api-trello.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="4f415-120">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="4f415-120">Connector-specific details</span></span>

<span data-ttu-id="4f415-121">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/trello/).</span><span class="sxs-lookup"><span data-stu-id="4f415-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/trello/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="4f415-122">Más conectores</span><span class="sxs-lookup"><span data-stu-id="4f415-122">More connectors</span></span>
<span data-ttu-id="4f415-123">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4f415-123">Go back to the [APIs list](apis-list.md).</span></span>
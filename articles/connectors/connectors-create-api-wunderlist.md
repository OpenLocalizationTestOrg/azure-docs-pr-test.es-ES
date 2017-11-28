---
title: Conector de Wunderlist en Azure Logic Apps | Microsoft Docs
description: "Cree una conexión con Wunderlist y úsela para crear un flujo de trabajo en las aplicaciones lógicas."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 899110992cc52ca5edf1706320fd5570473de784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-wunderlist-connector"></a><span data-ttu-id="b82ec-103">Introducción al conector Wunderlist</span><span class="sxs-lookup"><span data-stu-id="b82ec-103">Get started with the Wunderlist connector</span></span>
<span data-ttu-id="b82ec-104">Wunderlist proporciona una lista de tareas pendientes y un administrador de tareas para ayudar a los usuarios a hacer su trabajo.</span><span class="sxs-lookup"><span data-stu-id="b82ec-104">Wunderlist provide a todo list and task manager to help people get their stuff done.</span></span>  <span data-ttu-id="b82ec-105">Ya sea que comparta una lista de la compra con un ser querido, trabaje en un proyecto o planee unas vacaciones, capturar, compartir y completar tareas pendientes con Wunderlist es sencillo.</span><span class="sxs-lookup"><span data-stu-id="b82ec-105">Whether you’re sharing a grocery list with a loved one, working on a project, or planning a vacation, Wunderlist makes it easy to capture, share, and complete your to¬dos.</span></span> <span data-ttu-id="b82ec-106">Wunderlist sincroniza de forma instantánea su teléfono, tableta o PC para que pueda tener acceso a todas las tareas desde cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="b82ec-106">Wunderlist instantly syncs between your phone, tablet and computer, so you can access all your tasks from anywhere.</span></span>

<span data-ttu-id="b82ec-107">Empiece por crear una aplicación lógica ahora. Para ello, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b82ec-107">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-wunderlist"></a><span data-ttu-id="b82ec-108">Creación de una conexión a Wunderlist</span><span class="sxs-lookup"><span data-stu-id="b82ec-108">Create a connection to Wunderlist</span></span>
<span data-ttu-id="b82ec-109">Para crear aplicaciones lógicas con Wunderlist, primero necesita establecer una **conexión** y, después, especificar los detalles de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="b82ec-109">To create Logic apps with Wunderlist, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="b82ec-110">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b82ec-110">Property</span></span> | <span data-ttu-id="b82ec-111">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b82ec-111">Required</span></span> | <span data-ttu-id="b82ec-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="b82ec-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b82ec-113">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="b82ec-113">Token</span></span> |<span data-ttu-id="b82ec-114">Sí</span><span class="sxs-lookup"><span data-stu-id="b82ec-114">Yes</span></span> |<span data-ttu-id="b82ec-115">Proporciona las credenciales de Wunderlist.</span><span class="sxs-lookup"><span data-stu-id="b82ec-115">Provide Wunderlist Credentials</span></span> |

<span data-ttu-id="b82ec-116">Después de crear la conexión, puede usarla para ejecutar las acciones y escuchar los desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="b82ec-116">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Wunderlist](../../includes/connectors-create-api-wunderlist.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="b82ec-117">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="b82ec-117">Connector-specific details</span></span>

<span data-ttu-id="b82ec-118">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/wunderlist/).</span><span class="sxs-lookup"><span data-stu-id="b82ec-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/wunderlist/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="b82ec-119">Más conectores</span><span class="sxs-lookup"><span data-stu-id="b82ec-119">More connectors</span></span>
<span data-ttu-id="b82ec-120">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b82ec-120">Go back to the [APIs list](apis-list.md).</span></span>
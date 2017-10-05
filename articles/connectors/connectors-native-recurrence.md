---
title: "Adición del desencadenador de periodicidad en Logic Apps | Microsoft Docs"
description: "Información general sobre el desencadenador de periodicidad y cómo utilizarlo con una aplicación lógica de Azure."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="dbafb-103">Introducción al desencadenador de periodicidad</span><span class="sxs-lookup"><span data-stu-id="dbafb-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="dbafb-104">Con el desencadenador de periodicidad, puede crear flujos de trabajo eficaces en la nube.</span><span class="sxs-lookup"><span data-stu-id="dbafb-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="dbafb-105">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="dbafb-105">For example, you can:</span></span>

* <span data-ttu-id="dbafb-106">Programar un flujo de trabajo para ejecutar un procedimiento almacenado de SQL cada día.</span><span class="sxs-lookup"><span data-stu-id="dbafb-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="dbafb-107">Enviar por correo electrónico un resumen de todos los tweets de la última semana sobre un determinado hashtag.</span><span class="sxs-lookup"><span data-stu-id="dbafb-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="dbafb-108">Para empezar a usar la acción de periodicidad en una aplicación lógica, consulte [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="dbafb-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="dbafb-109">Uso de un desencadenador de periodicidad</span><span class="sxs-lookup"><span data-stu-id="dbafb-109">Use a recurrence trigger</span></span>
<span data-ttu-id="dbafb-110">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="dbafb-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="dbafb-111">[Más información sobre los desencadenadores](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dbafb-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="dbafb-112">Esta es una secuencia de ejemplo de cómo configurar un desencadenador de periodicidad en una aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="dbafb-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="dbafb-113">Agregue el desencadenador de **periodicidad** como primer paso en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="dbafb-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="dbafb-114">Rellene los parámetros para el intervalo de periodicidad.</span><span class="sxs-lookup"><span data-stu-id="dbafb-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="dbafb-115">La aplicación lógica inicia ahora una ejecución después de cada intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="dbafb-115">The logic app now starts a run after each interval of time.</span></span>

![Desencadenador HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="dbafb-117">Detalles del desencadenador</span><span class="sxs-lookup"><span data-stu-id="dbafb-117">Trigger details</span></span>
<span data-ttu-id="dbafb-118">El desencadenador de periodicidad tiene las siguientes propiedades que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="dbafb-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="dbafb-119">Active una aplicación lógica después de un intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="dbafb-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="dbafb-120">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="dbafb-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="dbafb-121">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="dbafb-121">Display name</span></span> | <span data-ttu-id="dbafb-122">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="dbafb-122">Property name</span></span> | <span data-ttu-id="dbafb-123">Description</span><span class="sxs-lookup"><span data-stu-id="dbafb-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbafb-124">Frecuencia*</span><span class="sxs-lookup"><span data-stu-id="dbafb-124">Frequency*</span></span> |<span data-ttu-id="dbafb-125">frequency</span><span class="sxs-lookup"><span data-stu-id="dbafb-125">frequency</span></span> |<span data-ttu-id="dbafb-126">La unidad de tiempo: `Second`, `Minute`, `Hour`, `Day` o `Year`.</span><span class="sxs-lookup"><span data-stu-id="dbafb-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="dbafb-127">Intervalo*</span><span class="sxs-lookup"><span data-stu-id="dbafb-127">Interval*</span></span> |<span data-ttu-id="dbafb-128">interval</span><span class="sxs-lookup"><span data-stu-id="dbafb-128">interval</span></span> |<span data-ttu-id="dbafb-129">Intervalo de frecuencia definido para la periodicidad.</span><span class="sxs-lookup"><span data-stu-id="dbafb-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="dbafb-130">Zona horaria</span><span class="sxs-lookup"><span data-stu-id="dbafb-130">Time Zone</span></span> |<span data-ttu-id="dbafb-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="dbafb-131">timeZone</span></span> |<span data-ttu-id="dbafb-132">Si se especifica una hora de inicio sin una diferencia horaria con UTC, se usará esta zona horaria.</span><span class="sxs-lookup"><span data-stu-id="dbafb-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="dbafb-133">Hora de inicio</span><span class="sxs-lookup"><span data-stu-id="dbafb-133">Start time</span></span> |<span data-ttu-id="dbafb-134">startTime</span><span class="sxs-lookup"><span data-stu-id="dbafb-134">startTime</span></span> |<span data-ttu-id="dbafb-135">Hora de inicio en [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="dbafb-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="dbafb-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dbafb-136">Next steps</span></span>
<span data-ttu-id="dbafb-137">Ahora, pruebe la plataforma y [cree una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="dbafb-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="dbafb-138">Puede explorar los demás conectores disponibles en aplicaciones lógicas consultando nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="dbafb-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>


---
title: "desencadenador de periodicidad de hello aaaAdd en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general de desencadenador de periodicidad de hello y cómo toouse con una aplicación de Azure lógica."
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
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="0ca69-103">Empezar a trabajar con el desencadenador de periodicidad de Hola</span><span class="sxs-lookup"><span data-stu-id="0ca69-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="0ca69-104">Mediante el uso de desencadenador de periodicidad de hello, puede crear flujos de trabajo eficaces en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ca69-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="0ca69-105">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="0ca69-105">For example, you can:</span></span>

* <span data-ttu-id="0ca69-106">Programar un toorun de flujo de trabajo un procedimiento almacenado SQL cada día.</span><span class="sxs-lookup"><span data-stu-id="0ca69-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="0ca69-107">Enviar por correo electrónico un resumen de todos los tweets dentro de la última semana acerca de un determinado hashtag Hola.</span><span class="sxs-lookup"><span data-stu-id="0ca69-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="0ca69-108">tooget a usar el desencadenador de periodicidad de hello en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0ca69-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="0ca69-109">Uso de un desencadenador de periodicidad</span><span class="sxs-lookup"><span data-stu-id="0ca69-109">Use a recurrence trigger</span></span>
<span data-ttu-id="0ca69-110">Un desencadenador es un evento que puede ser el flujo de trabajo hello toostart utilizado que se define en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="0ca69-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="0ca69-111">[Más información sobre los desencadenadores](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ca69-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="0ca69-112">Este es un ejemplo de secuencia de cómo tooset una una periodicidad desencadenar en una aplicación de lógica:</span><span class="sxs-lookup"><span data-stu-id="0ca69-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="0ca69-113">Agregar hello **periodicidad** desencadenador como primer paso en una aplicación de la lógica de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ca69-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="0ca69-114">Rellenar los parámetros de hello para el intervalo de periodicidad de saludo.</span><span class="sxs-lookup"><span data-stu-id="0ca69-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="0ca69-115">aplicación de la lógica de Hello ahora inicia una ejecución después de cada intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="0ca69-115">hello logic app now starts a run after each interval of time.</span></span>

![Desencadenador HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="0ca69-117">Detalles del desencadenador</span><span class="sxs-lookup"><span data-stu-id="0ca69-117">Trigger details</span></span>
<span data-ttu-id="0ca69-118">desencadenador de periodicidad de Hello tiene Hola propiedades que puede configurar siguientes.</span><span class="sxs-lookup"><span data-stu-id="0ca69-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="0ca69-119">Active una aplicación lógica después de un intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="0ca69-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="0ca69-120">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="0ca69-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="0ca69-121">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="0ca69-121">Display name</span></span> | <span data-ttu-id="0ca69-122">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="0ca69-122">Property name</span></span> | <span data-ttu-id="0ca69-123">Description</span><span class="sxs-lookup"><span data-stu-id="0ca69-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ca69-124">Frecuencia*</span><span class="sxs-lookup"><span data-stu-id="0ca69-124">Frequency*</span></span> |<span data-ttu-id="0ca69-125">frequency</span><span class="sxs-lookup"><span data-stu-id="0ca69-125">frequency</span></span> |<span data-ttu-id="0ca69-126">unidad de Hola de tiempo: `Second`, `Minute`, `Hour`, `Day`, o `Year`.</span><span class="sxs-lookup"><span data-stu-id="0ca69-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="0ca69-127">Intervalo*</span><span class="sxs-lookup"><span data-stu-id="0ca69-127">Interval*</span></span> |<span data-ttu-id="0ca69-128">interval</span><span class="sxs-lookup"><span data-stu-id="0ca69-128">interval</span></span> |<span data-ttu-id="0ca69-129">intervalo de saludo de hello dada la frecuencia de repetición de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ca69-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="0ca69-130">Zona horaria</span><span class="sxs-lookup"><span data-stu-id="0ca69-130">Time Zone</span></span> |<span data-ttu-id="0ca69-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="0ca69-131">timeZone</span></span> |<span data-ttu-id="0ca69-132">Si se especifica una hora de inicio sin una diferencia horaria con UTC, se usará esta zona horaria.</span><span class="sxs-lookup"><span data-stu-id="0ca69-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="0ca69-133">Hora de inicio</span><span class="sxs-lookup"><span data-stu-id="0ca69-133">Start time</span></span> |<span data-ttu-id="0ca69-134">startTime</span><span class="sxs-lookup"><span data-stu-id="0ca69-134">startTime</span></span> |<span data-ttu-id="0ca69-135">hora de inicio de Hello en [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="0ca69-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="0ca69-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ca69-136">Next steps</span></span>
<span data-ttu-id="0ca69-137">Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0ca69-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="0ca69-138">Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0ca69-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>


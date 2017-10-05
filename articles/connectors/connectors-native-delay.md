---
title: "Adición de retraso en Logic Apps | Microsoft Docs"
description: "Información general sobre las acciones de retraso y retraso hasta y cómo usarlas con una aplicación lógica de Azure."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="5d298-103">Introducción a las acciones de retraso y retraso hasta</span><span class="sxs-lookup"><span data-stu-id="5d298-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="5d298-104">Con las acciones de retraso y retraso hasta, puede completar escenarios de flujo de trabajo como los siguientes.</span><span class="sxs-lookup"><span data-stu-id="5d298-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="5d298-105">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="5d298-105">For example, you can:</span></span>

* <span data-ttu-id="5d298-106">Esperar hasta un día de la semana para enviar una actualización de estado por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="5d298-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="5d298-107">Retrasar el flujo de trabajo hasta que una llamada HTTP tenga tiempo para completarse antes de reanudarse y recuperar el resultado.</span><span class="sxs-lookup"><span data-stu-id="5d298-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="5d298-108">Para empezar a usar la acción de retraso en una aplicación lógica, consulte [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5d298-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="5d298-109">Uso de las acciones de retraso</span><span class="sxs-lookup"><span data-stu-id="5d298-109">Use the delay actions</span></span>
<span data-ttu-id="5d298-110">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="5d298-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="5d298-111">[Más información acerca de las acciones](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d298-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="5d298-112">Esta es una secuencia de ejemplo de cómo usar un paso de retraso en una aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="5d298-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="5d298-113">Después de agregar un desencadenador, haga clic en **Nuevo paso** para agregar una acción.</span><span class="sxs-lookup"><span data-stu-id="5d298-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="5d298-114">Busque **delay** para mostrar las acciones de retraso.</span><span class="sxs-lookup"><span data-stu-id="5d298-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="5d298-115">En este ejemplo, se seleccionará **Delay**.</span><span class="sxs-lookup"><span data-stu-id="5d298-115">In this example, we will select **Delay**.</span></span>
   
    ![Acciones de retraso](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="5d298-117">Complete cualquiera de las propiedades de acción para configurar el retraso.</span><span class="sxs-lookup"><span data-stu-id="5d298-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![Configuración de retraso](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="5d298-119">Haga clic en **Guardar** para publicar y activar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="5d298-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="5d298-120">Detalles de la acción</span><span class="sxs-lookup"><span data-stu-id="5d298-120">Action details</span></span>
<span data-ttu-id="5d298-121">El desencadenador de periodicidad tiene las siguientes propiedades que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="5d298-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="5d298-122">Acción de retraso</span><span class="sxs-lookup"><span data-stu-id="5d298-122">Delay action</span></span>
<span data-ttu-id="5d298-123">Esta acción retrasa la ejecución durante un determinado intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="5d298-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="5d298-124">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="5d298-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="5d298-125">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="5d298-125">Display name</span></span> | <span data-ttu-id="5d298-126">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="5d298-126">Property name</span></span> | <span data-ttu-id="5d298-127">Description</span><span class="sxs-lookup"><span data-stu-id="5d298-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d298-128">Recuento*</span><span class="sxs-lookup"><span data-stu-id="5d298-128">Count*</span></span> |<span data-ttu-id="5d298-129">count</span><span class="sxs-lookup"><span data-stu-id="5d298-129">count</span></span> |<span data-ttu-id="5d298-130">El número de unidades de tiempo de retraso</span><span class="sxs-lookup"><span data-stu-id="5d298-130">The number of time units to delay</span></span> |
| <span data-ttu-id="5d298-131">Unidad*</span><span class="sxs-lookup"><span data-stu-id="5d298-131">Unit*</span></span> |<span data-ttu-id="5d298-132">unit</span><span class="sxs-lookup"><span data-stu-id="5d298-132">unit</span></span> |<span data-ttu-id="5d298-133">La unidad de tiempo: `Second`, `Minute`, `Hour` o `Day`.</span><span class="sxs-lookup"><span data-stu-id="5d298-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="5d298-134">Acción de retraso hasta</span><span class="sxs-lookup"><span data-stu-id="5d298-134">Delay-until action</span></span>
<span data-ttu-id="5d298-135">Esta acción retrasa la ejecución hasta una fecha u hora especificada.</span><span class="sxs-lookup"><span data-stu-id="5d298-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="5d298-136">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="5d298-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="5d298-137">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="5d298-137">Display name</span></span> | <span data-ttu-id="5d298-138">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="5d298-138">Property name</span></span> | <span data-ttu-id="5d298-139">Description</span><span class="sxs-lookup"><span data-stu-id="5d298-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d298-140">Año*</span><span class="sxs-lookup"><span data-stu-id="5d298-140">Year*</span></span> |<span data-ttu-id="5d298-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="5d298-141">timestamp</span></span> |<span data-ttu-id="5d298-142">El año hasta el que retrasar (GMT)</span><span class="sxs-lookup"><span data-stu-id="5d298-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="5d298-143">Mes*</span><span class="sxs-lookup"><span data-stu-id="5d298-143">Month*</span></span> |<span data-ttu-id="5d298-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="5d298-144">timestamp</span></span> |<span data-ttu-id="5d298-145">El mes hasta el que retrasar (GMT)</span><span class="sxs-lookup"><span data-stu-id="5d298-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="5d298-146">Día*</span><span class="sxs-lookup"><span data-stu-id="5d298-146">Day*</span></span> |<span data-ttu-id="5d298-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="5d298-147">timestamp</span></span> |<span data-ttu-id="5d298-148">El día hasta el que retrasar (GMT)</span><span class="sxs-lookup"><span data-stu-id="5d298-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="5d298-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5d298-149">Next steps</span></span>
<span data-ttu-id="5d298-150">Ahora, pruebe la plataforma y [cree una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5d298-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5d298-151">Puede explorar los demás conectores disponibles en aplicaciones lógicas consultando nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5d298-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>


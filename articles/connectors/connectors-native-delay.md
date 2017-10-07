---
title: "un retraso en las aplicaciones lógicas aaaAdd | Documentos de Microsoft"
description: "Información general de hello retraso y retraso-hasta que las acciones y cómo toouse con una aplicación de Azure lógica."
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
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="fe394-103">Empezar a trabajar con hello retraso y retraso-hasta acciones</span><span class="sxs-lookup"><span data-stu-id="fe394-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="fe394-104">Mediante el uso de retraso de Hola y "retraso-hasta" acciones, puede completar los escenarios de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fe394-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="fe394-105">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="fe394-105">For example, you can:</span></span>

* <span data-ttu-id="fe394-106">Espere hasta que actualice un estado de día de la semana toosend por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="fe394-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="fe394-107">Flujo de trabajo de hello de retraso hasta que una llamada HTTP tiene toofinish de tiempo antes de reanudar y recuperar el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="fe394-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="fe394-108">tooget se hayan iniciado mediante la acción de retraso de hello en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fe394-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="fe394-109">Usar acciones de retraso de Hola</span><span class="sxs-lookup"><span data-stu-id="fe394-109">Use hello delay actions</span></span>
<span data-ttu-id="fe394-110">Una acción es una operación que se lleva a cabo por flujo de trabajo de Hola que se define en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="fe394-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="fe394-111">[Más información acerca de las acciones](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe394-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="fe394-112">Este es un ejemplo de secuencia de cómo toouse un retraso paso a paso en una aplicación de lógica:</span><span class="sxs-lookup"><span data-stu-id="fe394-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="fe394-113">Después de agregar un desencadenador, haga clic en **nuevo paso** tooadd una acción.</span><span class="sxs-lookup"><span data-stu-id="fe394-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="fe394-114">Busque **retraso** toobring las acciones de retraso de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe394-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="fe394-115">En este ejemplo, se seleccionará **Delay**.</span><span class="sxs-lookup"><span data-stu-id="fe394-115">In this example, we will select **Delay**.</span></span>
   
    ![Acciones de retraso](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="fe394-117">Siga cualquiera de retraso de hello acción propiedades tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="fe394-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![Configuración de retraso](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="fe394-119">Haga clic en **guardar** toopublish y activar la aplicación de la lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="fe394-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="fe394-120">Detalles de la acción</span><span class="sxs-lookup"><span data-stu-id="fe394-120">Action details</span></span>
<span data-ttu-id="fe394-121">desencadenador de periodicidad de Hello tiene Hola propiedades que se pueden configurar siguientes.</span><span class="sxs-lookup"><span data-stu-id="fe394-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="fe394-122">Acción de retraso</span><span class="sxs-lookup"><span data-stu-id="fe394-122">Delay action</span></span>
<span data-ttu-id="fe394-123">Ejecute este Hola de retrasos de acción para un intervalo de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="fe394-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="fe394-124">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="fe394-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="fe394-125">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="fe394-125">Display name</span></span> | <span data-ttu-id="fe394-126">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="fe394-126">Property name</span></span> | <span data-ttu-id="fe394-127">Description</span><span class="sxs-lookup"><span data-stu-id="fe394-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe394-128">Recuento*</span><span class="sxs-lookup"><span data-stu-id="fe394-128">Count*</span></span> |<span data-ttu-id="fe394-129">count</span><span class="sxs-lookup"><span data-stu-id="fe394-129">count</span></span> |<span data-ttu-id="fe394-130">número de Hola de toodelay de unidades de tiempo</span><span class="sxs-lookup"><span data-stu-id="fe394-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="fe394-131">Unidad*</span><span class="sxs-lookup"><span data-stu-id="fe394-131">Unit*</span></span> |<span data-ttu-id="fe394-132">unit</span><span class="sxs-lookup"><span data-stu-id="fe394-132">unit</span></span> |<span data-ttu-id="fe394-133">unidad de Hola de tiempo: `Second`, `Minute`, `Hour`, o`Day`</span><span class="sxs-lookup"><span data-stu-id="fe394-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="fe394-134">Acción de retraso hasta</span><span class="sxs-lookup"><span data-stu-id="fe394-134">Delay-until action</span></span>
<span data-ttu-id="fe394-135">Esta acción retrasa Hola ejecutar hasta una fecha u hora especificada.</span><span class="sxs-lookup"><span data-stu-id="fe394-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="fe394-136">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="fe394-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="fe394-137">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="fe394-137">Display name</span></span> | <span data-ttu-id="fe394-138">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="fe394-138">Property name</span></span> | <span data-ttu-id="fe394-139">Description</span><span class="sxs-lookup"><span data-stu-id="fe394-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe394-140">Año*</span><span class="sxs-lookup"><span data-stu-id="fe394-140">Year*</span></span> |<span data-ttu-id="fe394-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="fe394-141">timestamp</span></span> |<span data-ttu-id="fe394-142">Hola toodelay año hasta (GMT)</span><span class="sxs-lookup"><span data-stu-id="fe394-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="fe394-143">Mes*</span><span class="sxs-lookup"><span data-stu-id="fe394-143">Month*</span></span> |<span data-ttu-id="fe394-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="fe394-144">timestamp</span></span> |<span data-ttu-id="fe394-145">Hola toodelay mes hasta (GMT)</span><span class="sxs-lookup"><span data-stu-id="fe394-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="fe394-146">Día*</span><span class="sxs-lookup"><span data-stu-id="fe394-146">Day*</span></span> |<span data-ttu-id="fe394-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="fe394-147">timestamp</span></span> |<span data-ttu-id="fe394-148">Hola toodelay día hasta (GMT)</span><span class="sxs-lookup"><span data-stu-id="fe394-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="fe394-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe394-149">Next steps</span></span>
<span data-ttu-id="fe394-150">Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fe394-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="fe394-151">Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="fe394-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>


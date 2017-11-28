---
title: "acción de consulta de hello aaaAdd en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general de la acción de consulta de Hola para realizar acciones como matriz de filtro."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="32d99-103">Introducción a la acción de consulta de Hola</span><span class="sxs-lookup"><span data-stu-id="32d99-103">Get started with hello query action</span></span>
<span data-ttu-id="32d99-104">Mediante la acción de consulta de hello, puede trabajar con lotes y matrices tooaccomplish los flujos de trabajo:</span><span class="sxs-lookup"><span data-stu-id="32d99-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="32d99-105">Crear una tarea para todos los registros de alta prioridad desde una base de datos.</span><span class="sxs-lookup"><span data-stu-id="32d99-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="32d99-106">Guardar todos los datos adjuntos en PDF de correos electrónicos en un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="32d99-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="32d99-107">tooget se hayan iniciado mediante la acción de consulta de hello en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="32d99-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="32d99-108">Use la acción de consulta de Hola</span><span class="sxs-lookup"><span data-stu-id="32d99-108">Use hello query action</span></span>
<span data-ttu-id="32d99-109">Una acción es una operación que se lleva a cabo por flujo de trabajo de Hola que se define en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="32d99-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="32d99-110">[Más información acerca de las acciones](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32d99-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="32d99-111">acción de consulta de Hello tiene actualmente una operación, denominada matriz de filtro de hello, que se expone en el Diseñador de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d99-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="32d99-112">Esto permite tooquery una matriz y devolver un conjunto de resultados filtrados.</span><span class="sxs-lookup"><span data-stu-id="32d99-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="32d99-113">Este es el procedimiento para agregarlo en una aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="32d99-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="32d99-114">Seleccione hello **nuevo paso** botón.</span><span class="sxs-lookup"><span data-stu-id="32d99-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="32d99-115">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="32d99-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="32d99-116">En el cuadro de búsqueda de la acción de hello, escriba **filtro** hello toolist **matriz filtro** acción.</span><span class="sxs-lookup"><span data-stu-id="32d99-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Seleccione la acción de consulta de Hola](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="32d99-118">Seleccione un toofilter de matriz.</span><span class="sxs-lookup"><span data-stu-id="32d99-118">Select an array toofilter.</span></span> <span data-ttu-id="32d99-119">(hello captura de pantalla siguiente muestra hello matriz de resultados de búsqueda de Twitter.)</span><span class="sxs-lookup"><span data-stu-id="32d99-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="32d99-120">Crear una condición tooevaluate en cada elemento.</span><span class="sxs-lookup"><span data-stu-id="32d99-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="32d99-121">(Hola siguiente captura de pantalla de filtros de tweets de usuarios que tienen más de 100 seguidores).</span><span class="sxs-lookup"><span data-stu-id="32d99-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Acción de consulta de hello completa](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="32d99-123">acción de Hello darán como resultado una nueva matriz que contiene solo los resultados que cumplen los requisitos de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d99-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="32d99-124">Haga clic en la esquina superior izquierda de Hola de hello toosave de barra de herramientas y la lógica aplicación guardará ambos y publicar (activar).</span><span class="sxs-lookup"><span data-stu-id="32d99-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="32d99-125">Acción de consulta</span><span class="sxs-lookup"><span data-stu-id="32d99-125">Query action</span></span>
<span data-ttu-id="32d99-126">A continuación encontrará los detalles de hello para la acción de hello admitido por este conector.</span><span class="sxs-lookup"><span data-stu-id="32d99-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="32d99-127">Conector de Hello tiene una acción posible.</span><span class="sxs-lookup"><span data-stu-id="32d99-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="32d99-128">Acción</span><span class="sxs-lookup"><span data-stu-id="32d99-128">Action</span></span> | <span data-ttu-id="32d99-129">Description</span><span class="sxs-lookup"><span data-stu-id="32d99-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="32d99-130">Filter array</span><span class="sxs-lookup"><span data-stu-id="32d99-130">Filter array</span></span> |<span data-ttu-id="32d99-131">Evalúa una condición para cada elemento de una matriz y devuelve los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="32d99-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="32d99-132">Detalles de la acción</span><span class="sxs-lookup"><span data-stu-id="32d99-132">Action details</span></span>
<span data-ttu-id="32d99-133">acción de consulta de Hello incluye una acción posible.</span><span class="sxs-lookup"><span data-stu-id="32d99-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="32d99-134">Hello en las tablas siguientes se describen Hola necesarios y campos de entrada opcionales para acción de Hola y detalles salida correspondientes Hola que están asociados con el uso de la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d99-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="32d99-135">Filter array</span><span class="sxs-lookup"><span data-stu-id="32d99-135">Filter array</span></span>
<span data-ttu-id="32d99-136">los siguientes Hola son campos de entrada para la acción de hello, que realiza una solicitud de salida HTTP.</span><span class="sxs-lookup"><span data-stu-id="32d99-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="32d99-137">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="32d99-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="32d99-138">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="32d99-138">Display name</span></span> | <span data-ttu-id="32d99-139">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="32d99-139">Property name</span></span> | <span data-ttu-id="32d99-140">Description</span><span class="sxs-lookup"><span data-stu-id="32d99-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32d99-141">De*</span><span class="sxs-lookup"><span data-stu-id="32d99-141">From*</span></span> |<span data-ttu-id="32d99-142">De</span><span class="sxs-lookup"><span data-stu-id="32d99-142">from</span></span> |<span data-ttu-id="32d99-143">Hola matriz toofilter</span><span class="sxs-lookup"><span data-stu-id="32d99-143">hello array toofilter</span></span> |
| <span data-ttu-id="32d99-144">Condición*</span><span class="sxs-lookup"><span data-stu-id="32d99-144">Condition*</span></span> |<span data-ttu-id="32d99-145">donde</span><span class="sxs-lookup"><span data-stu-id="32d99-145">where</span></span> |<span data-ttu-id="32d99-146">Hola tooevaluate de condición para cada elemento</span><span class="sxs-lookup"><span data-stu-id="32d99-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="32d99-147">Detalles de salida</span><span class="sxs-lookup"><span data-stu-id="32d99-147">Output details</span></span>
<span data-ttu-id="32d99-148">siguiente Hola es detalles de salida de respuesta HTTP Hola.</span><span class="sxs-lookup"><span data-stu-id="32d99-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="32d99-149">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="32d99-149">Property name</span></span> | <span data-ttu-id="32d99-150">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="32d99-150">Data type</span></span> | <span data-ttu-id="32d99-151">Description</span><span class="sxs-lookup"><span data-stu-id="32d99-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32d99-152">Matriz filtrada</span><span class="sxs-lookup"><span data-stu-id="32d99-152">Filtered array</span></span> |<span data-ttu-id="32d99-153">array</span><span class="sxs-lookup"><span data-stu-id="32d99-153">array</span></span> |<span data-ttu-id="32d99-154">Una matriz que contiene un objeto de cada resultado filtrado</span><span class="sxs-lookup"><span data-stu-id="32d99-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="32d99-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32d99-155">Next steps</span></span>
<span data-ttu-id="32d99-156">Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="32d99-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="32d99-157">Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="32d99-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>


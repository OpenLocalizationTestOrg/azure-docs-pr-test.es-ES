---
title: "Adición de la acción de consulta a Logic Apps | Microsoft Docs"
description: "En este artículo se muestra información general sobre las acciones de consulta para realizar acciones como Filter array (Filtrar matriz)."
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
ms.openlocfilehash: a992fa17a07d6167297c4cf5fe9fb3b58181d7df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="8e8f7-103">Introducción a la acción de consulta</span><span class="sxs-lookup"><span data-stu-id="8e8f7-103">Get started with the query action</span></span>
<span data-ttu-id="8e8f7-104">Mediante la acción de consulta puede utilizar lotes y matrices para realizar flujos de trabajo como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="8e8f7-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="8e8f7-105">Crear una tarea para todos los registros de alta prioridad desde una base de datos.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="8e8f7-106">Guardar todos los datos adjuntos en PDF de correos electrónicos en un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="8e8f7-107">Para empezar a usar la acción de consulta en una aplicación lógica, consulte [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="8e8f7-108">Uso de la acción de consulta</span><span class="sxs-lookup"><span data-stu-id="8e8f7-108">Use the query action</span></span>
<span data-ttu-id="8e8f7-109">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="8e8f7-110">[Más información acerca de las acciones](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="8e8f7-111">En estos momentos, la acción de consulta tiene una operación expuesta en el diseñador que se denomina Filter array (Filtrar matriz).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="8e8f7-112">Gracias a ella, podrá consultar una matriz y devolver un conjunto de resultados filtrados.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="8e8f7-113">Este es el procedimiento para agregarlo en una aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="8e8f7-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="8e8f7-114">Seleccione el botón **Nuevo paso** .</span><span class="sxs-lookup"><span data-stu-id="8e8f7-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="8e8f7-115">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="8e8f7-116">En el cuadro de búsqueda de la acción, escriba **Filtrar** para mostrar la acción **Filtrar matriz**.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![Seleccione la acción de consulta](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="8e8f7-118">Seleccione la matriz que se va a filtrar.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-118">Select an array to filter.</span></span> <span data-ttu-id="8e8f7-119">(La captura de pantalla siguiente muestra la matriz de resultados de búsqueda de Twitter).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="8e8f7-120">Cree una condición para evaluar en cada elemento.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="8e8f7-121">(La captura de pantalla siguiente filtra tweets de usuarios que tienen más de 100 seguidores).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Complete la acción de consulta](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="8e8f7-123">La acción generará una nueva matriz que contiene solo los resultados que cumplen los requisitos de filtro.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="8e8f7-124">Haga clic en la esquina superior izquierda de la barra de herramientas para guardarla; la aplicación lógica se guardará y se publicará (activará).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="8e8f7-125">Acción de consulta</span><span class="sxs-lookup"><span data-stu-id="8e8f7-125">Query action</span></span>
<span data-ttu-id="8e8f7-126">Aquí se muestran los detalles de la acción que admite este conector.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-126">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="8e8f7-127">El conector tiene una acción posible.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-127">The connector has one possible action.</span></span>

| <span data-ttu-id="8e8f7-128">Acción</span><span class="sxs-lookup"><span data-stu-id="8e8f7-128">Action</span></span> | <span data-ttu-id="8e8f7-129">Description</span><span class="sxs-lookup"><span data-stu-id="8e8f7-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e8f7-130">Filter array</span><span class="sxs-lookup"><span data-stu-id="8e8f7-130">Filter array</span></span> |<span data-ttu-id="8e8f7-131">Evalúa una condición de cada elemento de una matriz y devuelve los resultados</span><span class="sxs-lookup"><span data-stu-id="8e8f7-131">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="8e8f7-132">Detalles de la acción</span><span class="sxs-lookup"><span data-stu-id="8e8f7-132">Action details</span></span>
<span data-ttu-id="8e8f7-133">La acción de consulta incluye una acción posible.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-133">The query action comes with one possible action.</span></span> <span data-ttu-id="8e8f7-134">Las tablas siguientes describen los campos de entrada obligatorios y opcionales para la acción y los detalles de salida correspondientes asociados a su uso.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="8e8f7-135">Filter array</span><span class="sxs-lookup"><span data-stu-id="8e8f7-135">Filter array</span></span>
<span data-ttu-id="8e8f7-136">Los siguientes son los campos de entrada para la acción que realiza una solicitud de salida HTTP.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-136">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="8e8f7-137">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="8e8f7-138">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="8e8f7-138">Display name</span></span> | <span data-ttu-id="8e8f7-139">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="8e8f7-139">Property name</span></span> | <span data-ttu-id="8e8f7-140">Description</span><span class="sxs-lookup"><span data-stu-id="8e8f7-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e8f7-141">De*</span><span class="sxs-lookup"><span data-stu-id="8e8f7-141">From*</span></span> |<span data-ttu-id="8e8f7-142">from</span><span class="sxs-lookup"><span data-stu-id="8e8f7-142">from</span></span> |<span data-ttu-id="8e8f7-143">La matriz que se va a filtrar.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-143">The array to filter</span></span> |
| <span data-ttu-id="8e8f7-144">Condición*</span><span class="sxs-lookup"><span data-stu-id="8e8f7-144">Condition*</span></span> |<span data-ttu-id="8e8f7-145">donde</span><span class="sxs-lookup"><span data-stu-id="8e8f7-145">where</span></span> |<span data-ttu-id="8e8f7-146">La condición que se va a evaluar en cada elemento.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-146">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="8e8f7-147">Detalles de salida</span><span class="sxs-lookup"><span data-stu-id="8e8f7-147">Output details</span></span>
<span data-ttu-id="8e8f7-148">Los detalles de la salida de la respuesta HTTP son los siguientes.</span><span class="sxs-lookup"><span data-stu-id="8e8f7-148">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="8e8f7-149">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="8e8f7-149">Property name</span></span> | <span data-ttu-id="8e8f7-150">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="8e8f7-150">Data type</span></span> | <span data-ttu-id="8e8f7-151">Description</span><span class="sxs-lookup"><span data-stu-id="8e8f7-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e8f7-152">Matriz filtrada</span><span class="sxs-lookup"><span data-stu-id="8e8f7-152">Filtered array</span></span> |<span data-ttu-id="8e8f7-153">array</span><span class="sxs-lookup"><span data-stu-id="8e8f7-153">array</span></span> |<span data-ttu-id="8e8f7-154">Una matriz que contiene un objeto de cada resultado filtrado</span><span class="sxs-lookup"><span data-stu-id="8e8f7-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8e8f7-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e8f7-155">Next steps</span></span>
<span data-ttu-id="8e8f7-156">Ahora, pruebe la plataforma y [cree una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="8e8f7-157">Puede explorar los demás conectores disponibles en aplicaciones lógicas consultando nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8e8f7-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>


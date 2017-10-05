---
title: Embudos de Azure Application Insights
description: "Obtenga información sobre cómo usar Funnels para descubrir la forma en que los clientes interactúan con la aplicación."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 85f47daaaff8967eb83c330bab839023f128b486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="5681a-103">Descubra cómo los clientes usan la aplicación con los embudos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5681a-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="5681a-104">Conocer la experiencia de los clientes es de suma importancia para su negocio.</span><span class="sxs-lookup"><span data-stu-id="5681a-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="5681a-105">Si la aplicación implica varias fases, debe saber si la mayoría de los clientes avanzan a través de todo el proceso, o si finalizan el proceso en algún momento.</span><span class="sxs-lookup"><span data-stu-id="5681a-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="5681a-106">La progresión a través de una serie de pasos en una aplicación web se conoce como "embudo".</span><span class="sxs-lookup"><span data-stu-id="5681a-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="5681a-107">Puede usar los embudos de Application Insights para obtener información sobre los usuarios y supervisar las tasas de conversión paso a paso.</span><span class="sxs-lookup"><span data-stu-id="5681a-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="5681a-108">Introducción a la hoja Embudos</span><span class="sxs-lookup"><span data-stu-id="5681a-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="5681a-109">La manera más fácil de obtener información sobre los embudos es a través de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5681a-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="5681a-110">En las siguientes ilustraciones se muestran los pasos que los propietarios de un negocio de comercio electrónico deberían seguir para obtener información sobre cómo sus clientes interactúan con su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5681a-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="5681a-111">Creación de un embudo</span><span class="sxs-lookup"><span data-stu-id="5681a-111">Create your funnel</span></span>
<span data-ttu-id="5681a-112">Antes de crear el embudo, debe decidir la pregunta a la que quiere obtener respuesta.</span><span class="sxs-lookup"><span data-stu-id="5681a-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="5681a-113">Por ejemplo, podría plantearse cuántos clientes de los que visitan su página principal hacen clic en un anuncio.</span><span class="sxs-lookup"><span data-stu-id="5681a-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="5681a-114">En este ejemplo, los propietarios de la empresa Fabrikam Fiber desean saber el porcentaje de clientes que realizan una compra después de agregar artículos a la cesta durante el último mes.</span><span class="sxs-lookup"><span data-stu-id="5681a-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="5681a-115">Estos son los pasos que deben seguir para crear un embudo.</span><span class="sxs-lookup"><span data-stu-id="5681a-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="5681a-116">Haga clic en el botón Nuevo en la hoja Embudos.</span><span class="sxs-lookup"><span data-stu-id="5681a-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="5681a-117">Seleccione el intervalo de tiempo "Último mes" en la lista desplegable **Intervalo de tiempo**.</span><span class="sxs-lookup"><span data-stu-id="5681a-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="5681a-118">Seleccione el evento **Página del producto** en la lista desplegable **Paso 1**.</span><span class="sxs-lookup"><span data-stu-id="5681a-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="5681a-119">Seleccione el evento **Añadir a cesta** en la lista desplegable **Paso 2**.</span><span class="sxs-lookup"><span data-stu-id="5681a-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="5681a-120">Seleccione el evento **Haga clic en Comprar** en la lista desplegable **Paso 3**.</span><span class="sxs-lookup"><span data-stu-id="5681a-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="5681a-121">Agregue un nombre para el embudo y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5681a-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="5681a-122">En la siguiente ilustración se muestran los datos que la hoja Embudos genera.</span><span class="sxs-lookup"><span data-stu-id="5681a-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="5681a-123">Desde aquí los propietarios de Fabrikam pueden ver que, durante la última semana, el 22,7 % de los clientes que han agregado algún artículo a la cesta han completado la compra.</span><span class="sxs-lookup"><span data-stu-id="5681a-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="5681a-124">También pueden ver que el 1% de los clientes hicieron clic en un anuncio antes de visitar la página del producto y que el 20% de los clientes cerraron la sesión después de completar la compra.</span><span class="sxs-lookup"><span data-stu-id="5681a-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Hoja Embudos con datos](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="5681a-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5681a-126">Next steps</span></span>
- <span data-ttu-id="5681a-127">Obtenga más información sobre los [análisis de uso](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5681a-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 

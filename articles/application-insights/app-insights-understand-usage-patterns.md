---
title: "aaaAzure Embudos de visión de aplicación"
description: "Obtenga información acerca de cómo puede utilizar Embudos toodiscover cómo interactúan los clientes con la aplicación."
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
ms.openlocfilehash: 3a90cfd11cb193e303136504df44008ffd04a290
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="20ff3-103">Descubra cómo los clientes están usando la aplicación con hello Embudos de visión de aplicación</span><span class="sxs-lookup"><span data-stu-id="20ff3-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="20ff3-104">Experiencia del usuario de descripción es de negocio de tooyour de hello máxima importancia.</span><span class="sxs-lookup"><span data-stu-id="20ff3-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="20ff3-105">Si la aplicación implica varias fases, necesitará tooknow si la mayoría de los clientes avanzan por proceso completo de hello, o si está finalizando el proceso de hello en algún momento.</span><span class="sxs-lookup"><span data-stu-id="20ff3-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="20ff3-106">progresión de Hola a través de una serie de pasos en una aplicación web se conoce como "embudo".</span><span class="sxs-lookup"><span data-stu-id="20ff3-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="20ff3-107">Puede usar Hola aplicación visión Embudos toogain visiones los usuarios y los tipos de conversión paso a paso de monitor.</span><span class="sxs-lookup"><span data-stu-id="20ff3-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="20ff3-108">Introducción a la hoja de Embudos Hola</span><span class="sxs-lookup"><span data-stu-id="20ff3-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="20ff3-109">Hola toolearn de manera más fácil sobre Embudos es toowalk aunque muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="20ff3-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="20ff3-110">Hello en las ilustraciones siguientes muestran los propietarios de pasos de Hola de una empresa de comercio electrónico tardaría toolearn cómo interactúan los clientes con su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="20ff3-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="20ff3-111">Creación de un embudo</span><span class="sxs-lookup"><span data-stu-id="20ff3-111">Create your funnel</span></span>
<span data-ttu-id="20ff3-112">Antes de crear el embudo, necesita toodecide en la pregunta de hello desea tooanswer.</span><span class="sxs-lookup"><span data-stu-id="20ff3-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="20ff3-113">Por ejemplo, puede tooknow cuántos clientes ver el página principal, haga clic en un anuncio.</span><span class="sxs-lookup"><span data-stu-id="20ff3-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="20ff3-114">En este ejemplo, los propietarios de Hola de hello empresa Fabrikam Fiber deseen porcentaje de hello tooknow de clientes que realizan una compra después de agregar tootheir elementos carro de la compra durante el último mes Hola.</span><span class="sxs-lookup"><span data-stu-id="20ff3-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="20ff3-115">Estos son los pasos de hello toman toocreate su embudo.</span><span class="sxs-lookup"><span data-stu-id="20ff3-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="20ff3-116">Haga clic en botón nuevo de hello en la hoja de Embudos Hola.</span><span class="sxs-lookup"><span data-stu-id="20ff3-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="20ff3-117">Seleccionar intervalo de tiempo de Hola de "Último mes" de hello **intervalo de tiempo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="20ff3-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="20ff3-118">Seleccione hello **página del producto** eventos de hello **paso 1** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="20ff3-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="20ff3-119">Seleccione hello **agregar tooshopping carro** eventos de hello **paso 2** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="20ff3-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="20ff3-120">Seleccione hello **haga clic en compra** eventos de hello **paso 3** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="20ff3-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="20ff3-121">Agregar un embudo de toohello de nombre y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="20ff3-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="20ff3-122">Hello en la ilustración siguiente se muestra hello data Hola Embudos módulo genera.</span><span class="sxs-lookup"><span data-stu-id="20ff3-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="20ff3-123">Desde aquí Hola propietarios de Fabrikam pueden ver que, durante la última semana hello, 22.7% de los clientes que se agregan un elemento tootheir la compra carro compra Hola completada.</span><span class="sxs-lookup"><span data-stu-id="20ff3-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="20ff3-124">También puede ver que 1% de los clientes de hello hace clic en un anuncio antes de visitar la página del producto hello y 20% de sus clientes la sesión después de completar su compra.</span><span class="sxs-lookup"><span data-stu-id="20ff3-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Hoja Embudos con datos](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="20ff3-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20ff3-126">Next steps</span></span>
- <span data-ttu-id="20ff3-127">Obtenga más información sobre los [análisis de uso](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20ff3-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 

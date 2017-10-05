---
title: "Implementación de Azure Mobile Engagement para una aplicación de juegos"
description: "Escenario de aplicación de juegos para implementar Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="47ae3-103">Implementación de Mobile Engagement con una aplicación de juegos</span><span class="sxs-lookup"><span data-stu-id="47ae3-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="47ae3-104">Información general</span><span class="sxs-lookup"><span data-stu-id="47ae3-104">Overview</span></span>
<span data-ttu-id="47ae3-105">Una nueva empresa de juegos ha lanzado una aplicación de juego de estrategia/juego de rol dedicada a la pesca.</span><span class="sxs-lookup"><span data-stu-id="47ae3-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="47ae3-106">El juego lleva 6 meses en activo.</span><span class="sxs-lookup"><span data-stu-id="47ae3-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="47ae3-107">Ha cosechado un gran éxito, con millones de descargas, y la retención es muy alta en comparación con otras aplicaciones de juego de nuevas empresas.</span><span class="sxs-lookup"><span data-stu-id="47ae3-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="47ae3-108">En la reunión de revisión trimestral, las partes interesadas están de acuerdo en que necesitan aumentar los ingresos medios por usuario (ARPU).</span><span class="sxs-lookup"><span data-stu-id="47ae3-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="47ae3-109">Los módulos premium en el juego están disponibles como ofertas especiales.</span><span class="sxs-lookup"><span data-stu-id="47ae3-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="47ae3-110">Estos módulos de juego permiten a los usuarios actualizar la apariencia y el rendimiento de los sedales y los cebos o aparejos en el juego.</span><span class="sxs-lookup"><span data-stu-id="47ae3-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="47ae3-111">Sin embargo, las ventas de módulos son muy bajas.</span><span class="sxs-lookup"><span data-stu-id="47ae3-111">However, package sales are very low.</span></span> <span data-ttu-id="47ae3-112">Por tanto, deciden en primer lugar analizar la experiencia del cliente con una herramienta de análisis y después desarrollar un programa de compromiso para aumentar las ventas mediante la segmentación avanzada.</span><span class="sxs-lookup"><span data-stu-id="47ae3-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="47ae3-113">Partiendo de [Azure Mobile Engagement: Guía de introducción con procedimientos recomendados](mobile-engagement-getting-started-best-practices.md) , crean una estrategia de compromiso.</span><span class="sxs-lookup"><span data-stu-id="47ae3-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="47ae3-114">Objetivos y KPI</span><span class="sxs-lookup"><span data-stu-id="47ae3-114">Objectives and KPIs</span></span>
<span data-ttu-id="47ae3-115">Las partes interesadas clave para el juego se reúnen.</span><span class="sxs-lookup"><span data-stu-id="47ae3-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="47ae3-116">Todos están de acuerdo en un objetivo principal: aumentar las ventas de módulos premium en un 15%.</span><span class="sxs-lookup"><span data-stu-id="47ae3-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="47ae3-117">Crean indicadores clave de rendimiento (KPI) de negocio para medir y promover este objetivo.</span><span class="sxs-lookup"><span data-stu-id="47ae3-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="47ae3-118">¿En qué nivel del juego se compran estos módulos?</span><span class="sxs-lookup"><span data-stu-id="47ae3-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="47ae3-119">¿Cuáles son los ingresos por usuario, por sesión, por semana y por mes?</span><span class="sxs-lookup"><span data-stu-id="47ae3-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="47ae3-120">¿Cuáles son los tipos favoritos de compra?</span><span class="sxs-lookup"><span data-stu-id="47ae3-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="47ae3-121">En la parte 1 de la [Guía de introducción](mobile-engagement-getting-started-best-practices.md) , se explica cómo definir los objetivos y los KPI.</span><span class="sxs-lookup"><span data-stu-id="47ae3-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="47ae3-122">Con los KPI de negocio ya definidos, la encargada de productos móviles crea los KPI de compromiso para determinar la retención y las nuevas tendencias de usuarios.</span><span class="sxs-lookup"><span data-stu-id="47ae3-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="47ae3-123">Supervisar la retención y el uso en los siguientes intervalos: a diario, cada 2 días, semanalmente, mensualmente y cada tres meses</span><span class="sxs-lookup"><span data-stu-id="47ae3-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="47ae3-124">Recuentos de usuarios activos</span><span class="sxs-lookup"><span data-stu-id="47ae3-124">Active user counts</span></span>
* <span data-ttu-id="47ae3-125">La clasificación de la aplicación en la tienda</span><span class="sxs-lookup"><span data-stu-id="47ae3-125">The app rating in the store</span></span>

<span data-ttu-id="47ae3-126">Según las recomendaciones del equipo de TI, se han agregado los siguientes KPI técnicos para responder a las preguntas siguientes:</span><span class="sxs-lookup"><span data-stu-id="47ae3-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="47ae3-127">¿Cuál es la ruta de acceso de los usuarios (qué página visitan, cuánto tiempo pasan los usuarios en ella)?</span><span class="sxs-lookup"><span data-stu-id="47ae3-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="47ae3-128">Número de bloqueos o errores encontrados por sesión</span><span class="sxs-lookup"><span data-stu-id="47ae3-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="47ae3-129">¿Qué versiones de sistema operativo ejecutan mis usuarios?</span><span class="sxs-lookup"><span data-stu-id="47ae3-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="47ae3-130">¿Cuál es el tamaño medio de pantalla de mis usuarios?</span><span class="sxs-lookup"><span data-stu-id="47ae3-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="47ae3-131">¿Qué tipo de conectividad de Internet tienen mis usuarios?</span><span class="sxs-lookup"><span data-stu-id="47ae3-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="47ae3-132">Para cada KPI, la encargada de productos móviles especifica los datos que necesita y dónde se encuentran en su cuaderno de estrategias.</span><span class="sxs-lookup"><span data-stu-id="47ae3-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="47ae3-133">Programa de compromiso e integración</span><span class="sxs-lookup"><span data-stu-id="47ae3-133">Engagement program and integration</span></span>
<span data-ttu-id="47ae3-134">Antes de crear un programa avanzado de compromiso, el director de proyectos móviles a cargo del proyecto debe comprender a fondo cómo y cuándo los usuarios consumen los productos.</span><span class="sxs-lookup"><span data-stu-id="47ae3-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="47ae3-135">Después de 3 meses, el director de proyectos móviles ha recopilado datos suficientes para mejorar las ventas por notificación push en aplicación.</span><span class="sxs-lookup"><span data-stu-id="47ae3-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="47ae3-136">Descubre que:</span><span class="sxs-lookup"><span data-stu-id="47ae3-136">He learns that:</span></span>

* <span data-ttu-id="47ae3-137">La primera compra generalmente se produce en el nivel 14.</span><span class="sxs-lookup"><span data-stu-id="47ae3-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="47ae3-138">En el 90% de los casos, la compra es de nuevas armas legendarias por 3 USD.</span><span class="sxs-lookup"><span data-stu-id="47ae3-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="47ae3-139">En el 80% de los casos, los usuarios que han realizado una compra siguen usando el producto y hacen más compras.</span><span class="sxs-lookup"><span data-stu-id="47ae3-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="47ae3-140">Los usuarios que han superado el nivel 20 empiezan a gastar más de 10 USD por semana.</span><span class="sxs-lookup"><span data-stu-id="47ae3-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="47ae3-141">Los usuarios tienden a comprar módulos premium en los niveles 16, 24 y 32.</span><span class="sxs-lookup"><span data-stu-id="47ae3-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="47ae3-142">Gracias a este análisis, el director de proyectos móviles decide crear secuencias específicas de notificaciones push para aumentar las ventas en aplicación.</span><span class="sxs-lookup"><span data-stu-id="47ae3-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="47ae3-143">Crea tres secuencias push denominadas: Programa de bienvenida, Programa de ventas y Programa de inactivos.</span><span class="sxs-lookup"><span data-stu-id="47ae3-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="47ae3-144">Para obtener más información, consulte el [guías](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="47ae3-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->

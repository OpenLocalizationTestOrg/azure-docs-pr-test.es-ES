---
title: "implementación de Mobile Engagement aaaAzure para la aplicación de juegos"
description: "Tooimplement de escenario de aplicación de juegos Azure Mobile Engagement"
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
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="1fd3a-103">Implementación de Mobile Engagement con una aplicación de juegos</span><span class="sxs-lookup"><span data-stu-id="1fd3a-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="1fd3a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1fd3a-104">Overview</span></span>
<span data-ttu-id="1fd3a-105">Una nueva empresa de juegos ha lanzado una aplicación de juego de estrategia/juego de rol dedicada a la pesca.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="1fd3a-106">juego Hola ha estado ejecutando durante 6 meses.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="1fd3a-107">Este juego es una enorme se ejecuta correctamente y tiene millones de descargas y retención de hello es muy alta tooother comparados inicio juego aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="1fd3a-108">En la reunión de revisión trimestral de hello, las partes interesadas acuerdan que necesitan tooincrease ingresos medios por usuario (ARPU).</span><span class="sxs-lookup"><span data-stu-id="1fd3a-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="1fd3a-109">Los módulos premium en el juego están disponibles como ofertas especiales.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="1fd3a-110">Estos módulos de juegos permiten la apariencia de los usuarios tooupgrade Hola y el rendimiento de sus líneas de pesca y cebos para o enfrenta en juego Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="1fd3a-111">Sin embargo, las ventas de módulos son muy bajas.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-111">However, package sales are very low.</span></span> <span data-ttu-id="1fd3a-112">Por lo que deciden primer cliente de hello tooanalyze experiencia con una herramienta de análisis y, a continuación, toodevelop una interacción programa tooincrease ventas mediante avanzado segmentación.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="1fd3a-113">En función de hello [Azure Mobile Engagement - Guía de introducción a los procedimientos recomendados](mobile-engagement-getting-started-best-practices.md) , crear una estrategia de contratación.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="1fd3a-114">Objetivos y KPI</span><span class="sxs-lookup"><span data-stu-id="1fd3a-114">Objectives and KPIs</span></span>
<span data-ttu-id="1fd3a-115">Cumplir con las partes interesadas para el juego de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="1fd3a-116">Todos los equipos acuerdan un objetivo principal - tooincrease ventas de paquete premium en un 15%.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="1fd3a-117">Crear unidad y los indicadores clave de rendimiento (KPI) empresariales toomeasure este objetivo</span><span class="sxs-lookup"><span data-stu-id="1fd3a-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="1fd3a-118">¿En qué nivel de juego Hola se compran estos paquetes?</span><span class="sxs-lookup"><span data-stu-id="1fd3a-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="1fd3a-119">¿Qué es ingresos de Hola por usuario, por sesión, por semana y al mes?</span><span class="sxs-lookup"><span data-stu-id="1fd3a-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="1fd3a-120">¿Qué tipos de compra favoritos Hola?</span><span class="sxs-lookup"><span data-stu-id="1fd3a-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="1fd3a-121">Parte 1 de hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explica cómo toodefine Hola objetivos y los KPI.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="1fd3a-122">Con hello que KPI comerciales ya definido, Hola Mobile producto Manager crea la retención y tendencias de KPI de contratación toodetermine nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="1fd3a-123">Supervisar la retención y usar a través de hello siguientes intervalos: diariamente, cada 2 días, semanales, mensuales y cada tres meses.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="1fd3a-124">Recuentos de usuarios activos</span><span class="sxs-lookup"><span data-stu-id="1fd3a-124">Active user counts</span></span>
* <span data-ttu-id="1fd3a-125">clasificación de aplicación Hola Hola almacenar</span><span class="sxs-lookup"><span data-stu-id="1fd3a-125">hello app rating in hello store</span></span>

<span data-ttu-id="1fd3a-126">En función de las recomendaciones del equipo de TI de hello, Hola siguientes KPI técnica se agregaron hello tooanswer siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="1fd3a-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="1fd3a-127">¿Cuál es la ruta de acceso de los usuarios (qué página visitan, cuánto tiempo pasan los usuarios en ella)?</span><span class="sxs-lookup"><span data-stu-id="1fd3a-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="1fd3a-128">Número de bloqueos o errores encontrados por sesión</span><span class="sxs-lookup"><span data-stu-id="1fd3a-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="1fd3a-129">¿Qué versiones de sistema operativo ejecutan mis usuarios?</span><span class="sxs-lookup"><span data-stu-id="1fd3a-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="1fd3a-130">¿Qué es el tamaño medio de Hola de pantalla para Mis usuarios?</span><span class="sxs-lookup"><span data-stu-id="1fd3a-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="1fd3a-131">¿Qué tipo de conectividad de Internet tienen mis usuarios?</span><span class="sxs-lookup"><span data-stu-id="1fd3a-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="1fd3a-132">Para cada KPI Hola Mobile producto Manager especifica los datos de Hola que necesita y donde se encuentra en la guía.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="1fd3a-133">Programa de compromiso e integración</span><span class="sxs-lookup"><span data-stu-id="1fd3a-133">Engagement program and integration</span></span>
<span data-ttu-id="1fd3a-134">Antes de compilar un programa de interacción avanzada, Hola Director de proyecto móvil responsable de proyecto de Hola debe tener un conocimiento profundo de cómo y cuándo productos son consumidos por los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="1fd3a-135">Después de 3 meses, Hola Director de proyecto móvil ha recopilado suficiente tooenhance datos sus ventas de notificación de inserción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="1fd3a-136">Descubre que:</span><span class="sxs-lookup"><span data-stu-id="1fd3a-136">He learns that:</span></span>

* <span data-ttu-id="1fd3a-137">primera compra de Hello generalmente se produce en el nivel de hello 14.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="1fd3a-138">Durante el 90% de los casos, compra hello es nuevas armas legendario para $3.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="1fd3a-139">En el 80% de los casos, los usuarios que hayan realizado ninguna compra, continuar con el producto de Hola y hacer más compras.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="1fd3a-140">Los usuarios que han superado el nivel de hello 20, inicie toospend más de 10 $/ semana.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="1fd3a-141">Los usuarios suelen toobuy paquetes de premium en nivel 16, 24 y 32.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="1fd3a-142">Gracias a analysis toothis Hola Director de proyecto móvil decide toocreate inserción específico notificación secuencias tooincrease en las ventas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="1fd3a-143">Crea tres secuencias push denominadas: Programa de bienvenida, Programa de ventas y Programa de inactivos.</span><span class="sxs-lookup"><span data-stu-id="1fd3a-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="1fd3a-144">Para obtener más información, consulte toohello [guías](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="1fd3a-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->

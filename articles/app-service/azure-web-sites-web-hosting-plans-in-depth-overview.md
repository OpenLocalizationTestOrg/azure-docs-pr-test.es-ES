---
title: "Introducción detallada sobre los planes de Azure App Service | Microsoft Docs"
description: "Obtenga información acerca de cómo funcionan los planes del Servicio de aplicaciones de Azure y cómo benefician a su experiencia de administración."
keywords: servicio de aplicaciones, servicio de aplicaciones de azure, escala, escalable, plan del servicio de aplicaciones, costo del servicio de aplicaciones
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="aafd2-104">Introducción detallada sobre los planes del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="aafd2-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="aafd2-105">Los planes de App Service representan la colección de recursos físicos usados para hospedar sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aafd2-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="aafd2-106">Los planes de App Service definen lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="aafd2-106">App Service plans define:</span></span>

- <span data-ttu-id="aafd2-107">Región (oeste de EE. UU., este de EE. UU., etc.)</span><span class="sxs-lookup"><span data-stu-id="aafd2-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="aafd2-108">Recuento de escala (uno, dos, tres instancias, etc.)</span><span class="sxs-lookup"><span data-stu-id="aafd2-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="aafd2-109">Tamaño de la instancia (pequeño, mediano, grande)</span><span class="sxs-lookup"><span data-stu-id="aafd2-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="aafd2-110">SKU (Gratis, Compartido, Básico, Estándar y Premium)</span><span class="sxs-lookup"><span data-stu-id="aafd2-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="aafd2-111">Web Apps, Mobile Apps, Function Apps (o Funciones) o API Apps, en [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) se ejecutan todas en un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="aafd2-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="aafd2-112">Las aplicaciones de la misma suscripción y región pueden compartir un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="aafd2-112">Apps in the same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="aafd2-113">Todas las aplicaciones asignadas a un **plan de App Service** comparten los recursos definidos por él.</span><span class="sxs-lookup"><span data-stu-id="aafd2-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="aafd2-114">Compartir ahorra dinero al hospedar varias aplicaciones en un único plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="aafd2-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="aafd2-115">Su **plan de App Service** puede escalarse de SKU **Gratis** y **Compartido** a SKU **Básico**, **Estándar** y **Premium**, lo que permite acceder a más recursos y características.</span><span class="sxs-lookup"><span data-stu-id="aafd2-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span>

<span data-ttu-id="aafd2-116">Si su plan de App Service está establecido en SKU **Básico** o superior, también puede controlar el **tamaño** y el recuento de escala de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="aafd2-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="aafd2-117">Por ejemplo, si el plan está configurado para usar dos instancias "pequeñas" en el nivel de servicio estándar, todas las aplicaciones asociadas a este plan se ejecutarán en ambas instancias.</span><span class="sxs-lookup"><span data-stu-id="aafd2-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="aafd2-118">Las aplicaciones también tienen acceso a las características del nivel de servicio estándar.</span><span class="sxs-lookup"><span data-stu-id="aafd2-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="aafd2-119">Las instancias del plan en las que se ejecutan las aplicaciones están totalmente administradas y tienen una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="aafd2-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aafd2-120">El **SKU** y la **escala** del plan de App Service determina el costo, no el número de aplicaciones hospedadas en él.</span><span class="sxs-lookup"><span data-stu-id="aafd2-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="aafd2-121">En este artículo exploraremos las características clave, como el nivel y la escala de un plan de App Service y el papel que juegan mientras administra sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aafd2-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="aafd2-122">Aplicaciones y planes del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="aafd2-122">Apps and App Service plans</span></span>

<span data-ttu-id="aafd2-123">Una aplicación del Servicio de aplicaciones se puede asociar a un solo plan de dicho servicio en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="aafd2-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="aafd2-124">Tanto las aplicaciones como los planes se incluyen en un **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="aafd2-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="aafd2-125">Un grupo de recursos sirve como límite del ciclo de vida de cada uno de los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="aafd2-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="aafd2-126">Los grupos de recursos le permiten administrar todos los componentes de una aplicación conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="aafd2-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="aafd2-127">Como un único grupo de recursos puede tener varios planes del Servicio de aplicaciones, se pueden asignar diferentes aplicaciones a diferentes recursos físicos.</span><span class="sxs-lookup"><span data-stu-id="aafd2-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span>

<span data-ttu-id="aafd2-128">Por ejemplo, puede separar los recursos entre entornos de desarrollo, pruebas y producción.</span><span class="sxs-lookup"><span data-stu-id="aafd2-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="aafd2-129">Tener entornos independientes para producción y desarrollo o pruebas le permite aislar los recursos.</span><span class="sxs-lookup"><span data-stu-id="aafd2-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="aafd2-130">De esta forma, las pruebas de carga de una nueva versión de las aplicaciones no competirán por los mismos recursos que las aplicaciones de producción, que prestan servicio a clientes reales.</span><span class="sxs-lookup"><span data-stu-id="aafd2-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="aafd2-131">Al tener varios planes en un único grupo de recursos, también puede definir una aplicación que se extienda entre regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="aafd2-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="aafd2-132">Por ejemplo, una aplicación de alta disponibilidad que se ejecute en dos regiones incluirá dos planes como mínimo, uno por cada región, y una aplicación asociada a cada plan.</span><span class="sxs-lookup"><span data-stu-id="aafd2-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="aafd2-133">En tal situación, todas las copias de la aplicación estarán contenidas en un solo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aafd2-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="aafd2-134">Al tener un grupo de recursos con varios planes y aplicaciones, la administración, el control y la visión del estado de la aplicación resultan más sencillos.</span><span class="sxs-lookup"><span data-stu-id="aafd2-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="aafd2-135">Creación de un plan de App Service o uso de uno ya existente</span><span class="sxs-lookup"><span data-stu-id="aafd2-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="aafd2-136">Al crear una aplicación, debe considerar la creación de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aafd2-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="aafd2-137">Por otro lado, si la aplicación es un componente de otra aplicación más grande, créela dentro del grupo de recursos asignado a dicha aplicación de mayor tamaño.</span><span class="sxs-lookup"><span data-stu-id="aafd2-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="aafd2-138">Con independencia de que la aplicación sea totalmente nueva o parte de otra más grande, puede aprovechar un plan existente para hospedarla o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="aafd2-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="aafd2-139">Esta decisión es más bien una cuestión de capacidad y de carga esperada.</span><span class="sxs-lookup"><span data-stu-id="aafd2-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="aafd2-140">Se recomienda aislar la aplicación en un nuevo plan de App Service en los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="aafd2-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="aafd2-141">La aplicación consume muchos recursos.</span><span class="sxs-lookup"><span data-stu-id="aafd2-141">App is resource-intensive.</span></span>
- <span data-ttu-id="aafd2-142">La aplicación tiene factores de escalado diferentes de las otras aplicaciones hospedadas en un plan existente.</span><span class="sxs-lookup"><span data-stu-id="aafd2-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="aafd2-143">La aplicación necesita recursos de una región geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="aafd2-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="aafd2-144">De esta forma, puede asignar un nuevo conjunto de recursos para la aplicación y tener un mayor control de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aafd2-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="aafd2-145">Creación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="aafd2-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="aafd2-146">Si tiene un entorno de App Service, puede revisar la documentación específica para los entornos de App Service aquí: [Creación de un plan de App Service en un entorno de App Service](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan).</span><span class="sxs-lookup"><span data-stu-id="aafd2-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="aafd2-147">Puede crear un plan del Servicio de aplicaciones vacío desde la experiencia de exploración del plan del Servicio de aplicaciones o como parte de la creación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aafd2-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="aafd2-148">En [Azure Portal](https://portal.azure.com), haga clic en **Nuevo** > **Web y móvil** y, a continuación, seleccione **Aplicación web** u otro tipo de aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="aafd2-148">In the [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Cree una aplicación en Azure Portal.][createWebApp]

<span data-ttu-id="aafd2-150">A continuación, puede seleccionar o crear el plan del Servicio de aplicaciones para la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="aafd2-150">You can then select or create the App Service plan for the new app.</span></span>

 ![Creación de un plan del Servicio de aplicaciones.][createASP]

<span data-ttu-id="aafd2-152">Para crear un plan de App Service, haga clic en **[+] Crear nuevo**, escriba el nombre del **plan de App Service** y luego seleccione una **ubicación** adecuada.</span><span class="sxs-lookup"><span data-stu-id="aafd2-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="aafd2-153">Haga clic en **Plan de tarifa**y seleccione un plan de tarifa adecuado para el servicio.</span><span class="sxs-lookup"><span data-stu-id="aafd2-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="aafd2-154">Seleccione **Ver todos** para ver más opciones de precios, como **Gratis** y **Compartido**.</span><span class="sxs-lookup"><span data-stu-id="aafd2-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="aafd2-155">Una vez haya seleccionado el plan de tarifa, haga clic en el botón **Seleccionar** .</span><span class="sxs-lookup"><span data-stu-id="aafd2-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="aafd2-156">Cambio de una aplicación a un plan del Servicio de aplicaciones diferente</span><span class="sxs-lookup"><span data-stu-id="aafd2-156">Move an app to a different App Service plan</span></span>

<span data-ttu-id="aafd2-157">Puede mover una aplicación a un plan distinto de App Service en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aafd2-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="aafd2-158">Las aplicaciones pueden moverse entre los planes, siempre y cuando estos se encuentren en el mismo grupo de recursos y región geográfica.</span><span class="sxs-lookup"><span data-stu-id="aafd2-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="aafd2-159">Para mover una aplicación a otro plan:</span><span class="sxs-lookup"><span data-stu-id="aafd2-159">To move an app to another plan:</span></span>

- <span data-ttu-id="aafd2-160">Vaya a la aplicación que desea trasladar.</span><span class="sxs-lookup"><span data-stu-id="aafd2-160">Navigate to the app that you want to move.</span></span>
- <span data-ttu-id="aafd2-161">En el **Menú**, busque la sección **plan de App Service**.</span><span class="sxs-lookup"><span data-stu-id="aafd2-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="aafd2-162">Seleccione **Cambiar plan de App Service** para iniciar el proceso.</span><span class="sxs-lookup"><span data-stu-id="aafd2-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="aafd2-163">**Cambiar plan de App Service** abre el selector **plan de App Service**.</span><span class="sxs-lookup"><span data-stu-id="aafd2-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="aafd2-164">Llegados a este punto, puede elegir un plan existente para trasladar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aafd2-164">At this point, you can pick an existing plan to move this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aafd2-165">La interfaz de usuario del plan de App Service seleccionado se filtra por los siguientes criterios:</span><span class="sxs-lookup"><span data-stu-id="aafd2-165">The select App Service plan UI is filtered by the following criteria:</span></span>
> - <span data-ttu-id="aafd2-166">Existe dentro del mismo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="aafd2-166">Exists within the same Resource Group</span></span>
> - <span data-ttu-id="aafd2-167">Existe en la misma región geográfica</span><span class="sxs-lookup"><span data-stu-id="aafd2-167">Exists in the same Geographical Region</span></span>
> - <span data-ttu-id="aafd2-168">Existe dentro del mismo espacio web</span><span class="sxs-lookup"><span data-stu-id="aafd2-168">Exists within the same Webspace</span></span>
>
> <span data-ttu-id="aafd2-169">Un espacio web es una construcción lógica dentro de App Service que define una agrupación de recursos del servidor.</span><span class="sxs-lookup"><span data-stu-id="aafd2-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="aafd2-170">Una región geográfica (por ejemplo, Oeste de EE. UU.) contiene muchos espacios web para poder asignar a los clientes que usan App Service.</span><span class="sxs-lookup"><span data-stu-id="aafd2-170">A Geographical region (such as West US) contains many Webspaces in order to allocate customers using App Service.</span></span> <span data-ttu-id="aafd2-171">En la actualidad, no se pueden mover los recursos de App Service entre los espacios web.</span><span class="sxs-lookup"><span data-stu-id="aafd2-171">Currently, App Service resources aren’t able to be moved between Webspaces.</span></span>
>

![Selector de plan del Servicio de aplicaciones.][change]

<span data-ttu-id="aafd2-173">Cada plan tiene su propio plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="aafd2-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="aafd2-174">Por ejemplo, al mover un sitio de un nivel Gratis a un nivel Estándar, todas las aplicaciones asignadas puedan usar las características y los recursos del nivel Estándar.</span><span class="sxs-lookup"><span data-stu-id="aafd2-174">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="aafd2-175">Clonación de una aplicación en un plan del Servicio de aplicaciones diferente</span><span class="sxs-lookup"><span data-stu-id="aafd2-175">Clone an app to a different App Service plan</span></span>

<span data-ttu-id="aafd2-176">Si desea mover la aplicación a una región diferente, una alternativa es clonar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aafd2-176">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="aafd2-177">La clonación hará una copia de su aplicación en un plan de App Service nuevo o existente en cualquier región.</span><span class="sxs-lookup"><span data-stu-id="aafd2-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="aafd2-178">Puede encontrar **Clonar aplicación** en la sección **Herramientas de desarrollo** del menú.</span><span class="sxs-lookup"><span data-stu-id="aafd2-178">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aafd2-179">La clonación presenta algunas limitaciones sobre las que puede leer en [Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante el Portal de Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aafd2-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="aafd2-180">Escalación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="aafd2-180">Scale an App Service plan</span></span>

<span data-ttu-id="aafd2-181">Existen tres formas de escalar un plan:</span><span class="sxs-lookup"><span data-stu-id="aafd2-181">There are three ways to scale a plan:</span></span>

- <span data-ttu-id="aafd2-182">**Cambiar el nivel del plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="aafd2-182">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="aafd2-183">Un plan en el nivel Básico se puede convertir a Estándar y todas las aplicaciones asignadas a él usar las características del nivel Estándar.</span><span class="sxs-lookup"><span data-stu-id="aafd2-183">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
- <span data-ttu-id="aafd2-184">**Cambiar el tamaño de instancia del plan**.</span><span class="sxs-lookup"><span data-stu-id="aafd2-184">**Change the plan’s instance size**.</span></span> <span data-ttu-id="aafd2-185">Por ejemplo, un plan en el nivel Básico que usa instancias pequeñas puede cambiarse que use instancias grandes.</span><span class="sxs-lookup"><span data-stu-id="aafd2-185">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="aafd2-186">Todas las aplicaciones asociadas a dicho plan pueden usar la memoria y los recursos de CPU adicionales que ofrece el tamaño de instancia más grande.</span><span class="sxs-lookup"><span data-stu-id="aafd2-186">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
- <span data-ttu-id="aafd2-187">**Cambiar el recuento de instancias del plan**.</span><span class="sxs-lookup"><span data-stu-id="aafd2-187">**Change the plan’s instance count**.</span></span> <span data-ttu-id="aafd2-188">Por ejemplo, un plan Estándar que se ha escalado horizontalmente a tres instancias se puede escalar hasta 10 instancias.</span><span class="sxs-lookup"><span data-stu-id="aafd2-188">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="aafd2-189">Un plan Premium puede escalarse horizontalmente hasta a 20 instancias (según disponibilidad).</span><span class="sxs-lookup"><span data-stu-id="aafd2-189">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="aafd2-190">Todas las aplicaciones asociadas a dicho plan pueden usar la memoria y los recursos de CPU adicionales que ofrece el mayor recuento de instancias.</span><span class="sxs-lookup"><span data-stu-id="aafd2-190">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="aafd2-191">Puede cambiar el plan de tarifa y el tamaño de la instancia haciendo clic en el elemento **Escalar verticalmente** en la configuración de la aplicación o del plan del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aafd2-191">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="aafd2-192">Los cambios se aplicarán al plan de App Service y afectarán a todas las aplicaciones que hospede.</span><span class="sxs-lookup"><span data-stu-id="aafd2-192">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![Establecimiento de valores para escalar verticalmente una aplicación.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="aafd2-194">Limpieza del plan de App Service</span><span class="sxs-lookup"><span data-stu-id="aafd2-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aafd2-195">Los **planes de App Service** que no tienen aplicaciones asociadas a ellos seguirán generando cargos ya que siguen reservando capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="aafd2-195">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="aafd2-196">Para evitar cargos imprevistos, cuando se elimina la última aplicación hospedada en un plan de App Service, también se elimina el plan de App Service vacío resultante.</span><span class="sxs-lookup"><span data-stu-id="aafd2-196">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="aafd2-197">Resumen</span><span class="sxs-lookup"><span data-stu-id="aafd2-197">Summary</span></span>

<span data-ttu-id="aafd2-198">Los planes del Servicio de aplicaciones representan un conjunto de características y capacidades que puede compartir entre las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aafd2-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="aafd2-199">Los planes del Servicio de aplicaciones ofrecen la flexibilidad necesaria para asignar aplicaciones específicas a un conjunto de recursos y optimizar aún más el uso de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="aafd2-199">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="aafd2-200">De esta forma, si desea ahorrar gastos en el entorno de pruebas, puede compartir un plan entre varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aafd2-200">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="aafd2-201">Asimismo, puede escalarlo entre varias regiones y planes para maximizar el rendimiento del entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="aafd2-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="aafd2-202">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="aafd2-202">What's changed</span></span>

- <span data-ttu-id="aafd2-203">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="aafd2-203">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png

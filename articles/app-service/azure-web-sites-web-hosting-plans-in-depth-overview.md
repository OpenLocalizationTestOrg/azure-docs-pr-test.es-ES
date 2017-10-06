---
title: "información general detallada de planes de aaaAzure servicio de aplicaciones | Documentos de Microsoft"
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
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="da5cf-104">Introducción detallada sobre los planes del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="da5cf-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="da5cf-105">Planes de servicio de aplicaciones representan colección Hola de recursos físicos que usa toohost sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="da5cf-106">Los planes de App Service definen lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="da5cf-106">App Service plans define:</span></span>

- <span data-ttu-id="da5cf-107">Región (oeste de EE. UU., este de EE. UU., etc.)</span><span class="sxs-lookup"><span data-stu-id="da5cf-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="da5cf-108">Recuento de escala (uno, dos, tres instancias, etc.)</span><span class="sxs-lookup"><span data-stu-id="da5cf-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="da5cf-109">Tamaño de la instancia (pequeño, mediano, grande)</span><span class="sxs-lookup"><span data-stu-id="da5cf-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="da5cf-110">SKU (Gratis, Compartido, Básico, Estándar y Premium)</span><span class="sxs-lookup"><span data-stu-id="da5cf-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="da5cf-111">Web Apps, Mobile Apps, Function Apps (o Funciones) o API Apps, en [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) se ejecutan todas en un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="da5cf-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="da5cf-112">Aplicaciones de hello misma suscripción y región pueden compartir un plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="da5cf-113">Todas las aplicaciones asignan tooan **plan de servicio de aplicaciones** compartir recursos de hello definidos por dicha.</span><span class="sxs-lookup"><span data-stu-id="da5cf-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="da5cf-114">Compartir ahorra dinero al hospedar varias aplicaciones en un único plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="da5cf-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="da5cf-115">Su **plan de servicio de aplicaciones** puede escalarse desde **libre** y **Shared** SKU demasiado**básica**, **estándar**, y **Premium** SKU que lo que le proporciona acceso a recursos de toomore y características a lo largo de hello forma.</span><span class="sxs-lookup"><span data-stu-id="da5cf-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="da5cf-116">Si su plan de servicio de aplicaciones se establece demasiado**básica** SKU o superior, a continuación, puede controlar hello **tamaño** y escalar el recuento de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="da5cf-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="da5cf-117">Por ejemplo, si el plan está configurado toouse dos instancias de "pequeño" en el nivel de servicio estándar de hello, todas las aplicaciones que están asociadas a ese plan se ejecutan en ambas instancias.</span><span class="sxs-lookup"><span data-stu-id="da5cf-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="da5cf-118">Aplicaciones también tienen características de nivel de servicio estándar de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="da5cf-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="da5cf-119">Las instancias del plan en las que se ejecutan las aplicaciones están totalmente administradas y tienen una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="da5cf-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da5cf-120">Hola **SKU** y **escala** de servicio de aplicaciones de hello plan determina Hola costo y no Hola el número de aplicaciones hospedadas en ella.</span><span class="sxs-lookup"><span data-stu-id="da5cf-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="da5cf-121">Este artículo explora características clave de hello, como capa de escala de un plan de servicio de aplicaciones y cómo entran en juego al administrar sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="da5cf-122">Aplicaciones y planes del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="da5cf-122">Apps and App Service plans</span></span>

<span data-ttu-id="da5cf-123">Una aplicación del Servicio de aplicaciones se puede asociar a un solo plan de dicho servicio en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="da5cf-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="da5cf-124">Tanto las aplicaciones como los planes se incluyen en un **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="da5cf-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="da5cf-125">Un grupo de recursos actúa como límite de ciclo de vida de Hola para todos los recursos que está dentro de él.</span><span class="sxs-lookup"><span data-stu-id="da5cf-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="da5cf-126">Puede usar recursos grupos toomanage todas las piezas de Hola de una aplicación juntos.</span><span class="sxs-lookup"><span data-stu-id="da5cf-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="da5cf-127">Dado que un grupo de recursos solo puede tener varios planes de servicio de aplicaciones, puede asignar diferentes aplicaciones toodifferent los recursos físicos.</span><span class="sxs-lookup"><span data-stu-id="da5cf-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="da5cf-128">Por ejemplo, puede separar los recursos entre entornos de desarrollo, pruebas y producción.</span><span class="sxs-lookup"><span data-stu-id="da5cf-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="da5cf-129">Tener entornos independientes para producción y desarrollo o pruebas le permite aislar los recursos.</span><span class="sxs-lookup"><span data-stu-id="da5cf-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="da5cf-130">De esta manera, pruebas de carga con una nueva versión de las aplicaciones no compiten por hello mismo recursos como las aplicaciones de producción, que prestan servicio a los clientes reales.</span><span class="sxs-lookup"><span data-stu-id="da5cf-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="da5cf-131">Al tener varios planes en un único grupo de recursos, también puede definir una aplicación que se extienda entre regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="da5cf-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="da5cf-132">Por ejemplo, una aplicación de alta disponibilidad que se ejecute en dos regiones incluirá dos planes como mínimo, uno por cada región, y una aplicación asociada a cada plan.</span><span class="sxs-lookup"><span data-stu-id="da5cf-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="da5cf-133">En esta situación, todas las copias de Hola de aplicación hello, a continuación, se incluyen en un único grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="da5cf-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="da5cf-134">Tener un grupo de recursos con varios planes y varias aplicaciones hace fácil toomanage, control y ver el estado de aplicación Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="da5cf-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="da5cf-135">Creación de un plan de App Service o uso de uno ya existente</span><span class="sxs-lookup"><span data-stu-id="da5cf-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="da5cf-136">Al crear una aplicación, debe considerar la creación de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="da5cf-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="da5cf-137">En Hola otra parte, si esta aplicación es un componente de una aplicación mayor, créelo en grupo de recursos de Hola que se asigna para esa aplicación mayor.</span><span class="sxs-lookup"><span data-stu-id="da5cf-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="da5cf-138">Si la aplicación hello es una aplicación completamente nueva o parte de otro más grande, puede elegir toouse un toohost plan existente, o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="da5cf-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="da5cf-139">Esta decisión es más bien una cuestión de capacidad y de carga esperada.</span><span class="sxs-lookup"><span data-stu-id="da5cf-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="da5cf-140">Se recomienda aislar la aplicación en un nuevo plan de App Service en los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="da5cf-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="da5cf-141">La aplicación consume muchos recursos.</span><span class="sxs-lookup"><span data-stu-id="da5cf-141">App is resource-intensive.</span></span>
- <span data-ttu-id="da5cf-142">Aplicación tiene diferentes factores de escala de hello otras aplicaciones hospedadas en un plan existente.</span><span class="sxs-lookup"><span data-stu-id="da5cf-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="da5cf-143">La aplicación necesita recursos de una región geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="da5cf-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="da5cf-144">De esta forma, puede asignar un nuevo conjunto de recursos para la aplicación y tener un mayor control de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="da5cf-145">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="da5cf-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="da5cf-146">Si tiene un entorno de servicio de aplicaciones, puede revisar Hola documentación específica tooApp entornos del servicio aquí: [crear un plan de servicio de aplicaciones en un entorno de servicio de aplicaciones](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="da5cf-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="da5cf-147">Puede crear un plan de servicio de aplicaciones vacío de hello experiencia de exploración del plan de servicio de aplicaciones o como parte de la creación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="da5cf-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="da5cf-148">Hola [portal de Azure](https://portal.azure.com), haga clic en **New** > **Web y móvil**y, a continuación, seleccione **aplicación Web** o en otro tipo de aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Crear una aplicación Hola portal de Azure.][createWebApp]

<span data-ttu-id="da5cf-150">A continuación, puede seleccionar o crear plan de servicio de aplicaciones para la nueva aplicación de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="da5cf-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![Creación de un plan del Servicio de aplicaciones.][createASP]

<span data-ttu-id="da5cf-152">toocreate un plan de servicio de aplicaciones, haga clic en **[+] crear nuevos**, Hola de tipo **plan de servicio de aplicaciones** nombre y, a continuación, seleccione un **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="da5cf-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="da5cf-153">Haga clic en **tarifa**y, a continuación, seleccione un nivel de precios adecuado para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="da5cf-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="da5cf-154">Seleccione **todas las ver** tooview más precios opciones, como **libre** y **Shared**.</span><span class="sxs-lookup"><span data-stu-id="da5cf-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="da5cf-155">Después de haber seleccionado el nivel de precios de hello, haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="da5cf-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="da5cf-156">Mover un plan de servicio de aplicaciones diferentes de aplicaciones tooa</span><span class="sxs-lookup"><span data-stu-id="da5cf-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="da5cf-157">Puede mover un plan de servicio de aplicaciones diferentes de aplicaciones tooa Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="da5cf-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="da5cf-158">Puede mover aplicaciones entre planes siempre sea planes Hola Hola mismo grupo de recursos y la región geográfica.</span><span class="sxs-lookup"><span data-stu-id="da5cf-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="da5cf-159">toomove un plan de tooanother de aplicación:</span><span class="sxs-lookup"><span data-stu-id="da5cf-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="da5cf-160">Navegue aplicación toohello que desea toomove.</span><span class="sxs-lookup"><span data-stu-id="da5cf-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="da5cf-161">Hola **menú**, busque hello **Plan de servicio de aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="da5cf-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="da5cf-162">Seleccione **plan de servicio de aplicaciones de cambio** toostart proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="da5cf-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="da5cf-163">**Plan de servicio de aplicaciones de cambio** abre hello **plan de servicio de aplicaciones** selector.</span><span class="sxs-lookup"><span data-stu-id="da5cf-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="da5cf-164">En este momento, puede seleccionar esta aplicación en un toomove de plan existente.</span><span class="sxs-lookup"><span data-stu-id="da5cf-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da5cf-165">plan de servicio de aplicaciones seleccione Hola interfaz de usuario se filtra por hello siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="da5cf-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="da5cf-166">Existe dentro de hello mismo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="da5cf-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="da5cf-167">Existe en hello misma región geográfica</span><span class="sxs-lookup"><span data-stu-id="da5cf-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="da5cf-168">Existe dentro de hello mismo espacio Web</span><span class="sxs-lookup"><span data-stu-id="da5cf-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="da5cf-169">Un espacio web es una construcción lógica dentro de App Service que define una agrupación de recursos del servidor.</span><span class="sxs-lookup"><span data-stu-id="da5cf-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="da5cf-170">Una región geográfica (por ejemplo, oeste de Estados Unidos) contiene muchos espacios Web en orden tooallocate a los clientes usar servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="da5cf-171">Actualmente, los recursos del servicio de aplicación no están toobe pueden movido entre espacios Web.</span><span class="sxs-lookup"><span data-stu-id="da5cf-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![Selector de plan del Servicio de aplicaciones.][change]

<span data-ttu-id="da5cf-173">Cada plan tiene su propio plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="da5cf-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="da5cf-174">Por ejemplo, mover un sitio desde un nivel de estándar de tooa nivel gratis, habilita todas las aplicaciones asignadas características de tooit toouse hello y recursos de nivel estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="da5cf-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="da5cf-175">Clonar un plan de servicio de aplicaciones diferentes de aplicaciones tooa</span><span class="sxs-lookup"><span data-stu-id="da5cf-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="da5cf-176">Si desea que la región diferente de toomove Hola aplicación tooa, una alternativa es la aplicación de clonación.</span><span class="sxs-lookup"><span data-stu-id="da5cf-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="da5cf-177">La clonación hará una copia de su aplicación en un plan de App Service nuevo o existente en cualquier región.</span><span class="sxs-lookup"><span data-stu-id="da5cf-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="da5cf-178">Puede encontrar **clonar aplicación** en hello **herramientas de desarrollo** sección del menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="da5cf-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da5cf-179">La clonación presenta algunas limitaciones sobre las que puede leer en [Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante el Portal de Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="da5cf-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="da5cf-180">Escalación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="da5cf-180">Scale an App Service plan</span></span>

<span data-ttu-id="da5cf-181">Hay tres tooscale formas un plan:</span><span class="sxs-lookup"><span data-stu-id="da5cf-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="da5cf-182">**El nivel de precios del plan de cambio hello**.</span><span class="sxs-lookup"><span data-stu-id="da5cf-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="da5cf-183">Un plan en el nivel básico de hello puede ser tooStandard convertido y todas las aplicaciones asignan tooit toouse características Hola de nivel estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="da5cf-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="da5cf-184">**Cambiar el tamaño de las instancias del plan de hello**.</span><span class="sxs-lookup"><span data-stu-id="da5cf-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="da5cf-185">Por ejemplo, un plan en el nivel básico de Hola que usa instancias pequeñas puede ser instancias grandes de toouse modificadas.</span><span class="sxs-lookup"><span data-stu-id="da5cf-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="da5cf-186">Todas las aplicaciones que están asociadas a ese plan ahora pueden usar memoria adicional de Hola y recursos de CPU que Hola ofertas de tamaño mayor de instancia.</span><span class="sxs-lookup"><span data-stu-id="da5cf-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="da5cf-187">**Cambiar el número de instancias del plan de hello**.</span><span class="sxs-lookup"><span data-stu-id="da5cf-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="da5cf-188">Por ejemplo, un plan estándar que se escala toothree instancias puede ser instancias de escalado too10.</span><span class="sxs-lookup"><span data-stu-id="da5cf-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="da5cf-189">Un plan de Premium se puede escalar horizontalmente too20 instancias (asunto tooavailability).</span><span class="sxs-lookup"><span data-stu-id="da5cf-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="da5cf-190">Todas las aplicaciones que están asociadas a ese plan ahora pueden usar memoria adicional de Hola y recursos de CPU que Hola mayores ofertas de recuento de instancia.</span><span class="sxs-lookup"><span data-stu-id="da5cf-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="da5cf-191">Puede cambiar Hola tamaño de instancia y de nivel de precios haciendo clic en hello **escalar vertical** elemento bajo Configuración de aplicación hello ni Hola plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="da5cf-192">Cambios aplican toohello plan de servicio de aplicaciones y afecta a todas las aplicaciones que lo hospeda.</span><span class="sxs-lookup"><span data-stu-id="da5cf-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![Tooscale de valores de conjunto de seguridad de una aplicación.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="da5cf-194">Limpieza del plan de App Service</span><span class="sxs-lookup"><span data-stu-id="da5cf-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da5cf-195">**Planes de servicio de aplicaciones** que no tienen ningún toothem aplicaciones asociadas seguirán generando cargos puesto que continúan capacidad de cálculo de tooreserve Hola.</span><span class="sxs-lookup"><span data-stu-id="da5cf-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="da5cf-196">tooavoid inesperados cargos, cuando se elimina la aplicación última hello hospedada en un plan de servicio de aplicaciones, Hola vacío resultante también se elimina el plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="da5cf-197">Resumen</span><span class="sxs-lookup"><span data-stu-id="da5cf-197">Summary</span></span>

<span data-ttu-id="da5cf-198">Los planes del Servicio de aplicaciones representan un conjunto de características y capacidades que puede compartir entre las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="da5cf-199">Los planes de servicio de aplicaciones permiten Hola conjunto de tooa de flexibilidad tooallocate aplicaciones específicas de recursos y optimizar aún más la utilización de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="da5cf-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="da5cf-200">De este modo, si desea que toosave dinero en su entorno de pruebas, puede compartir un plan entre varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da5cf-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="da5cf-201">Asimismo, puede escalarlo entre varias regiones y planes para maximizar el rendimiento del entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="da5cf-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="da5cf-202">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="da5cf-202">What's changed</span></span>

- <span data-ttu-id="da5cf-203">Para que un cambio de toohello Guía de tooApp servicio de sitios Web, vea: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="da5cf-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png

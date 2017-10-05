---
title: "Aplicación de niveles múltiples .NET mediante Azure Service Bus | Microsoft Docs"
description: "Un tutorial .NET que le ayuda a desarrollar una aplicación de varios niveles en Azure que usa colas del Bus de servicio para comunicarse entre los niveles."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 8b502f5ac5d89801d390a872e7a8b06e094ecbba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="0e931-103">Aplicación de niveles múltiples .NET con colas del Bus de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="0e931-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="0e931-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="0e931-104">Introduction</span></span>
<span data-ttu-id="0e931-105">Desarrollar para Microsoft Azure es muy sencillo con Visual Studio y el SDK de Azure para .NET gratis.</span><span class="sxs-lookup"><span data-stu-id="0e931-105">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span></span> <span data-ttu-id="0e931-106">Este tutorial lo guía por los pasos para crear una aplicación que usa varios recursos de Azure que se ejecutan en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="0e931-106">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="0e931-107">Aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e931-107">You will learn the following:</span></span>

* <span data-ttu-id="0e931-108">Cómo habilitar el equipo para el desarrollo de Azure con una única descarga e instalación.</span><span class="sxs-lookup"><span data-stu-id="0e931-108">How to enable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="0e931-109">Cómo utilizar Visual Studio para desarrollar para Azure.</span><span class="sxs-lookup"><span data-stu-id="0e931-109">How to use Visual Studio to develop for Azure.</span></span>
* <span data-ttu-id="0e931-110">Cómo crear una aplicación de niveles múltiples en Azure mediante el uso de roles web y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0e931-110">How to create a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="0e931-111">Cómo comunicarse entre niveles mediante las colas del bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="0e931-111">How to communicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="0e931-112">En este tutorial compilará y ejecutará la aplicación de niveles múltiples en un servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e931-112">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="0e931-113">El front-end es un rol web de ASP.NET MVC y el back-end es un rol de trabajo que usa una cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0e931-113">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="0e931-114">Puede crear la misma aplicación de niveles múltiples con el front-end como un proyecto web, que se implementa en un sitio web de Azure, en lugar de en un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="0e931-114">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span></span> <span data-ttu-id="0e931-115">También puede probar el tutorial de [aplicación híbrida en la nube/local .NET](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md).</span><span class="sxs-lookup"><span data-stu-id="0e931-115">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="0e931-116">La siguiente captura de pantalla muestra la aplicación completada.</span><span class="sxs-lookup"><span data-stu-id="0e931-116">The following screen shot shows the completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="0e931-117">Información general del escenario: comunicación entre roles</span><span class="sxs-lookup"><span data-stu-id="0e931-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="0e931-118">Para enviar una orden para su procesamiento, el componente de la interfaz de usuario de front-end, que se ejecuta en el rol web, debe interactuar con la lógica del nivel intermedio que se ejecuta en el rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0e931-118">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span></span> <span data-ttu-id="0e931-119">En ese ejemplo se utiliza la mensajería de Service Bus para la comunicación entre los niveles.</span><span class="sxs-lookup"><span data-stu-id="0e931-119">This example uses Service Bus messaging for the communication between the tiers.</span></span>

<span data-ttu-id="0e931-120">El uso de la mensajería de Service Bus entre los niveles de web e intermedio desacopla los dos componentes.</span><span class="sxs-lookup"><span data-stu-id="0e931-120">Using Service Bus messaging between the web and middle tiers decouples the two components.</span></span> <span data-ttu-id="0e931-121">Al contrario que en la mensajería directa (es decir, TCP o HTTP), el nivel web no se conecta directamente al nivel intermedio; por el contrario, inserta unidades de trabajo, como mensajes, en el Bus de servicio, que los conserva de manera confiable hasta que el nivel intermedio esté preparado para consumirlas y procesarlas.</span><span class="sxs-lookup"><span data-stu-id="0e931-121">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span></span>

<span data-ttu-id="0e931-122">El bus de servicio ofrece dos entidades para admitir la mensajería asincrónica: colas y temas.</span><span class="sxs-lookup"><span data-stu-id="0e931-122">Service Bus provides two entities to support brokered messaging: queues and topics.</span></span> <span data-ttu-id="0e931-123">Con las colas, cada mensaje enviado a la cola lo consume un único receptor.</span><span class="sxs-lookup"><span data-stu-id="0e931-123">With queues, each message sent to the queue is consumed by a single receiver.</span></span> <span data-ttu-id="0e931-124">Los temas admiten el patrón de publicación/suscripción, en el cual cada mensaje publicado está disponible para una suscripción registrada con el tema.</span><span class="sxs-lookup"><span data-stu-id="0e931-124">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span></span> <span data-ttu-id="0e931-125">Cada suscripción mantiene lógicamente su propia cola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="0e931-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="0e931-126">Las suscripciones también se pueden configurar con reglas de filtro que restringen el conjunto de mensajes pasados a la cola de suscripción a aquellos que coinciden con el filtro.</span><span class="sxs-lookup"><span data-stu-id="0e931-126">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span></span> <span data-ttu-id="0e931-127">En este ejemplo se usan las colas de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="0e931-127">The following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="0e931-128">Este mecanismo de comunicación tiene varias ventajas sobre la mensajería directa:</span><span class="sxs-lookup"><span data-stu-id="0e931-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="0e931-129">**Desacoplamiento temporal.**</span><span class="sxs-lookup"><span data-stu-id="0e931-129">**Temporal decoupling.**</span></span> <span data-ttu-id="0e931-130">Con el patrón de mensajería asincrónica, los productores y los consumidores no tienen que estar en línea al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="0e931-130">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span></span> <span data-ttu-id="0e931-131">El bus de servicio almacena los mensajes de manera confiable hasta que la parte consumidora esté lista para recibirlos.</span><span class="sxs-lookup"><span data-stu-id="0e931-131">Service Bus reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="0e931-132">De esta forma, los componentes de la aplicación distribuida se pueden desconectar, ya sea voluntariamente, por ejemplo, para mantenimiento, o debido a un bloqueo del componente, sin que afecte al sistema en su conjunto.</span><span class="sxs-lookup"><span data-stu-id="0e931-132">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="0e931-133">Es más, puede que la aplicación consumidora solo necesite estar en línea durante determinados períodos del día.</span><span class="sxs-lookup"><span data-stu-id="0e931-133">Furthermore, the consuming application might only need to come online during certain times of the day.</span></span>
* <span data-ttu-id="0e931-134">**Redistribución de la carga.**</span><span class="sxs-lookup"><span data-stu-id="0e931-134">**Load leveling.**</span></span> <span data-ttu-id="0e931-135">En muchas aplicaciones, la carga del sistema varía con el tiempo, mientras que el tiempo de procesamiento requerido para cada unidad de trabajo suele ser constante.</span><span class="sxs-lookup"><span data-stu-id="0e931-135">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="0e931-136">La intermediación de productores y consumidores de mensajes con una cola implica que la aplicación consumidora (el trabajador) solo necesita ser aprovisionada para acomodar una carga promedio en lugar de una carga pico.</span><span class="sxs-lookup"><span data-stu-id="0e931-136">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span></span> <span data-ttu-id="0e931-137">La profundidad de la cola aumenta y se contrae a medida que varíe la carga entrante,</span><span class="sxs-lookup"><span data-stu-id="0e931-137">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="0e931-138">lo que permite ahorrar dinero directamente en función de la cantidad de infraestructura requerida para dar servicio a la carga de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-138">This directly saves money in terms of the amount of infrastructure required to service the application load.</span></span>
* <span data-ttu-id="0e931-139">**Equilibrio de carga.**</span><span class="sxs-lookup"><span data-stu-id="0e931-139">**Load balancing.**</span></span> <span data-ttu-id="0e931-140">A medida que aumenta la carga, se pueden agregar más procesos de trabajo para que puedan leerse desde la cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-140">As load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="0e931-141">Cada mensaje se procesa únicamente por uno de los procesos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0e931-141">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="0e931-142">Además, este equilibrio de carga permite el uso óptimo de las máquinas de trabajo aunque estas máquinas difieran en términos de capacidad de procesamiento, ya que extraerán mensajes a su frecuencia máxima propia.</span><span class="sxs-lookup"><span data-stu-id="0e931-142">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="0e931-143">Este patrón con frecuencia se denomina patrón de *consumo de competidor*.</span><span class="sxs-lookup"><span data-stu-id="0e931-143">This pattern is often termed the *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="0e931-144">En las secciones siguientes se explica el código que implementa esta arquitectura.</span><span class="sxs-lookup"><span data-stu-id="0e931-144">The following sections discuss the code that implements this architecture.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="0e931-145">Configuración del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="0e931-145">Set up the development environment</span></span>
<span data-ttu-id="0e931-146">Antes de comenzar a desarrollar aplicaciones de Azure, obtenga las herramientas y configure el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="0e931-146">Before you can begin developing Azure applications, get the tools and set up your development environment.</span></span>

1. <span data-ttu-id="0e931-147">Instale el SDK de Azure para .NET desde la [página de descargas](https://azure.microsoft.com/downloads/) del SDK.</span><span class="sxs-lookup"><span data-stu-id="0e931-147">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="0e931-148">En la columna **.NET**, haga clic en la versión de [Visual Studio](http://www.visualstudio.com) que está usando.</span><span class="sxs-lookup"><span data-stu-id="0e931-148">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="0e931-149">Los pasos de este tutorial utilizan Visual Studio 2015, pero también funcionan con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="0e931-149">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="0e931-150">Cuando se le solicite ejecutar o guardar el programa de instalación, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="0e931-150">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="0e931-151">En el **instalador de plataforma web**, haga clic en **Instalar** y continúe con la instalación.</span><span class="sxs-lookup"><span data-stu-id="0e931-151">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="0e931-152">Cuando la instalación se complete, dispondrá de todo lo necesario para iniciar el desarrollo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-152">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="0e931-153">El SDK incluye las herramientas que le permiten desarrollar fácilmente aplicaciones Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e931-153">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="0e931-154">Creación de un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="0e931-154">Create a namespace</span></span>
<span data-ttu-id="0e931-155">El siguiente paso es crear un espacio de nombres de servicio y obtener una clave de Firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="0e931-155">The next step is to create a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="0e931-156">Un espacio de nombres proporciona un límite de aplicación para cada aplicación que se expone a través del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="0e931-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="0e931-157">El sistema genera una clave SAS cuando se crea un espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="0e931-157">A SAS key is generated by the system when a namespace is created.</span></span> <span data-ttu-id="0e931-158">La combinación del espacio de nombres y la clave SAS proporciona las credenciales de Bus de servicio para autenticar el acceso a una aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-158">The combination of namespace and SAS key provides the credentials for Service Bus to authenticate access to an application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="0e931-159">Creación de un rol web</span><span class="sxs-lookup"><span data-stu-id="0e931-159">Create a web role</span></span>
<span data-ttu-id="0e931-160">En esta sección, va a crear el front-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-160">In this section, you build the front end of your application.</span></span> <span data-ttu-id="0e931-161">En primer lugar, va a crear las páginas que mostrará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-161">First, you create the pages that your application displays.</span></span>
<span data-ttu-id="0e931-162">Después, va a agregar el código que envía elementos a una cola del Bus de servicio y muestra información de estado sobre la cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-162">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="0e931-163">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="0e931-163">Create the project</span></span>
1. <span data-ttu-id="0e931-164">Inicie Visual Studio con privilegios de administrador: haga clic con el botón derecho en el icono del programa **Visual Studio** y después haga clic en **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="0e931-164">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="0e931-165">El emulador de proceso de Azure, descrito posteriormente en este artículo, requiere que se inicie Visual Studio con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="0e931-165">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="0e931-166">En Visual Studio, en el menú **Archivo**, haga clic en **Nuevo** y, a continuación, en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="0e931-166">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="0e931-167">En **Plantillas instaladas**, en **Visual C#**, haga clic en **Nube** y, a continuación, en **Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="0e931-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="0e931-168">Denomine el proyecto **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="0e931-168">Name the project **MultiTierApp**.</span></span> <span data-ttu-id="0e931-169">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0e931-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="0e931-170">En los roles de **.NET Framework 4.5**, haga doble clic en **Rol web de ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="0e931-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="0e931-171">Mantenga el cursor sobre **WebRole1** en **Solución de servicio de nube de Azure**, haga clic en el icono de lápiz y cambie el nombre del rol web a **FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="0e931-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span></span> <span data-ttu-id="0e931-172">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0e931-172">Then click **OK**.</span></span> <span data-ttu-id="0e931-173">(Asegúrese de que escribe "Frontend" con "e" minúscula, no "FrontEnd").</span><span class="sxs-lookup"><span data-stu-id="0e931-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="0e931-174">En el cuadro de diálogo **Nuevo proyecto de ASP.NET**, en la lista **Seleccionar una plantilla**, haga clic en **MVC**.</span><span class="sxs-lookup"><span data-stu-id="0e931-174">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="0e931-175">Todavía en el cuadro de diálogo **Nuevo proyecto de ASP.NET**, haga clic en el botón **Cambiar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="0e931-175">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span></span> <span data-ttu-id="0e931-176">En el cuadro de diálogo **Cambiar autenticación**, haga clic en **Sin autenticación** y, a continuación, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0e931-176">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="0e931-177">En este tutorial, va a implementar una aplicación que no necesita un inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="0e931-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="0e931-178">De vuelta en el cuadro de diálogo **Nuevo proyecto de ASP.NET**, haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0e931-178">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span></span>
8. <span data-ttu-id="0e931-179">En el **Explorador de soluciones**, en el proyecto **FrontendWebRole**, haga clic con el botón derecho en **Referencias** y haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0e931-179">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="0e931-180">Haga clic en la pestaña **Examinar** y luego busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="0e931-180">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="0e931-181">Seleccione el paquete **WindowsAzure.ServiceBus**, haga clic en **Instalar** y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="0e931-181">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="0e931-182">Tenga en cuenta que ahora se hace referencia a los ensamblados del cliente requeridos y que se han agregado algunos archivos de código nuevos.</span><span class="sxs-lookup"><span data-stu-id="0e931-182">Note that the required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="0e931-183">En el **Explorador de soluciones**, haga clic con el botón derecho en **Modelos** y, luego, en **Agregar** y, por último, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="0e931-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="0e931-184">En el cuadro **Nombre**, escriba el nombre **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="0e931-184">In the **Name** box, type the name **OnlineOrder.cs**.</span></span> <span data-ttu-id="0e931-185">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0e931-185">Then click **Add**.</span></span>

### <a name="write-the-code-for-your-web-role"></a><span data-ttu-id="0e931-186">Especificación del código del rol web</span><span class="sxs-lookup"><span data-stu-id="0e931-186">Write the code for your web role</span></span>
<span data-ttu-id="0e931-187">En esta sección, creará las distintas páginas que va a mostrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-187">In this section, you create the various pages that your application displays.</span></span>

1. <span data-ttu-id="0e931-188">En el archivo OnlineOrder.cs en Visual Studio, sustituya la definición del espacio de nombres existentes por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="0e931-188">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="0e931-189">En el **Explorador de soluciones**, haga doble clic en **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="0e931-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="0e931-190">Agregue las siguientes instrucciones **using** en la parte superior del archivo para incluir los espacios de nombres en el modelo que acaba de crear, así como Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0e931-190">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="0e931-191">En el archivo HomeController.cs en Visual Studio, sustituya la definición del espacio de nombres existentes por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="0e931-191">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span> <span data-ttu-id="0e931-192">Este código contiene métodos para controlar el envío de elementos a la cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-192">This code contains methods for handling the submission of items to the queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect to Submit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for the submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from the submission
           // form.
           [HttpPost]
           // Attribute to help prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting to queue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="0e931-193">En el menú **Compilar**, haga clic en **Compilar solución** para probar la precisión del trabajo hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="0e931-193">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span></span>
5. <span data-ttu-id="0e931-194">Ahora, va a crear la vista para el método `Submit()` que creó antes.</span><span class="sxs-lookup"><span data-stu-id="0e931-194">Now, create the view for the `Submit()` method you created earlier.</span></span> <span data-ttu-id="0e931-195">Haga clic con el botón derecho en el método `Submit()` (la sobrecarga de `Submit()` que no acepta parámetros) y elija **Agregar vista**.</span><span class="sxs-lookup"><span data-stu-id="0e931-195">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="0e931-196">Se muestra un cuadro de diálogo para crear la vista.</span><span class="sxs-lookup"><span data-stu-id="0e931-196">A dialog box appears for creating the view.</span></span> <span data-ttu-id="0e931-197">En la lista **Plantilla**, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0e931-197">In the **Template** list, choose **Create**.</span></span> <span data-ttu-id="0e931-198">En la lista **Clase de modelo**, haga clic en la clase **OnlineOrder**.</span><span class="sxs-lookup"><span data-stu-id="0e931-198">In the **Model class** list, click the **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="0e931-199">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0e931-199">Click **Add**.</span></span>
8. <span data-ttu-id="0e931-200">Ahora, cambie el nombre mostrado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-200">Now, change the displayed name of your application.</span></span> <span data-ttu-id="0e931-201">En el **Explorador de soluciones**, haga doble clic en el archivo **Views\Shared\\_Layout.cshtml**para abrirlo en el editor de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e931-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="0e931-202">Reemplace todas las apariciones de **My ASP.NET Application** por **Productos de LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="0e931-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="0e931-203">Quite los vínculos **Página principal**, **Acerca de** y **Contacto**.</span><span class="sxs-lookup"><span data-stu-id="0e931-203">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="0e931-204">Elimine el código resaltado:</span><span class="sxs-lookup"><span data-stu-id="0e931-204">Delete the highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="0e931-205">Finalmente, modifique la página de envío para incluir información sobre la cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-205">Finally, modify the submission page to include some information about the queue.</span></span> <span data-ttu-id="0e931-206">En el **Explorador de soluciones**, haga doble clic en el archivo **Views\Home\Submit.cshtml** para abrirlo en el editor de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e931-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="0e931-207">Agregue la línea siguiente después de `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="0e931-207">Add the following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="0e931-208">Por ahora, `ViewBag.MessageCount` está vacío.</span><span class="sxs-lookup"><span data-stu-id="0e931-208">For now, the `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="0e931-209">Lo rellenará más adelante.</span><span class="sxs-lookup"><span data-stu-id="0e931-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting to be processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="0e931-210">Acaba de implementar su interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="0e931-210">You now have implemented your UI.</span></span> <span data-ttu-id="0e931-211">Puede presionar **F5** para ejecutar la aplicación y confirmar que tiene el aspecto previsto.</span><span class="sxs-lookup"><span data-stu-id="0e931-211">You can press **F5** to run your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-the-code-for-submitting-items-to-a-service-bus-queue"></a><span data-ttu-id="0e931-212">Especificación del código para enviar elementos a una cola del bus de servicio</span><span class="sxs-lookup"><span data-stu-id="0e931-212">Write the code for submitting items to a Service Bus queue</span></span>
<span data-ttu-id="0e931-213">Ahora, agregue el código para enviar elementos a una cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-213">Now, add code for submitting items to a queue.</span></span> <span data-ttu-id="0e931-214">En primer lugar, va a crear una clase que contiene la información de conexión a la cola del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="0e931-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="0e931-215">A continuación, inicialice la conexión en Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="0e931-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="0e931-216">Finalmente, actualice el código de envío que creó antes en HomeController.cs para enviar realmente los elementos a una cola del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="0e931-216">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span></span>

1. <span data-ttu-id="0e931-217">En el **Explorador de soluciones**, haga clic con el botón derecho en **FrontendWebRole** (haga clic con el botón derecho en el proyecto, no en el rol).</span><span class="sxs-lookup"><span data-stu-id="0e931-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span></span> <span data-ttu-id="0e931-218">Haga clic en **Agregar** y, a continuación, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="0e931-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="0e931-219">Asigne a la clase el nombre **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="0e931-219">Name the class **QueueConnector.cs**.</span></span> <span data-ttu-id="0e931-220">Haga clic en **Agregar** para crear la clase.</span><span class="sxs-lookup"><span data-stu-id="0e931-220">Click **Add** to create the class.</span></span>
3. <span data-ttu-id="0e931-221">Ahora va a agregar código que encapsula la información de conexión e inicializará la conexión a una cola de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="0e931-221">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span></span> <span data-ttu-id="0e931-222">Reemplace todo el contenido de QueueConnector.cs por el código siguiente y escriba valores para `your Service Bus namespace` (el nombre del espacio de nombres) y `yourKey`, la **clave principal** que obtuvo antes en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0e931-222">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from the portal.
           public const string Namespace = "your Service Bus namespace";
   
           // The name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create the namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http to be friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create the namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create the queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client to the queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="0e931-223">Ahora, asegúrese de que se llama al método **Initialize**.</span><span class="sxs-lookup"><span data-stu-id="0e931-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="0e931-224">En el **Explorador de soluciones**, haga doble clic en **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="0e931-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="0e931-225">Agregue la siguiente línea de código al final del método **Application_Start**.</span><span class="sxs-lookup"><span data-stu-id="0e931-225">Add the following line of code at the end of the **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="0e931-226">Por último, actualice el código web que creó anteriormente para enviar elementos a la cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-226">Finally, update the web code you created earlier, to submit items to the queue.</span></span> <span data-ttu-id="0e931-227">En el **Explorador de soluciones**, haga doble clic en **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="0e931-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="0e931-228">Actualice el método `Submit()` (la sobrecarga que no acepta parámetros) como sigue para obtener el número de mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-228">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you to perform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get the queue, and obtain the message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="0e931-229">Actualice el método `Submit(OnlineOrder order)` (la sobrecarga que no acepta parámetros) como sigue para enviar información de pedidos a la cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-229">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from the order.
           var message = new BrokeredMessage(order);
   
           // Submit the order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="0e931-230">Ahora puede volver a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-230">You can now run the application again.</span></span> <span data-ttu-id="0e931-231">Cada vez que envía un pedido, el contador de mensajes aumenta.</span><span class="sxs-lookup"><span data-stu-id="0e931-231">Each time you submit an order, the message count increases.</span></span>
   
   ![][18]

## <a name="create-the-worker-role"></a><span data-ttu-id="0e931-232">Creación del rol de trabajo</span><span class="sxs-lookup"><span data-stu-id="0e931-232">Create the worker role</span></span>
<span data-ttu-id="0e931-233">Ahora creará el rol de trabajo que procesa los envíos del pedido.</span><span class="sxs-lookup"><span data-stu-id="0e931-233">You will now create the worker role that processes the order submissions.</span></span> <span data-ttu-id="0e931-234">Este ejemplo utiliza la plantilla de proyecto de Visual Studio de **rol de trabajo con cola de Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="0e931-234">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="0e931-235">Ya ha obtenido las credenciales necesarias del portal.</span><span class="sxs-lookup"><span data-stu-id="0e931-235">You already obtained the required credentials from the portal.</span></span>

1. <span data-ttu-id="0e931-236">Asegúrese de que se ha conectado Visual Studio a su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e931-236">Make sure you have connected Visual Studio to your Azure account.</span></span>
2. <span data-ttu-id="0e931-237">En Visual Studio, en el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Roles** en el proyecto **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="0e931-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span></span>
3. <span data-ttu-id="0e931-238">Haga clic en **Agregar** y, a continuación, en **Nuevo proyecto de rol de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="0e931-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="0e931-239">Aparecerá el cuadro de diálogo **Agregar nuevo proyecto de rol**.</span><span class="sxs-lookup"><span data-stu-id="0e931-239">The **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="0e931-240">En el cuadro de diálogo **Agregar nuevo proyecto de rol**, haga clic en **Rol de trabajo con cola de Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="0e931-240">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="0e931-241">En el cuadro **Nombre**, asigne al proyecto el nombre **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="0e931-241">In the **Name** box, name the project **OrderProcessingRole**.</span></span> <span data-ttu-id="0e931-242">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0e931-242">Then click **Add**.</span></span>
6. <span data-ttu-id="0e931-243">Copie en el Portapapeles la cadena de conexión que obtuvo en el paso 9 de la sección "Creación de un espacio de nombres de bus de servicio".</span><span class="sxs-lookup"><span data-stu-id="0e931-243">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span></span>
7. <span data-ttu-id="0e931-244">En el **Explorador de soluciones**, haga clic con el botón derecho en el elemento **OrderProcessingRole** que creó en el paso 5 (asegúrese de hacer clic con el botón derecho en **OrderProcessingRole** en **Roles** y no en la clase).</span><span class="sxs-lookup"><span data-stu-id="0e931-244">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span></span> <span data-ttu-id="0e931-245">A continuación, haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="0e931-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="0e931-246">En la pestaña **Configuración** del cuadro de diálogo **Propiedades**, haga clic dentro del cuadro **Valor** para **Microsoft.ServiceBus.ConnectionString** y, a continuación, pegue el valor de punto de conexión que copió en el paso 6.</span><span class="sxs-lookup"><span data-stu-id="0e931-246">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="0e931-247">Cree una clase **OnlineOrder** para representar los pedidos cuando los procese desde la cola.</span><span class="sxs-lookup"><span data-stu-id="0e931-247">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span></span> <span data-ttu-id="0e931-248">Puede reutilizar una clase que ya ha creado.</span><span class="sxs-lookup"><span data-stu-id="0e931-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="0e931-249">En el **Explorador de soluciones**, haga clic con el botón derecho en la clase **OrderProcessingRole** (haga clic con el botón derecho en el icono de clase, no en el rol).</span><span class="sxs-lookup"><span data-stu-id="0e931-249">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span></span> <span data-ttu-id="0e931-250">Haga clic en **Agregar** y, a continuación, en **Elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="0e931-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="0e931-251">Busque **FrontendWebRole\Models** en la subcarpeta y haga doble clic en **OnlineOrder.cs** para agregarlo a este proyecto.</span><span class="sxs-lookup"><span data-stu-id="0e931-251">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span></span>
11. <span data-ttu-id="0e931-252">En **WorkerRole.cs**, cambie el valor de la variable **QueueName** de `"ProcessingQueue"` a `"OrdersQueue"`, como se muestra en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="0e931-252">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span></span>
    
    ```csharp
    // The name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="0e931-253">Agregue la siguiente instrucción using en la parte superior del archivo WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="0e931-253">Add the following using statement at the top of the WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="0e931-254">En la función `Run()`, dentro de la llamada `OnMessage()`, reemplace el contenido de la cláusula `try` por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="0e931-254">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View the message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="0e931-255">Ha completado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e931-255">You have completed the application.</span></span> <span data-ttu-id="0e931-256">Puede probar la aplicación completa haciendo clic con el botón derecho en el proyecto MultiTierApp en el Explorador de soluciones, seleccionando **Establecer como proyecto de inicio** y, a continuación, presionando F5.</span><span class="sxs-lookup"><span data-stu-id="0e931-256">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="0e931-257">Tenga en cuenta que el contador de mensajes no se aumenta, ya que el rol de trabajo procesa los elementos de la cola y los marca como finalizados.</span><span class="sxs-lookup"><span data-stu-id="0e931-257">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span></span> <span data-ttu-id="0e931-258">Puede ver el resultado de seguimiento de su rol de trabajo viendo la interfaz de usuario del emulador de proceso de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e931-258">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span></span> <span data-ttu-id="0e931-259">Para ello, haga clic con el botón derecho en el icono del emulador del área de notificación de la barra de tareas y seleccione **Mostrar interfaz de usuario del emulador de proceso**.</span><span class="sxs-lookup"><span data-stu-id="0e931-259">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="0e931-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e931-260">Next steps</span></span>
<span data-ttu-id="0e931-261">Para obtener más información sobre el bus de servicio, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="0e931-261">To learn more about Service Bus, see the following resources:</span></span>  

* <span data-ttu-id="0e931-262">[Documentación de Azure Service Bus][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="0e931-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="0e931-263">[Página de servicio de Service Bus][sbacom]</span><span class="sxs-lookup"><span data-stu-id="0e931-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="0e931-264">[Utilización de las colas de Service Bus][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="0e931-264">[How to Use Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="0e931-265">Para más información sobre los escenarios de niveles múltiples, consulte:</span><span class="sxs-lookup"><span data-stu-id="0e931-265">To learn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="0e931-266">[Aplicación de niveles múltiples .NET mediante tablas, colas y blobs de Storage][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="0e931-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36

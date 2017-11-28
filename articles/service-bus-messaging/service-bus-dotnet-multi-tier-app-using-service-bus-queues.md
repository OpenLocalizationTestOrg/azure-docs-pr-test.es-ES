---
title: "aplicación de varios niveles de aaa.NET uso del Bus de servicio de Azure | Documentos de Microsoft"
description: "Un tutorial de .NET que ayuda a desarrollar una aplicación de varios nivel en Azure que usa toocommunicate de colas de Bus de servicio entre las capas."
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
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="b8b8e-103">Aplicación de niveles múltiples .NET con colas del Bus de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="b8b8e-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="b8b8e-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="b8b8e-104">Introduction</span></span>
<span data-ttu-id="b8b8e-105">Desarrollar para Microsoft Azure es fácil con Visual Studio y Hola libre Azure SDK para. NET.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="b8b8e-106">Este tutorial le guía a través de hello pasos toocreate una aplicación que usa varios recursos de Azure ejecutando en su entorno local.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="b8b8e-107">Aprenderá siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="b8b8e-107">You will learn hello following:</span></span>

* <span data-ttu-id="b8b8e-108">Cómo tooenable el equipo de desarrollo de Azure con una sola descargar e instalar.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="b8b8e-109">Cómo toouse toodevelop de Visual Studio para Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="b8b8e-110">¿Cómo toocreate una aplicación de varios niveles en Azure con roles web y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="b8b8e-111">Cómo toocommunicate entre niveles de uso de colas de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="b8b8e-112">En este tutorial podrá crear y ejecutar la aplicación de varios niveles de hello en un servicio de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="b8b8e-113">Hola front-end es un rol web de ASP.NET MVC y back-end de hello es un rol de trabajo que utiliza una cola de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="b8b8e-114">Puede crear Hola la misma aplicación de varios nivel con front-end de Hola como un proyecto web, que está implementado tooan sitio Web de Azure en lugar de un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="b8b8e-115">También puede probar hello [aplicación de .NET en local y la nube híbrida](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="b8b8e-116">Hello siguiente captura de pantalla muestra aplicación hello completado.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="b8b8e-117">Información general del escenario: comunicación entre roles</span><span class="sxs-lookup"><span data-stu-id="b8b8e-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="b8b8e-118">toosubmit un pedido para el procesamiento, el componente interfaz de usuario de hello front-end, ejecuta en rol de hello web, debe interactuar con la lógica de nivel intermedio de hello ejecuta en rol de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="b8b8e-119">Este ejemplo utiliza la mensajería de Bus de servicio para la comunicación de hello entre las capas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="b8b8e-120">Uso del Bus de servicio de mensajería entre los niveles intermedios y web Hola desacopla los dos componentes.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="b8b8e-121">En cambio toodirect mensajería (es decir, TCP o HTTP), Hola nivel web no conecta nivel intermedio toohello directamente; en su lugar inserta unidades de trabajo, como mensajes, en el Bus de servicio, que se mantiene hasta que el nivel intermedio de hello es tooconsume listo y procesarlos de forma confiable.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="b8b8e-122">Bus de servicio proporciona dos entidades toosupport asíncrona mensajería: colas y temas.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="b8b8e-123">Con las colas, cada mensaje enviado toohello cola es utilizado por un único receptor.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="b8b8e-124">Temas de admiten el patrón de publicación/suscripción de hello en el que cada mensaje publicado se pone tooa disponibles las suscripciones registradas con el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="b8b8e-125">Cada suscripción mantiene lógicamente su propia cola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="b8b8e-126">Las suscripciones también pueden configurarse con reglas de filtro que restringen el conjunto de Hola de mensajes que se pasan a toothose de cola de suscripción de Hola que coinciden con el filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="b8b8e-127">Hello en el ejemplo siguiente se utiliza colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="b8b8e-128">Este mecanismo de comunicación tiene varias ventajas sobre la mensajería directa:</span><span class="sxs-lookup"><span data-stu-id="b8b8e-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="b8b8e-129">**Desacoplamiento temporal.**</span><span class="sxs-lookup"><span data-stu-id="b8b8e-129">**Temporal decoupling.**</span></span> <span data-ttu-id="b8b8e-130">Con el patrón de mensajería asincrónica de hello, los productores y consumidores no necesitan ser en línea en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="b8b8e-131">Bus de servicio almacena de forma confiable los mensajes hasta que esté preparada para recibirlos, parte consumidora Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="b8b8e-132">Esto permite a los componentes de Hola de toobe de aplicación Hola distribuido desconectados, ya sea voluntariamente, por ejemplo, para mantenimiento o debido a un bloqueo del componente tooa, sin afectar a todo el sistema.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="b8b8e-133">Además, Hola consumiendo aplicación solo necesita toocome en línea durante determinadas horas del día de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="b8b8e-134">**Redistribución de la carga.**</span><span class="sxs-lookup"><span data-stu-id="b8b8e-134">**Load leveling.**</span></span> <span data-ttu-id="b8b8e-135">En muchas aplicaciones, la carga del sistema cambia con el tiempo, mientras el tiempo de procesamiento de hello necesario para cada unidad de trabajo es normalmente constante.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="b8b8e-136">Intermediar de mensaje de productores y consumidores con una cola significa que Hola consumiendo toobe de necesidades de aplicación (trabajo hello) solo aprovisionado carga media de tooaccommodate en lugar de carga máxima.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="b8b8e-137">profundidad de Hola de cola de hello aumenta y disminuye medida que varía la carga entrante Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="b8b8e-138">Esto directamente ahorra dinero en cuanto a la cantidad de Hola de carga de aplicaciones de infraestructura necesario tooservice Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="b8b8e-139">**Equilibrio de carga.**</span><span class="sxs-lookup"><span data-stu-id="b8b8e-139">**Load balancing.**</span></span> <span data-ttu-id="b8b8e-140">Conforme aumenta la carga, más procesos de trabajo se pueden agregar tooread de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="b8b8e-141">Cada mensaje se procesa solamente mediante uno de los procesos de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="b8b8e-142">Además, este equilibrio de carga basados en extracción permite un uso óptimo de los equipos de trabajo de hello incluso si los equipos de trabajo difieren en cuanto a capacidad de procesamiento, ya que extraerán mensajes a su propia velocidad máxima.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="b8b8e-143">Este patrón se denomina a menudo hello *consumidor en competencia* patrón.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="b8b8e-144">Hola las secciones siguientes tratan sobre código de hello que implementa esta arquitectura.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="b8b8e-145">Configurar el entorno de desarrollo de Hola</span><span class="sxs-lookup"><span data-stu-id="b8b8e-145">Set up hello development environment</span></span>
<span data-ttu-id="b8b8e-146">Antes de empezar a desarrollar aplicaciones de Azure, obtener herramientas de Hola y configurar el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="b8b8e-147">Instalar hello Azure SDK para .NET de hello SDK [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b8b8e-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="b8b8e-148">Hola **.NET** columna, haga clic en la versión de Hola de [Visual Studio](http://www.visualstudio.com) que usa.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="b8b8e-149">Hola los pasos de este tutorial, use Visual Studio 2015, pero también funcionan con Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="b8b8e-150">Cuando se le pida toorun o guardar el instalador de hello, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="b8b8e-151">Hola **instalador de plataforma Web**, haga clic en **instalar** y continuar con la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="b8b8e-152">Una vez completada la instalación de hello, tendrá todo lo necesario toostart toodevelop Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="b8b8e-153">Hola SDK incluye herramientas que le permiten desarrollar fácilmente aplicaciones de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="b8b8e-154">Creación de un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="b8b8e-154">Create a namespace</span></span>
<span data-ttu-id="b8b8e-155">Hola siguiente paso es toocreate un espacio de nombres de servicio y obtener una clave de firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="b8b8e-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="b8b8e-156">Un espacio de nombres proporciona un límite de aplicación para cada aplicación que se expone a través del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="b8b8e-157">Cuando se crea un espacio de nombres, se genera una clave SAS sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="b8b8e-158">combinación de Hola de espacio de nombres y la clave SAS proporciona credenciales de Hola para aplicación de Bus de servicio tooauthenticate acceso tooan.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="b8b8e-159">Creación de un rol web</span><span class="sxs-lookup"><span data-stu-id="b8b8e-159">Create a web role</span></span>
<span data-ttu-id="b8b8e-160">En esta sección, creará front-end de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="b8b8e-161">En primer lugar, cree páginas de Hola que muestra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="b8b8e-162">A continuación, agregue código que envía la cola de Bus de servicio tooa los elementos y se muestra información de estado acerca de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="b8b8e-163">Crear proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="b8b8e-163">Create hello project</span></span>
1. <span data-ttu-id="b8b8e-164">Con privilegios de administrador, inicie Visual Studio: Hola contextual **Visual Studio** icono del programa y, a continuación, haga clic en **ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="b8b8e-165">emulador de proceso de Azure de Hello, descrito más adelante en este artículo, requiere que se puede iniciar Visual Studio con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="b8b8e-166">En Visual Studio, en hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="b8b8e-167">En **Plantillas instaladas**, en **Visual C#**, haga clic en **Nube** y, a continuación, en **Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="b8b8e-168">Proyecto de hello Name **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="b8b8e-169">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="b8b8e-170">En los roles de **.NET Framework 4.5**, haga doble clic en **Rol web de ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="b8b8e-171">Mantenga el mouse sobre **WebRole1** en **solución de servicio de nube de Azure**, haga clic en el icono de lápiz hello y cambiar el nombre de rol web de hello demasiado**FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="b8b8e-172">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-172">Then click **OK**.</span></span> <span data-ttu-id="b8b8e-173">(Asegúrese de que escribe "Frontend" con "e" minúscula, no "FrontEnd").</span><span class="sxs-lookup"><span data-stu-id="b8b8e-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="b8b8e-174">De hello **nuevo proyecto ASP.NET** cuadro de diálogo hello **seleccione una plantilla de** lista, haga clic en **MVC**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="b8b8e-175">Aún en hello **nuevo proyecto ASP.NET** diálogo cuadro, haga clic en hello **Cambiar autenticación** botón.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="b8b8e-176">Hola **Cambiar autenticación** cuadro de diálogo, haga clic en **sin autenticación**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="b8b8e-177">En este tutorial, va a implementar una aplicación que no necesita un inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="b8b8e-178">Nuevo en hello **nuevo proyecto ASP.NET** cuadro de diálogo, haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="b8b8e-179">En **el Explorador de soluciones**, Hola **FrontendWebRole** proyecto de equipo y haga clic en **referencias**, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="b8b8e-180">Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="b8b8e-181">Seleccione hello **WindowsAzure.ServiceBus** del paquete, haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="b8b8e-182">Tenga en cuenta que Hola ahora ensamblados de cliente al que se hace referencia y se han agregado algunos nuevos archivos de código.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="b8b8e-183">En el **Explorador de soluciones**, haga clic con el botón derecho en **Modelos** y, luego, en **Agregar** y, por último, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="b8b8e-184">Hola **nombre** cuadro, escriba un nombre hello **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="b8b8e-185">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="b8b8e-186">Escribir código de hello para el rol web</span><span class="sxs-lookup"><span data-stu-id="b8b8e-186">Write hello code for your web role</span></span>
<span data-ttu-id="b8b8e-187">En esta sección, creará Hola distintas páginas que muestra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="b8b8e-188">En el archivo de OnlineOrder.cs hello en Visual Studio, reemplace la definición de espacio de nombres existente con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="b8b8e-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
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
2. <span data-ttu-id="b8b8e-189">En el **Explorador de soluciones**, haga doble clic en **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="b8b8e-190">Agregue Hola siguiente **con** las instrucciones en la parte superior de Hola de hello tooinclude Hola espacios de nombres para el modelo que acaba de crear, así como de Bus de servicio de archivos.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="b8b8e-191">También en el archivo HomeController.cs de hello en Visual Studio, reemplace la definición de espacio de nombres existente con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="b8b8e-192">Este código contiene métodos para controlar la presentación de Hola de cola de toohello los elementos.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
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
4. <span data-ttu-id="b8b8e-193">De hello **generar** menú, haga clic en **generar solución** precisión de hello tootest de su trabajo hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="b8b8e-194">Ahora, crear vista de Hola para hello `Submit()` método que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="b8b8e-195">Haga clic en hello `Submit()` método (sobrecarga Hola de `Submit()` que no toma ningún parámetro) y, a continuación, elija **agregar vista**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="b8b8e-196">Aparece un cuadro de diálogo para crear vista Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="b8b8e-197">Hola **plantilla** elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="b8b8e-198">Hola **clase modelo** lista, haga clic en hello **OnlineOrder** clase.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="b8b8e-199">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-199">Click **Add**.</span></span>
8. <span data-ttu-id="b8b8e-200">Ahora, cambie el nombre hello muestra de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="b8b8e-201">En **el Explorador de soluciones**, haga doble clic en el **Views\Shared\\_Layout.cshtml** tooopen de archivos en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="b8b8e-202">Reemplace todas las apariciones de **My ASP.NET Application** por **Productos de LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="b8b8e-203">Quitar hello **inicio**, **sobre**, y **póngase en contacto con** vínculos.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="b8b8e-204">Eliminar código de hello resaltado:</span><span class="sxs-lookup"><span data-stu-id="b8b8e-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="b8b8e-205">Por último, modifique Hola envío página tooinclude cierta información acerca de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="b8b8e-206">En **el Explorador de soluciones**, haga doble clic en el **Views\Home\Submit.cshtml** tooopen de archivos en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="b8b8e-207">Hola después de línea después de agregar `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="b8b8e-208">Por ahora, Hola `ViewBag.MessageCount` está vacía.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="b8b8e-209">Lo rellenará más adelante.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="b8b8e-210">Acaba de implementar su interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-210">You now have implemented your UI.</span></span> <span data-ttu-id="b8b8e-211">Puede presionar **F5** toorun la aplicación y confirme que lo haga según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="b8b8e-212">Escribir código de hello para el envío de cola de Bus de servicio tooa los elementos</span><span class="sxs-lookup"><span data-stu-id="b8b8e-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="b8b8e-213">Ahora, agregue código para el envío de cola de tooa los elementos.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="b8b8e-214">En primer lugar, va a crear una clase que contiene la información de conexión a la cola del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="b8b8e-215">A continuación, inicialice la conexión en Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="b8b8e-216">Por último, actualizar código de envío de Hola que creó anteriormente en la cola de Bus de servicio de tooa de HomeController.cs tooactually enviar elementos.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="b8b8e-217">En **el Explorador de soluciones**, haga clic en **FrontendWebRole** (proyecto de Hola de menú contextual, no Hola rol).</span><span class="sxs-lookup"><span data-stu-id="b8b8e-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="b8b8e-218">Haga clic en **Agregar** y, a continuación, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="b8b8e-219">Nombre de la clase hello **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="b8b8e-220">Haga clic en **agregar** clase de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="b8b8e-221">Ahora, agregue código que encapsula la información de conexión de hello e inicializa la cola de Bus de servicio de hello conexión tooa.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="b8b8e-222">Reemplace Hola todo contenido de QueueConnector.cs con el siguiente código de hello y especifique los valores de `your Service Bus namespace` (el nombre de espacio de nombres) y `yourKey`, que es hello **clave principal** ha obtenido anteriormente de hello Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
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
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="b8b8e-223">Ahora, asegúrese de que se llama al método **Initialize**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="b8b8e-224">En el **Explorador de soluciones**, haga doble clic en **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="b8b8e-225">Agregar Hola después de la línea de código al final de Hola de hello **Application_Start** método.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="b8b8e-226">Por último, actualizar código de hello web que creó anteriormente, para enviar elementos toohello cola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="b8b8e-227">En el **Explorador de soluciones**, haga doble clic en **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="b8b8e-228">Hola de actualización `Submit()` método (sobrecarga de Hola que no toma ningún parámetro) como se indica a continuación tooget Hola número de mensajes para la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="b8b8e-229">Hola de actualización `Submit(OnlineOrder order)` método (sobrecarga de Hola que toma un parámetro) como se indica a continuación toosubmit ordenar cola toohello de información.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="b8b8e-230">Ahora puede ejecutar la aplicación hello nuevo.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-230">You can now run hello application again.</span></span> <span data-ttu-id="b8b8e-231">Cada vez que envíe un pedido, aumenta el número de mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="b8b8e-232">Crear rol de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="b8b8e-232">Create hello worker role</span></span>
<span data-ttu-id="b8b8e-233">Rol de trabajo de Hola que procesa los envíos de orden de hello creará ahora.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="b8b8e-234">Este ejemplo utiliza hello **rol de trabajo con cola de Service Bus** plantilla de proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="b8b8e-235">Ya obtenido credenciales Hola necesario desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="b8b8e-236">Asegúrese de que se ha conectado a Visual Studio tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="b8b8e-237">En Visual Studio, en **el Explorador de soluciones** haga clic en el **Roles** carpeta bajo hello **MultiTierApp** proyecto.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="b8b8e-238">Haga clic en **Agregar** y, a continuación, en **Nuevo proyecto de rol de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="b8b8e-239">Hola **Agregar nuevo proyecto de rol** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="b8b8e-240">Hola **Agregar nuevo proyecto de rol** cuadro de diálogo, haga clic en **rol de trabajo con cola de Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="b8b8e-241">Hola **nombre** cuadro, proyecto de hello name **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="b8b8e-242">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-242">Then click **Add**.</span></span>
6. <span data-ttu-id="b8b8e-243">Copie la cadena de conexión de Hola que obtuvo en el paso 9 del Portapapeles de toohello de sección de Hola "Crear un espacio de nombres de Bus de servicio".</span><span class="sxs-lookup"><span data-stu-id="b8b8e-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="b8b8e-244">En **el Explorador de soluciones**, contextual hello **OrderProcessingRole** que creó en el paso 5 (asegúrese de que haga **OrderProcessingRole** en **Roles**, y no Hola clase).</span><span class="sxs-lookup"><span data-stu-id="b8b8e-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="b8b8e-245">A continuación, haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="b8b8e-246">En hello **configuración** ficha de hello **propiedades** cuadro de diálogo, haga clic dentro de hello **valor** cuadro **Microsoft.ServiceBus.ConnectionString**y, a continuación, pegue el valor de punto de conexión de Hola que copió en el paso 6.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="b8b8e-247">Crear un **OnlineOrder** clase toorepresent Hola pedidos como procesarlos de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="b8b8e-248">Puede reutilizar una clase que ya ha creado.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="b8b8e-249">En **el Explorador de soluciones**, contextual hello **OrderProcessingRole** clase (icono de clase de Hola de menú contextual, no Hola rol).</span><span class="sxs-lookup"><span data-stu-id="b8b8e-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="b8b8e-250">Haga clic en **Agregar** y, a continuación, en **Elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="b8b8e-251">Busque la subcarpeta toohello para **FrontendWebRole\Models**y, a continuación, haga doble clic en **OnlineOrder.cs** tooadd se toothis proyecto.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="b8b8e-252">En **WorkerRole.cs**, cambiar el valor Hola de hello **QueueName** variables de `"ProcessingQueue"` demasiado`"OrdersQueue"` tal y como se muestra en el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="b8b8e-253">Agregue los siguiente Hola using instrucción Hola principio del archivo WorkerRole.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="b8b8e-254">Hola `Run()` función dentro de hello `OnMessage()` llamar a, reemplace el contenido de Hola de hello `try` cláusula con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="b8b8e-255">Ha completado la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-255">You have completed hello application.</span></span> <span data-ttu-id="b8b8e-256">Puede probar la aplicación completa de hello haciendo clic en proyecto de MultiTierApp hello en el Explorador de soluciones, seleccione **establecer como proyecto de inicio**y, a continuación, presione la tecla F5.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="b8b8e-257">Tenga en cuenta que el número de mensajes no se incrementa, porque el rol de trabajo de hello procesa elementos de cola de Hola y las marca como completa.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="b8b8e-258">Puede ver los resultados de seguimiento de Hola de su rol de trabajo mediante la visualización Hola IU del emulador de proceso de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="b8b8e-259">Puede hacerlo haciendo clic en el icono del emulador Hola Hola área de notificación de la barra de tareas y seleccionando **Mostrar IU del emulador de proceso**.</span><span class="sxs-lookup"><span data-stu-id="b8b8e-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="b8b8e-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8b8e-260">Next steps</span></span>
<span data-ttu-id="b8b8e-261">toolearn más información acerca de Bus de servicio, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b8b8e-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="b8b8e-262">[Documentación de Azure Service Bus][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="b8b8e-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="b8b8e-263">[Página de servicio de Service Bus][sbacom]</span><span class="sxs-lookup"><span data-stu-id="b8b8e-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="b8b8e-264">[¿Cómo tooUse colas de Service Bus][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="b8b8e-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="b8b8e-265">toolearn más información acerca de los escenarios de varios niveles, vea:</span><span class="sxs-lookup"><span data-stu-id="b8b8e-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="b8b8e-266">[Aplicación de niveles múltiples .NET mediante tablas, colas y blobs de Storage][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="b8b8e-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

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

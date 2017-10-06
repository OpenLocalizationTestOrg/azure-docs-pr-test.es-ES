---
title: uso de tooenable de contexto de usuario de aaaSending experiencias en Azure Application Insights | Documentos de Microsoft
description: "Realice un seguimiento de cómo los usuarios navegan por el servicio mediante la asignación a cada uno de ellos de una cadena de identificador única y persistente en Application Insights."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="af01a-103">Uso de tooenable de contexto de usuario envío experiencias en Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="af01a-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="af01a-104">Seguimiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="af01a-104">Tracking users</span></span>

<span data-ttu-id="af01a-105">Application Insights permite toomonitor y realizar un seguimiento de los usuarios a través de un conjunto de herramientas de uso del producto:</span><span class="sxs-lookup"><span data-stu-id="af01a-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="af01a-106">Usuarios, sesiones, eventos</span><span class="sxs-lookup"><span data-stu-id="af01a-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="af01a-107">Embudos</span><span class="sxs-lookup"><span data-stu-id="af01a-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="af01a-108">Retención</span><span class="sxs-lookup"><span data-stu-id="af01a-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="af01a-109">Cohortes</span><span class="sxs-lookup"><span data-stu-id="af01a-109">Cohorts</span></span>
* [<span data-ttu-id="af01a-110">Libros</span><span class="sxs-lookup"><span data-stu-id="af01a-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="af01a-111">En orden tootrack lo que un usuario realiza por tiempo, Application Insights necesita un identificador para cada usuario o la sesión.</span><span class="sxs-lookup"><span data-stu-id="af01a-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="af01a-112">Incluya estos identificadores en cada evento personalizado o vista de página.</span><span class="sxs-lookup"><span data-stu-id="af01a-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="af01a-113">Usuarios, embudos, retención y cohortes: incluya el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="af01a-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="af01a-114">Sesiones: incluya el identificador de sesión.</span><span class="sxs-lookup"><span data-stu-id="af01a-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="af01a-115">Si la aplicación se integra con hello [SDK de JavaScript](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), es un seguimiento automático de Id. de usuario.</span><span class="sxs-lookup"><span data-stu-id="af01a-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="af01a-116">Elección de los identificadores de usuario</span><span class="sxs-lookup"><span data-stu-id="af01a-116">Choosing user IDs</span></span>

<span data-ttu-id="af01a-117">Id. de usuario debe conservarse en tootrack de sesiones de usuario el comportan de los usuarios con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="af01a-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="af01a-118">Hay varios enfoques para conservar Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="af01a-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="af01a-119">Una definición de un usuario que ya tiene en su servicio.</span><span class="sxs-lookup"><span data-stu-id="af01a-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="af01a-120">Si el servicio de Hola tiene explorador tooa de acceso, puede pasar una cookie con un Id. explorador hello en ella.</span><span class="sxs-lookup"><span data-stu-id="af01a-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="af01a-121">Id. de Hola se conservará para siempre que la cookie de hello permanezca en el explorador del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="af01a-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="af01a-122">Si es necesario, puede utilizar un nuevo identificador de cada sesión, pero se limitarán los resultados de hello acerca de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="af01a-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="af01a-123">Por ejemplo, no será capaz de toosee cómo cambia el comportamiento de un usuario con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="af01a-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="af01a-124">Hola identificador debe ser un Guid u otra cadena tooidentify lo suficientemente compleja como cada usuario forma única.</span><span class="sxs-lookup"><span data-stu-id="af01a-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="af01a-125">Por ejemplo, podría ser un número aleatorio largo.</span><span class="sxs-lookup"><span data-stu-id="af01a-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="af01a-126">Si identificador hello contiene información de identificación personal sobre el usuario de hello, no es un tooApplication de toosend visión de valor adecuado como un identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="af01a-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="af01a-127">Puede enviar un Id. como un [autenticado Id. de usuario](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), pero no cumple requisito de Id. de usuario de Hola para escenarios de uso.</span><span class="sxs-lookup"><span data-stu-id="af01a-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="af01a-128">Aplicaciones ASP.NET: Establecimiento del contexto de usuario en un inicializador de telemetría</span><span class="sxs-lookup"><span data-stu-id="af01a-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="af01a-129">Crear un inicializador de telemetría, tal y como se describe en detalle [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)y establezca Hola Context.User.Id y Hola Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="af01a-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="af01a-130">Este ejemplo establece el identificador de tooan de Id. de usuario de Hola que expira después de la sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="af01a-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="af01a-131">Si es posible, use un identificador de usuario que se conserve entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="af01a-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="af01a-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="af01a-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="af01a-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af01a-133">Next steps</span></span>
- <span data-ttu-id="af01a-134">uso de tooenable experimenta, empezar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [página vistas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="af01a-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="af01a-135">Si ya envía eventos personalizados o las vistas de página, explorar Hola uso herramientas toolearn cómo los usuarios utilizar el servicio.</span><span class="sxs-lookup"><span data-stu-id="af01a-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="af01a-136">Información general del uso</span><span class="sxs-lookup"><span data-stu-id="af01a-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="af01a-137">Usuarios, sesiones y eventos</span><span class="sxs-lookup"><span data-stu-id="af01a-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="af01a-138">Embudos</span><span class="sxs-lookup"><span data-stu-id="af01a-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="af01a-139">Retención</span><span class="sxs-lookup"><span data-stu-id="af01a-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="af01a-140">Libros</span><span class="sxs-lookup"><span data-stu-id="af01a-140">Workbooks</span></span>](app-insights-usage-workbooks.md)

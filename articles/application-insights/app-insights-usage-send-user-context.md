---
title: "Envío contexto de usuario para habilitar las experiencias de uso en Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 9350029c775643be0dcc679b0f4bb9238b5f8aca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
#  <a name="sending-user-context-to-enable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="4c9e0-103">Envío contexto de usuario para habilitar las experiencias de uso en Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="4c9e0-103">Sending user context to enable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="4c9e0-104">Seguimiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="4c9e0-104">Tracking users</span></span>

<span data-ttu-id="4c9e0-105">Application Insights le permite supervisar y realizar un seguimiento de los usuarios a través de un conjunto de herramientas de uso del producto:</span><span class="sxs-lookup"><span data-stu-id="4c9e0-105">Application Insights enables you to monitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="4c9e0-106">Usuarios, sesiones, eventos</span><span class="sxs-lookup"><span data-stu-id="4c9e0-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="4c9e0-107">Embudos</span><span class="sxs-lookup"><span data-stu-id="4c9e0-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="4c9e0-108">Retención</span><span class="sxs-lookup"><span data-stu-id="4c9e0-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="4c9e0-109">Cohortes</span><span class="sxs-lookup"><span data-stu-id="4c9e0-109">Cohorts</span></span>
* [<span data-ttu-id="4c9e0-110">Libros</span><span class="sxs-lookup"><span data-stu-id="4c9e0-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="4c9e0-111">Para realizar un seguimiento de lo que hace un usuario a lo largo del tiempo, Application Insights necesita un identificador para cada usuario o sesión.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-111">In order to track what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="4c9e0-112">Incluya estos identificadores en cada evento personalizado o vista de página.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="4c9e0-113">Usuarios, embudos, retención y cohortes: incluya el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="4c9e0-114">Sesiones: incluya el identificador de sesión.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="4c9e0-115">Si la aplicación se integra con el [SDK de JavaScript](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), se podrá hacer el seguimiento del identificador de usuario de forma automática.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-115">If your app is integrated with the [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="4c9e0-116">Elección de los identificadores de usuario</span><span class="sxs-lookup"><span data-stu-id="4c9e0-116">Choosing user IDs</span></span>

<span data-ttu-id="4c9e0-117">Los identificadores de usuario se deben conservar entre las sesiones de usuario para realizar un seguimiento de cómo se comportan los usuarios con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-117">User IDs should persist across user sessions to track how users behave over time.</span></span> <span data-ttu-id="4c9e0-118">Hay varios enfoques para conservar el identificador.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-118">There are various approaches for persisting the ID.</span></span>
- <span data-ttu-id="4c9e0-119">Una definición de un usuario que ya tiene en su servicio.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="4c9e0-120">Si el servicio tiene acceso a un explorador, puede pasar a este una cookie con un identificador en ella.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-120">If the service has access to a browser, it can pass the browser a cookie with an ID in it.</span></span> <span data-ttu-id="4c9e0-121">El identificador se conservará siempre que la cookie permanezca en el explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-121">The ID will persist for as long as the cookie remains in the user's browser.</span></span>
- <span data-ttu-id="4c9e0-122">Si es necesario, puede usar un nuevo identificador en cada sesión, pero los resultados sobre los usuarios serán limitados.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-122">If necessary, you can use a new ID each session, but the results about users will be limited.</span></span> <span data-ttu-id="4c9e0-123">Por ejemplo, no podrá ver cómo cambia el comportamiento de un usuario con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-123">For example, you won't be able to see how a user's behavior changes over time.</span></span>

<span data-ttu-id="4c9e0-124">El identificador debe ser un GUID u otra cadena lo suficientemente compleja como para identificar de forma única a cada usuario.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-124">The ID should be a Guid or another string complex enough to identify each user uniquely.</span></span> <span data-ttu-id="4c9e0-125">Por ejemplo, podría ser un número aleatorio largo.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="4c9e0-126">Si el identificador contiene información de identificación personal sobre el usuario, no es un valor adecuado para enviarlo a Application Insights como identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-126">If the ID contains personally identifying information about the user, it is not an appropriate value to send to Application Insights as a user ID.</span></span> <span data-ttu-id="4c9e0-127">Puede enviar un identificador de ese tipo como [identificador de usuario autenticado](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), pero no cumplirá el requisito de identificador de usuario para los escenarios de uso.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill the user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="4c9e0-128">Aplicaciones ASP.NET: Establecimiento del contexto de usuario en un inicializador de telemetría</span><span class="sxs-lookup"><span data-stu-id="4c9e0-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="4c9e0-129">Cree un inicializador de telemetría, tal y como se describe detalladamente [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer) y establezca el Context.User.Id y el Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set the Context.User.Id and the Context.Session.Id.</span></span>

<span data-ttu-id="4c9e0-130">Este ejemplo establece el identificador de usuario en un identificador que expira después de la sesión.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-130">This example sets the user ID to an identifier that expires after the session.</span></span> <span data-ttu-id="4c9e0-131">Si es posible, use un identificador de usuario que se conserve entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="4c9e0-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="4c9e0-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets the user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on the HttpContext Session.
            // Set the user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set the user id on the Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set the session id on the Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="4c9e0-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c9e0-133">Next steps</span></span>
- <span data-ttu-id="4c9e0-134">Para habilitar las experiencias de uso, empiece por enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [vistas de páginas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="4c9e0-134">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="4c9e0-135">Si ya ha enviado eventos personalizados o vistas de página, explore las herramientas de uso para obtener información sobre cómo los usuarios utilizan el servicio.</span><span class="sxs-lookup"><span data-stu-id="4c9e0-135">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    * [<span data-ttu-id="4c9e0-136">Información general del uso</span><span class="sxs-lookup"><span data-stu-id="4c9e0-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="4c9e0-137">Usuarios, sesiones y eventos</span><span class="sxs-lookup"><span data-stu-id="4c9e0-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="4c9e0-138">Embudos</span><span class="sxs-lookup"><span data-stu-id="4c9e0-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="4c9e0-139">Retención</span><span class="sxs-lookup"><span data-stu-id="4c9e0-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="4c9e0-140">Libros</span><span class="sxs-lookup"><span data-stu-id="4c9e0-140">Workbooks</span></span>](app-insights-usage-workbooks.md)

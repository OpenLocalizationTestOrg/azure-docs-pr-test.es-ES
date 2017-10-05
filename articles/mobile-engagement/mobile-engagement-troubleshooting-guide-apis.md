---
title: "Guía de solución de problemas de Azure Mobile Engagement - API"
description: "Guías de solución de problemas de Azure Mobile Engagement - API"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: a7ae0a83046f2d67b790f672dcd3ae261987357a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="87ad2-103">Guía de solución de problemas de la API</span><span class="sxs-lookup"><span data-stu-id="87ad2-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="87ad2-104">Los siguientes son posibles problemas que pueden producirse con cómo los administradores interactúan con Azure Mobile Engagement a través de las API.</span><span class="sxs-lookup"><span data-stu-id="87ad2-104">The following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via the APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="87ad2-105">Problemas de sintaxis</span><span class="sxs-lookup"><span data-stu-id="87ad2-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="87ad2-106">Problema</span><span class="sxs-lookup"><span data-stu-id="87ad2-106">Issue</span></span>
* <span data-ttu-id="87ad2-107">Errores de sintaxis mediante la API (o un comportamiento inesperado).</span><span class="sxs-lookup"><span data-stu-id="87ad2-107">Syntax Errors using the API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="87ad2-108">Causas</span><span class="sxs-lookup"><span data-stu-id="87ad2-108">Causes</span></span>
* <span data-ttu-id="87ad2-109">Problemas de sintaxis:</span><span class="sxs-lookup"><span data-stu-id="87ad2-109">Syntax issues:</span></span>
  * <span data-ttu-id="87ad2-110">Asegúrese de comprobar la sintaxis de la API específica que se utiliza para confirmar que la opción está disponible.</span><span class="sxs-lookup"><span data-stu-id="87ad2-110">Make sure to check the Syntax of the specific API you are using to confirm that the option is available.</span></span>
  * <span data-ttu-id="87ad2-111">Un problema común con el uso de la API consiste en confundir la API de cobertura y la API de inserción (la mayoría de las tareas debe realizarse con la API de cobertura en lugar de la API de inserción).</span><span class="sxs-lookup"><span data-stu-id="87ad2-111">A common issue with API usage is to confuse the Reach API and the Push API (most tasks should be performed with the Reach API instead of the Push API).</span></span> 
  * <span data-ttu-id="87ad2-112">Otro problema común con la integración del SDK y el uso de la API es confundir la clave del SDK y la clave de la API.</span><span class="sxs-lookup"><span data-stu-id="87ad2-112">Another common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>
  * <span data-ttu-id="87ad2-113">Las secuencias de comandos que se conectan a las API necesitan enviar datos al menos cada 10 minutos o la conexión agotará el tiempo de espera (especialmente frecuente en secuencias de comandos de API de supervisión que escuchan datos).</span><span class="sxs-lookup"><span data-stu-id="87ad2-113">Scripts that connect to the APIs need to send data at least every 10 minutes or the connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="87ad2-114">Para evitar los tiempos de espera, haga que la secuencia de comandos envíe un ping XMPP cada 10 minutos para mantener la sesión activa con el servidor.</span><span class="sxs-lookup"><span data-stu-id="87ad2-114">To prevent timeouts, have your script send an XMPP ping every 10 minutes to keep the session alive with the server.</span></span>

### <a name="see-also"></a><span data-ttu-id="87ad2-115">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="87ad2-115">See also</span></span>
* <span data-ttu-id="87ad2-116">[Documentación de la API][Link 4]</span><span class="sxs-lookup"><span data-stu-id="87ad2-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="87ad2-117">Información del protocolo XMPP</span><span class="sxs-lookup"><span data-stu-id="87ad2-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-to-use-the-api-to-perform-the-same-action-available-in-the-azure-mobile-engagement-ui"></a><span data-ttu-id="87ad2-118">No se puede usar la API para realizar la misma acción disponible en la interfaz de usuario de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="87ad2-118">Unable to use the API to perform the same action available in the Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="87ad2-119">Problema</span><span class="sxs-lookup"><span data-stu-id="87ad2-119">Issue</span></span>
* <span data-ttu-id="87ad2-120">Una acción que funciona desde la interfaz de usuario de Azure Mobile Engagement no funciona desde la API de Azure Mobile Engagement relacionada.</span><span class="sxs-lookup"><span data-stu-id="87ad2-120">An action that works from the Azure Mobile Engagement UI doesn't work from the related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="87ad2-121">Causas</span><span class="sxs-lookup"><span data-stu-id="87ad2-121">Causes</span></span>
* <span data-ttu-id="87ad2-122">Confirmar que puede realizar la misma acción desde la interfaz de usuario de Azure Mobile Engagement muestra que ha integrado correctamente esta función de Azure Mobile Engagement con el SDK.</span><span class="sxs-lookup"><span data-stu-id="87ad2-122">Confirming that you can perform the same action from the Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with the SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="87ad2-123">Consulte también</span><span class="sxs-lookup"><span data-stu-id="87ad2-123">See also</span></span>
* <span data-ttu-id="87ad2-124">[Documentación de la interfaz de usuario][Link 1]</span><span class="sxs-lookup"><span data-stu-id="87ad2-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="87ad2-125">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="87ad2-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="87ad2-126">Problema</span><span class="sxs-lookup"><span data-stu-id="87ad2-126">Issue</span></span>
* <span data-ttu-id="87ad2-127">Códigos de error mediante la API que se muestra en el tiempo de ejecución o en los registros.</span><span class="sxs-lookup"><span data-stu-id="87ad2-127">Error codes using the API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="87ad2-128">Causas</span><span class="sxs-lookup"><span data-stu-id="87ad2-128">Causes</span></span>
* <span data-ttu-id="87ad2-129">A continuación se muestra una lista compuesta de números de códigos de estado de API comunes de referencia y de solución de problemas preliminar:</span><span class="sxs-lookup"><span data-stu-id="87ad2-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from the current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in the response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). The parameters provided to the API or service are invalid. In this case, the HTTP response will embed more details. Make sure to test for the MIME type of the response as the payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check the AppID and SDK key).
        402        Billing lock. The application is either off its quotas or is currently in a bad billing state.
        403        The application is not enabled or the specific API is disabled for this application.
        403        Unauthorized access to the project or application, invalid access key (the key must match the one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), the suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and the campaign’s property named, manual Push must be set to true.
        403        The email address is already associated to another account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        The email address is not associated with an account. Please create or update the account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying to edit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for the first time.
        409        Name already associated to a different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or the period is too large to be displayed (the server didn’t retrieve the analytics because the user request is for a period that is too large).
        503        Analytics not available yet (the requested information is not computed yet for an application).
        504        The server was not able to handle your request in a reasonable time (if you make multiple calls to an API very quickly, try to make one call at a time and spread the calls out over time).

### <a name="see-also"></a><span data-ttu-id="87ad2-130">Consulte también</span><span class="sxs-lookup"><span data-stu-id="87ad2-130">See also</span></span>
* <span data-ttu-id="87ad2-131">[Documentación de API: para errores detallados en cada API específica][Link 4]</span><span class="sxs-lookup"><span data-stu-id="87ad2-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="87ad2-132">Errores silenciosos</span><span class="sxs-lookup"><span data-stu-id="87ad2-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="87ad2-133">Problema</span><span class="sxs-lookup"><span data-stu-id="87ad2-133">Issue</span></span>
* <span data-ttu-id="87ad2-134">Se produce un error en la acción de la API sin que se muestre ningún mensaje de error en el tiempo de ejecución o en los registros.</span><span class="sxs-lookup"><span data-stu-id="87ad2-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="87ad2-135">Causas</span><span class="sxs-lookup"><span data-stu-id="87ad2-135">Causes</span></span>
* <span data-ttu-id="87ad2-136">Muchos elementos se deshabilitarán en la interfaz de usuario de Azure Mobile Engagement si no se integran correctamente, pero se producirá un error silenciosamente a través de la API, por lo tanto, no olvide probar la misma funcionalidad desde la interfaz de usuario para ver si funciona.</span><span class="sxs-lookup"><span data-stu-id="87ad2-136">Many items will be disabled in the Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from the API, so remember to test the same functionality from the UI to see if it works.</span></span>
* <span data-ttu-id="87ad2-137">Azure Mobile Engagement y muchas funciones avanzadas de Azure Mobile Engagement que está intentando usar necesitan integrarse individualmente en su aplicación con el SDK en pasos distintos para poder utilizarlas.</span><span class="sxs-lookup"><span data-stu-id="87ad2-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting to use, need to be individually integrated into your app with the SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="87ad2-138">Consulte también</span><span class="sxs-lookup"><span data-stu-id="87ad2-138">See also</span></span>
* <span data-ttu-id="87ad2-139">[Guía de solución de problemas: SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="87ad2-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md


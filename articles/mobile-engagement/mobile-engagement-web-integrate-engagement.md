---
title: "Integración del SDK web de Azure Mobile Engagement | Microsoft Docs"
description: "Actualizaciones y procedimientos más recientes para el SDK web de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="5f676-103">Integración de Azure Mobile Engagement en una aplicación web</span><span class="sxs-lookup"><span data-stu-id="5f676-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f676-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="5f676-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="5f676-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="5f676-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="5f676-106">iOS</span><span class="sxs-lookup"><span data-stu-id="5f676-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="5f676-107">Android</span><span class="sxs-lookup"><span data-stu-id="5f676-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="5f676-108">En este procedimiento se describe la manera más sencilla de activar las funciones de análisis y supervisión de Azure Mobile Engagement en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5f676-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="5f676-109">Siga los pasos para activar los informes de registro necesarios para calcular todas las estadísticas acerca de los usuarios, las sesiones, las actividades, los bloqueos y los aspectos técnicos.</span><span class="sxs-lookup"><span data-stu-id="5f676-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="5f676-110">Para las estadísticas que dependen de la aplicación, tales como eventos, errores y trabajos, debe activar los informes de registro manualmente mediante la API de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="5f676-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="5f676-111">Para más información, aprenda a [usar la API de etiquetado de Mobile Engagement en una aplicación web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="5f676-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="5f676-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="5f676-112">Introduction</span></span>
<span data-ttu-id="5f676-113">[Descargue el SDK web de Azure Mobile Engagement](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="5f676-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="5f676-114">El SDK web de Mobile Engagement se distribuye como un único archivo de JavaScript llamado azure-engagement.js, que se debe incluir en cada página del sitio o aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5f676-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f676-115">Antes de ejecutar este script, debe ejecutar un fragmento de código o script que escriba para configurar Mobile Engagement para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f676-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="5f676-116">Compatibilidad con el explorador</span><span class="sxs-lookup"><span data-stu-id="5f676-116">Browser compatibility</span></span>
<span data-ttu-id="5f676-117">El SDK web de Mobile Engagement usa codificación y descodificación JSON nativas, además de solicitudes AJAX entre dominios (basadas en la especificación CORS del W3C).</span><span class="sxs-lookup"><span data-stu-id="5f676-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="5f676-118">Es compatible con los siguientes exploradores:</span><span class="sxs-lookup"><span data-stu-id="5f676-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="5f676-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="5f676-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="5f676-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="5f676-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="5f676-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="5f676-121">Firefox 3.5+</span></span>
* <span data-ttu-id="5f676-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="5f676-122">Chrome 4+</span></span>
* <span data-ttu-id="5f676-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="5f676-123">Safari 6+</span></span>
* <span data-ttu-id="5f676-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="5f676-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="5f676-125">Configuración de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5f676-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="5f676-126">Escriba un script que cree un objeto JavaScript `azureEngagement` global como en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5f676-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="5f676-127">Como el sitio puede tener varias páginas, en el ejemplo se da por hecho que el script se incluye en cada página.</span><span class="sxs-lookup"><span data-stu-id="5f676-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="5f676-128">En el ejemplo, el objeto JavaScript se llama `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="5f676-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="5f676-129">El valor de `connectionString` para la aplicación se muestra en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5f676-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5f676-130">`appVersionName` y `appVersionCode` son opcionales.</span><span class="sxs-lookup"><span data-stu-id="5f676-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="5f676-131">Sin embargo, se recomienda configurarlos para que el análisis pueda procesar la información acerca de la versión.</span><span class="sxs-lookup"><span data-stu-id="5f676-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="5f676-132">Incorporación de scripts de Mobile Engagement en las páginas</span><span class="sxs-lookup"><span data-stu-id="5f676-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="5f676-133">Agregue scripts de Mobile Engagement a las páginas de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="5f676-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="5f676-134">O bien:</span><span class="sxs-lookup"><span data-stu-id="5f676-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="5f676-135">Alias</span><span class="sxs-lookup"><span data-stu-id="5f676-135">Alias</span></span>
<span data-ttu-id="5f676-136">Una vez cargado el script del SDK web de Mobile Engagement, crea el alias **engagement** para obtener acceso a las API del SDK.</span><span class="sxs-lookup"><span data-stu-id="5f676-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="5f676-137">Este alias no se puede usar para definir la configuración del SDK.</span><span class="sxs-lookup"><span data-stu-id="5f676-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="5f676-138">El alias se usa como referencia en esta documentación.</span><span class="sxs-lookup"><span data-stu-id="5f676-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="5f676-139">Tenga en cuenta que si el alias predeterminado entra en conflicto con otra variable global de la página, puede volver a definirlo en la configuración antes de cargar el SDK web de Mobile Engagement, de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="5f676-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="5f676-140">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="5f676-140">Basic reporting</span></span>
<span data-ttu-id="5f676-141">Los informes básicos de Mobile Engagement incluyen estadísticas de nivel de sesión, tales como estadísticas sobre usuarios, sesiones, actividades y bloqueos.</span><span class="sxs-lookup"><span data-stu-id="5f676-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="5f676-142">Seguimiento de sesión</span><span class="sxs-lookup"><span data-stu-id="5f676-142">Session tracking</span></span>
<span data-ttu-id="5f676-143">Las sesiones de Mobile Engagement se dividen en secuencias de actividades que se identifican por el nombre.</span><span class="sxs-lookup"><span data-stu-id="5f676-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="5f676-144">En un sitio web clásico, se recomienda declarar una actividad diferente en cada página del sitio.</span><span class="sxs-lookup"><span data-stu-id="5f676-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="5f676-145">Para un sitio web o aplicación web en el que la página actual nunca cambia, puede realizar un seguimiento de las actividades en una escala menor, por ejemplo, dentro de la página.</span><span class="sxs-lookup"><span data-stu-id="5f676-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="5f676-146">En cualquier caso, para iniciar o cambiar la actividad del usuario actual, llame a la función `engagement.agent.startActivity` .</span><span class="sxs-lookup"><span data-stu-id="5f676-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="5f676-147">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5f676-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="5f676-148">El servidor de Mobile Engagement finaliza una sesión abierta 3 minutos después de que se cierre la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5f676-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="5f676-149">También puede finalizar una sesión manualmente mediante una llamada a `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="5f676-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="5f676-150">Esto establece la actividad del usuario actual en ‘Idle’ (inactiva).</span><span class="sxs-lookup"><span data-stu-id="5f676-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="5f676-151">La sesión finalizará 10 segundos después, a menos que una nueva llamada a `engagement.agent.startActivity` reanude la sesión.</span><span class="sxs-lookup"><span data-stu-id="5f676-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="5f676-152">Puede configurar el retraso de 10 segundos en el objeto engagement global, de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="5f676-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="5f676-153">No puede usar `engagement.agent.endActivity` en la devolución de llamada `onunload` porque no se pueden realizar llamadas AJAX en esta etapa.</span><span class="sxs-lookup"><span data-stu-id="5f676-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="5f676-154">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="5f676-154">Advanced reporting</span></span>
<span data-ttu-id="5f676-155">De manera opcional, si desea notificar eventos, errores y trabajos específicos de la aplicación, deberá usar la API de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="5f676-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="5f676-156">Se obtiene acceso a la API de Mobile Engagement mediante el objeto `engagement.agent` .</span><span class="sxs-lookup"><span data-stu-id="5f676-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="5f676-157">Puede acceder a todas las funcionalidades avanzadas de Mobile Engagement en la API de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="5f676-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="5f676-158">La API se describe con más detalle en el artículo sobre [cómo usar la API de etiquetado avanzada de Mobile Engagement en una aplicación web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="5f676-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="5f676-159">Direcciones URL personalizadas para las llamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="5f676-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="5f676-160">Puede personalizar las direcciones URL que usa el SDK web de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="5f676-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="5f676-161">Por ejemplo, para volver a definir la dirección URL de registro (punto de conexión del SDK para el registro), puede invalidar la configuración de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="5f676-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="5f676-162">Si las funciones de la dirección URL devuelven una cadena que empieza por `/`, `//`, `http://` o `https://`, no se usa el esquema predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5f676-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="5f676-163">De forma predeterminada, para esas direcciones URL se usa el esquema `https://` .</span><span class="sxs-lookup"><span data-stu-id="5f676-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="5f676-164">Si quiere personalizar el esquema predeterminado, invalide la configuración de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="5f676-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };

---
title: "integración con el SDK de Mobile Engagement Web aaaAzure | Documentos de Microsoft"
description: "Hola actualizaciones más recientes y procedimientos para hello Web SDK de Azure Mobile Engagement"
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
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="99862-103">Integración de Azure Mobile Engagement en una aplicación web</span><span class="sxs-lookup"><span data-stu-id="99862-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99862-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="99862-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="99862-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="99862-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="99862-106">iOS</span><span class="sxs-lookup"><span data-stu-id="99862-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="99862-107">Android</span><span class="sxs-lookup"><span data-stu-id="99862-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="99862-108">procedimientos de Hello en este artículo describen los análisis de Hola de manera más sencilla de hello tooactivate y las funciones de Azure Mobile Engagement en la aplicación web de supervisión.</span><span class="sxs-lookup"><span data-stu-id="99862-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="99862-109">Siga Hola pasos tooactivate Hola informes de registro que son necesario toocompute todas las estadísticas sobre los usuarios, sesiones, actividades, se bloquea y technicals.</span><span class="sxs-lookup"><span data-stu-id="99862-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="99862-110">Para las estadísticas depende de la aplicación, como eventos y errores, trabajos, deberá activar manualmente los informes del registro mediante el uso de API de Azure Mobile Engagement Hola.</span><span class="sxs-lookup"><span data-stu-id="99862-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="99862-111">Para obtener más información, consulte [cómo toouse Hola avanzada etiquetado API en una aplicación web de Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="99862-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="99862-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="99862-112">Introduction</span></span>
<span data-ttu-id="99862-113">[Descargar SDK de Azure Mobile Engagement Web hello](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="99862-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="99862-114">Hola Web de interacción móvil SDK se incluye como un único archivo de JavaScript, azure engagement.js, que tiene tooinclude en cada página de su sitio o aplicación web.</span><span class="sxs-lookup"><span data-stu-id="99862-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99862-115">Antes de ejecutar este script, debe ejecutar un script o que escriba tooconfigure Mobile Engagement para la aplicación de fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="99862-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="99862-116">Compatibilidad con el explorador</span><span class="sxs-lookup"><span data-stu-id="99862-116">Browser compatibility</span></span>
<span data-ttu-id="99862-117">Hola SDK de Mobile Engagement Web usa JSON nativo de codificación y descodificación, además de las solicitudes de AJAX de dominio toocross (depender de la especificación de W3C CORS Hola).</span><span class="sxs-lookup"><span data-stu-id="99862-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="99862-118">Es compatible con hello siguientes exploradores:</span><span class="sxs-lookup"><span data-stu-id="99862-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="99862-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="99862-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="99862-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="99862-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="99862-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="99862-121">Firefox 3.5+</span></span>
* <span data-ttu-id="99862-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="99862-122">Chrome 4+</span></span>
* <span data-ttu-id="99862-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="99862-123">Safari 6+</span></span>
* <span data-ttu-id="99862-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="99862-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="99862-125">Configuración de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="99862-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="99862-126">Escribir un script que crea global `azureEngagement` objeto de JavaScript, como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="99862-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="99862-127">Como el sitio puede tener varias páginas, en el ejemplo se da por hecho que el script se incluye en cada página.</span><span class="sxs-lookup"><span data-stu-id="99862-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="99862-128">En este ejemplo, se denomina objeto de JavaScript de hello `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="99862-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="99862-129">Hola `connectionString` valor de la aplicación se muestra en Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="99862-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="99862-130">`appVersionName` y `appVersionCode` son opcionales.</span><span class="sxs-lookup"><span data-stu-id="99862-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="99862-131">Sin embargo, se recomienda configurarlos para que el análisis pueda procesar la información acerca de la versión.</span><span class="sxs-lookup"><span data-stu-id="99862-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="99862-132">Incorporación de scripts de Mobile Engagement en las páginas</span><span class="sxs-lookup"><span data-stu-id="99862-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="99862-133">Agregar páginas de Mobile Engagement scripts tooyour de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="99862-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="99862-134">O bien:</span><span class="sxs-lookup"><span data-stu-id="99862-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="99862-135">Alias</span><span class="sxs-lookup"><span data-stu-id="99862-135">Alias</span></span>
<span data-ttu-id="99862-136">Después de carga hello secuencia de comandos de SDK de Mobile Engagement Web, crea hello **interacción** alias tooaccess Hola API del SDK.</span><span class="sxs-lookup"><span data-stu-id="99862-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="99862-137">No se puede usar esta configuración de SDK de alias toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="99862-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="99862-138">El alias se usa como referencia en esta documentación.</span><span class="sxs-lookup"><span data-stu-id="99862-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="99862-139">Tenga en cuenta que si alias predeterminado de hello entra en conflicto con otra variable global de la página, puede volver a definir, en configuración de hello como se indica a continuación antes de cargarlos Hola SDK de Mobile Engagement Web:</span><span class="sxs-lookup"><span data-stu-id="99862-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="99862-140">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="99862-140">Basic reporting</span></span>
<span data-ttu-id="99862-141">Los informes básicos de Mobile Engagement incluyen estadísticas de nivel de sesión, tales como estadísticas sobre usuarios, sesiones, actividades y bloqueos.</span><span class="sxs-lookup"><span data-stu-id="99862-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="99862-142">Seguimiento de sesión</span><span class="sxs-lookup"><span data-stu-id="99862-142">Session tracking</span></span>
<span data-ttu-id="99862-143">Las sesiones de Mobile Engagement se dividen en secuencias de actividades que se identifican por el nombre.</span><span class="sxs-lookup"><span data-stu-id="99862-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="99862-144">En un sitio web clásico, se recomienda declarar una actividad diferente en cada página del sitio.</span><span class="sxs-lookup"><span data-stu-id="99862-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="99862-145">Para un sitio Web o aplicación web en qué Hola página actual nunca cambia, conviene tootrack actividades de hello en una escala más pequeña, como en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="99862-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="99862-146">Ya sea cierto, toostart o cambiar Hola actividad del usuario actual, llamada hello `engagement.agent.startActivity` función.</span><span class="sxs-lookup"><span data-stu-id="99862-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="99862-147">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="99862-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="99862-148">servidor de Mobile Engagement Hola termina automáticamente una sesión abierta en tres minutos después de cerrar la página de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="99862-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="99862-149">También puede finalizar una sesión manualmente mediante una llamada a `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="99862-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="99862-150">Esto establece hello too'Idle de actividad de usuario actual.'</span><span class="sxs-lookup"><span data-stu-id="99862-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="99862-151">sesión de Hello finalizará 10 segundos más tarde, a menos que un nuevo llamar demasiado`engagement.agent.startActivity` se reanuda la sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="99862-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="99862-152">Puede configurar retraso de 10 segundos de hello en objetos de interacción global hello, como sigue:</span><span class="sxs-lookup"><span data-stu-id="99862-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="99862-153">No se puede utilizar `engagement.agent.endActivity` en hello `onunload` devolución de llamada porque no se puede realizar llamadas de AJAX en esta fase.</span><span class="sxs-lookup"><span data-stu-id="99862-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="99862-154">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="99862-154">Advanced reporting</span></span>
<span data-ttu-id="99862-155">Opcionalmente, si desea que los trabajos, los errores y eventos específicos de la aplicación de tooreport, deberá toouse Hola API de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="99862-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="99862-156">Tiene acceso a API de Mobile Engagement hello mediante hello `engagement.agent` objeto.</span><span class="sxs-lookup"><span data-stu-id="99862-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="99862-157">Puede tener acceso a toda Hola capacidades en Mobile Engagement en hello Mobile Engagement API avanzadas.</span><span class="sxs-lookup"><span data-stu-id="99862-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="99862-158">Hola API se detalla en el artículo hello [cómo toouse Hola avanzada etiquetado API en una aplicación web de Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="99862-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="99862-159">Personalizar direcciones URL de hello usadas para las llamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="99862-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="99862-160">Puede personalizar las direcciones URL que hello que usa el SDK de Mobile Engagement Web.</span><span class="sxs-lookup"><span data-stu-id="99862-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="99862-161">Por ejemplo, tooredefine Hola dirección URL de registro (Hola SDK punto de conexión para el registro), se puede invalidar la configuración de hello similar a éste:</span><span class="sxs-lookup"><span data-stu-id="99862-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="99862-162">Si las funciones de dirección URL devuelven una cadena que comienza con `/`, `//`, `http://`, o `https://`, no se utiliza el esquema predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="99862-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="99862-163">De forma predeterminada, Hola `https://` esquema se utiliza para las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="99862-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="99862-164">Si desea que el esquema predeterminado de toocustomize hello, invalidar la configuración de hello, similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="99862-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };

---
title: aaaGet a trabajar con Azure Mobile Engagement para las aplicaciones Web | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement a las notificaciones de inserción y de análisis para las aplicaciones Web."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="eba56-103">Introducción a Azure Mobile Engagement para Web Apps</span><span class="sxs-lookup"><span data-stu-id="eba56-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="eba56-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="eba56-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="eba56-105">servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible.</span><span class="sxs-lookup"><span data-stu-id="eba56-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="eba56-106">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="eba56-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="eba56-107">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="eba56-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="eba56-108">Visual Studio 2015, o cualquier otro editor que prefiera</span><span class="sxs-lookup"><span data-stu-id="eba56-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="eba56-109">SDK web</span><span class="sxs-lookup"><span data-stu-id="eba56-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="eba56-110">Este SDK Web está en vista previa y solo admite el análisis en el momento de Hola y todavía no admite notificaciones de inserción de explorador o de la aplicación de envío.</span><span class="sxs-lookup"><span data-stu-id="eba56-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="eba56-111">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="eba56-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="eba56-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="eba56-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="eba56-113">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="eba56-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="eba56-114">Configuración de Mobile Engagement para una aplicación web</span><span class="sxs-lookup"><span data-stu-id="eba56-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="eba56-115"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="eba56-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="eba56-116">Este tutorial presenta una "integración básica", que es Hola conjunto mínimo necesario toocollect datos.</span><span class="sxs-lookup"><span data-stu-id="eba56-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="eba56-117">Se creará una aplicación web básica con la integración de Visual Studio toodemonstrate Hola aunque puede seguir pasos de hello con cualquier aplicación web que se creó fuera de Visual Studio también.</span><span class="sxs-lookup"><span data-stu-id="eba56-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="eba56-118">Creación de una aplicación web nueva</span><span class="sxs-lookup"><span data-stu-id="eba56-118">Create a new Web App</span></span>
<span data-ttu-id="eba56-119">Hello siguientes pasos supone Hola uso de Visual Studio 2015 aunque Hola pasos son similares en versiones anteriores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eba56-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="eba56-120">Inicie Visual Studio y en hello **inicio** pantalla, seleccione **nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="eba56-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="eba56-121">En el menú emergente de hello, seleccione **Web** -> **aplicación Web ASP.Net**.</span><span class="sxs-lookup"><span data-stu-id="eba56-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="eba56-122">Rellene la aplicación hello **nombre**, **ubicación** y **nombre de la solución**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eba56-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="eba56-123">Hola **seleccione una plantilla de** ventana emergente, seleccione **vacía** en **ASP.Net 4.5 plantillas** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eba56-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="eba56-124">Ahora ha creado un nuevo proyecto de aplicación Web en blanco en el que se integrará hello Web de Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="eba56-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="eba56-125">Conectar el backend de interacción de tooMobile de aplicación</span><span class="sxs-lookup"><span data-stu-id="eba56-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="eba56-126">Cree una carpeta nueva denominada **javascript** en la solución y agregue el archivo de Web SDK JS hello **engagement.js azure** en él.</span><span class="sxs-lookup"><span data-stu-id="eba56-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="eba56-127">Agregar un nuevo archivo denominado **main.js** en esta carpeta de javascript con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="eba56-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="eba56-128">Asegúrese de cadena de conexión de hello tooupdate seguro.</span><span class="sxs-lookup"><span data-stu-id="eba56-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="eba56-129">Esto `azureEngagement` objeto será tooaccess usa métodos Web SDK.</span><span class="sxs-lookup"><span data-stu-id="eba56-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio con archivos js][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="eba56-131">Habilitación de la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="eba56-131">Enable real-time monitoring</span></span>
<span data-ttu-id="eba56-132">En orden toostart enviando los datos y asegurarse de que los usuarios de hello activos, debe enviar al menos una actividad toohello Mobile Engagement back-end.</span><span class="sxs-lookup"><span data-stu-id="eba56-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="eba56-133">Una actividad en el contexto de Hola de una aplicación web es una página web.</span><span class="sxs-lookup"><span data-stu-id="eba56-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="eba56-134">Cree una nueva página denominada **home.html** en la solución y se establece como Hola a partir de página de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="eba56-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="eba56-135">Incluir Hola dos archivos JavaScript que se agregó anteriormente en esta página agregando Hola siguientes dentro de la etiqueta body de Hola.</span><span class="sxs-lookup"><span data-stu-id="eba56-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="eba56-136">Actualizar Hola cuerpo etiqueta toocall EngagementAgent `startActivity` (método)</span><span class="sxs-lookup"><span data-stu-id="eba56-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="eba56-137">Así será **home.html** .</span><span class="sxs-lookup"><span data-stu-id="eba56-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="eba56-138">Conectar la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="eba56-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="eba56-139">Ampliación del análisis</span><span class="sxs-lookup"><span data-stu-id="eba56-139">Extend analytics</span></span>
<span data-ttu-id="eba56-140">Aquí están actualmente disponibles con el SDK de Web que puede usar para el análisis de todos los métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="eba56-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="eba56-141">Actividades y páginas web:</span><span class="sxs-lookup"><span data-stu-id="eba56-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="eba56-142">Eventos</span><span class="sxs-lookup"><span data-stu-id="eba56-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="eba56-143">Errors</span><span class="sxs-lookup"><span data-stu-id="eba56-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="eba56-144">Trabajos</span><span class="sxs-lookup"><span data-stu-id="eba56-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png


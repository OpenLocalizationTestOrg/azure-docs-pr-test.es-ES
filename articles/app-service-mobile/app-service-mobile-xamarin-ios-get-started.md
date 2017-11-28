---
title: "Introducción a Azure App Service Mobile Apps para aplicaciones Xamarin.iOS | Microsoft Docs"
description: "Siga este tutorial para empezar a usar Aplicaciones móviles para el desarrollo de Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 8dc965df2cd45366970effb29f246b0045a94717
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="18b9e-103">Creación de una aplicación Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="18b9e-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="18b9e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="18b9e-104">Overview</span></span>
<span data-ttu-id="18b9e-105">En este tutorial se muestra cómo agregar un servicio de back-end basado en la nube a una aplicación móvil Xamarin.iOS con un back-end de Aplicaciones móviles de Azure.</span><span class="sxs-lookup"><span data-stu-id="18b9e-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="18b9e-106">Creará tanto un back-end de aplicación móvil nuevo como una aplicación Xamarin.iOS simple de la *lista de tareas pendientes* que almacene los datos de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="18b9e-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="18b9e-107">Completar este tutorial es un requisito previo para todos los demás tutoriales de Xamarin.iOS sobre cómo usar la característica Aplicaciones móviles en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="18b9e-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18b9e-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18b9e-108">Prerequisites</span></span>
<span data-ttu-id="18b9e-109">Para completar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="18b9e-109">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="18b9e-110">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="18b9e-110">An active Azure account.</span></span> <span data-ttu-id="18b9e-111">Si no dispone de ninguna cuenta, regístrese para obtener una versión de evaluación de Azure y conseguir hasta 10 aplicaciones móviles gratuitas que podrá seguir usando incluso después de que finalice la evaluación.</span><span class="sxs-lookup"><span data-stu-id="18b9e-111">If you don't have an account, sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="18b9e-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18b9e-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="18b9e-113">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="18b9e-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="18b9e-114">Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="18b9e-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="18b9e-115">Un equipo Mac con Xcode v7.0 o versiones posteriores y Xamarin Studio Community instalados.</span><span class="sxs-lookup"><span data-stu-id="18b9e-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="18b9e-116">Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) y [Configuración, instalación y comprobaciones para usuarios de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="18b9e-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="18b9e-117">Creación de un nuevo back-end de Azure Mobile App</span><span class="sxs-lookup"><span data-stu-id="18b9e-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="18b9e-118">Siga estos pasos para crear un back-end de Mobile App.</span><span class="sxs-lookup"><span data-stu-id="18b9e-118">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="18b9e-119">Configuración del proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="18b9e-119">Configure the server project</span></span>
<span data-ttu-id="18b9e-120">Ahora ha aprovisionado un back-end de aplicación móvil de Azure que puede usarse por las aplicaciones del cliente móvil.</span><span class="sxs-lookup"><span data-stu-id="18b9e-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="18b9e-121">Después, descargue un proyecto de servidor para un back-end de "lista de tareas" sencillo y publíquelo en Azure.</span><span class="sxs-lookup"><span data-stu-id="18b9e-121">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

<span data-ttu-id="18b9e-122">Para configurar el proyecto de servidor para que use el back-end de Node.js o. NET, siga los pasos que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="18b9e-122">Follow the following steps to configure the server project to use either the Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinios-app"></a><span data-ttu-id="18b9e-123">Descarga y ejecución de la aplicación Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="18b9e-123">Download and run the Xamarin.iOS app</span></span>
1. <span data-ttu-id="18b9e-124">En el equipo Mac, abra el [Portal de Azure] en una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="18b9e-124">Open the [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="18b9e-125">En la hoja de configuración de la aplicación móvil, haga clic en **Introducción** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="18b9e-125">On the settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="18b9e-126">En el paso 3, haga clic en **Crear una nueva aplicación** , en caso de que no esté seleccionado.</span><span class="sxs-lookup"><span data-stu-id="18b9e-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="18b9e-127">A continuación, haga clic en el botón **Descargar** .</span><span class="sxs-lookup"><span data-stu-id="18b9e-127">Next click the **Download** button.</span></span>

      <span data-ttu-id="18b9e-128">Se descarga una aplicación cliente que se conecta a su back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="18b9e-128">A client application that connects to your mobile backend is downloaded.</span></span> <span data-ttu-id="18b9e-129">Guarde el archivo comprimido del proyecto en el equipo local y anote dónde lo guardó.</span><span class="sxs-lookup"><span data-stu-id="18b9e-129">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="18b9e-130">Extraiga el proyecto descargado y, después, ábralo en Xamarin Studio (o Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="18b9e-130">Extract the project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="18b9e-131">Presione la tecla F5 para compilar el proyecto e iniciar la aplicación en el emulador de iPhone.</span><span class="sxs-lookup"><span data-stu-id="18b9e-131">Press the F5 key to build the project and start the app in the iPhone emulator.</span></span>
5. <span data-ttu-id="18b9e-132">En la aplicación, escriba texto significativo, como *Aprender Xamarin*, y haga clic en el botón **+**.</span><span class="sxs-lookup"><span data-stu-id="18b9e-132">In the app, type meaningful text, such as *Learn Xamarin*, and then click the **+** button.</span></span>

    ![][10]

    <span data-ttu-id="18b9e-133">Los datos de la solicitud se insertan en la tabla TodoItem.</span><span class="sxs-lookup"><span data-stu-id="18b9e-133">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="18b9e-134">El back-end de aplicación móvil devuelve los elementos almacenados en la tabla y los datos se muestran en la lista.</span><span class="sxs-lookup"><span data-stu-id="18b9e-134">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="18b9e-135">Puede revisar el código que obtiene acceso al back-end de aplicación móvil para consultar e insertar datos en el archivo de C# QSTodoService.cs.</span><span class="sxs-lookup"><span data-stu-id="18b9e-135">You can review the code that accesses your mobile app backend to query and insert data in the QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="18b9e-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18b9e-136">Next steps</span></span>
* <span data-ttu-id="18b9e-137">[Add Offline Sync to your app](app-service-mobile-xamarin-ios-get-started-offline-data.md) (Incorporación de sincronización sin conexión a la aplicación)</span><span class="sxs-lookup"><span data-stu-id="18b9e-137">[Add Offline Sync to your app](app-service-mobile-xamarin-ios-get-started-offline-data.md)</span></span>
* [<span data-ttu-id="18b9e-138">Adición de la autenticación a la aplicación Xamarin.Android </span><span class="sxs-lookup"><span data-stu-id="18b9e-138">Add authentication to your app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="18b9e-139">Agregar notificaciones push a la aplicación de Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="18b9e-139">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="18b9e-140">Uso del cliente administrado para Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="18b9e-140">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
<span data-ttu-id="18b9e-141">[Portal de Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="18b9e-141">[Azure portal]: https://portal.azure.com/</span></span>

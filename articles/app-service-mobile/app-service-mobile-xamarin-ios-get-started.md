---
title: "aaaGet a trabajar con aplicaciones móviles de Azure aplicación de servicio para las aplicaciones de Xamarin.iOS | Documentos de Microsoft"
description: "Siga este tutorial tooget Introducción al uso de aplicaciones móviles para el desarrollo de Xamarin.iOS."
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
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="d719d-103">Creación de una aplicación Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="d719d-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="d719d-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d719d-104">Overview</span></span>
<span data-ttu-id="d719d-105">Este tutorial muestra cómo tooadd un back-end basado en la nube service aplicación móvil de tooa Xamarin.iOS mediante el uso de un aplicación móvil Azure de back-end.</span><span class="sxs-lookup"><span data-stu-id="d719d-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="d719d-106">Creará tanto un back-end de aplicación móvil nuevo como una aplicación Xamarin.iOS simple de la *lista de tareas pendientes* que almacene los datos de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="d719d-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="d719d-107">Completar este tutorial es un requisito previo para todos los otros tutoriales de Xamarin.iOS sobre cómo usar la característica de aplicaciones móviles de hello en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="d719d-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d719d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d719d-108">Prerequisites</span></span>
<span data-ttu-id="d719d-109">toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="d719d-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="d719d-110">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="d719d-110">An active Azure account.</span></span> <span data-ttu-id="d719d-111">Si no tiene una cuenta, registrarse para obtener una evaluación de Azure y desarrollar aplicaciones móviles gratuitas too10 que puede seguir usando incluso después de la prueba finaliza.</span><span class="sxs-lookup"><span data-stu-id="d719d-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="d719d-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d719d-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d719d-113">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="d719d-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="d719d-114">Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="d719d-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="d719d-115">Un equipo Mac con Xcode v7.0 o versiones posteriores y Xamarin Studio Community instalados.</span><span class="sxs-lookup"><span data-stu-id="d719d-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="d719d-116">Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) y [Configuración, instalación y comprobaciones para usuarios de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="d719d-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="d719d-117">Creación de un nuevo back-end de Azure Mobile App</span><span class="sxs-lookup"><span data-stu-id="d719d-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="d719d-118">Siga estos toocreate pasos un aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="d719d-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="d719d-119">Configurar el proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="d719d-119">Configure hello server project</span></span>
<span data-ttu-id="d719d-120">Ahora ha aprovisionado un back-end de aplicación móvil de Azure que puede usarse por las aplicaciones del cliente móvil.</span><span class="sxs-lookup"><span data-stu-id="d719d-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="d719d-121">A continuación, descargar un proyecto de servidor para un simple "lista de tareas" back-end y publicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d719d-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="d719d-122">Siga Hola siguiendo los pasos tooconfigure Hola servidor proyecto toouse cualquier hello Node.js o .NET back-end.</span><span class="sxs-lookup"><span data-stu-id="d719d-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="d719d-123">Descargue y ejecute la aplicación de hello Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="d719d-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="d719d-124">Abra hello [portal de Azure] en una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="d719d-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="d719d-125">En la hoja de configuración de Hola para su aplicación móvil, haga clic en **Introducción** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="d719d-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="d719d-126">En el paso 3, haga clic en **Crear una nueva aplicación** , en caso de que no esté seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d719d-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="d719d-127">A continuación haga clic en hello **descargar** botón.</span><span class="sxs-lookup"><span data-stu-id="d719d-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="d719d-128">Se descarga una aplicación cliente que se conecta back-end de tooyour móvil.</span><span class="sxs-lookup"><span data-stu-id="d719d-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="d719d-129">Guarde el archivo de proyecto comprimida de hello en el equipo local y tome nota donde se guarda.</span><span class="sxs-lookup"><span data-stu-id="d719d-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="d719d-130">Extraer el proyecto de Hola que ha descargado y, a continuación, ábralo en Xamarin Studio (o Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d719d-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="d719d-131">Presione proyecto Hola de hello F5 toobuild clave e iniciar aplicación hello en el emulador de iPhone Hola.</span><span class="sxs-lookup"><span data-stu-id="d719d-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="d719d-132">En la aplicación hello, escriba texto significativo, como *Obtenga información acerca de Xamarin*y, a continuación, haga clic en hello  **+**  botón.</span><span class="sxs-lookup"><span data-stu-id="d719d-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="d719d-133">Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola.</span><span class="sxs-lookup"><span data-stu-id="d719d-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="d719d-134">Se devuelven los elementos almacenados en la tabla de hello back-end de aplicación móvil de Hola y los datos se muestran en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="d719d-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="d719d-135">Puede revisar el código de hello que tiene acceso a su tooquery de back-end de la aplicación móvil e insertar datos en hello archivo QSTodoService.cs C#.</span><span class="sxs-lookup"><span data-stu-id="d719d-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d719d-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d719d-136">Next steps</span></span>
* [<span data-ttu-id="d719d-137">Agregar aplicación de sincronización sin conexión tooyour</span><span class="sxs-lookup"><span data-stu-id="d719d-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="d719d-138">Agregar aplicación de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="d719d-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="d719d-139">Agregar aplicación de Xamarin.Android de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="d719d-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="d719d-140">Cómo toouse Hola administra a cliente para aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="d719d-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

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
[portal de Azure]: https://portal.azure.com/

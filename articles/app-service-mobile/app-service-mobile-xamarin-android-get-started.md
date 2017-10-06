---
title: aaaGet iniciado con aplicaciones de Azure Mobile para aplicaciones de Xamarin.Android
description: "Siga este tutorial tooget iniciado con aplicaciones móviles de Azure para desarrollo de Xamarin para Android"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="1c3c3-103">Creación de una aplicación Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="1c3c3-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1c3c3-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1c3c3-104">Overview</span></span>
<span data-ttu-id="1c3c3-105">Este tutorial muestra cómo tooadd un back-end basado en la nube service tooa Xamarin.Android aplicación.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="1c3c3-106">Para obtener más información, consulte [¿Qué son las aplicaciones móviles?](app-service-mobile-value-prop.md)</span><span class="sxs-lookup"><span data-stu-id="1c3c3-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="1c3c3-107">Una captura de pantalla de la aplicación hello completado es menor que:</span><span class="sxs-lookup"><span data-stu-id="1c3c3-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="1c3c3-108">Completar este tutorial es un requisito previo para todos los tutoriales de aplicaciones móviles para aplicaciones Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c3c3-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1c3c3-109">Prerequisites</span></span>
<span data-ttu-id="1c3c3-110">toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="1c3c3-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="1c3c3-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-111">An active Azure account.</span></span> <span data-ttu-id="1c3c3-112">Si no tiene una cuenta, suscríbase a una versión de evaluación de Azure y desarrollar aplicaciones móviles gratuitas de too10.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="1c3c3-113">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c3c3-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1c3c3-114">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="1c3c3-115">Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="1c3c3-116">Creación de un nuevo back-end de Azure Mobile App</span><span class="sxs-lookup"><span data-stu-id="1c3c3-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="1c3c3-117">Siga estos toocreate pasos un aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="1c3c3-118">Ahora ha aprovisionado un back-end de aplicación móvil de Azure que puede usarse por las aplicaciones del cliente móvil.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="1c3c3-119">A continuación, descargar un proyecto de servidor para un simple "lista de tareas" back-end y publicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="1c3c3-120">Configurar el proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="1c3c3-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="1c3c3-121">Descargue y ejecute la aplicación de hello Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="1c3c3-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="1c3c3-122">En **descargar y ejecutar el proyecto Xamarin.Android**, haga clic en hello **descargar** botón.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="1c3c3-123">Guardar el equipo local del tooyour de archivo comprimido proyectos hello y tome nota donde se guarda.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="1c3c3-124">Hola presione **F5** clave proyecto de hello toobuild e iniciar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="1c3c3-125">En la aplicación hello, escriba texto significativo, como *tutorial Hola completa* y, a continuación, haga clic en hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="1c3c3-126">Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="1c3c3-127">Se devuelven los elementos almacenados en la tabla de hello back-end de aplicación móvil de Hola y los datos aparecen en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1c3c3-128">Puede revisar el código de hello que tiene acceso a su tooquery de back-end de la aplicación móvil e insertar datos, que se encuentra en hello archivo ToDoActivity.cs C#.</span><span class="sxs-lookup"><span data-stu-id="1c3c3-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="1c3c3-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1c3c3-129">Next steps</span></span>
* [<span data-ttu-id="1c3c3-130">Agregar aplicación de sincronización sin conexión tooyour</span><span class="sxs-lookup"><span data-stu-id="1c3c3-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="1c3c3-131">Agregar aplicación de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="1c3c3-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="1c3c3-132">Agregar aplicación de Xamarin.Android de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="1c3c3-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="1c3c3-133">Cómo toouse Hola administra a cliente para aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="1c3c3-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203

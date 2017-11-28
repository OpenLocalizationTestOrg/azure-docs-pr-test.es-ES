---
title: "aaaCreate una plataforma Universal de Windows (UWP) que se usa en aplicaciones móviles | Documentos de Microsoft"
description: "Siga este tutorial tooget Introducción al uso de back-ends de aplicaciones móviles Azure para desarrollo de aplicaciones de plataforma Universal de Windows (UWP) en C#, Visual Basic o JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="a57fc-103">Creación de una aplicación para Windows</span><span class="sxs-lookup"><span data-stu-id="a57fc-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a57fc-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a57fc-104">Overview</span></span>
<span data-ttu-id="a57fc-105">Este tutorial muestra cómo tooadd un back-end basado en la nube service tooa aplicación de plataforma Universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="a57fc-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="a57fc-106">Para obtener más información, consulte [¿Qué son las aplicaciones móviles?](app-service-mobile-value-prop.md)</span><span class="sxs-lookup"><span data-stu-id="a57fc-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="a57fc-107">son las siguientes Hola capturas de pantalla de la aplicación hello completado:</span><span class="sxs-lookup"><span data-stu-id="a57fc-107">hello following are screen captures from hello completed app:</span></span>

![Aplicación de escritorio completada](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="a57fc-109">Ejecutándose en un equipo de escritorio</span><span class="sxs-lookup"><span data-stu-id="a57fc-109">Running on a desktop.</span></span>

![Aplicación de teléfono completada](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="a57fc-111">Ejecutándose en un teléfono</span><span class="sxs-lookup"><span data-stu-id="a57fc-111">Running on a phone</span></span>

<span data-ttu-id="a57fc-112">Completar este tutorial es un requisito previo para todos los tutoriales de aplicaciones móviles para aplicaciones para UWP.</span><span class="sxs-lookup"><span data-stu-id="a57fc-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a57fc-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a57fc-113">Prerequisites</span></span>
<span data-ttu-id="a57fc-114">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a57fc-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a57fc-115">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="a57fc-115">An active Azure account.</span></span> <span data-ttu-id="a57fc-116">Si no tiene una cuenta, puede registrarse para obtener una evaluación de Azure y desarrollar aplicaciones móviles gratuitas too10 que puede seguir usando incluso después de la prueba finaliza.</span><span class="sxs-lookup"><span data-stu-id="a57fc-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="a57fc-117">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a57fc-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a57fc-118">[Visual Studio Community 2015] o versión posterior.</span><span class="sxs-lookup"><span data-stu-id="a57fc-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="a57fc-119">Creación de un nuevo back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="a57fc-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="a57fc-120">Siga estos toocreate pasos aplicación móvil back-end.</span><span class="sxs-lookup"><span data-stu-id="a57fc-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="a57fc-121">Ahora ha aprovisionado un back-end de aplicación móvil de Azure que puede usarse por las aplicaciones del cliente móvil.</span><span class="sxs-lookup"><span data-stu-id="a57fc-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="a57fc-122">A continuación, se descargará un proyecto de servidor para un simple "lista de tareas" back-end y publicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a57fc-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="a57fc-123">Configurar el proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="a57fc-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="a57fc-124">Descargue y ejecute el proyecto de cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="a57fc-124">Download and run hello client project</span></span>
<span data-ttu-id="a57fc-125">Una vez haya configurado el aplicación móvil de back-end, puede crear una nueva aplicación de cliente o modificar una existente tooAzure tooconnect de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a57fc-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="a57fc-126">En esta sección, descargar un proyecto de plantilla de aplicación UWP que está personalizado tooconnect tooyour aplicación móvil back-end.</span><span class="sxs-lookup"><span data-stu-id="a57fc-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="a57fc-127">En hello **inicio rápido** hoja para su aplicación móvil de back-end, haga clic en **crear una nueva aplicación** > **descargar**, a continuación, extraer los archivos de proyecto de hello comprimido tooyour equipo local.</span><span class="sxs-lookup"><span data-stu-id="a57fc-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Descargar el proyecto de inicio rápido de Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="a57fc-129">(Opcional) Agregar toohello de proyecto de aplicación UWP Hola misma solución como proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a57fc-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="a57fc-130">Esto facilita toodebug y prueba ambos Hola back-end de aplicación y hello en Hola la misma solución de Visual Studio, si elige toodo lo.</span><span class="sxs-lookup"><span data-stu-id="a57fc-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="a57fc-131">tooadd una solución de toohello del proyecto de aplicación UWP, debe utilizar Visual Studio 2015 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="a57fc-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="a57fc-132">Con la aplicación UWP hello como proyecto de inicio de hello, presione Hola F5 clave toodeploy y aplicación hello de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a57fc-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="a57fc-133">En la aplicación hello, escriba texto significativo, como *tutorial Hola completa*, Hola **insertar un TodoItem** cuadro de texto y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="a57fc-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Inicio rápido de Windows completo - Escritorio](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="a57fc-135">Esto envía un POST solicitud toohello nueva aplicación móvil back-end que se hospeda en Azure.</span><span class="sxs-lookup"><span data-stu-id="a57fc-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="a57fc-136">(Opcional) Detener aplicación hello y reiniciarlo en un dispositivo diferente o un emulador de dispositivos móvil.</span><span class="sxs-lookup"><span data-stu-id="a57fc-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Inicio rápido de Windows completo - Teléfono](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="a57fc-138">Tenga en cuenta que guardó en el paso anterior de hello carga los datos de Azure después de hello aplicación UWP se inicia.</span><span class="sxs-lookup"><span data-stu-id="a57fc-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a57fc-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a57fc-139">Next steps</span></span>
* [<span data-ttu-id="a57fc-140">Agregar aplicación de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="a57fc-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="a57fc-141">Obtenga información acerca de cómo tooauthenticate a los usuarios de la aplicación con un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="a57fc-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="a57fc-142">Agregar aplicación de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="a57fc-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="a57fc-143">Obtenga información acerca de cómo las notificaciones de inserción de tooadd son compatibles con la aplicación tooyour y configurar las notificaciones de inserción de toosend de aplicación móvil back-end toouse centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="a57fc-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="a57fc-144">Habilitación de la sincronización sin conexión para su aplicación</span><span class="sxs-lookup"><span data-stu-id="a57fc-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="a57fc-145">Obtenga información acerca de cómo tooadd sin conexión son compatibles con la aplicación con un aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="a57fc-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="a57fc-146">Sincronización sin conexión permite a los usuarios finales toointeract con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="a57fc-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203

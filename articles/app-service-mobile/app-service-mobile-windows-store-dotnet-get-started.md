---
title: "Creación de una Plataforma universal de Windows (UWP) que se use en Mobile Apps | Microsoft Docs"
description: "Siga este tutorial para aprender a usar back-ends de aplicación móvil de Azure para el desarrollo de aplicaciones para Plataforma universal de Windows (UWP) en C#, Visual Basic o JavaScript."
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
ms.openlocfilehash: 5408e032670dda7f149c442e08f52b02abe23f05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="b65eb-103">Creación de una aplicación para Windows</span><span class="sxs-lookup"><span data-stu-id="b65eb-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="b65eb-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b65eb-104">Overview</span></span>
<span data-ttu-id="b65eb-105">En este tutorial se muestra cómo agregar un servicio back-end basado en la nube a una aplicación para Plataforma universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="b65eb-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="b65eb-106">Para obtener más información, consulte [¿Qué son las aplicaciones móviles?](app-service-mobile-value-prop.md)</span><span class="sxs-lookup"><span data-stu-id="b65eb-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="b65eb-107">A continuación se muestran las capturas de pantalla de la aplicación completada:</span><span class="sxs-lookup"><span data-stu-id="b65eb-107">The following are screen captures from the completed app:</span></span>

![Aplicación de escritorio completada](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="b65eb-109">Ejecutándose en un equipo de escritorio</span><span class="sxs-lookup"><span data-stu-id="b65eb-109">Running on a desktop.</span></span>

![Aplicación de teléfono completada](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="b65eb-111">Ejecutándose en un teléfono</span><span class="sxs-lookup"><span data-stu-id="b65eb-111">Running on a phone</span></span>

<span data-ttu-id="b65eb-112">Completar este tutorial es un requisito previo para todos los tutoriales de aplicaciones móviles para aplicaciones para UWP.</span><span class="sxs-lookup"><span data-stu-id="b65eb-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b65eb-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b65eb-113">Prerequisites</span></span>
<span data-ttu-id="b65eb-114">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b65eb-114">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b65eb-115">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b65eb-115">An active Azure account.</span></span> <span data-ttu-id="b65eb-116">Si no dispone de ninguna cuenta, puede registrarse para obtener una versión de evaluación de Azure y conseguir hasta 10 aplicaciones móviles gratuitas que podrá seguir usando incluso después de que finalice la evaluación.</span><span class="sxs-lookup"><span data-stu-id="b65eb-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="b65eb-117">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b65eb-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b65eb-118">[Visual Studio Community 2015] o versión posterior.</span><span class="sxs-lookup"><span data-stu-id="b65eb-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="b65eb-119">Creación de un nuevo back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="b65eb-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="b65eb-120">Siga estos pasos para crear un nuevo back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="b65eb-120">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="b65eb-121">Ahora ha aprovisionado un back-end de aplicación móvil de Azure que puede usarse por las aplicaciones del cliente móvil.</span><span class="sxs-lookup"><span data-stu-id="b65eb-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="b65eb-122">Después, descargará un proyecto de servidor para un back-end de "lista de tareas" sencillo y lo publicará en Azure.</span><span class="sxs-lookup"><span data-stu-id="b65eb-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="b65eb-123">Configuración del proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="b65eb-123">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a><span data-ttu-id="b65eb-124">Descarga y ejecución del proyecto de cliente</span><span class="sxs-lookup"><span data-stu-id="b65eb-124">Download and run the client project</span></span>
<span data-ttu-id="b65eb-125">Una vez configurado el back-end de aplicación móvil, puede crear una nueva aplicación cliente o modificar una aplicación existente para conectarse a Azure.</span><span class="sxs-lookup"><span data-stu-id="b65eb-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span></span> <span data-ttu-id="b65eb-126">En esta sección, descargará un proyecto de plantilla de aplicación para UWP que se personaliza para conectarse al back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="b65eb-126">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span></span>

1. <span data-ttu-id="b65eb-127">De nuevo en la hoja **Inicio rápido** para el back-end de aplicación móvil, haga clic en **Crear una nueva aplicación** > **Descargar** y extraiga los archivos de proyecto comprimidos en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="b65eb-127">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span></span>

    ![Descargar el proyecto de inicio rápido de Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="b65eb-129">(Opcional) Agregue el proyecto de aplicación para UWP a la misma solución que el proyecto de servidor.</span><span class="sxs-lookup"><span data-stu-id="b65eb-129">(Optional) Add the UWP app project to the same solution as the server project.</span></span> <span data-ttu-id="b65eb-130">Esto hace que sea más fácil depurar y probar la aplicación y el back-end en la misma solución de Visual Studio, si decide hacer esto.</span><span class="sxs-lookup"><span data-stu-id="b65eb-130">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span></span> <span data-ttu-id="b65eb-131">Para agregar un proyecto de aplicación para UWP a la solución, debe usar Visual Studio 2015 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="b65eb-131">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="b65eb-132">Con la aplicación para UWP como proyecto de inicio, presione la tecla F5 para implementar y ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b65eb-132">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span></span>
4. <span data-ttu-id="b65eb-133">En la aplicación, escriba texto significativo, como *Realice el tutorial*, en el cuadro de texto **Insertar un TodoItem** y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b65eb-133">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Inicio rápido de Windows completo - Escritorio](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="b65eb-135">Esta acción envía una solicitud POST al nuevo back-end de aplicación móvil hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="b65eb-135">This sends a POST request to the new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="b65eb-136">(Opcional) Detenga la aplicación y reiníciela en un dispositivo diferente o un emulador de dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="b65eb-136">(Optional) Stop the app and restart it on a different device or mobile emulator.</span></span>

    ![Inicio rápido de Windows completo - Teléfono](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="b65eb-138">Tenga en cuenta que los datos guardados en el paso anterior se cargan desde Azure después de que se inicie la aplicación para UWP.</span><span class="sxs-lookup"><span data-stu-id="b65eb-138">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b65eb-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b65eb-139">Next steps</span></span>
* [<span data-ttu-id="b65eb-140">Incorporación de autenticación a la aplicación</span><span class="sxs-lookup"><span data-stu-id="b65eb-140">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="b65eb-141">Aprenda a autenticar a los usuarios de su aplicación con un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="b65eb-141">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="b65eb-142">Incorporación de notificaciones push a su aplicación</span><span class="sxs-lookup"><span data-stu-id="b65eb-142">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="b65eb-143">: aprenda a agregar a la aplicación compatibilidad con notificaciones push y a configurar su back-end de aplicación móvil para usar Azure Notification Hubs para enviar notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="b65eb-143">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="b65eb-144">Habilitación de la sincronización sin conexión para su aplicación</span><span class="sxs-lookup"><span data-stu-id="b65eb-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="b65eb-145">: aprenda a agregar compatibilidad sin conexión a su aplicación con un back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="b65eb-145">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="b65eb-146">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil (ver, agregar o modificar datos) aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="b65eb-146">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="b65eb-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span><span class="sxs-lookup"><span data-stu-id="b65eb-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span></span>

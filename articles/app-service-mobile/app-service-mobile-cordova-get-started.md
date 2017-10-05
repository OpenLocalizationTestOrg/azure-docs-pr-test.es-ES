---
title: "Creación de una aplicación de Cordova en Azure App Service Mobile Apps | Microsoft Docs"
description: "Siga este tutorial para aprender a usar back-ends de aplicación móvil de Azure para el desarrollo de Apache Cordova."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: "cordova, javascript, móvil, cliente"
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: b620465cdc3cfa04933dc6e70163fc32aa9a839b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="ade9e-104">Creación de una aplicación de Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="ade9e-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ade9e-105">Información general</span><span class="sxs-lookup"><span data-stu-id="ade9e-105">Overview</span></span>
<span data-ttu-id="ade9e-106">En este tutorial se muestra cómo agregar un servicio back-end basado en la nube a una aplicación móvil de Apache Cordova usando un back-end de la aplicación móvil de Azure.</span><span class="sxs-lookup"><span data-stu-id="ade9e-106">This tutorial shows you how to add a cloud-based backend service to an Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="ade9e-107">Creará un back-end de aplicación móvil nuevo y una aplicación simple de *lista de tareas pendientes* de Apache Cordova que almacena los datos de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="ade9e-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="ade9e-108">Completar este tutorial es un requisito previo para todos los demás tutoriales de Apache Cordova acerca de cómo usar la característica Aplicaciones móviles en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="ade9e-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ade9e-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ade9e-109">Prerequisites</span></span>
<span data-ttu-id="ade9e-110">Para completar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="ade9e-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="ade9e-111">Un equipo con [Visual Studio Community 2017], o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="ade9e-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="ade9e-112">[Visual Studio Tools para Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="ade9e-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="ade9e-113">Una [cuenta de Azure activa](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ade9e-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="ade9e-114">También puede omitir Visual Studio y utilizar la línea de comandos de Apache Cordova directamente.</span><span class="sxs-lookup"><span data-stu-id="ade9e-114">You may also bypass Visual Studio and use the Apache Cordova command line directly.</span></span>  <span data-ttu-id="ade9e-115">El uso de la línea de comandos es útil si realiza el tutorial en un equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="ade9e-115">Using the command line is useful when completing the tutorial on a Mac computer.</span></span>  <span data-ttu-id="ade9e-116">Este tutorial no aborda la compilación de aplicaciones de cliente de Apache Cordova con la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="ade9e-116">Compiling Apache Cordova client applications using the command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="ade9e-117">Creación de un nuevo back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="ade9e-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="ade9e-118">Visualización de un vídeo donde se muestren pasos similares</span><span class="sxs-lookup"><span data-stu-id="ade9e-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-the-server-project"></a><span data-ttu-id="ade9e-119">Configuración del proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="ade9e-119">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-apache-cordova-app"></a><span data-ttu-id="ade9e-120">Descarga y ejecución de la aplicación Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="ade9e-120">Download and run the Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="ade9e-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ade9e-121">Next Steps</span></span>
<span data-ttu-id="ade9e-122">Ahora que ha completado este tutorial de inicio rápido, continúe con uno de los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="ade9e-122">Now that you completed this quick start tutorial, move on to one of the following tutorials:</span></span>

* <span data-ttu-id="ade9e-123">[Agregar datos sin conexión](app-service-mobile-cordova-get-started-offline-data.md) a su aplicación de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ade9e-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="ade9e-124">[Agregar autenticación](app-service-mobile-cordova-get-started-users.md) a su aplicación de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ade9e-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="ade9e-125">[Agregar notificaciones push](app-service-mobile-cordova-get-started-push.md) a su aplicación de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ade9e-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) to your Apache Cordova app.</span></span>

<span data-ttu-id="ade9e-126">Obtenga más información acerca de los conceptos principales con el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="ade9e-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="ade9e-127">[Datos sin conexión]</span><span class="sxs-lookup"><span data-stu-id="ade9e-127">[Offline Data]</span></span>
* <span data-ttu-id="ade9e-128">[Autenticación]</span><span class="sxs-lookup"><span data-stu-id="ade9e-128">[Authentication]</span></span>
* <span data-ttu-id="ade9e-129">[Notificaciones de inserción]</span><span class="sxs-lookup"><span data-stu-id="ade9e-129">[Push Notifications]</span></span>

<span data-ttu-id="ade9e-130">Obtenga información sobre cómo usar los SDK.</span><span class="sxs-lookup"><span data-stu-id="ade9e-130">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="ade9e-131">[SDK de Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="ade9e-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="ade9e-132">[SDK de servidor ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="ade9e-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="ade9e-133">[SDK de servidor Node.js]</span><span class="sxs-lookup"><span data-stu-id="ade9e-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="ade9e-134">[Visual Studio Community 2017]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="ade9e-134">[Visual Studio Community 2017]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="ade9e-135">[Visual Studio Tools para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="ade9e-135">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
<span data-ttu-id="ade9e-136">[Datos sin conexión]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="ade9e-136">[Offline Data]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="ade9e-137">[Autenticación]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="ade9e-137">[Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="ade9e-138">[Notificaciones de inserción]: ../notification-hubs/notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="ade9e-138">[Push Notifications]: ../notification-hubs/notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="ade9e-139">[SDK de Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="ade9e-139">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="ade9e-140">[SDK de servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="ade9e-140">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="ade9e-141">[SDK de servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="ade9e-141">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>

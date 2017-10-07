---
title: "aaaCreate una aplicación de Cordova en aplicaciones de Mobile de servicio de aplicación de Azure | Documentos de Microsoft"
description: "Siga este tutorial tooget Introducción al uso de back-ends de aplicaciones móviles Azure para el desarrollo de Apache Cordova"
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
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="c0e77-104">Creación de una aplicación de Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="c0e77-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c0e77-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c0e77-105">Overview</span></span>
<span data-ttu-id="c0e77-106">Este tutorial muestra cómo tooadd un back-end basado en la nube service aplicación móvil de tooan Apache Cordova mediante el uso de un aplicación móvil Azure de back-end.</span><span class="sxs-lookup"><span data-stu-id="c0e77-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="c0e77-107">Creará un back-end de aplicación móvil nuevo y una aplicación simple de *lista de tareas pendientes* de Apache Cordova que almacena los datos de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e77-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="c0e77-108">Completar este tutorial es un requisito previo para todos los otros tutoriales de Apache Cordova sobre cómo usar la característica de aplicaciones móviles de hello en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e77-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0e77-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c0e77-109">Prerequisites</span></span>
<span data-ttu-id="c0e77-110">toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="c0e77-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="c0e77-111">Un equipo con [Visual Studio Community 2017], o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="c0e77-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="c0e77-112">[Visual Studio Tools para Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="c0e77-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="c0e77-113">Una [cuenta de Azure activa](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0e77-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="c0e77-114">También puede omitir Visual Studio y usar línea de comandos de Apache Cordova Hola directamente.</span><span class="sxs-lookup"><span data-stu-id="c0e77-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="c0e77-115">Utilizando la línea de comandos de hello es útil al completar el tutorial de hello en un equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="c0e77-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="c0e77-116">Compilar aplicaciones de cliente de Apache Cordova mediante la línea de comandos de hello no está cubierto por este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c0e77-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="c0e77-117">Creación de un nuevo back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="c0e77-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="c0e77-118">Visualización de un vídeo donde se muestren pasos similares</span><span class="sxs-lookup"><span data-stu-id="c0e77-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="c0e77-119">Configurar el proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="c0e77-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="c0e77-120">Descargue y ejecute la aplicación de Apache Cordova de hello</span><span class="sxs-lookup"><span data-stu-id="c0e77-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="c0e77-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0e77-121">Next Steps</span></span>
<span data-ttu-id="c0e77-122">Completado este tutorial de inicio rápido, mueva en tooone de hello tutoriales:</span><span class="sxs-lookup"><span data-stu-id="c0e77-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="c0e77-123">[Agregar datos sin conexión](app-service-mobile-cordova-get-started-offline-data.md) tooyour aplicaciones de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="c0e77-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="c0e77-124">[Agregar autenticación](app-service-mobile-cordova-get-started-users.md) tooyour aplicaciones de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="c0e77-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="c0e77-125">[Agregar las notificaciones de inserción](app-service-mobile-cordova-get-started-push.md) tooyour aplicaciones de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="c0e77-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="c0e77-126">Obtenga más información acerca de los conceptos principales con el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e77-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="c0e77-127">[Datos sin conexión]</span><span class="sxs-lookup"><span data-stu-id="c0e77-127">[Offline Data]</span></span>
* <span data-ttu-id="c0e77-128">[Autenticación]</span><span class="sxs-lookup"><span data-stu-id="c0e77-128">[Authentication]</span></span>
* <span data-ttu-id="c0e77-129">[Notificaciones de inserción]</span><span class="sxs-lookup"><span data-stu-id="c0e77-129">[Push Notifications]</span></span>

<span data-ttu-id="c0e77-130">Obtenga información acerca de cómo toouse Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="c0e77-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="c0e77-131">[SDK de Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="c0e77-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="c0e77-132">[SDK de servidor ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="c0e77-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="c0e77-133">[SDK de servidor Node.js]</span><span class="sxs-lookup"><span data-stu-id="c0e77-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Datos sin conexión]: app-service-mobile-offline-data-sync.md
[Autenticación]: app-service-mobile-auth.md
[Notificaciones de inserción]: ../notification-hubs/notification-hubs-push-notification-overview.md
[SDK de Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[SDK de servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[SDK de servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md

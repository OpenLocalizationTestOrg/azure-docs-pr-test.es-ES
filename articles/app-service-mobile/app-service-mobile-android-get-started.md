---
title: "aaaCreate una aplicación Android en aplicaciones de Mobile de servicio de aplicación de Azure | Documentos de Microsoft"
description: "Siga este tutorial tooget Introducción al uso de back-ends de aplicaciones móviles Azure para desarrollo de Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="9d663-103">Creación de una aplicación de Android</span><span class="sxs-lookup"><span data-stu-id="9d663-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="9d663-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9d663-104">Overview</span></span>
<span data-ttu-id="9d663-105">Este tutorial muestra cómo tooadd un back-end basado en la nube service tooan de aplicación móvil Android mediante el uso de un aplicación móvil Azure de back-end.</span><span class="sxs-lookup"><span data-stu-id="9d663-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="9d663-106">Creará tanto un back-end de aplicación móvil nuevo como una aplicación de Android simple de la *lista de tareas pendientes* que almacene los datos de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="9d663-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="9d663-107">Completar este tutorial es un requisito previo para todos los otros tutoriales de Android acerca del uso de características de aplicaciones móviles de hello en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d663-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d663-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d663-108">Prerequisites</span></span>
<span data-ttu-id="9d663-109">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9d663-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="9d663-110">[Las herramientas de desarrollador Android](https://developer.android.com/sdk/index.html), que incluye el entorno de desarrollo integrado de Android Studio hello y plataforma de Android más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d663-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="9d663-111">Azure Mobile Android SDK, que se hace referencia como parte del proyecto de inicio rápido de Hola que descargue automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9d663-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="9d663-112">Una [cuenta de Azure activa](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d663-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="9d663-113">Creación de un nuevo back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="9d663-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="9d663-114">Configurar el proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="9d663-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="9d663-115">Descargue y ejecute la aplicación de Android hello</span><span class="sxs-lookup"><span data-stu-id="9d663-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203

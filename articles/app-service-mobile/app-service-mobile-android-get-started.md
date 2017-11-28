---
title: "Creación de una aplicación de Android en Azure App Service Mobile Apps | Microsoft Docs"
description: "Siga este tutorial para aprender a usar back-ends de aplicación móvil de Azure para el desarrollo de Android"
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
ms.openlocfilehash: 418a5229a084d570bc6cab5925dbd8d30945a3c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="55857-103">Creación de una aplicación de Android</span><span class="sxs-lookup"><span data-stu-id="55857-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="55857-104">Información general</span><span class="sxs-lookup"><span data-stu-id="55857-104">Overview</span></span>
<span data-ttu-id="55857-105">En este tutorial se muestra cómo agregar un servicio back-end basado en la nube a una aplicación móvil de Android con un back-end de la aplicación móvil de Azure.</span><span class="sxs-lookup"><span data-stu-id="55857-105">This tutorial shows you how to add a cloud-based backend service to an Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="55857-106">Creará tanto un back-end de aplicación móvil nuevo como una aplicación de Android simple de la *lista de tareas pendientes* que almacene los datos de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="55857-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="55857-107">Completar este tutorial es un requisito previo para todos los demás tutoriales de Android sobre cómo usar la característica Aplicaciones móviles en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="55857-107">Completing this tutorial is a prerequisite for all other Android tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55857-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="55857-108">Prerequisites</span></span>
<span data-ttu-id="55857-109">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="55857-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="55857-110">[Herramientas para desarrolladores de Android](https://developer.android.com/sdk/index.html), que incluyen el entorno de desarrollo integrado de Android Studio y la plataforma de Android más reciente.</span><span class="sxs-lookup"><span data-stu-id="55857-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>
* <span data-ttu-id="55857-111">El SDK de Android móvil de Azure, al que se hace automáticamente referencia como parte del proyecto de inicio rápido que puede descargar.</span><span class="sxs-lookup"><span data-stu-id="55857-111">Azure Mobile Android SDK, which is automatically referenced as part of the quickstart project you download.</span></span>
* <span data-ttu-id="55857-112">Una [cuenta de Azure activa](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55857-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="55857-113">Creación de un nuevo back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="55857-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="55857-114">Configuración del proyecto de servidor</span><span class="sxs-lookup"><span data-stu-id="55857-114">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-android-app"></a><span data-ttu-id="55857-115">Descarga y ejecución de la aplicación de Android</span><span class="sxs-lookup"><span data-stu-id="55857-115">Download and run the Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203

---
title: "Creación de una aplicación de iOS en Azure App Service Mobile Apps | Microsoft Docs"
description: "Siga este tutorial para aprender a usar back-ends de la aplicación móvil de Azure para el desarrollo de iOS en Objective-C o Swift."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 6461a899-9340-42dd-b118-ffc5ba00e846
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 36936ae66c458fcbedeec95cfa2f573a40c8af53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ios-app"></a><span data-ttu-id="69705-103">Creación de una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="69705-103">Create an iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="69705-104">Información general</span><span class="sxs-lookup"><span data-stu-id="69705-104">Overview</span></span>
<span data-ttu-id="69705-105">En este tutorial se muestra cómo agregar [Aplicaciones móviles de Azure](app-service-mobile-value-prop.md), un servicio back-end basado en la nube, a una aplicación de iOS.</span><span class="sxs-lookup"><span data-stu-id="69705-105">This tutorial shows how to add [Azure Mobile Apps](app-service-mobile-value-prop.md), a cloud backend service, to an iOS app.</span></span> <span data-ttu-id="69705-106">En primer lugar, vamos a crear un nuevo back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="69705-106">We'll first create a new mobile backend.</span></span> <span data-ttu-id="69705-107">Después, usaremos una sencilla aplicación de iOS de *lista de tareas* para almacenar datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="69705-107">Then, we'll use a simple *Todo list* iOS app to store data in Azure.</span></span>

<span data-ttu-id="69705-108">Para completar este tutorial, es preciso tener un Mac y una [cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="69705-108">To complete this tutorial, you need a Mac and [an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

## <a name="step-i-create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="69705-109">Paso 1: Creación de un nuevo back-end de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="69705-109">Step I: Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="step-ii-configure-the-backend-project"></a><span data-ttu-id="69705-110">Paso 2: Configuración del proyecto de back-end</span><span class="sxs-lookup"><span data-stu-id="69705-110">Step II: Configure the backend project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="step-iii-download-and-run-the-ios-app"></a><span data-ttu-id="69705-111">Paso 3: Descarga y ejecución de la aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="69705-111">Step III: Download and run the iOS app</span></span>
[!INCLUDE [app-service-mobile-ios-run-app](../../includes/app-service-mobile-ios-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203

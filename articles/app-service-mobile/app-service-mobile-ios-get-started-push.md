---
title: "Incorporación de notificaciones push a la aplicación iOS con las Aplicaciones móviles de Azure"
description: "Obtenga información acerca de cómo usar las Aplicaciones móviles de Azure para enviar notificaciones push a su aplicación iOS."
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="667b4-103">Incorporación de notificaciones push a la aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="667b4-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="667b4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="667b4-104">Overview</span></span>
<span data-ttu-id="667b4-105">En este tutorial, agregará notificaciones de inserción al proyecto de [inicio rápido de iOS] para que cada vez que se envíe una notificación de inserción al dispositivo, se inserte un registro.</span><span class="sxs-lookup"><span data-stu-id="667b4-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="667b4-106">Si no usa el proyecto de servidor de inicio rápido descargado, necesitará el paquete de extensión de la notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="667b4-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="667b4-107">Vea [Trabajar con el SDK de servidor de back-end de .NET para Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="667b4-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="667b4-108">El [simulador de iOS no admite notificaciones de inserción](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="667b4-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="667b4-109">Necesita un dispositivo de iOS físico y una [suscripción de Apple Developer Program](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="667b4-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="667b4-110"><a name="configure-hub"></a>Configurar el Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="667b4-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="667b4-111"><a id="register"></a>Registro de aplicaciones para notificaciones push</span><span class="sxs-lookup"><span data-stu-id="667b4-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="667b4-112">Configuración de Azure para enviar notificaciones push</span><span class="sxs-lookup"><span data-stu-id="667b4-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="667b4-113"><a id="update-server"></a>Actualizar el back-end para enviar notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="667b4-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="667b4-114"><a id="add-push"></a>Agregar notificaciones push a la aplicación</span><span class="sxs-lookup"><span data-stu-id="667b4-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="667b4-115"><a id="test"></a>Probar notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="667b4-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="667b4-116"><a id="more"></a>Más</span><span class="sxs-lookup"><span data-stu-id="667b4-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="667b4-117">Las plantillas proporcionan flexibilidad para enviar inserciones multiplataforma e inserciones localizadas.</span><span class="sxs-lookup"><span data-stu-id="667b4-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="667b4-118">[Uso de la biblioteca de cliente de iOS para Aplicaciones móviles de Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) muestra cómo registrar plantillas.</span><span class="sxs-lookup"><span data-stu-id="667b4-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="667b4-119">[inicio rápido de iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="667b4-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>

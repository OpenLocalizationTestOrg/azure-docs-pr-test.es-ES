---
title: "aaaAdd tooiOS de notificaciones Push aplicación con aplicaciones móviles de Azure"
description: "Obtenga información acerca de cómo toouse toosend de aplicaciones móviles de Azure aplicación de iOS de tooyour de notificaciones de inserción."
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
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="c317b-103">Agregar aplicación de iOS de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="c317b-103">Add Push Notifications tooyour iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="c317b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c317b-104">Overview</span></span>
<span data-ttu-id="c317b-105">En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido de iOS] del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.</span><span class="sxs-lookup"><span data-stu-id="c317b-105">In this tutorial, you add push notifications toohello [iOS quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="c317b-106">Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="c317b-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="c317b-107">Vea [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c317b-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="c317b-108">Hola [simulador de iOS no admite notificaciones de inserción](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="c317b-108">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="c317b-109">Necesita un dispositivo de iOS físico y una [suscripción de Apple Developer Program](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="c317b-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="c317b-110"><a name="configure-hub"></a>Configurar el Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="c317b-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="c317b-111"><a id="register"></a>Registro de aplicaciones para notificaciones push</span><span class="sxs-lookup"><span data-stu-id="c317b-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="c317b-112">Configurar notificaciones de inserción de Azure toosend</span><span class="sxs-lookup"><span data-stu-id="c317b-112">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="c317b-113"><a id="update-server"></a>Actualizar notificaciones de inserción de back-end toosend</span><span class="sxs-lookup"><span data-stu-id="c317b-113"><a id="update-server"></a>Update backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="c317b-114"><a id="add-push"></a>Agregar tooapp de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="c317b-114"><a id="add-push"></a>Add push notifications tooapp</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="c317b-115"><a id="test"></a>Probar notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="c317b-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="c317b-116"><a id="more"></a>Más</span><span class="sxs-lookup"><span data-stu-id="c317b-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="c317b-117">Plantillas de proporcionan inserciones de flexibilidad toosend multiplataforma e inserciones localizados.</span><span class="sxs-lookup"><span data-stu-id="c317b-117">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="c317b-118">[¿Cómo tooUse iOS biblioteca de cliente para aplicaciones móviles de Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) le enseña cómo tooregister plantillas.</span><span class="sxs-lookup"><span data-stu-id="c317b-118">[How tooUse iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how tooregister templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[inicio rápido de iOS]: app-service-mobile-ios-get-started.md

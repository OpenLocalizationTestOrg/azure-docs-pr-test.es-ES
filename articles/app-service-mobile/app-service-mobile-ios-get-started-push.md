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
# <a name="add-push-notifications-tooyour-ios-app"></a>Agregar aplicación de iOS de tooyour de notificaciones de inserción
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Información general
En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido de iOS] del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.

Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción. Vea [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.

Hola [simulador de iOS no admite notificaciones de inserción](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html). Necesita un dispositivo de iOS físico y una [suscripción de Apple Developer Program](https://developer.apple.com/programs/ios/).

## <a name="configure-hub"></a>Configurar el Centro de notificaciones
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Registro de aplicaciones para notificaciones push
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Configurar notificaciones de inserción de Azure toosend
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a>Actualizar notificaciones de inserción de back-end toosend
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>Agregar tooapp de notificaciones de inserción
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>Probar notificaciones de inserción
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a>Más
* Plantillas de proporcionan inserciones de flexibilidad toosend multiplataforma e inserciones localizados. [¿Cómo tooUse iOS biblioteca de cliente para aplicaciones móviles de Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) le enseña cómo tooregister plantillas.

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[inicio rápido de iOS]: app-service-mobile-ios-get-started.md

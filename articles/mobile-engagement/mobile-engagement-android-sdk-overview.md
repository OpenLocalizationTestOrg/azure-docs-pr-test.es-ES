---
title: "aaaAndroid integración con el SDK de Azure Mobile Engagement"
description: "Describe cómo toointegrate SDK de Azure Mobile Engagement en aplicaciones de Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Integración del SDK de Android para Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Windows universal](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

Este documento describe todos los Hola integración y configuración de opciones disponibles para Android SDK de Azure Mobile Engagement.

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>Características avanzadas
### <a name="reporting-features"></a>Características de informes
Puede agregar estas características:

1. [Opciones de informes avanzados](mobile-engagement-android-advanced-reporting.md)
2. [Opciones de informes de ubicación](mobile-engagement-android-location-reporting.md)
3. [Opciones de configuración avanzada](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>Notificaciones:
[¿Cómo toointegrate alcance (notificaciones) en la aplicación Android](mobile-engagement-android-integrate-engagement-reach.md)

1. Mensajería de nube de Google (GCM): [cómo tooIntegrate GCM con Mobile Engagement](mobile-engagement-android-gcm-integrate.md)
2. Mensajería de dispositivos de Amazon (ADM): [cómo tooIntegrate ADM con Mobile Engagement](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>Implementación del plan de etiquetas:
[¿Cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Android](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>Notas de la versión

### <a name="431-07172017"></a>4.3.1 (17/07/2017)
* Se ha corregido un bloqueo que rara vez puede suceder cuando se llama a `EngagementAgentUtils.isInDedicatedEngagementProcess`, que también usan hello `EngagementApplication` clase.

### <a name="430-06272017"></a>4.3.0 (27/06/2017)
* Android admiten 8 (versiones anteriores de hello SDK no funcionarán en Android 8).
* Desaparece la dependencia de la biblioteca de soporte.
* Se quita la clase `EngagementFragmentActivity`.
* Vencimiento demasiado[límites de la ejecución de fondo](https://developer.android.com/preview/features/background.html) en 8 Android, registros en segundo plano se retrasa hasta que el usuario de hello interactúa con el dispositivo de hello, esto tendrá un impacto en la campaña de inserción **entregados** y **Notificación del sistema mostrada** estadísticas que se retrasa si se encontraba inactivo el dispositivo hello (Hola notificación seguirán mostrándose, se anillo y Vibrar en tiempo real sin problemas).
* Vencimiento demasiado[límites de ubicación de fondo](https://developer.android.com/preview/features/background-location-limits.html), ubicación de tiempo real de hello en segundo plano no se actualizará con frecuencia en 8 Android.

Para todas las versiones, vea hello [completar notas de la versión](mobile-engagement-android-release-notes.md).

## <a name="upgrade-procedures"></a>Procedimientos de actualización
Si ya ha integrado una versión anterior de nuestro SDK en su aplicación, consulte [Procedimientos de actualización](mobile-engagement-android-upgrade-procedure.md).


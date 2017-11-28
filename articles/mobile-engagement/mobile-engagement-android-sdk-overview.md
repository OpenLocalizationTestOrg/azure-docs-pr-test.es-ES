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
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="e84eb-103">Integración del SDK de Android para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e84eb-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e84eb-104">Windows universal</span><span class="sxs-lookup"><span data-stu-id="e84eb-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="e84eb-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="e84eb-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="e84eb-106">iOS</span><span class="sxs-lookup"><span data-stu-id="e84eb-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="e84eb-107">Android</span><span class="sxs-lookup"><span data-stu-id="e84eb-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="e84eb-108">Este documento describe todos los Hola integración y configuración de opciones disponibles para Android SDK de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e84eb-108">This document describes all hello integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e84eb-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e84eb-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="e84eb-110">Características avanzadas</span><span class="sxs-lookup"><span data-stu-id="e84eb-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="e84eb-111">Características de informes</span><span class="sxs-lookup"><span data-stu-id="e84eb-111">Reporting Features</span></span>
<span data-ttu-id="e84eb-112">Puede agregar estas características:</span><span class="sxs-lookup"><span data-stu-id="e84eb-112">You can add these features:</span></span>

1. [<span data-ttu-id="e84eb-113">Opciones de informes avanzados</span><span class="sxs-lookup"><span data-stu-id="e84eb-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="e84eb-114">Opciones de informes de ubicación</span><span class="sxs-lookup"><span data-stu-id="e84eb-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="e84eb-115">Opciones de configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="e84eb-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="e84eb-116">Notificaciones:</span><span class="sxs-lookup"><span data-stu-id="e84eb-116">Notifications:</span></span>
[<span data-ttu-id="e84eb-117">¿Cómo toointegrate alcance (notificaciones) en la aplicación Android</span><span class="sxs-lookup"><span data-stu-id="e84eb-117">How toointegrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="e84eb-118">Mensajería de nube de Google (GCM): [cómo tooIntegrate GCM con Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="e84eb-118">Google Cloud Messaging (GCM): [How tooIntegrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="e84eb-119">Mensajería de dispositivos de Amazon (ADM): [cómo tooIntegrate ADM con Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="e84eb-119">Amazon Device Messaging (ADM): [How tooIntegrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="e84eb-120">Implementación del plan de etiquetas:</span><span class="sxs-lookup"><span data-stu-id="e84eb-120">Tag plan implementation:</span></span>
[<span data-ttu-id="e84eb-121">¿Cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Android</span><span class="sxs-lookup"><span data-stu-id="e84eb-121">How toouse hello advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="e84eb-122">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="e84eb-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="e84eb-123">4.3.1 (17/07/2017)</span><span class="sxs-lookup"><span data-stu-id="e84eb-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="e84eb-124">Se ha corregido un bloqueo que rara vez puede suceder cuando se llama a `EngagementAgentUtils.isInDedicatedEngagementProcess`, que también usan hello `EngagementApplication` clase.</span><span class="sxs-lookup"><span data-stu-id="e84eb-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="e84eb-125">4.3.0 (27/06/2017)</span><span class="sxs-lookup"><span data-stu-id="e84eb-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="e84eb-126">Android admiten 8 (versiones anteriores de hello SDK no funcionarán en Android 8).</span><span class="sxs-lookup"><span data-stu-id="e84eb-126">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="e84eb-127">Desaparece la dependencia de la biblioteca de soporte.</span><span class="sxs-lookup"><span data-stu-id="e84eb-127">No more dependency on support library.</span></span>
* <span data-ttu-id="e84eb-128">Se quita la clase `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="e84eb-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="e84eb-129">Vencimiento demasiado[límites de la ejecución de fondo](https://developer.android.com/preview/features/background.html) en 8 Android, registros en segundo plano se retrasa hasta que el usuario de hello interactúa con el dispositivo de hello, esto tendrá un impacto en la campaña de inserción **entregados** y **Notificación del sistema mostrada** estadísticas que se retrasa si se encontraba inactivo el dispositivo hello (Hola notificación seguirán mostrándose, se anillo y Vibrar en tiempo real sin problemas).</span><span class="sxs-lookup"><span data-stu-id="e84eb-129">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="e84eb-130">Vencimiento demasiado[límites de ubicación de fondo](https://developer.android.com/preview/features/background-location-limits.html), ubicación de tiempo real de hello en segundo plano no se actualizará con frecuencia en 8 Android.</span><span class="sxs-lookup"><span data-stu-id="e84eb-130">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="e84eb-131">Para todas las versiones, vea hello [completar notas de la versión](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="e84eb-131">For all versions, see hello [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="e84eb-132">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="e84eb-132">Upgrade procedures</span></span>
<span data-ttu-id="e84eb-133">Si ya ha integrado una versión anterior de nuestro SDK en su aplicación, consulte [Procedimientos de actualización](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="e84eb-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>


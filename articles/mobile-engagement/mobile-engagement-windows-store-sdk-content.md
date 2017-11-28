---
title: aaaWindows contenido de SDK de aplicaciones Universal
description: "Obtenga información sobre el contenido de Hola de SDK de aplicaciones universales de Windows hello para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="7703c-103">Contenido del SDK de Windows Universal Apps</span><span class="sxs-lookup"><span data-stu-id="7703c-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="7703c-104">Este documento enumera y describe el contenido de hello implementada por hello SDK en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7703c-104">This document lists and describes hello content deployed by hello SDK in your application.</span></span>

## <a name="hello-resources-folder"></a><span data-ttu-id="7703c-105">Hola `/Resources` carpeta</span><span class="sxs-lookup"><span data-stu-id="7703c-105">hello `/Resources` folder</span></span>
<span data-ttu-id="7703c-106">Esta carpeta contiene todos los recursos de Hola que necesita de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7703c-106">This folder contains all hello resources that Mobile Engagement needs.</span></span> <span data-ttu-id="7703c-107">También puede personalizar toofit la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7703c-107">You can also customize them toofit your app.</span></span>

* <span data-ttu-id="7703c-108">`EngagementConfiguration.xml`: Hola archivo de configuración de Mobile Engagement, que es donde puede personalizar la configuración de Mobile Engagement (cadena de conexión de Mobile Engagement, bloqueo de informes...).</span><span class="sxs-lookup"><span data-stu-id="7703c-108">`EngagementConfiguration.xml` : hello Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="7703c-109">Carpeta /html</span><span class="sxs-lookup"><span data-stu-id="7703c-109">/html folder</span></span>
* <span data-ttu-id="7703c-110">`EngagementNotification.html`: Hola `Notification` vista de diseño de html para los titulares de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7703c-110">`EngagementNotification.html` : hello `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="7703c-111">`EngagementAnnouncement.html`: Hola `Announcement` vista de diseño de html para las vistas intersticiales en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7703c-111">`EngagementAnnouncement.html` : hello `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="7703c-112">Carpeta /images</span><span class="sxs-lookup"><span data-stu-id="7703c-112">/images folder</span></span>
* <span data-ttu-id="7703c-113">`EngagementIconNotification.png`: icono de marca de hello mostrado en hello a la izquierda de una notificación, remplazar éste mediante el icono de marca.</span><span class="sxs-lookup"><span data-stu-id="7703c-113">`EngagementIconNotification.png` : hello brand icon displayed at hello left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="7703c-114">`EngagementIconOk.png`: Hola `Ok` icono de páginas de contenido de alcance de hello para el botón de acción o validación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7703c-114">`EngagementIconOk.png` : hello `Ok` icon of hello reach content pages for hello action or validation button.</span></span>
* <span data-ttu-id="7703c-115">`EngagementIconNOK.png`: Hola `NOK` icono usado cuando se deshabilita el botón de validación de Hola Hola alcance páginas de contenido.</span><span class="sxs-lookup"><span data-stu-id="7703c-115">`EngagementIconNOK.png` : hello `NOK` icon used when hello validation button of hello reach content pages is disabled.</span></span>
* <span data-ttu-id="7703c-116">`EngagementIconClose.png`: Hola `Close` icono del programa Hola a llegar a las notificaciones y contenidos de hello descartar botón.</span><span class="sxs-lookup"><span data-stu-id="7703c-116">`EngagementIconClose.png` : hello `Close` icon of hello reach notifications and contents for hello dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="7703c-117">Carpeta /overlay</span><span class="sxs-lookup"><span data-stu-id="7703c-117">/overlay folder</span></span>
* <span data-ttu-id="7703c-118">`EngagementPageOverlay.cs`: página de superposición de hello responsable de agregar Hola interacción alcanzar secundarios de tooits de interfaz de usuario de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7703c-118">`EngagementPageOverlay.cs` : hello overlay page responsible for adding hello Engagement reach in-app UI tooits child.</span></span>


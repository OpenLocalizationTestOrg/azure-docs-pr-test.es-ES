---
title: Contenido del SDK de Windows Universal Apps
description: "Obtenga información sobre el contenido del SDK de Windows Universal Apps para Azure Mobile Engagement"
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
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="3a304-103">Contenido del SDK de Windows Universal Apps</span><span class="sxs-lookup"><span data-stu-id="3a304-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="3a304-104">En este documento se enumera y describe el contenido implementado por el SDK de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a304-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="3a304-105">La carpeta `/Resources`</span><span class="sxs-lookup"><span data-stu-id="3a304-105">The `/Resources` folder</span></span>
<span data-ttu-id="3a304-106">En esta carpeta se incluyen todos los recursos que necesita Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3a304-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="3a304-107">Además, puede personalizarlas para adaptarlas a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a304-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="3a304-108">`EngagementConfiguration.xml` : el archivo de configuración de Mobile Engagement, donde puede personalizar la configuración de Mobile Engagement (cadena de conexión de Mobile Engagement, bloqueo de informes, etc.).</span><span class="sxs-lookup"><span data-stu-id="3a304-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="3a304-109">Carpeta /html</span><span class="sxs-lookup"><span data-stu-id="3a304-109">/html folder</span></span>
* <span data-ttu-id="3a304-110">`EngagementNotification.html` : El diseño html de vista web `Notification` para banners en aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a304-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="3a304-111">`EngagementAnnouncement.html` : El diseño html de vista web `Announcement` para vistas intersticiales en aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a304-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="3a304-112">Carpeta /images</span><span class="sxs-lookup"><span data-stu-id="3a304-112">/images folder</span></span>
* <span data-ttu-id="3a304-113">`EngagementIconNotification.png`: el icono de marca que se muestra a la izquierda de una notificación, sustituya este por el icono de la marca.</span><span class="sxs-lookup"><span data-stu-id="3a304-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="3a304-114">`EngagementIconOk.png`: el icono `Ok` de las páginas de contenido de Cobertura para el botón de acción o validación.</span><span class="sxs-lookup"><span data-stu-id="3a304-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="3a304-115">`EngagementIconNOK.png`: el icono `NOK` que se usa cuando se deshabilita el botón de validación de las páginas de contenido de Cobertura.</span><span class="sxs-lookup"><span data-stu-id="3a304-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="3a304-116">`EngagementIconClose.png`: el icono `Close` de las notificaciones y el contenido de Cobertura para el botón Descartar.</span><span class="sxs-lookup"><span data-stu-id="3a304-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="3a304-117">Carpeta /overlay</span><span class="sxs-lookup"><span data-stu-id="3a304-117">/overlay folder</span></span>
* <span data-ttu-id="3a304-118">`EngagementPageOverlay.cs` : La página de superposición responsable de agregar la IU en aplicación de Engagement Reach a su hijo.</span><span class="sxs-lookup"><span data-stu-id="3a304-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>


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
# <a name="windows-universal-apps-sdk-content"></a>Contenido del SDK de Windows Universal Apps
Este documento enumera y describe el contenido de hello implementada por hello SDK en la aplicación.

## <a name="hello-resources-folder"></a>Hola `/Resources` carpeta
Esta carpeta contiene todos los recursos de Hola que necesita de Mobile Engagement. También puede personalizar toofit la aplicación.

* `EngagementConfiguration.xml`: Hola archivo de configuración de Mobile Engagement, que es donde puede personalizar la configuración de Mobile Engagement (cadena de conexión de Mobile Engagement, bloqueo de informes...).

### <a name="html-folder"></a>Carpeta /html
* `EngagementNotification.html`: Hola `Notification` vista de diseño de html para los titulares de la aplicación web.
* `EngagementAnnouncement.html`: Hola `Announcement` vista de diseño de html para las vistas intersticiales en la aplicación web.

### <a name="images-folder"></a>Carpeta /images
* `EngagementIconNotification.png`: icono de marca de hello mostrado en hello a la izquierda de una notificación, remplazar éste mediante el icono de marca.
* `EngagementIconOk.png`: Hola `Ok` icono de páginas de contenido de alcance de hello para el botón de acción o validación de Hola.
* `EngagementIconNOK.png`: Hola `NOK` icono usado cuando se deshabilita el botón de validación de Hola Hola alcance páginas de contenido.
* `EngagementIconClose.png`: Hola `Close` icono del programa Hola a llegar a las notificaciones y contenidos de hello descartar botón.

### <a name="overlay-folder"></a>Carpeta /overlay
* `EngagementPageOverlay.cs`: página de superposición de hello responsable de agregar Hola interacción alcanzar secundarios de tooits de interfaz de usuario de la aplicación.


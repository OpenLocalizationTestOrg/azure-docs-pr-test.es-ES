---
title: "Actividad de inicio de sesión irregular"
description: "Informe que incluye inicios de sesión que nuestros algoritmos de aprendizaje automático identificaron como anómalos."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a>Actividad de inicio de sesión irregular
Los inicios de sesión irregulares son aquellos que han identificado los algoritmos de aprendizaje automático, de acuerdo con una condición de "viaje imposible" combinada con una ubicación y un dispositivo de inicio de sesión anómalos. Esto puede indicar que un hacker ha inicio sesión con esta cuenta.
Se enviará una notificación por correo electrónico a los administradores globales si encontramos 10 o más eventos de inicio de sesión anómalos dentro de un intervalo de 30 días o menos. Asegúrese de incluir aad-alerts-noreply@mail.windowsazure.com en la lista de remitentes seguros.


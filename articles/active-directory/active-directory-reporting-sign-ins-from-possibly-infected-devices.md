---
title: "Inicios de sesión desde dispositivos posiblemente infectados"
description: "Un informe que incluye intentos de inicio de sesión que se han ejecutado desde dispositivos en los que se puede estar ejecutando algún malware (software malintencionado)."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: d0361662-d970-4a66-8eb3-72e9f8824dcf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 3809e20937d8d9829675e20f893101cb849dcea2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-possibly-infected-devices"></a><span data-ttu-id="477f0-103">Inicios de sesión desde dispositivos posiblemente infectados</span><span class="sxs-lookup"><span data-stu-id="477f0-103">Sign ins from possibly infected devices</span></span>
<span data-ttu-id="477f0-104">Este informe intenta identificar los dispositivos de usuario que se han infectado y ahora forman parte de una red de robots (botnet).</span><span class="sxs-lookup"><span data-stu-id="477f0-104">This report attempts to identify your users' devices that that have become infected and are now part of a botnet.</span></span> <span data-ttu-id="477f0-105">Ponemos en correlación las direcciones IP de los inicios de sesión de los usuarios con las direcciones IP que sabemos que están en contacto con servidores de botnets.</span><span class="sxs-lookup"><span data-stu-id="477f0-105">We correlate IP addresses of users' sign-ins against IP addresses that we know to be in contact with botnet servers.</span></span>

<span data-ttu-id="477f0-106">Recomendación: este informe marca direcciones IP y no dispositivos de usuario.</span><span class="sxs-lookup"><span data-stu-id="477f0-106">Recommendation: This report flags IP addresses, not user devices.</span></span> <span data-ttu-id="477f0-107">Se recomienda ponerse en contacto con el usuario y examinar todos sus dispositivos para estar seguro.</span><span class="sxs-lookup"><span data-stu-id="477f0-107">We recommend that you contact the user and scan all the user's devices to be certain.</span></span> <span data-ttu-id="477f0-108">También es posible que el dispositivo personal del usuario esté infectado o que alguien que no sea el usuario, que estaba usando la misma dirección IP que el usuario, tenga un dispositivo infectado.</span><span class="sxs-lookup"><span data-stu-id="477f0-108">It is also possible that a user's personal device is infected, or that someone other than the user, who was using the same IP address as the user, has an infected device.</span></span>

<span data-ttu-id="477f0-109">Para obtener más información acerca de cómo tratar infecciones de malware, consulte el [Centro de protección contra malware](http://go.microsoft.com/fwlink/?linkid=335773).</span><span class="sxs-lookup"><span data-stu-id="477f0-109">For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773).</span></span>

![Inicios de sesión desde dispositivos posiblemente infectados](./media/active-directory-reporting-sign-ins-from-possibly-infected-devices/signInsFromPossiblyInfectedDevices.PNG)


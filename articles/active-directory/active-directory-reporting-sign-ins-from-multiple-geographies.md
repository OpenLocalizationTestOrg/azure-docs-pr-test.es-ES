---
title: "Inicios de sesión desde varias ubicaciones geográficas"
description: "Informe que señala usuarios en los que dos inicios de sesión parecían originarse en distintas regiones y, por el tiempo transcurrido entre inicios de sesión, resultaba imposible que el usuario viajase entre dichas regiones."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a><span data-ttu-id="4cc72-103">Inicios de sesión desde varias ubicaciones geográficas</span><span class="sxs-lookup"><span data-stu-id="4cc72-103">Sign-ins from multiple geographies</span></span>
<span data-ttu-id="4cc72-104">En este informe se incluyen inicios de sesión correctos de un usuario en los que parece que dos inicios de sesión se originaron desde distintas regiones y que, según el tiempo transcurrido entre ellos, parece imposible que el usuario haya viajado entre dichas regiones.</span><span class="sxs-lookup"><span data-stu-id="4cc72-104">This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions.</span></span> <span data-ttu-id="4cc72-105">Entre las posibles causas se incluyen las siguientes:</span><span class="sxs-lookup"><span data-stu-id="4cc72-105">Possible causes include:</span></span>

* <span data-ttu-id="4cc72-106">El usuario comparte su contraseña con otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="4cc72-106">User is sharing their password with other users</span></span>
* <span data-ttu-id="4cc72-107">El usuario usa un escritorio remoto para iniciar un navegador web para el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4cc72-107">User is using a remote desktop to launch a web browser for sign-in</span></span>
* <span data-ttu-id="4cc72-108">Un hacker inició sesión en la cuenta de un usuario desde un país diferente.</span><span class="sxs-lookup"><span data-stu-id="4cc72-108">A hacker has signed in to the account of a user from a different country</span></span>
* <span data-ttu-id="4cc72-109">El usuario está utilizando un proxy o una VPN.</span><span class="sxs-lookup"><span data-stu-id="4cc72-109">User is using a VPN or proxy</span></span>
* <span data-ttu-id="4cc72-110">El usuario ha iniciado sesión desde varios dispositivos al mismo tiempo, como un equipo de escritorio y un teléfono móvil, y la dirección IP del teléfono móvil es poco común.</span><span class="sxs-lookup"><span data-stu-id="4cc72-110">User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.</span></span>

<span data-ttu-id="4cc72-111">Los resultados de este informe mostrarán los eventos de inicio de sesión correctos, así como el tiempo transcurrido entre ellos, las regiones de donde parecían provenir y el tiempo de viaje estimado entre dichas regiones.</span><span class="sxs-lookup"><span data-stu-id="4cc72-111">Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions.</span></span> <span data-ttu-id="4cc72-112">El tiempo de viaje mostrado constituye solo una estimación y puede diferir del tiempo de viaje real entre las ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="4cc72-112">The travel time shown is only an estimate and may be different from the actual travel time between the locations.</span></span>

![Inicios de sesión desde varias ubicaciones geográficas](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)


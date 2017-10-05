---
title: "Inicios de sesión desde orígenes desconocidos"
description: "Un informe que indica los usuarios que han iniciado sesión correctamente en el directorio a partir de una dirección IP de un proxy anónimo."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: 2f045543-1578-4972-bf70-b35310f23110
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 90006121e4b3392f6e3ecffb4a56aca330feb02f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-unknown-sources"></a><span data-ttu-id="6f654-103">Inicios de sesión desde orígenes desconocidos</span><span class="sxs-lookup"><span data-stu-id="6f654-103">Sign ins from unknown sources</span></span>
<span data-ttu-id="6f654-104">En este informe se incluyen los usuarios que han iniciado sesión correctamente en su directorio cuando tenían asignada una dirección IP de cliente que Microsoft ha reconocido como dirección IP de proxy anónimo (por ejemplo, una dirección IP Tor).</span><span class="sxs-lookup"><span data-stu-id="6f654-104">This report indicates users who have successfully signed in to your directory while assigned a client IP address that has been recognized by Microsoft as an anonymous proxy IP address (for example, a Tor IP address).</span></span> <span data-ttu-id="6f654-105">Estos servidores proxy los usan a menudo los usuarios que desean ocultar la dirección IP del equipo y es posible que se usen con fines malintencionados.</span><span class="sxs-lookup"><span data-stu-id="6f654-105">These proxies are often used by users that want to hide their computer’s IP address, and may be used for malicious intent.</span></span>

<span data-ttu-id="6f654-106">Los resultados de este informe mostrarán el número de veces que un usuario ha iniciado sesión correctamente en su directorio desde esa dirección y la dirección IP de proxy.</span><span class="sxs-lookup"><span data-stu-id="6f654-106">Results from this report will show the number of times a user successfully signed in to your directory from that address and the proxy’s IP address.</span></span>

![Inicios de sesión desde orígenes desconocidos](./media/active-directory-reporting-sign-ins-from-unknown-sources/signInsFromUnknownSources.PNG)


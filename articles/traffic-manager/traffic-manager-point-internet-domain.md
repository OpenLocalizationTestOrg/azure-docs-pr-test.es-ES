---
title: aaaPoint un nombre de dominio de empresa Internet dominio tooa Traffic Manager | Documentos de Microsoft
description: "Este artículo le ayudará a dirigir su nombre de dominio de empresa dominio nombre tooa Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a><span data-ttu-id="ed717-103">Seleccione un dominio de Azure Traffic Manager empresa tooan de dominio de Internet</span><span class="sxs-lookup"><span data-stu-id="ed717-103">Point a company Internet domain tooan Azure Traffic Manager domain</span></span>

<span data-ttu-id="ed717-104">Cuando se crea un perfil de Traffic Manager, Azure asigna automáticamente un nombre DNS para ese perfil.</span><span class="sxs-lookup"><span data-stu-id="ed717-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="ed717-105">toouse un nombre de la zona DNS, cree un registro CNAME DNS que asigna el nombre de dominio toohello de su perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="ed717-105">toouse a name from your DNS zone, create a CNAME DNS record that maps toohello domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="ed717-106">Puede encontrar el nombre de dominio de Traffic Manager de Hola Hola **General** sección en la página de configuración de Hola de hello perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="ed717-106">You can find hello Traffic Manager domain name in hello **General** section on hello Configuration page of hello Traffic Manager profile.</span></span>

<span data-ttu-id="ed717-107">Por ejemplo, www.contoso.com toohello contoso.trafficmanager.net de nombre de DNS de Traffic Manager de toopoint nombre, crearía Hola siguiendo el registro de recursos DNS:</span><span class="sxs-lookup"><span data-stu-id="ed717-107">For example, toopoint name www.contoso.com toohello Traffic Manager DNS name contoso.trafficmanager.net, you would create hello following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="ed717-108">Todo el tráfico de solicitudes demasiado*www.contoso.com* dirigidos demasiado*contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="ed717-108">All traffic requests too*www.contoso.com* get directed too*contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed717-109">No puede apuntar a un dominio de segundo nivel, como *contoso.com*, dominio de Traffic Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="ed717-109">You cannot point a second-level domain, such as *contoso.com*, toohello Traffic Manager domain.</span></span> <span data-ttu-id="ed717-110">Los estándares de protocolo DNS no permiten registros CNAME para nombres de dominio de segundo nivel.</span><span class="sxs-lookup"><span data-stu-id="ed717-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed717-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed717-111">Next steps</span></span>

* [<span data-ttu-id="ed717-112">Métodos de enrutamiento del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="ed717-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="ed717-113">Administrador de tráfico: deshabilitación, habilitación o eliminación de un perfil</span><span class="sxs-lookup"><span data-stu-id="ed717-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="ed717-114">Administrador de tráfico: deshabilitación o habilitación de un extremo</span><span class="sxs-lookup"><span data-stu-id="ed717-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)

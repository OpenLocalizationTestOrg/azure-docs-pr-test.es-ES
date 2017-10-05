---
title: "Hacer que un dominio de Internet de la compañía indique un nombre de dominio de Traffic Manager | Microsoft Docs"
description: "Este artículo le ayudará a que el nombre de dominio de la empresa indique un nombre de dominio del Administrador de tráfico."
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
ms.openlocfilehash: 0322b3510cfd4f94031d8c1db8f1cc032b997fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="point-a-company-internet-domain-to-an-azure-traffic-manager-domain"></a><span data-ttu-id="2a30c-103">Hacer que un dominio de Internet de la compañía indique un dominio de Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2a30c-103">Point a company Internet domain to an Azure Traffic Manager domain</span></span>

<span data-ttu-id="2a30c-104">Cuando se crea un perfil de Traffic Manager, Azure asigna automáticamente un nombre DNS para ese perfil.</span><span class="sxs-lookup"><span data-stu-id="2a30c-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="2a30c-105">Para usar un nombre de la zona DNS, cree un registro DNS CNAME que se asigne al nombre de dominio de su perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2a30c-105">To use a name from your DNS zone, create a CNAME DNS record that maps to the domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="2a30c-106">Puede encontrar el nombre de dominio de Traffic Manager en la sección **General** de la página Configuración del perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2a30c-106">You can find the Traffic Manager domain name in the **General** section on the Configuration page of the Traffic Manager profile.</span></span>

<span data-ttu-id="2a30c-107">Por ejemplo, para que el nombre www.contoso.com apunte al nombre DNS de Traffic Manager contoso.trafficmanager.net, debe crear el siguiente registro de recursos DNS:</span><span class="sxs-lookup"><span data-stu-id="2a30c-107">For example, to point name www.contoso.com to the Traffic Manager DNS name contoso.trafficmanager.net, you would create the following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="2a30c-108">Todas las solicitudes de tráfico hacia *www.contoso.com* se redirigen a *contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="2a30c-108">All traffic requests to *www.contoso.com* get directed to *contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a30c-109">No puede hacer que un dominio de segundo nivel como por ejemplo *contoso.com*, indique el dominio del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="2a30c-109">You cannot point a second-level domain, such as *contoso.com*, to the Traffic Manager domain.</span></span> <span data-ttu-id="2a30c-110">Los estándares de protocolo DNS no permiten registros CNAME para nombres de dominio de segundo nivel.</span><span class="sxs-lookup"><span data-stu-id="2a30c-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a30c-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a30c-111">Next steps</span></span>

* [<span data-ttu-id="2a30c-112">Métodos de enrutamiento del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2a30c-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="2a30c-113">Administrador de tráfico: deshabilitación, habilitación o eliminación de un perfil</span><span class="sxs-lookup"><span data-stu-id="2a30c-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="2a30c-114">Administrador de tráfico: deshabilitación o habilitación de un extremo</span><span class="sxs-lookup"><span data-stu-id="2a30c-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)

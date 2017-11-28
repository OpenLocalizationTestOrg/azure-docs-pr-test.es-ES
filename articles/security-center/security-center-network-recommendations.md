---
title: aaaProtecting la red en el centro de seguridad de Azure | Documentos de Microsoft
description: "En este documento se explica cómo las recomendaciones de Azure Security Center ayudan a proteger las redes y a cumplir las directivas de seguridad."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="6a3b0-103">Protección de las redes en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6a3b0-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="6a3b0-104">Centro de seguridad de Azure analiza el estado de seguridad de Hola de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="6a3b0-105">Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, crea las recomendaciones que le guiarán a lo largo de proceso de Hola de configuración de controles de Hola que sea necesitado.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="6a3b0-106">Las recomendaciones aplican tipos de recursos de tooAzure: máquinas virtuales (VM), redes, aplicaciones y SQL.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="6a3b0-107">Este artículo tratan las recomendaciones que se aplican tooyour red.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="6a3b0-108">Las recomendaciones sobre redes se centran en los firewalls de próxima generación, los grupos de seguridad de red, la configuración de reglas de tráfico entrantes y mucho más.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="6a3b0-109">Uso de tabla de Hola a continuación como un toohelp de referencia comprende las recomendaciones de red disponible de Hola y lo que hace cada uno de ellos si se aplica.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="6a3b0-110">Recomendaciones sobre redes disponibles</span><span class="sxs-lookup"><span data-stu-id="6a3b0-110">Available network recommendations</span></span>
| <span data-ttu-id="6a3b0-111">Recomendación</span><span class="sxs-lookup"><span data-stu-id="6a3b0-111">Recommendation</span></span> | <span data-ttu-id="6a3b0-112">Description</span><span class="sxs-lookup"><span data-stu-id="6a3b0-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="6a3b0-113">Agregar un firewall de próxima generación</span><span class="sxs-lookup"><span data-stu-id="6a3b0-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="6a3b0-114">Recomienda agregar un servidor de seguridad de próxima generación (NGFW) desde un tooincrease de partner de Microsoft la protección de la seguridad.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="6a3b0-115">Enrutar el tráfico solo a través de NGFW</span><span class="sxs-lookup"><span data-stu-id="6a3b0-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="6a3b0-116">Se recomienda que configure reglas de grupo (NSG) de seguridad de red que fuerce el tráfico entrante tooyour máquina virtual a través de su NGFW.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="6a3b0-117">Habilitar grupos de seguridad de red en subredes o máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6a3b0-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="6a3b0-118">Recomienda habilitar NSG en subredes o máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="6a3b0-119">Restringir el acceso a través de puntos de conexión accesibles desde Internet</span><span class="sxs-lookup"><span data-stu-id="6a3b0-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="6a3b0-120">Recomienda configurar reglas de tráfico de entrada para los NSG.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="6a3b0-121">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6a3b0-121">See also</span></span>
<span data-ttu-id="6a3b0-122">toolearn más información acerca de las recomendaciones que se aplican tooother tipos de recursos de Azure, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6a3b0-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="6a3b0-123">Protección de las máquinas virtuales en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6a3b0-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="6a3b0-124">Protección de las aplicaciones en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6a3b0-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="6a3b0-125">Protección del servicio SQL de Azure en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6a3b0-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="6a3b0-126">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6a3b0-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="6a3b0-127">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="6a3b0-128">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="6a3b0-129">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a3b0-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>

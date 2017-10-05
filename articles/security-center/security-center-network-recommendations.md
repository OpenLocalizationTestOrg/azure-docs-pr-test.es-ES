---
title: "Protección de las redes en Azure Security Center | Microsoft Docs"
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
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="bcb55-103">Protección de las redes en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="bcb55-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="bcb55-104">El Centro de seguridad de Azure analiza el estado de seguridad de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb55-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="bcb55-105">Cuando Security Center identifica posibles vulnerabilidades de seguridad, crea recomendaciones que lo guiarán por el proceso de configuración de los controles necesarios.</span><span class="sxs-lookup"><span data-stu-id="bcb55-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="bcb55-106">Las recomendaciones se aplican a los tipos de recursos de Azure: máquinas virtuales, redes, SQL y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bcb55-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="bcb55-107">Este artículo aborda las recomendaciones sobre redes.</span><span class="sxs-lookup"><span data-stu-id="bcb55-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="bcb55-108">Las recomendaciones sobre redes se centran en los firewalls de próxima generación, los grupos de seguridad de red, la configuración de reglas de tráfico entrantes y mucho más.</span><span class="sxs-lookup"><span data-stu-id="bcb55-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="bcb55-109">Use la tabla siguiente como referencia para ayudarlo a entender las recomendaciones disponibles sobre redes y lo que harán cada una de ellas si se aplican.</span><span class="sxs-lookup"><span data-stu-id="bcb55-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="bcb55-110">Recomendaciones sobre redes disponibles</span><span class="sxs-lookup"><span data-stu-id="bcb55-110">Available network recommendations</span></span>
| <span data-ttu-id="bcb55-111">Recomendación</span><span class="sxs-lookup"><span data-stu-id="bcb55-111">Recommendation</span></span> | <span data-ttu-id="bcb55-112">Description</span><span class="sxs-lookup"><span data-stu-id="bcb55-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="bcb55-113">Add a Next Generation Firewall</span><span class="sxs-lookup"><span data-stu-id="bcb55-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="bcb55-114">Recomienda agregar un firewall de próxima generación (NGFW) de un asociado de Microsoft para aumentar la protección.</span><span class="sxs-lookup"><span data-stu-id="bcb55-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="bcb55-115">Enrutar el tráfico solo a través de NGFW</span><span class="sxs-lookup"><span data-stu-id="bcb55-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="bcb55-116">Recomienda configurar reglas de grupos de seguridad de red (NSG) que fuercen que el tráfico entrante pase a su máquina virtual mediante el NGFW.</span><span class="sxs-lookup"><span data-stu-id="bcb55-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="bcb55-117">Habilitar grupos de seguridad de red en subredes o máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="bcb55-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="bcb55-118">Recomienda habilitar NSG en subredes o máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bcb55-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="bcb55-119">Restringir el acceso a través de puntos de conexión accesibles desde Internet</span><span class="sxs-lookup"><span data-stu-id="bcb55-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="bcb55-120">Recomienda configurar reglas de tráfico de entrada para los NSG.</span><span class="sxs-lookup"><span data-stu-id="bcb55-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="bcb55-121">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="bcb55-121">See also</span></span>
<span data-ttu-id="bcb55-122">Para obtener más información sobre las recomendaciones que se aplican a otros tipos de recursos de Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="bcb55-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="bcb55-123">Protección de las máquinas virtuales en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="bcb55-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="bcb55-124">Protección de las aplicaciones en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="bcb55-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="bcb55-125">Protección del servicio SQL de Azure en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="bcb55-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="bcb55-126">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="bcb55-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="bcb55-127">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md) : aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb55-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="bcb55-128">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md) : obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="bcb55-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="bcb55-129">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : encuentre las preguntas más frecuentes sobre el uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="bcb55-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>

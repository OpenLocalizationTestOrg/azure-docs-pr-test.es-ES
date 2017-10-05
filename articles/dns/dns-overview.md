---
title: "Información general de DNS de Azure | Microsoft Docs"
description: "Información general del servicio de hospedaje de DNS en Microsoft Azure. Hospede el dominio en Microsoft Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: 3705457e4c90f8869496f7f5177531bd128d1057
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="3b1eb-104">Introducción a DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="3b1eb-104">Azure DNS overview</span></span>

<span data-ttu-id="3b1eb-105">El sistema de nombres de dominio, o DNS, es responsable de traducir (o resolver) el nombre del sitio web o del servicio en su dirección IP.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="3b1eb-106">DNS de Azure es un servicio de hospedaje para los dominios DNS, que permite resolver nombres mediante la infraestructura de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="3b1eb-107">Al hospedar dominios en Azure, puede administrar los registros DNS con las mismas credenciales, API, herramientas y facturación que con los demás servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Información general de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="3b1eb-109">Características</span><span class="sxs-lookup"><span data-stu-id="3b1eb-109">Features</span></span>

* <span data-ttu-id="3b1eb-110">**Fiabilidad y rendimiento**: los dominios DNS de DNS de Azure se hospedan en la red global de servidores de nombres DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="3b1eb-111">Utilizamos redes de difusión por proximidad, por lo que cada consulta de DNS la responde el servidor DNS disponible más cercano.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-111">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="3b1eb-112">Esto ofrece un rendimiento rápido y alta disponibilidad para el dominio.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="3b1eb-113">**Integración sin problemas**: el servicio DNS de Azure puede usarse para administrar registros DNS de los servicios de Azure y para proporcionar DNS también para los recursos externos.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-113">**Seamless integration** - The Azure DNS service can be used to manage DNS records for your Azure services and can be used to provide DNS for your external resources as well.</span></span> <span data-ttu-id="3b1eb-114">DNS de Azure está integrado en Azure Portal y usa las mismas credenciales, la misma facturación y el mismo contrato de soporte técnico que los demás servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-114">Azure DNS is integrated in the Azure portal and uses the same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="3b1eb-115">**Seguridad**: el servicio DNS de Azure se basa en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-115">**Security** - The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="3b1eb-116">Como tal, se beneficia de características Resource Manager, como control de acceso basado en roles, registros de auditoría y bloqueo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="3b1eb-117">Los dominios y registros pueden administrarse mediante Azure Portal, cmdlets de Azure PowerShell y la CLI de Azure multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-117">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="3b1eb-118">Las aplicaciones que requieren la administración automática de DNS pueden integrarse con el servicio a través de los SDK y API de REST.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-118">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="3b1eb-119">DNS de Azure actualmente no admite la adquisición de nombres de dominio.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="3b1eb-120">Si desea adquirir dominios, debe usar un registrador de nombres de dominio de un tercero.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-120">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="3b1eb-121">El registrador suele cobrar una tarifa anual reducida.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-121">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="3b1eb-122">Los dominios se pueden hospedar en DNS de Azure para la administración de registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-122">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="3b1eb-123">Consulte [Delegación de un dominio en DNS de Azure](dns-domain-delegation.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-123">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="3b1eb-124">Precios</span><span class="sxs-lookup"><span data-stu-id="3b1eb-124">Pricing</span></span>

<span data-ttu-id="3b1eb-125">La facturación de Azure se basa en el número de zonas DNS hospedadas en Azure y en el número de consultas DNS.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-125">DNS billing is based on the number of DNS zones hosted in Azure and by the number of DNS queries.</span></span> <span data-ttu-id="3b1eb-126">Para más información sobre precios, visite [DNS de Azure Precios](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="3b1eb-126">To learn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="3b1eb-127">P+F</span><span class="sxs-lookup"><span data-stu-id="3b1eb-127">FAQ</span></span>

<span data-ttu-id="3b1eb-128">Para ver las preguntas más frecuentes sobre DNS de Azure, vea [Azure DNS FAQ (P+F de DNS de Azure)](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3b1eb-128">For frequently asked questions about Azure DNS, see the [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b1eb-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b1eb-129">Next steps</span></span>

<span data-ttu-id="3b1eb-130">Visite [Información general sobre zonas y registros de DNS](dns-zones-records.md) para obtener más información sobre zonas y registros DNS.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="3b1eb-131">Más información sobre cómo [crear una zona DNS](./dns-getstarted-create-dnszone-portal.md) en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-131">Learn how to [create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="3b1eb-132">Aprenda sobre las demás [funcionalidades de red](../networking/networking-overview.md) clave de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b1eb-132">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>


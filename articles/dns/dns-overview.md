---
title: aaaOverview de DNS de Azure | Documentos de Microsoft
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
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="dd857-104">Introducción a DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="dd857-104">Azure DNS overview</span></span>

<span data-ttu-id="dd857-105">Hola sistema de nombres de dominio o DNS, es responsable de traducir (o la resolución de) un sitio Web o servicio name tooits dirección IP.</span><span class="sxs-lookup"><span data-stu-id="dd857-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="dd857-106">DNS de Azure es un servicio de hospedaje para los dominios DNS, que permite resolver nombres mediante la infraestructura de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dd857-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="dd857-107">Mediante el hospedaje de los dominios en Azure, puede administrar su DNS los registros mediante Hola mismas credenciales, API, herramientas y facturación como los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd857-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Información general de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="dd857-109">Características</span><span class="sxs-lookup"><span data-stu-id="dd857-109">Features</span></span>

* <span data-ttu-id="dd857-110">**Fiabilidad y rendimiento**: los dominios DNS de DNS de Azure se hospedan en la red global de servidores de nombres DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd857-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="dd857-111">Utilizamos difusión por proximidad de red para que cada consulta DNS se responde por servidor DNS más cercano disponible de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd857-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="dd857-112">Esto ofrece un rendimiento rápido y alta disponibilidad para el dominio.</span><span class="sxs-lookup"><span data-stu-id="dd857-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="dd857-113">**Integración sin problemas** -servicio de DNS de Azure de hello puede ser usado toomanage registros DNS para los servicios de Azure y puede ser usado tooprovide DNS para los recursos externos, así.</span><span class="sxs-lookup"><span data-stu-id="dd857-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="dd857-114">DNS de Azure está integrado en hello portal de Azure y utiliza Hola mismas credenciales, facturación y contrato de soporte técnico como los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd857-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="dd857-115">**Seguridad** -Hola servicio DNS de Azure se basa en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd857-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="dd857-116">Como tal, se beneficia de características Resource Manager, como control de acceso basado en roles, registros de auditoría y bloqueo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd857-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="dd857-117">Los dominios y los registros se pueden administrar a través de hello portal de Azure, cmdlets de PowerShell de Azure y Hola CLI de Azure entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="dd857-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="dd857-118">Las aplicaciones que requieren la administración automática de DNS pueden integrar con el servicio de Hola a través de hello REST API y SDK.</span><span class="sxs-lookup"><span data-stu-id="dd857-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="dd857-119">DNS de Azure actualmente no admite la adquisición de nombres de dominio.</span><span class="sxs-lookup"><span data-stu-id="dd857-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="dd857-120">Si desea toopurchase dominios, deberá toouse un registrador de nombres de dominio de otro fabricante.</span><span class="sxs-lookup"><span data-stu-id="dd857-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="dd857-121">registrador de Hello suelen cobra una pequeña cuota anual.</span><span class="sxs-lookup"><span data-stu-id="dd857-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="dd857-122">dominios de Hello, a continuación, se pueden hospedar en DNS de Azure para la administración de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="dd857-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="dd857-123">Vea [delegar un tooAzure de dominio DNS](dns-domain-delegation.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="dd857-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="dd857-124">Precios</span><span class="sxs-lookup"><span data-stu-id="dd857-124">Pricing</span></span>

<span data-ttu-id="dd857-125">Facturación de DNS se basa en el número de Hola de las zonas DNS hospedadas en Azure y por número de Hola de las consultas DNS.</span><span class="sxs-lookup"><span data-stu-id="dd857-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="dd857-126">más sobre los precios visita toolearn [precios de Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="dd857-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="dd857-127">P+F</span><span class="sxs-lookup"><span data-stu-id="dd857-127">FAQ</span></span>

<span data-ttu-id="dd857-128">Para las preguntas más frecuentes acerca de DNS de Azure, vea hello [preguntas más frecuentes de Azure DNS](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="dd857-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd857-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd857-129">Next steps</span></span>

<span data-ttu-id="dd857-130">Visite [Información general sobre zonas y registros de DNS](dns-zones-records.md) para obtener más información sobre zonas y registros DNS.</span><span class="sxs-lookup"><span data-stu-id="dd857-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="dd857-131">Obtenga información acerca de cómo demasiado[crear una zona DNS](./dns-getstarted-create-dnszone-portal.md) en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd857-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="dd857-132">Obtener información sobre algunas de hello otra clave [capacidades de red](../networking/networking-overview.md) de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd857-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>


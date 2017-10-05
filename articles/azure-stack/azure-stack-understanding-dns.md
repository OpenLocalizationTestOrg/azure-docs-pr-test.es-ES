---
title: "Información acerca de DNS en Azure Stack | Microsoft Docs"
description: "Información acerca de las características y funcionalidades de DNS en Azure Stack"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: 2a19b435777ba848835dcd90a1ebb8a0cbcb0e9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="33ab7-103">Presentación de iDNS para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="33ab7-103">Introducing iDNS for Azure Stack</span></span>
================================

<span data-ttu-id="33ab7-104">iDNS es una característica de Azure Stack que permite resolver nombres DNS externos (por ejemplo, http://www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="33ab7-104">iDNS is a feature in Azure Stack that allows you to resolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="33ab7-105">También permite registrar los nombres de redes virtuales internas.</span><span class="sxs-lookup"><span data-stu-id="33ab7-105">It also allows you to register internal virtual network names.</span></span> <span data-ttu-id="33ab7-106">Al hacerlo, puede resolver las máquinas virtuales en la misma red virtual por nombre, en lugar de por dirección IP, sin tener que especificar entradas del servidor DNS personalizadas.</span><span class="sxs-lookup"><span data-stu-id="33ab7-106">By doing so, you can resolve VMs on the same virtual network by name rather than IP address, without having to provide custom DNS server entries.</span></span>

<span data-ttu-id="33ab7-107">Es algo con lo que siempre ha contado Azure, pero ahora también está disponible en Windows Server 2016 y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="33ab7-107">It’s something that’s always been there in Azure, but it's available in Windows Server 2016 and Azure Stack too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="33ab7-108">¿Para qué sirve iDNS?</span><span class="sxs-lookup"><span data-stu-id="33ab7-108">What does iDNS do?</span></span>
<span data-ttu-id="33ab7-109">Con iDNS en Azure Stack, dispone de las siguientes funcionalidades sin tener que especificar entradas del servidor DNS personalizadas.</span><span class="sxs-lookup"><span data-stu-id="33ab7-109">With iDNS in Azure Stack, you get the following capabilities, without having to specify custom DNS server entries.</span></span>

* <span data-ttu-id="33ab7-110">Servicios de resolución de nombres Compartir los servicios de resolución de nombres DNS compartidos para las cargas de trabajo del inquilino.</span><span class="sxs-lookup"><span data-stu-id="33ab7-110">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="33ab7-111">Servicio DNS autoritativo para la resolución de nombres y el registro DNS en la red virtual del inquilino.</span><span class="sxs-lookup"><span data-stu-id="33ab7-111">Authoritative DNS service for name resolution and DNS registration within the tenant virtual network.</span></span>
* <span data-ttu-id="33ab7-112">Servicio DNS recursivo para la resolución de los nombres de Internet de las máquinas virtuales de los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="33ab7-112">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="33ab7-113">Los inquilinos ya no se necesitan especificar entradas de DNS personalizadas para resolver nombres de Internet (por ejemplo, www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="33ab7-113">Tenants no longer need to specify custom DNS entries to resolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="33ab7-114">Si lo desea, puede traer su propio DNS y utilizar servidores DNS personalizados.</span><span class="sxs-lookup"><span data-stu-id="33ab7-114">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="33ab7-115">Pero si solo desea poder resolver nombres de DNS de Internet y conectarse a otras máquinas virtuales de la misma red virtual, aunque no especifique nada funcionará correctamente.</span><span class="sxs-lookup"><span data-stu-id="33ab7-115">But now, if you just want to be able to resolve Internet DNS names and be able to connect to other virtual machines in the same virtual network, you don’t need to specify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="33ab7-116">¿Qué es lo que iDNS no hace?</span><span class="sxs-lookup"><span data-stu-id="33ab7-116">What does iDNS not do?</span></span>
<span data-ttu-id="33ab7-117">Lo que iDNS no permite hacer es crear un registro DNS para un nombre que se pueda resolver desde fuera de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="33ab7-117">What iDNS does not allow you to do is create a DNS record for a name that can be resolved from outside the virtual network.</span></span>

<span data-ttu-id="33ab7-118">En Azure, tiene la opción de especificar una etiqueta de nombre DNS que se puede asociar con una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="33ab7-118">In Azure, you have the option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="33ab7-119">Puede elegir la etiqueta (prefijo), pero Azure elige el sufijo, que depende de la región en la que crea la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="33ab7-119">You can choose the label (prefix), but Azure chooses the suffix, which is based on the region in which you create the public IP address.</span></span>

![Captura de pantalla de etiqueta de nombre DNS](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="33ab7-121">En la imagen anterior, Azure creará un registro "A" en DNS para la etiqueta de nombre DNS especificada en la zona **westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="33ab7-121">In the image above, Azure will create an “A” record in DNS for the DNS name label specified under the zone **westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="33ab7-122">De forma conjunta, el prefijo y el sufijo constituyen un dominio nombre completo (FQDN) que se pueda resolver desde cualquier lugar de la red Internet pública.</span><span class="sxs-lookup"><span data-stu-id="33ab7-122">The prefix and the suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on the public Internet.</span></span>

<span data-ttu-id="33ab7-123">Azure Stack solo admite iDNS para el registro de nombres interno, por lo que no puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="33ab7-123">Azure Stack only supports iDNS for internal name registration, so it cannot do the following.</span></span>

* <span data-ttu-id="33ab7-124">Crear un registro DNS en una zona DNS hospedada existente (por ejemplo, local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="33ab7-124">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="33ab7-125">Crear una zona DNS (como Contoso.com).</span><span class="sxs-lookup"><span data-stu-id="33ab7-125">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="33ab7-126">Crear un registro en su propia zona DNS personalizada.</span><span class="sxs-lookup"><span data-stu-id="33ab7-126">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="33ab7-127">Admitir la compra de nombres de dominio.</span><span class="sxs-lookup"><span data-stu-id="33ab7-127">Support the purchase of domain names.</span></span>


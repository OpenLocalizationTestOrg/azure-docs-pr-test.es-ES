---
title: aaaUnderstanding DNS en la pila de Azure | Documentos de Microsoft
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
ms.openlocfilehash: f60128cf98af8e98ac2bc87172b54132ed06cd8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="481aa-103">Presentación de iDNS para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="481aa-103">Introducing iDNS for Azure Stack</span></span>
================================

<span data-ttu-id="481aa-104">IDN es una característica de pila de Azure que permite tooresolve de nombres DNS externos (por ejemplo, http://www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="481aa-104">iDNS is a feature in Azure Stack that allows you tooresolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="481aa-105">También permite nombres de red virtual interna tooregister.</span><span class="sxs-lookup"><span data-stu-id="481aa-105">It also allows you tooregister internal virtual network names.</span></span> <span data-ttu-id="481aa-106">Al hacerlo, puede resolver las máquinas virtuales en hello misma red virtual por nombre en lugar de IP de direcciones, sin necesidad de entradas de servidor DNS personalizadas tooprovide.</span><span class="sxs-lookup"><span data-stu-id="481aa-106">By doing so, you can resolve VMs on hello same virtual network by name rather than IP address, without having tooprovide custom DNS server entries.</span></span>

<span data-ttu-id="481aa-107">Es algo con lo que siempre ha contado Azure, pero ahora también está disponible en Windows Server 2016 y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="481aa-107">It’s something that’s always been there in Azure, but it's available in Windows Server 2016 and Azure Stack too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="481aa-108">¿Para qué sirve iDNS?</span><span class="sxs-lookup"><span data-stu-id="481aa-108">What does iDNS do?</span></span>
<span data-ttu-id="481aa-109">Con IDN en la pila de Azure, obtendrá Hola siguientes capacidades, sin necesidad de entradas de servidor DNS personalizadas toospecify.</span><span class="sxs-lookup"><span data-stu-id="481aa-109">With iDNS in Azure Stack, you get hello following capabilities, without having toospecify custom DNS server entries.</span></span>

* <span data-ttu-id="481aa-110">Servicios de resolución de nombres Compartir los servicios de resolución de nombres DNS compartidos para las cargas de trabajo del inquilino.</span><span class="sxs-lookup"><span data-stu-id="481aa-110">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="481aa-111">Servicio DNS autoritativo para la resolución de nombres y el registro DNS en la red virtual del inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="481aa-111">Authoritative DNS service for name resolution and DNS registration within hello tenant virtual network.</span></span>
* <span data-ttu-id="481aa-112">Servicio DNS recursivo para la resolución de los nombres de Internet de las máquinas virtuales de los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="481aa-112">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="481aa-113">Los inquilinos ya no necesitan toospecify DNS entradas tooresolve Internet nombres personalizados (por ejemplo, www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="481aa-113">Tenants no longer need toospecify custom DNS entries tooresolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="481aa-114">Si lo desea, puede traer su propio DNS y utilizar servidores DNS personalizados.</span><span class="sxs-lookup"><span data-stu-id="481aa-114">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="481aa-115">Pero ahora, si simplemente desea nombres de DNS de Internet pueda tooresolve toobe y ser capaz de tooconnect tooother máquinas virtuales Hola misma red virtual, no necesita toospecify nada y funcionarán correctamente.</span><span class="sxs-lookup"><span data-stu-id="481aa-115">But now, if you just want toobe able tooresolve Internet DNS names and be able tooconnect tooother virtual machines in hello same virtual network, you don’t need toospecify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="481aa-116">¿Qué es lo que iDNS no hace?</span><span class="sxs-lookup"><span data-stu-id="481aa-116">What does iDNS not do?</span></span>
<span data-ttu-id="481aa-117">Qué IDN no permite toodo es crear un registro DNS para un nombre que se pueda resolver desde la red virtual externa Hola.</span><span class="sxs-lookup"><span data-stu-id="481aa-117">What iDNS does not allow you toodo is create a DNS record for a name that can be resolved from outside hello virtual network.</span></span>

<span data-ttu-id="481aa-118">En Azure, tiene la opción de Hola de especificar una etiqueta de nombre DNS que se puede asociar con una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="481aa-118">In Azure, you have hello option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="481aa-119">Puede elegir la etiqueta de hello (prefijo), pero Azure elige sufijo hello, que se basa en la región de hello en el que crear la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="481aa-119">You can choose hello label (prefix), but Azure chooses hello suffix, which is based on hello region in which you create hello public IP address.</span></span>

![Captura de pantalla de etiqueta de nombre DNS](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="481aa-121">En la imagen anterior de hello, Azure creará un registro "A" en DNS para la etiqueta de nombre DNS de hello especificado en la zona de hello **westus.cloudapp.azure.com**. El sufijo hello y prefijo juntas componen un dominio nombre completo (FQDN) que se puede resolver desde cualquier lugar en Hola Internet pública.</span><span class="sxs-lookup"><span data-stu-id="481aa-121">In hello image above, Azure will create an “A” record in DNS for hello DNS name label specified under hello zone **westus.cloudapp.azure.com**. The prefix and hello suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on hello public Internet.</span></span>

<span data-ttu-id="481aa-122">Azure pila solo admite IDN para el registro de nombres interna, por lo que no es posible Hola después.</span><span class="sxs-lookup"><span data-stu-id="481aa-122">Azure Stack only supports iDNS for internal name registration, so it cannot do hello following.</span></span>

* <span data-ttu-id="481aa-123">Crear un registro DNS en una zona DNS hospedada existente (por ejemplo, local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="481aa-123">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="481aa-124">Crear una zona DNS (como Contoso.com).</span><span class="sxs-lookup"><span data-stu-id="481aa-124">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="481aa-125">Crear un registro en su propia zona DNS personalizada.</span><span class="sxs-lookup"><span data-stu-id="481aa-125">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="481aa-126">Admite la compra de Hola de nombres de dominio.</span><span class="sxs-lookup"><span data-stu-id="481aa-126">Support hello purchase of domain names.</span></span>


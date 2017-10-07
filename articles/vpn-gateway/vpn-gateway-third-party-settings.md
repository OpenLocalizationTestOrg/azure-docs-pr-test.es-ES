---
title: "Configuración del dispositivo de firewall o VPN de terceros sugerida por la comunidad para Azure VPN Gateway | Microsoft Docs"
description: "Obtenga información sobre la configuración del dispositivo de firewall o VPN de terceros sugerida por la comunidad para Azure VPN Gateway."
services: vpn-gateway
documentationcenter: 
author: chadmath
manager: cshepard
editor: 
tags: azure-vpn-gateway
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: delhan
ms.openlocfilehash: c695d23167ddba11283f6e223769e29b18a5c7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="community-suggested-third-party-vpn-or-firewall-device-settings-for-azure-vpn-gateway"></a><span data-ttu-id="dcf20-103">Configuración del dispositivo de firewall o VPN de terceros sugerida por la comunidad para Azure VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="dcf20-103">Community-suggested third-party VPN or firewall device settings for Azure VPN gateway</span></span>

<span data-ttu-id="dcf20-104">Este artículo proporciona varias soluciones sugeridas para dispositivos de firewall o VPN de terceros que se usan con Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="dcf20-104">This article provides several suggested solutions for third-party VPN or firewall devices that are used with Azure VPN gateway.</span></span>

> [!Note]
> <span data-ttu-id="dcf20-105">Proveedor del dispositivo Hola proporciona soporte técnico para los dispositivos VPN o firewall de terceros.</span><span class="sxs-lookup"><span data-stu-id="dcf20-105">Technical support for third-party VPN or firewall devices is provided by hello device vendor.</span></span> 

## <a name="more-information"></a><span data-ttu-id="dcf20-106">Más información</span><span class="sxs-lookup"><span data-stu-id="dcf20-106">More information</span></span>

<span data-ttu-id="dcf20-107">Hello en la tabla siguiente enumera varios dispositivos comunes y ayuda relacionado:</span><span class="sxs-lookup"><span data-stu-id="dcf20-107">hello following table lists several common devices and related help:</span></span>

|<span data-ttu-id="dcf20-108">Producto</span><span class="sxs-lookup"><span data-stu-id="dcf20-108">Product</span></span>    |<span data-ttu-id="dcf20-109">Referencia</span><span class="sxs-lookup"><span data-stu-id="dcf20-109">Reference</span></span>                                                |
|-----------|-----------------------------------------------------------|
|<span data-ttu-id="dcf20-110">Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="dcf20-110">Cisco ASA</span></span>  |[<span data-ttu-id="dcf20-111">Soluciones sugeridas por la comunidad para Cisco ASA en VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="dcf20-111">Community suggested solutions for Cisco ASA on Azure VPN</span></span>](https://search.cisco.com/search?query=%22Azure%20VPN%22%20ASA&locale=enUS&tab=Cisco)   |
|<span data-ttu-id="dcf20-112">Cisco ISR</span><span class="sxs-lookup"><span data-stu-id="dcf20-112">Cisco ISR</span></span>  |[<span data-ttu-id="dcf20-113">Soluciones sugeridas por la comunidad para Cisco ISR en VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="dcf20-113">Community suggested solutions for Cisco ISR on Azure VPN</span></span>](https://search.cisco.com/search?query=%22Azure%20VPN%22%20ISR&locale=enUS&tab=Cisco)   |
|<span data-ttu-id="dcf20-114">Cisco ASR</span><span class="sxs-lookup"><span data-stu-id="dcf20-114">Cisco ASR</span></span>  |[<span data-ttu-id="dcf20-115">Soluciones sugeridas por la comunidad para Cisco ASR en VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="dcf20-115">Community suggested solutions for Cisco ASR on Azure VPN</span></span>](https://search.cisco.com/search?query=%22Azure%20VPN%22%20ASR&locale=enUS&tab=Cisco)   |
|<span data-ttu-id="dcf20-116">Sonicwall</span><span class="sxs-lookup"><span data-stu-id="dcf20-116">Sonicwall</span></span> |<span data-ttu-id="dcf20-117">Busque **VPN de Azure** en el [sitio de Sonicwall](https://support.sonicwall.com/search)</span><span class="sxs-lookup"><span data-stu-id="dcf20-117">Search for **Azure VPN** on [Sonicwall site](https://support.sonicwall.com/search)</span></span> |
| <span data-ttu-id="dcf20-118">Punto de control</span><span class="sxs-lookup"><span data-stu-id="dcf20-118">Checkpoint</span></span>    |<span data-ttu-id="dcf20-119">Busque **VPN de Azure** en el [sitio de Checkpoint](https://supportcenter.checkpoint.com/supportcenter/portal)</span><span class="sxs-lookup"><span data-stu-id="dcf20-119">Search for **Azure VPN** on [Checkpoint site](https://supportcenter.checkpoint.com/supportcenter/portal)</span></span> |
|<span data-ttu-id="dcf20-120">Juniper</span><span class="sxs-lookup"><span data-stu-id="dcf20-120">Juniper</span></span> |<span data-ttu-id="dcf20-121">Busque **VPN de Azure** en el [sitio de Juniper]( http://www.juniper.net/search/public/)</span><span class="sxs-lookup"><span data-stu-id="dcf20-121">Search for **Azure VPN** on [Juniper site]( http://www.juniper.net/search/public/)</span></span>|
|<span data-ttu-id="dcf20-122">Barracuda</span><span class="sxs-lookup"><span data-stu-id="dcf20-122">Barracuda</span></span>  |[<span data-ttu-id="dcf20-123">Soluciones sugeridas por la comunidad para Barracuda en VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="dcf20-123">Community suggested solutions for Barracuda on Azure VPN</span></span>](https://campus.barracuda.com/search/?q=%22Azure+VPN%22&x=0&y=0)   |
|<span data-ttu-id="dcf20-124">F5</span><span class="sxs-lookup"><span data-stu-id="dcf20-124">F5</span></span>         |[<span data-ttu-id="dcf20-125">Soluciones sugeridas por la comunidad para F5 en VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="dcf20-125">Community suggested solutions for F5 on Azure VPN</span></span>](https://support.f5.com/csp/#/federated-search?q=%22Azure%20VPN%22&source=support)          |
|<span data-ttu-id="dcf20-126">Palo</span><span class="sxs-lookup"><span data-stu-id="dcf20-126">Palo</span></span>       |[<span data-ttu-id="dcf20-127">Soluciones sugeridas por la comunidad para Palo en VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="dcf20-127">Community suggested solutions for Palo on Azure VPN</span></span>](https://live.paloaltonetworks.com/t5/forums/searchpage/tab/message?q=Azure+VPN)        |
|<span data-ttu-id="dcf20-128">WatchGuard</span><span class="sxs-lookup"><span data-stu-id="dcf20-128">Watchguard</span></span> |[<span data-ttu-id="dcf20-129">Soluciones sugeridas por la comunidad para Watchguard en VPN de Azure</span><span class="sxs-lookup"><span data-stu-id="dcf20-129">Community suggested solutions for Watchguard on Azure VPN</span></span>](http://watchguardsupport.force.com/SupportSearch#q=Azure%20VPN&t=All&sort=relevancy)  |

## <a name="next-step"></a><span data-ttu-id="dcf20-130">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="dcf20-130">Next step</span></span>

[<span data-ttu-id="dcf20-131">Configuración de las puertas de enlace de Azure</span><span class="sxs-lookup"><span data-stu-id="dcf20-131">Azure Gateways settings</span></span>](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#a-nameipsecaipsecike-parameters)

[<span data-ttu-id="dcf20-132">Dispositivos compatibles conocidos</span><span class="sxs-lookup"><span data-stu-id="dcf20-132">Known compatible devices</span></span>](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#validated-vpn-devices)


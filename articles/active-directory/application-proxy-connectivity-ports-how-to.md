---
title: "puertos del firewall aaaHow tooopen Hola necesarios para una aplicación de Proxy de aplicación | Documentos de Microsoft"
description: "Averiguar qué tooopen puertos para toowork de Proxy de aplicación de Azure AD Hola correctamente"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="92266-103">¿Cómo tooopen Hola puertos de firewall necesarios para una aplicación de Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="92266-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="92266-104">toosee una lista completa de los puertos de hello necesario y la función de Hola de cada puerto, consulte la sección de requisitos previos de Hola de hello [documentación del Proxy de aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="92266-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="92266-105">Tenga en cuenta que el proxy de aplicación solo usa puertos de salida.</span><span class="sxs-lookup"><span data-stu-id="92266-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="92266-106">También puede comprobar si tiene todos los puertos abiertos de hello necesario abrir hello [herramienta de prueba de puertos de conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) desde la red local.</span><span class="sxs-lookup"><span data-stu-id="92266-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="92266-107">Cuanto mayor sea el número de marcas de verificación verdes, mayor será la resistencia.</span><span class="sxs-lookup"><span data-stu-id="92266-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="92266-108">Regiones de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="92266-108">App Proxy regions</span></span>

<span data-ttu-id="92266-109">Estamos trabajando en una forma toolet ya sabe cuáles de estas regiones necesita toobe verde para usted.</span><span class="sxs-lookup"><span data-stu-id="92266-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="92266-110">Por ahora, asegúrese de que todas ellas lo estén.</span><span class="sxs-lookup"><span data-stu-id="92266-110">For now, make sure they all are.</span></span> <span data-ttu-id="92266-111">También se necesita Centro de EE. UU., independientemente de en qué región se encuentre.</span><span class="sxs-lookup"><span data-stu-id="92266-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="92266-112">toomake seguro Hola herramienta proporciona Hola resultados correctos, no olvide:</span><span class="sxs-lookup"><span data-stu-id="92266-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="92266-113">Abra la herramienta de hello en un explorador desde servidor hello donde esté instalado Hola conector.</span><span class="sxs-lookup"><span data-stu-id="92266-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="92266-114">Asegúrese de que cualquier tooyour aplicable de firewalls o servidores proxy conector también son aplicado toothis página.</span><span class="sxs-lookup"><span data-stu-id="92266-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="92266-115">Esto puede hacerse en Internet Explorer, vaya demasiado**configuración**  - &gt; **opciones de Internet**  - &gt; **conexiones**  - &gt; **Configuración de Lan**.</span><span class="sxs-lookup"><span data-stu-id="92266-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="92266-116">En esta página, verá el campo Hola "Use a Proxy Server para su LAN".</span><span class="sxs-lookup"><span data-stu-id="92266-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="92266-117">Active esta casilla y coloca la dirección de proxy de hello en el campo de "Dirección" Hola.</span><span class="sxs-lookup"><span data-stu-id="92266-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92266-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="92266-118">Next steps</span></span>
[<span data-ttu-id="92266-119">Descripción de los conectores del Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="92266-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)

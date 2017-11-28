---
title: "Apertura de los puertos de firewall necesarios para una aplicación de proxy de aplicación | Microsoft Docs"
description: "Averigüe qué puertos se deben abrir para que el proxy de aplicación de Azure AD funcione correctamente"
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
ms.openlocfilehash: 8ecd6d7e666d362194126a4abba7a65f2c7b8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="2499d-103">Apertura de los puertos de firewall necesarios para una aplicación de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="2499d-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="2499d-104">Para ver una lista completa de los puertos necesarios y la función de cada uno, consulte la sección Requisitos previos de la [documentación del proxy de aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="2499d-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="2499d-105">Tenga en cuenta que el proxy de aplicación solo usa puertos de salida.</span><span class="sxs-lookup"><span data-stu-id="2499d-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="2499d-106">También puede comprobar si tiene todos los puertos necesarios abiertos abriendo la [herramienta de prueba de puertos de conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) desde la red local.</span><span class="sxs-lookup"><span data-stu-id="2499d-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="2499d-107">Cuanto mayor sea el número de marcas de verificación verdes, mayor será la resistencia.</span><span class="sxs-lookup"><span data-stu-id="2499d-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="2499d-108">Regiones de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="2499d-108">App Proxy regions</span></span>

<span data-ttu-id="2499d-109">Se está trabajando en una forma de hacerle saber cuál de estas regiones debe estar verde para su caso.</span><span class="sxs-lookup"><span data-stu-id="2499d-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="2499d-110">Por ahora, asegúrese de que todas ellas lo estén.</span><span class="sxs-lookup"><span data-stu-id="2499d-110">For now, make sure they all are.</span></span> <span data-ttu-id="2499d-111">También se necesita Centro de EE. UU., independientemente de en qué región se encuentre.</span><span class="sxs-lookup"><span data-stu-id="2499d-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="2499d-112">Para asegurarse de que la herramienta ofrezca los resultados correctos, debe:</span><span class="sxs-lookup"><span data-stu-id="2499d-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="2499d-113">Abrir la herramienta en un explorador desde el servidor donde esté instalado el conector.</span><span class="sxs-lookup"><span data-stu-id="2499d-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="2499d-114">Asegurarse de que los servidores proxy o firewalls aplicables a su conector también estén aplicados a esta página.</span><span class="sxs-lookup"><span data-stu-id="2499d-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="2499d-115">Para hacerlo en Internet Explorer, vaya a **Configuración** -&gt; **Opciones de Internet** -&gt; **Conexiones** -&gt; **Configuración de LAN**.</span><span class="sxs-lookup"><span data-stu-id="2499d-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="2499d-116">En esta página, verá el campo "Usar un servidor proxy para la LAN".</span><span class="sxs-lookup"><span data-stu-id="2499d-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="2499d-117">Active esta casilla y escriba la dirección del proxy en el campo "Dirección".</span><span class="sxs-lookup"><span data-stu-id="2499d-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2499d-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2499d-118">Next steps</span></span>
[<span data-ttu-id="2499d-119">Descripción de los conectores del Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2499d-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)

---
title: "Personalización de reglas de firewall de aplicaciones web en Azure Application Gateway (Azure Portal) | Microsoft Docs"
description: "En este artículo se proporciona información acerca de cómo personalizar reglas de firewall de aplicaciones web en Application Gateway con Azure Portal."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="01198-103">Personalización de reglas de firewall de aplicaciones web mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="01198-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="01198-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="01198-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="01198-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01198-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="01198-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="01198-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="01198-107">El firewall de aplicaciones web (WAF) de Azure Application Gateway proporciona protección a las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="01198-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="01198-108">Dicha protección la proporciona Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span><span class="sxs-lookup"><span data-stu-id="01198-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="01198-109">Algunas reglas pueden producir falsos positivos y bloquear el tráfico real.</span><span class="sxs-lookup"><span data-stu-id="01198-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="01198-110">Por este motivo, Application Gateway ofrece la posibilidad de personalizar reglas y grupos de reglas.</span><span class="sxs-lookup"><span data-stu-id="01198-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="01198-111">Para más información acerca de reglas y grupos de reglas específicos, consulte [Lista de reglas y grupos de reglas de CRS de firewall de aplicaciones web que se ofrecen](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="01198-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="01198-112">Si la puerta de enlace de aplicaciones no usa el nivel WAF, la opción para actualizar la puerta de enlace de aplicaciones al nivel WAF aparece en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="01198-112">If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.</span></span> 

![Habilitar WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="01198-114">Visualización de reglas y grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="01198-114">View rule groups and rules</span></span>

<span data-ttu-id="01198-115">**Para ver reglas y grupos de reglas**</span><span class="sxs-lookup"><span data-stu-id="01198-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="01198-116">Navegue hasta la puerta de enlace de aplicaciones y seleccione **Firewall de aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="01198-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="01198-117">Seleccione **Configuración de reglas avanzada**.</span><span class="sxs-lookup"><span data-stu-id="01198-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="01198-118">Esta vista muestra una tabla en la página de todos los grupos de reglas proporcionados con el conjunto de reglas elegido.</span><span class="sxs-lookup"><span data-stu-id="01198-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="01198-119">Todas las casillas de la regla están seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="01198-119">All of the rule's check boxes are selected.</span></span>

![Configurar reglas deshabilitadas][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="01198-121">Búsqueda de reglas para deshabilitar</span><span class="sxs-lookup"><span data-stu-id="01198-121">Search for rules to disable</span></span>

<span data-ttu-id="01198-122">La hoja **Web application firewall settings** (Configuración del firewall de aplicaciones web) ofrece la posibilidad de filtrar las reglas a través de una búsqueda de texto.</span><span class="sxs-lookup"><span data-stu-id="01198-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="01198-123">El resultado muestra solo las reglas y los grupos de reglas que contienen el texto que se ha buscado.</span><span class="sxs-lookup"><span data-stu-id="01198-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![Buscar reglas][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="01198-125">Deshabilitación de reglas y grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="01198-125">Disable rule groups and rules</span></span>

<span data-ttu-id="01198-126">Al deshabilitar reglas, se puede deshabilitar un grupo de reglas completo o reglas específicas de uno o más grupos de reglas.</span><span class="sxs-lookup"><span data-stu-id="01198-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="01198-127">**Para deshabilitar grupos de reglas o reglas concretas**</span><span class="sxs-lookup"><span data-stu-id="01198-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="01198-128">Busque las reglas o los grupos de reglas que desea deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="01198-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="01198-129">Desactive las casillas de las reglas que desea deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="01198-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="01198-130">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01198-130">Select **Save**.</span></span> 

![Guardar cambios][3]

## <a name="next-steps"></a><span data-ttu-id="01198-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01198-132">Next steps</span></span>

<span data-ttu-id="01198-133">Después de configurar las reglas deshabilitadas, puede aprender a ver los registros de WAFS.</span><span class="sxs-lookup"><span data-stu-id="01198-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="01198-134">Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="01198-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png

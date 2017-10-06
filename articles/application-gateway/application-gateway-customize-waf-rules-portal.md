---
title: "reglas de firewall de aplicación aaaCustomize web en la puerta de enlace de la aplicación de Azure: portal de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información sobre cómo las reglas firewall de aplicación web de toocustomize en la puerta de enlace de aplicaciones con hello portal de Azure."
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
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="b816f-103">Personalizar reglas de firewall de aplicación web a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b816f-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b816f-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b816f-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="b816f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b816f-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="b816f-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b816f-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="b816f-107">servidor de aplicaciones web de Hello puerta de enlace de aplicaciones de Azure (WAFS) proporciona protección para las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="b816f-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="b816f-108">Estas protecciones proceden de hello Abrir proyecto de seguridad aplicación de Web (OWASP) Core regla establecer (CR).</span><span class="sxs-lookup"><span data-stu-id="b816f-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="b816f-109">Algunas reglas pueden producir falsos positivos y bloquear el tráfico real.</span><span class="sxs-lookup"><span data-stu-id="b816f-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="b816f-110">Por esta razón, puerta de enlace de aplicaciones proporciona reglas y grupos de reglas de hello capacidad toocustomize.</span><span class="sxs-lookup"><span data-stu-id="b816f-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="b816f-111">Para obtener más información sobre los grupos de reglas específicos de Hola y reglas, consulte [lista de reglas y grupos de reglas de web application firewall CR](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="b816f-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="b816f-112">Si la puerta de enlace de la aplicación no está usando capa de hello WAFS, Hola opción tooupgrade Hola puerta de enlace toohello WAFS capa de aplicación aparece en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="b816f-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![Habilitar WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="b816f-114">Visualización de reglas y grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="b816f-114">View rule groups and rules</span></span>

<span data-ttu-id="b816f-115">**las reglas y grupos de reglas de tooview**</span><span class="sxs-lookup"><span data-stu-id="b816f-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="b816f-116">Vaya toohello puerta de enlace de aplicaciones y, a continuación, seleccione **firewall de aplicación Web**.</span><span class="sxs-lookup"><span data-stu-id="b816f-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="b816f-117">Seleccione **Configuración de reglas avanzada**.</span><span class="sxs-lookup"><span data-stu-id="b816f-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="b816f-118">Esta vista muestra una tabla en la página de Hola de todos los grupos de reglas de hello proporcionada con hello elegido el conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="b816f-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="b816f-119">Se seleccionan todos de casillas de verificación de la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b816f-119">All of hello rule's check boxes are selected.</span></span>

![Configurar reglas deshabilitadas][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="b816f-121">Buscar reglas toodisable</span><span class="sxs-lookup"><span data-stu-id="b816f-121">Search for rules toodisable</span></span>

<span data-ttu-id="b816f-122">Hola **configuración de firewall de aplicación Web** hoja proporciona capacidad de hello toofilter reglas de Hola a través de una búsqueda de texto.</span><span class="sxs-lookup"><span data-stu-id="b816f-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="b816f-123">resultado de Hello muestra solo los grupos de reglas de Hola y las reglas que contengan texto hello buscado.</span><span class="sxs-lookup"><span data-stu-id="b816f-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![Buscar reglas][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="b816f-125">Deshabilitación de reglas y grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="b816f-125">Disable rule groups and rules</span></span>

<span data-ttu-id="b816f-126">Al deshabilitar reglas, se puede deshabilitar un grupo de reglas completo o reglas específicas de uno o más grupos de reglas.</span><span class="sxs-lookup"><span data-stu-id="b816f-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="b816f-127">**grupos de reglas de toodisable o reglas específicas**</span><span class="sxs-lookup"><span data-stu-id="b816f-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="b816f-128">Buscar reglas de Hola o grupos de reglas que desea toodisable.</span><span class="sxs-lookup"><span data-stu-id="b816f-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="b816f-129">Desactive casillas de verificación de Hola para hello las reglas que desea toodisable.</span><span class="sxs-lookup"><span data-stu-id="b816f-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="b816f-130">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b816f-130">Select **Save**.</span></span> 

![Guardar cambios][3]

## <a name="next-steps"></a><span data-ttu-id="b816f-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b816f-132">Next steps</span></span>

<span data-ttu-id="b816f-133">Después de configurar las reglas deshabilitadas, aprenderá cómo tooview los registros WAFS.</span><span class="sxs-lookup"><span data-stu-id="b816f-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="b816f-134">Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="b816f-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png

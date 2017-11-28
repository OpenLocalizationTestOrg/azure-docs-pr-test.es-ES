---
title: direcciones de aaaIP usadas por Application Insights | Documentos de Microsoft
description: Excepciones para el firewall del servidor requeridas por Application Insights
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="71c6f-103">Direcciones IP que emplea Application Insights</span><span class="sxs-lookup"><span data-stu-id="71c6f-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="71c6f-104">Hola [Azure Application Insights](app-insights-overview.md) servicio utiliza un número de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="71c6f-104">hello [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="71c6f-105">Podría necesitar tooknow estas direcciones si se hospeda la aplicación hello que se está supervisando detrás de un firewall.</span><span class="sxs-lookup"><span data-stu-id="71c6f-105">You might need tooknow these addresses if hello app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="71c6f-106">Aunque estas direcciones son estáticas, es posible que necesitaremos toochange del tootime de tiempo.</span><span class="sxs-lookup"><span data-stu-id="71c6f-106">Although these addresses are static, it's possible that we will need toochange them from time tootime.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="71c6f-107">Puertos de salida</span><span class="sxs-lookup"><span data-stu-id="71c6f-107">Outgoing ports</span></span>
<span data-ttu-id="71c6f-108">Necesita tooopen algunos puertos de salida de hello tooallow de firewall del servidor Application Insights SDK o el portal de supervisión de estado toosend datos toohello:</span><span class="sxs-lookup"><span data-stu-id="71c6f-108">You need tooopen some outgoing ports in your server's firewall tooallow hello Application Insights SDK and/or Status Monitor toosend data toohello portal:</span></span>

| <span data-ttu-id="71c6f-109">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-109">Purpose</span></span> | <span data-ttu-id="71c6f-110">URL</span><span class="sxs-lookup"><span data-stu-id="71c6f-110">URL</span></span> | <span data-ttu-id="71c6f-111">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-111">IP</span></span> | <span data-ttu-id="71c6f-112">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-113">Telemetría</span><span class="sxs-lookup"><span data-stu-id="71c6f-113">Telemetry</span></span> |<span data-ttu-id="71c6f-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="71c6f-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="71c6f-116">40.114.241.141</span></span><br/><span data-ttu-id="71c6f-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="71c6f-117">104.45.136.42</span></span><br/><span data-ttu-id="71c6f-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="71c6f-118">40.84.189.107</span></span><br/><span data-ttu-id="71c6f-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="71c6f-119">168.63.242.221</span></span><br/><span data-ttu-id="71c6f-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="71c6f-120">52.167.221.184</span></span><br/><span data-ttu-id="71c6f-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="71c6f-121">52.169.64.244</span></span> |<span data-ttu-id="71c6f-122">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-122">443</span></span> |
| <span data-ttu-id="71c6f-123">Secuencia de métricas en directo</span><span class="sxs-lookup"><span data-stu-id="71c6f-123">Live Metrics Stream</span></span> |<span data-ttu-id="71c6f-124">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-125">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="71c6f-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="71c6f-126">23.96.28.38</span></span><br/><span data-ttu-id="71c6f-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="71c6f-127">13.92.40.198</span></span> |<span data-ttu-id="71c6f-128">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-128">443</span></span> |
| <span data-ttu-id="71c6f-129">Telemetría interna</span><span class="sxs-lookup"><span data-stu-id="71c6f-129">Internal Telemetry</span></span> |<span data-ttu-id="71c6f-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="71c6f-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="71c6f-131">52.161.11.71</span></span> |<span data-ttu-id="71c6f-132">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="71c6f-133">Monitor de estado</span><span class="sxs-lookup"><span data-stu-id="71c6f-133">Status Monitor</span></span>
<span data-ttu-id="71c6f-134">Configuración del Monitor de estado; solo lo necesitará en caso de que tenga que hacer cambios.</span><span class="sxs-lookup"><span data-stu-id="71c6f-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="71c6f-135">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-135">Purpose</span></span> | <span data-ttu-id="71c6f-136">URL</span><span class="sxs-lookup"><span data-stu-id="71c6f-136">URL</span></span> | <span data-ttu-id="71c6f-137">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-137">IP</span></span> | <span data-ttu-id="71c6f-138">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-139">Configuración</span><span class="sxs-lookup"><span data-stu-id="71c6f-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="71c6f-140">Configuración</span><span class="sxs-lookup"><span data-stu-id="71c6f-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="71c6f-141">Configuración</span><span class="sxs-lookup"><span data-stu-id="71c6f-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="71c6f-142">Configuración</span><span class="sxs-lookup"><span data-stu-id="71c6f-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="71c6f-143">Configuración</span><span class="sxs-lookup"><span data-stu-id="71c6f-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="71c6f-144">Configuración</span><span class="sxs-lookup"><span data-stu-id="71c6f-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="71c6f-145">Configuración</span><span class="sxs-lookup"><span data-stu-id="71c6f-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="71c6f-146">Instalación</span><span class="sxs-lookup"><span data-stu-id="71c6f-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="71c6f-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="71c6f-147">HockeyApp</span></span>
| <span data-ttu-id="71c6f-148">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-148">Purpose</span></span> | <span data-ttu-id="71c6f-149">URL</span><span class="sxs-lookup"><span data-stu-id="71c6f-149">URL</span></span> | <span data-ttu-id="71c6f-150">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-150">IP</span></span> | <span data-ttu-id="71c6f-151">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-152">Datos de bloqueo</span><span class="sxs-lookup"><span data-stu-id="71c6f-152">Crash data</span></span> |<span data-ttu-id="71c6f-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="71c6f-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="71c6f-154">104.45.136.42</span></span> |<span data-ttu-id="71c6f-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="71c6f-156">Pruebas de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="71c6f-156">Availability tests</span></span>
<span data-ttu-id="71c6f-157">Se trata Hola lista de direcciones desde el que [disponibilidad las pruebas web](app-insights-monitor-web-app-availability.md) se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="71c6f-157">This is hello list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="71c6f-158">Si desea toorun las pruebas web en la aplicación, pero el servidor web está restringido tooserving clientes específicos, tendrá que toopermit el tráfico entrante desde nuestros servidores de prueba de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="71c6f-158">If you want toorun web tests on your app, but your web server is restricted tooserving specific clients, then you will have toopermit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="71c6f-159">Abra los puertos 80 (http) y 443 (https) para asumir el tráfico entrante de estas direcciones (las IP se agrupan por ubicación):</span><span class="sxs-lookup"><span data-stu-id="71c6f-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="71c6f-160">API de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="71c6f-160">Data access API</span></span>
| <span data-ttu-id="71c6f-161">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-161">Purpose</span></span> | <span data-ttu-id="71c6f-162">URI</span><span class="sxs-lookup"><span data-stu-id="71c6f-162">URI</span></span> | <span data-ttu-id="71c6f-163">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-163">IP</span></span> | <span data-ttu-id="71c6f-164">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-165">API</span><span class="sxs-lookup"><span data-stu-id="71c6f-165">API</span></span> |<span data-ttu-id="71c6f-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="71c6f-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="71c6f-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="71c6f-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="71c6f-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="71c6f-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="71c6f-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="71c6f-172">13.82.26.252</span></span><br/><span data-ttu-id="71c6f-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="71c6f-173">40.76.213.73</span></span> |<span data-ttu-id="71c6f-174">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-174">80,443</span></span> |
| <span data-ttu-id="71c6f-175">Documentos de API</span><span class="sxs-lookup"><span data-stu-id="71c6f-175">API docs</span></span> |<span data-ttu-id="71c6f-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="71c6f-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="71c6f-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="71c6f-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="71c6f-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="71c6f-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="71c6f-182">13.82.24.149</span></span><br/><span data-ttu-id="71c6f-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="71c6f-183">40.114.82.10</span></span> |<span data-ttu-id="71c6f-184">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-184">80,443</span></span> |
| <span data-ttu-id="71c6f-185">API Interna</span><span class="sxs-lookup"><span data-stu-id="71c6f-185">Internal API</span></span> |<span data-ttu-id="71c6f-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="71c6f-193">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-193">dynamic</span></span>|<span data-ttu-id="71c6f-194">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="71c6f-195">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="71c6f-195">Application Insights Analytics</span></span>

| <span data-ttu-id="71c6f-196">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-196">Purpose</span></span> | <span data-ttu-id="71c6f-197">URI</span><span class="sxs-lookup"><span data-stu-id="71c6f-197">URI</span></span> | <span data-ttu-id="71c6f-198">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-198">IP</span></span> | <span data-ttu-id="71c6f-199">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-200">Portal de Analytics</span><span class="sxs-lookup"><span data-stu-id="71c6f-200">Analytics Portal</span></span> | <span data-ttu-id="71c6f-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="71c6f-202">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-202">dynamic</span></span> | <span data-ttu-id="71c6f-203">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-203">80,443</span></span> |
| <span data-ttu-id="71c6f-204">CDN</span><span class="sxs-lookup"><span data-stu-id="71c6f-204">CDN</span></span> | <span data-ttu-id="71c6f-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="71c6f-206">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-206">dynamic</span></span> | <span data-ttu-id="71c6f-207">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-207">80,443</span></span> |
| <span data-ttu-id="71c6f-208">Medios + CDN</span><span class="sxs-lookup"><span data-stu-id="71c6f-208">Media CDN</span></span> | <span data-ttu-id="71c6f-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="71c6f-210">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-210">dynamic</span></span> | <span data-ttu-id="71c6f-211">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-211">80,443</span></span> |

<span data-ttu-id="71c6f-212">Nota: el dominio *.applicationinsights.io es propiedad del equipo de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="71c6f-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="71c6f-213">Extensión de Application Insights de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="71c6f-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="71c6f-214">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-214">Purpose</span></span> | <span data-ttu-id="71c6f-215">URI</span><span class="sxs-lookup"><span data-stu-id="71c6f-215">URI</span></span> | <span data-ttu-id="71c6f-216">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-216">IP</span></span> | <span data-ttu-id="71c6f-217">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-218">Extensión de Application Insights</span><span class="sxs-lookup"><span data-stu-id="71c6f-218">Application Insights Extension</span></span> | <span data-ttu-id="71c6f-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="71c6f-220">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-220">dynamic</span></span> | <span data-ttu-id="71c6f-221">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-221">80,443</span></span> |
| <span data-ttu-id="71c6f-222">CDN de la extensión Application Insights</span><span class="sxs-lookup"><span data-stu-id="71c6f-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="71c6f-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="71c6f-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="71c6f-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="71c6f-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="71c6f-226">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-226">dynamic</span></span> | <span data-ttu-id="71c6f-227">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="71c6f-228">SDK de Application Insights</span><span class="sxs-lookup"><span data-stu-id="71c6f-228">Application Insights SDKs</span></span>

| <span data-ttu-id="71c6f-229">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-229">Purpose</span></span> | <span data-ttu-id="71c6f-230">URI</span><span class="sxs-lookup"><span data-stu-id="71c6f-230">URI</span></span> | <span data-ttu-id="71c6f-231">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-231">IP</span></span> | <span data-ttu-id="71c6f-232">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-233">CDN del SDK de JS de Application Insights</span><span class="sxs-lookup"><span data-stu-id="71c6f-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="71c6f-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="71c6f-235">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-235">dynamic</span></span> | <span data-ttu-id="71c6f-236">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-236">80,443</span></span> |
| <span data-ttu-id="71c6f-237">SDK de Java de Application Insights</span><span class="sxs-lookup"><span data-stu-id="71c6f-237">Application Insights Java SDK</span></span> | <span data-ttu-id="71c6f-238">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="71c6f-239">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-239">dynamic</span></span> | <span data-ttu-id="71c6f-240">80 443</span><span class="sxs-lookup"><span data-stu-id="71c6f-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="71c6f-241">Generador de perfiles</span><span class="sxs-lookup"><span data-stu-id="71c6f-241">Profiler</span></span>

| <span data-ttu-id="71c6f-242">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-242">Purpose</span></span> | <span data-ttu-id="71c6f-243">URI</span><span class="sxs-lookup"><span data-stu-id="71c6f-243">URI</span></span> | <span data-ttu-id="71c6f-244">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-244">IP</span></span> | <span data-ttu-id="71c6f-245">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-246">Agente</span><span class="sxs-lookup"><span data-stu-id="71c6f-246">Agent</span></span> | <span data-ttu-id="71c6f-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="71c6f-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="71c6f-249">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-249">dynamic</span></span> | <span data-ttu-id="71c6f-250">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-250">443</span></span>
| <span data-ttu-id="71c6f-251">Portal</span><span class="sxs-lookup"><span data-stu-id="71c6f-251">Portal</span></span> | <span data-ttu-id="71c6f-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="71c6f-253">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-253">dynamic</span></span> | <span data-ttu-id="71c6f-254">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-254">443</span></span>
| <span data-ttu-id="71c6f-255">Almacenamiento</span><span class="sxs-lookup"><span data-stu-id="71c6f-255">Storage</span></span> | <span data-ttu-id="71c6f-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-256">*.core.windows.net</span></span> | <span data-ttu-id="71c6f-257">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-257">dynamic</span></span> | <span data-ttu-id="71c6f-258">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="71c6f-259">Depurador de instantáneas</span><span class="sxs-lookup"><span data-stu-id="71c6f-259">Snapshot Debugger</span></span>

| <span data-ttu-id="71c6f-260">Propósito</span><span class="sxs-lookup"><span data-stu-id="71c6f-260">Purpose</span></span> | <span data-ttu-id="71c6f-261">URI</span><span class="sxs-lookup"><span data-stu-id="71c6f-261">URI</span></span> | <span data-ttu-id="71c6f-262">IP</span><span class="sxs-lookup"><span data-stu-id="71c6f-262">IP</span></span> | <span data-ttu-id="71c6f-263">Puertos</span><span class="sxs-lookup"><span data-stu-id="71c6f-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71c6f-264">Agente</span><span class="sxs-lookup"><span data-stu-id="71c6f-264">Agent</span></span> | <span data-ttu-id="71c6f-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="71c6f-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="71c6f-267">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-267">dynamic</span></span> | <span data-ttu-id="71c6f-268">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-268">443</span></span>
| <span data-ttu-id="71c6f-269">Portal</span><span class="sxs-lookup"><span data-stu-id="71c6f-269">Portal</span></span> | <span data-ttu-id="71c6f-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="71c6f-271">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-271">dynamic</span></span> | <span data-ttu-id="71c6f-272">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-272">443</span></span>
| <span data-ttu-id="71c6f-273">Almacenamiento</span><span class="sxs-lookup"><span data-stu-id="71c6f-273">Storage</span></span> | <span data-ttu-id="71c6f-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="71c6f-274">*.core.windows.net</span></span> | <span data-ttu-id="71c6f-275">dinámico</span><span class="sxs-lookup"><span data-stu-id="71c6f-275">dynamic</span></span> | <span data-ttu-id="71c6f-276">443</span><span class="sxs-lookup"><span data-stu-id="71c6f-276">443</span></span>

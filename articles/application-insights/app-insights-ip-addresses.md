---
title: Direcciones IP que emplea Application Insights | Microsoft Docs
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
ms.openlocfilehash: 3bb076c63223fc1567c6b7b25c1a513bbc81ed58
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="d1d05-103">Direcciones IP que emplea Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d05-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="d1d05-104">El servicio [Azure Application Insights](app-insights-overview.md) usa diversas direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="d1d05-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="d1d05-105">Quizás deba conocer estas direcciones si la aplicación que está supervisando se hospeda bajo el amparo de un firewall.</span><span class="sxs-lookup"><span data-stu-id="d1d05-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="d1d05-106">Aunque estas direcciones son estáticas, es posible que tengamos que cambiarlas de vez en cuando.</span><span class="sxs-lookup"><span data-stu-id="d1d05-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="d1d05-107">Puertos de salida</span><span class="sxs-lookup"><span data-stu-id="d1d05-107">Outgoing ports</span></span>
<span data-ttu-id="d1d05-108">Debe abrir algunos puertos de salida en el firewall del servidor para permitir que el SDK de Application Insights o el Monitor de estado envíe datos al portal:</span><span class="sxs-lookup"><span data-stu-id="d1d05-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="d1d05-109">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-109">Purpose</span></span> | <span data-ttu-id="d1d05-110">URL</span><span class="sxs-lookup"><span data-stu-id="d1d05-110">URL</span></span> | <span data-ttu-id="d1d05-111">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-111">IP</span></span> | <span data-ttu-id="d1d05-112">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-113">Telemetría</span><span class="sxs-lookup"><span data-stu-id="d1d05-113">Telemetry</span></span> |<span data-ttu-id="d1d05-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="d1d05-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="d1d05-116">40.114.241.141</span></span><br/><span data-ttu-id="d1d05-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="d1d05-117">104.45.136.42</span></span><br/><span data-ttu-id="d1d05-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="d1d05-118">40.84.189.107</span></span><br/><span data-ttu-id="d1d05-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="d1d05-119">168.63.242.221</span></span><br/><span data-ttu-id="d1d05-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="d1d05-120">52.167.221.184</span></span><br/><span data-ttu-id="d1d05-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="d1d05-121">52.169.64.244</span></span> |<span data-ttu-id="d1d05-122">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-122">443</span></span> |
| <span data-ttu-id="d1d05-123">Secuencia de métricas en directo</span><span class="sxs-lookup"><span data-stu-id="d1d05-123">Live Metrics Stream</span></span> |<span data-ttu-id="d1d05-124">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-125">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="d1d05-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="d1d05-126">23.96.28.38</span></span><br/><span data-ttu-id="d1d05-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="d1d05-127">13.92.40.198</span></span> |<span data-ttu-id="d1d05-128">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-128">443</span></span> |
| <span data-ttu-id="d1d05-129">Telemetría interna</span><span class="sxs-lookup"><span data-stu-id="d1d05-129">Internal Telemetry</span></span> |<span data-ttu-id="d1d05-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="d1d05-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="d1d05-131">52.161.11.71</span></span> |<span data-ttu-id="d1d05-132">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="d1d05-133">Monitor de estado</span><span class="sxs-lookup"><span data-stu-id="d1d05-133">Status Monitor</span></span>
<span data-ttu-id="d1d05-134">Configuración del Monitor de estado; solo lo necesitará en caso de que tenga que hacer cambios.</span><span class="sxs-lookup"><span data-stu-id="d1d05-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="d1d05-135">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-135">Purpose</span></span> | <span data-ttu-id="d1d05-136">URL</span><span class="sxs-lookup"><span data-stu-id="d1d05-136">URL</span></span> | <span data-ttu-id="d1d05-137">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-137">IP</span></span> | <span data-ttu-id="d1d05-138">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-139">Configuración</span><span class="sxs-lookup"><span data-stu-id="d1d05-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="d1d05-140">Configuración</span><span class="sxs-lookup"><span data-stu-id="d1d05-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="d1d05-141">Configuración</span><span class="sxs-lookup"><span data-stu-id="d1d05-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="d1d05-142">Configuración</span><span class="sxs-lookup"><span data-stu-id="d1d05-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="d1d05-143">Configuración</span><span class="sxs-lookup"><span data-stu-id="d1d05-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="d1d05-144">Configuración</span><span class="sxs-lookup"><span data-stu-id="d1d05-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="d1d05-145">Configuración</span><span class="sxs-lookup"><span data-stu-id="d1d05-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="d1d05-146">Instalación</span><span class="sxs-lookup"><span data-stu-id="d1d05-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="d1d05-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="d1d05-147">HockeyApp</span></span>
| <span data-ttu-id="d1d05-148">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-148">Purpose</span></span> | <span data-ttu-id="d1d05-149">URL</span><span class="sxs-lookup"><span data-stu-id="d1d05-149">URL</span></span> | <span data-ttu-id="d1d05-150">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-150">IP</span></span> | <span data-ttu-id="d1d05-151">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-152">Datos de bloqueo</span><span class="sxs-lookup"><span data-stu-id="d1d05-152">Crash data</span></span> |<span data-ttu-id="d1d05-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="d1d05-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="d1d05-154">104.45.136.42</span></span> |<span data-ttu-id="d1d05-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="d1d05-156">Pruebas de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="d1d05-156">Availability tests</span></span>
<span data-ttu-id="d1d05-157">Esta es la lista de direcciones a partir de las cuales se ejecutan [pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md) .</span><span class="sxs-lookup"><span data-stu-id="d1d05-157">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="d1d05-158">Si quiere ejecutar pruebas web en su aplicación, pero su servidor web está restringido atender únicamente las solicitudes de clientes específicos, tendrá que permitir el tráfico entrante de nuestros servidores de pruebas de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="d1d05-158">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="d1d05-159">Abra los puertos 80 (http) y 443 (https) para asumir el tráfico entrante de estas direcciones (las IP se agrupan por ubicación):</span><span class="sxs-lookup"><span data-stu-id="d1d05-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

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

## <a name="data-access-api"></a><span data-ttu-id="d1d05-160">API de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="d1d05-160">Data access API</span></span>
| <span data-ttu-id="d1d05-161">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-161">Purpose</span></span> | <span data-ttu-id="d1d05-162">URI</span><span class="sxs-lookup"><span data-stu-id="d1d05-162">URI</span></span> | <span data-ttu-id="d1d05-163">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-163">IP</span></span> | <span data-ttu-id="d1d05-164">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-165">API</span><span class="sxs-lookup"><span data-stu-id="d1d05-165">API</span></span> |<span data-ttu-id="d1d05-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="d1d05-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="d1d05-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="d1d05-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="d1d05-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="d1d05-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="d1d05-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="d1d05-172">13.82.26.252</span></span><br/><span data-ttu-id="d1d05-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="d1d05-173">40.76.213.73</span></span> |<span data-ttu-id="d1d05-174">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-174">80,443</span></span> |
| <span data-ttu-id="d1d05-175">Documentos de API</span><span class="sxs-lookup"><span data-stu-id="d1d05-175">API docs</span></span> |<span data-ttu-id="d1d05-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="d1d05-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="d1d05-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="d1d05-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="d1d05-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="d1d05-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="d1d05-182">13.82.24.149</span></span><br/><span data-ttu-id="d1d05-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="d1d05-183">40.114.82.10</span></span> |<span data-ttu-id="d1d05-184">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-184">80,443</span></span> |
| <span data-ttu-id="d1d05-185">API Interna</span><span class="sxs-lookup"><span data-stu-id="d1d05-185">Internal API</span></span> |<span data-ttu-id="d1d05-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="d1d05-193">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-193">dynamic</span></span>|<span data-ttu-id="d1d05-194">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="d1d05-195">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="d1d05-195">Application Insights Analytics</span></span>

| <span data-ttu-id="d1d05-196">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-196">Purpose</span></span> | <span data-ttu-id="d1d05-197">URI</span><span class="sxs-lookup"><span data-stu-id="d1d05-197">URI</span></span> | <span data-ttu-id="d1d05-198">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-198">IP</span></span> | <span data-ttu-id="d1d05-199">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-200">Portal de Analytics</span><span class="sxs-lookup"><span data-stu-id="d1d05-200">Analytics Portal</span></span> | <span data-ttu-id="d1d05-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="d1d05-202">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-202">dynamic</span></span> | <span data-ttu-id="d1d05-203">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-203">80,443</span></span> |
| <span data-ttu-id="d1d05-204">CDN</span><span class="sxs-lookup"><span data-stu-id="d1d05-204">CDN</span></span> | <span data-ttu-id="d1d05-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="d1d05-206">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-206">dynamic</span></span> | <span data-ttu-id="d1d05-207">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-207">80,443</span></span> |
| <span data-ttu-id="d1d05-208">Medios + CDN</span><span class="sxs-lookup"><span data-stu-id="d1d05-208">Media CDN</span></span> | <span data-ttu-id="d1d05-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="d1d05-210">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-210">dynamic</span></span> | <span data-ttu-id="d1d05-211">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-211">80,443</span></span> |

<span data-ttu-id="d1d05-212">Nota: el dominio *.applicationinsights.io es propiedad del equipo de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d1d05-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="d1d05-213">Extensión de Application Insights de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1d05-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="d1d05-214">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-214">Purpose</span></span> | <span data-ttu-id="d1d05-215">URI</span><span class="sxs-lookup"><span data-stu-id="d1d05-215">URI</span></span> | <span data-ttu-id="d1d05-216">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-216">IP</span></span> | <span data-ttu-id="d1d05-217">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-218">Extensión de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d05-218">Application Insights Extension</span></span> | <span data-ttu-id="d1d05-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="d1d05-220">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-220">dynamic</span></span> | <span data-ttu-id="d1d05-221">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-221">80,443</span></span> |
| <span data-ttu-id="d1d05-222">CDN de la extensión Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d05-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="d1d05-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d1d05-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d1d05-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d1d05-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="d1d05-226">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-226">dynamic</span></span> | <span data-ttu-id="d1d05-227">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="d1d05-228">SDK de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d05-228">Application Insights SDKs</span></span>

| <span data-ttu-id="d1d05-229">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-229">Purpose</span></span> | <span data-ttu-id="d1d05-230">URI</span><span class="sxs-lookup"><span data-stu-id="d1d05-230">URI</span></span> | <span data-ttu-id="d1d05-231">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-231">IP</span></span> | <span data-ttu-id="d1d05-232">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-233">CDN del SDK de JS de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d05-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="d1d05-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="d1d05-235">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-235">dynamic</span></span> | <span data-ttu-id="d1d05-236">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-236">80,443</span></span> |
| <span data-ttu-id="d1d05-237">SDK de Java de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d05-237">Application Insights Java SDK</span></span> | <span data-ttu-id="d1d05-238">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="d1d05-239">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-239">dynamic</span></span> | <span data-ttu-id="d1d05-240">80 443</span><span class="sxs-lookup"><span data-stu-id="d1d05-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="d1d05-241">Generador de perfiles</span><span class="sxs-lookup"><span data-stu-id="d1d05-241">Profiler</span></span>

| <span data-ttu-id="d1d05-242">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-242">Purpose</span></span> | <span data-ttu-id="d1d05-243">URI</span><span class="sxs-lookup"><span data-stu-id="d1d05-243">URI</span></span> | <span data-ttu-id="d1d05-244">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-244">IP</span></span> | <span data-ttu-id="d1d05-245">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-246">Agente</span><span class="sxs-lookup"><span data-stu-id="d1d05-246">Agent</span></span> | <span data-ttu-id="d1d05-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="d1d05-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="d1d05-249">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-249">dynamic</span></span> | <span data-ttu-id="d1d05-250">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-250">443</span></span>
| <span data-ttu-id="d1d05-251">Portal</span><span class="sxs-lookup"><span data-stu-id="d1d05-251">Portal</span></span> | <span data-ttu-id="d1d05-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="d1d05-253">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-253">dynamic</span></span> | <span data-ttu-id="d1d05-254">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-254">443</span></span>
| <span data-ttu-id="d1d05-255">Almacenamiento</span><span class="sxs-lookup"><span data-stu-id="d1d05-255">Storage</span></span> | <span data-ttu-id="d1d05-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-256">*.core.windows.net</span></span> | <span data-ttu-id="d1d05-257">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-257">dynamic</span></span> | <span data-ttu-id="d1d05-258">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="d1d05-259">Depurador de instantáneas</span><span class="sxs-lookup"><span data-stu-id="d1d05-259">Snapshot Debugger</span></span>

| <span data-ttu-id="d1d05-260">Propósito</span><span class="sxs-lookup"><span data-stu-id="d1d05-260">Purpose</span></span> | <span data-ttu-id="d1d05-261">URI</span><span class="sxs-lookup"><span data-stu-id="d1d05-261">URI</span></span> | <span data-ttu-id="d1d05-262">IP</span><span class="sxs-lookup"><span data-stu-id="d1d05-262">IP</span></span> | <span data-ttu-id="d1d05-263">Puertos</span><span class="sxs-lookup"><span data-stu-id="d1d05-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1d05-264">Agente</span><span class="sxs-lookup"><span data-stu-id="d1d05-264">Agent</span></span> | <span data-ttu-id="d1d05-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="d1d05-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="d1d05-267">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-267">dynamic</span></span> | <span data-ttu-id="d1d05-268">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-268">443</span></span>
| <span data-ttu-id="d1d05-269">Portal</span><span class="sxs-lookup"><span data-stu-id="d1d05-269">Portal</span></span> | <span data-ttu-id="d1d05-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="d1d05-271">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-271">dynamic</span></span> | <span data-ttu-id="d1d05-272">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-272">443</span></span>
| <span data-ttu-id="d1d05-273">Almacenamiento</span><span class="sxs-lookup"><span data-stu-id="d1d05-273">Storage</span></span> | <span data-ttu-id="d1d05-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d1d05-274">*.core.windows.net</span></span> | <span data-ttu-id="d1d05-275">dinámico</span><span class="sxs-lookup"><span data-stu-id="d1d05-275">dynamic</span></span> | <span data-ttu-id="d1d05-276">443</span><span class="sxs-lookup"><span data-stu-id="d1d05-276">443</span></span>

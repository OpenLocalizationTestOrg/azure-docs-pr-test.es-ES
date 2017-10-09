---
title: arquitectura de conectividad de base de datos de SQL aaaAzure | Documentos de Microsoft
description: Este documento explica Hola de arquitectura de conectividad SQLDB de Azure desde dentro de Azure o desde fuera de Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="7493e-103">Arquitectura de conectividad de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="7493e-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="7493e-104">En este artículo se explica la arquitectura de conectividad de base de datos de SQL Azure de Hola y explica el funcionan de los distintos componentes de hello toodirect instancia de tooyour de tráfico de la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7493e-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="7493e-105">Estos componentes de conectividad de base de datos de SQL Azure funcionen toohello de tráfico de red de toodirect base de datos de Azure con clientes que se conectan desde dentro de Azure y con clientes que se conectan desde fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="7493e-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="7493e-106">En este artículo también proporciona toochange de ejemplos de script cómo se produce la conectividad y consideraciones de hello relacionados con la configuración de conectividad de toochanging Hola predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7493e-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="7493e-107">Si le surge alguna pregunta después de leer este artículo, póngase en contacto con Dhruv en dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="7493e-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="7493e-108">Arquitectura de conectividad</span><span class="sxs-lookup"><span data-stu-id="7493e-108">Connectivity architecture</span></span>

<span data-ttu-id="7493e-109">Hola siguiente diagrama proporciona una descripción general de hello arquitectura de conectividad de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7493e-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="7493e-111">Hello pasos siguientes describen cómo es la conexión establecida tooan base de datos SQL de Azure a través de puerta de enlace de base de datos de SQL Azure de Hola y Hola base de datos de SQL Azure software equilibrador de carga (SLB).</span><span class="sxs-lookup"><span data-stu-id="7493e-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="7493e-112">Los clientes dentro de Azure o fuera de Azure conectan toohello SLB, que tiene una dirección IP pública y escucha en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="7493e-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="7493e-113">Hola SLB dirige la puerta de enlace de tráfico toohello base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7493e-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="7493e-114">puerta de enlace de Hello redirige Hola tráfico toohello correcta del proxy middleware.</span><span class="sxs-lookup"><span data-stu-id="7493e-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="7493e-115">Hola proxy middleware redirige Hola tráfico toohello SQL Azure base de datos correspondiente.</span><span class="sxs-lookup"><span data-stu-id="7493e-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7493e-116">Cada uno de estos componentes distribuye de denegación de protección de servicio (DDoS) integrado en la red de Hola y de capa de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="7493e-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="7493e-117">Conectividad desde dentro de Azure</span><span class="sxs-lookup"><span data-stu-id="7493e-117">Connectivity from within Azure</span></span>

<span data-ttu-id="7493e-118">Si va a conectarse desde dentro de Azure, las conexiones tienen una directiva de conexión predeterminada basada en el **redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="7493e-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="7493e-119">Una directiva de **redirigir** significa que las conexiones después de la sesión TCP hello es la base de datos de SQL Azure de toohello establecida, sesión de cliente de hello es, a continuación, redirige toohello middleware de proxy con una cambio toohello destino dirección IP virtual de de hello toothat de puerta de enlace de base de datos de SQL Azure de middleware de proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="7493e-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="7493e-120">Por lo tanto, todos los paquetes posteriores fluyen directamente a través de middleware de proxy de hello, omitiendo la puerta de enlace de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="7493e-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="7493e-121">Hola siguiente diagrama ilustra este flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="7493e-121">hello following diagram illustrates this traffic flow.</span></span>

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="7493e-123">Conectividad desde fuera de Azure</span><span class="sxs-lookup"><span data-stu-id="7493e-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="7493e-124">Si va a conectarse desde fuera de Azure, las conexiones tienen una directiva de conexión predeterminada basada en el **proxy**.</span><span class="sxs-lookup"><span data-stu-id="7493e-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="7493e-125">Una directiva de **Proxy** significa que la sesión TCP de Hola se establece a través de puerta de enlace de base de datos de SQL Azure hello y todos los paquetes posteriores fluyen a través de Hola puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7493e-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="7493e-126">Hola siguiente diagrama ilustra este flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="7493e-126">hello following diagram illustrates this traffic flow.</span></span>

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="7493e-128">Direcciones IP de la puerta de enlace de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="7493e-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="7493e-129">tooconnect tooan SQL Azure base de datos de recursos locales, deberá tooallow puerta de enlace de red saliente tráfico toohello base de datos de SQL Azure para su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="7493e-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="7493e-130">Las conexiones sólo se van a través de puerta de enlace de hello al conectarse en modo de Proxy, que es el predeterminado de hello cuando se conecta desde recursos locales.</span><span class="sxs-lookup"><span data-stu-id="7493e-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="7493e-131">Hola tabla siguiente se muestran Hola principal y secundaria de direcciones IP de puerta de enlace de base de datos de SQL Azure de Hola para todas las regiones de datos.</span><span class="sxs-lookup"><span data-stu-id="7493e-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="7493e-132">En algunas regiones, hay dos direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="7493e-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="7493e-133">En estas regiones, dirección IP principal de hello es Hola dirección IP de puerta de enlace de Hola y Hola segunda dirección IP es una dirección IP de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="7493e-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="7493e-134">dirección de conmutación por error de Hello es Hola dirección toowhich tengamos que pasamos la disponibilidad del servicio de servidor tookeep Hola alta.</span><span class="sxs-lookup"><span data-stu-id="7493e-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="7493e-135">Para estas regiones, se recomienda permitir saliente tooboth direcciones IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="7493e-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="7493e-136">dirección IP de la segunda Hello es propiedad de Microsoft y no escuchar todos los servicios hasta que se activa por las conexiones de base de datos de SQL Azure tooaccept.</span><span class="sxs-lookup"><span data-stu-id="7493e-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="7493e-137">Nombre de región</span><span class="sxs-lookup"><span data-stu-id="7493e-137">Region Name</span></span> | <span data-ttu-id="7493e-138">Dirección IP principal</span><span class="sxs-lookup"><span data-stu-id="7493e-138">Primary IP address</span></span> | <span data-ttu-id="7493e-139">Dirección IP secundaria</span><span class="sxs-lookup"><span data-stu-id="7493e-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="7493e-140">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="7493e-140">Australia East</span></span> | <span data-ttu-id="7493e-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="7493e-141">191.238.66.109</span></span> | <span data-ttu-id="7493e-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="7493e-142">13.75.149.87</span></span> |
| <span data-ttu-id="7493e-143">Sudeste de Australia</span><span class="sxs-lookup"><span data-stu-id="7493e-143">Australia South East</span></span> | <span data-ttu-id="7493e-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="7493e-144">191.239.192.109</span></span> | <span data-ttu-id="7493e-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="7493e-145">13.73.109.251</span></span> |
| <span data-ttu-id="7493e-146">Sur de Brasil</span><span class="sxs-lookup"><span data-stu-id="7493e-146">Brazil South</span></span> | <span data-ttu-id="7493e-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="7493e-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="7493e-148">Centro de Canadá</span><span class="sxs-lookup"><span data-stu-id="7493e-148">Canada Central</span></span> | <span data-ttu-id="7493e-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="7493e-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="7493e-150">Este de Canadá</span><span class="sxs-lookup"><span data-stu-id="7493e-150">Canada East</span></span> | <span data-ttu-id="7493e-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="7493e-151">40.86.226.166</span></span> | |
| <span data-ttu-id="7493e-152">Central EE. UU.:</span><span class="sxs-lookup"><span data-stu-id="7493e-152">Central US</span></span> | <span data-ttu-id="7493e-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="7493e-153">23.99.160.139</span></span> | <span data-ttu-id="7493e-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="7493e-154">13.67.215.62</span></span> |
| <span data-ttu-id="7493e-155">Asia oriental</span><span class="sxs-lookup"><span data-stu-id="7493e-155">East Asia</span></span> | <span data-ttu-id="7493e-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="7493e-156">191.234.2.139</span></span> | <span data-ttu-id="7493e-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="7493e-157">52.175.33.150</span></span> |
| <span data-ttu-id="7493e-158">Este de EE. UU. 1</span><span class="sxs-lookup"><span data-stu-id="7493e-158">East US 1</span></span> | <span data-ttu-id="7493e-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="7493e-159">191.238.6.43</span></span> | <span data-ttu-id="7493e-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="7493e-160">40.121.158.30</span></span> |
| <span data-ttu-id="7493e-161">Este de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="7493e-161">East US 2</span></span> | <span data-ttu-id="7493e-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="7493e-162">191.239.224.107</span></span> | <span data-ttu-id="7493e-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="7493e-163">40.79.84.180</span></span> |
| <span data-ttu-id="7493e-164">India central</span><span class="sxs-lookup"><span data-stu-id="7493e-164">India Central</span></span> | <span data-ttu-id="7493e-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="7493e-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="7493e-166">Sur de India</span><span class="sxs-lookup"><span data-stu-id="7493e-166">India South</span></span> | <span data-ttu-id="7493e-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="7493e-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="7493e-168">India occidental</span><span class="sxs-lookup"><span data-stu-id="7493e-168">India West</span></span> | <span data-ttu-id="7493e-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="7493e-169">104.211.160.80</span></span> | |
| <span data-ttu-id="7493e-170">Este de Japón</span><span class="sxs-lookup"><span data-stu-id="7493e-170">Japan East</span></span> | <span data-ttu-id="7493e-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="7493e-171">191.237.240.43</span></span> | <span data-ttu-id="7493e-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="7493e-172">13.78.61.196</span></span> |
| <span data-ttu-id="7493e-173">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="7493e-173">Japan West</span></span> | <span data-ttu-id="7493e-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="7493e-174">191.238.68.11</span></span> | <span data-ttu-id="7493e-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="7493e-175">104.214.148.156</span></span> |
| <span data-ttu-id="7493e-176">Corea Central</span><span class="sxs-lookup"><span data-stu-id="7493e-176">Korea Central</span></span> | <span data-ttu-id="7493e-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="7493e-177">52.231.32.42</span></span> | |
| <span data-ttu-id="7493e-178">Corea del Sur</span><span class="sxs-lookup"><span data-stu-id="7493e-178">Korea South</span></span> | <span data-ttu-id="7493e-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="7493e-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="7493e-180">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="7493e-180">North Central US</span></span> | <span data-ttu-id="7493e-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="7493e-181">23.98.55.75</span></span> | <span data-ttu-id="7493e-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="7493e-182">23.96.178.199</span></span> |
| <span data-ttu-id="7493e-183">Europa del Norte</span><span class="sxs-lookup"><span data-stu-id="7493e-183">North Europe</span></span> | <span data-ttu-id="7493e-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="7493e-184">191.235.193.75</span></span> | <span data-ttu-id="7493e-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="7493e-185">40.113.93.91</span></span> |
| <span data-ttu-id="7493e-186">Centro-Sur de EE. UU</span><span class="sxs-lookup"><span data-stu-id="7493e-186">South Central US</span></span> | <span data-ttu-id="7493e-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="7493e-187">23.98.162.75</span></span> | <span data-ttu-id="7493e-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="7493e-188">13.66.62.124</span></span> |
| <span data-ttu-id="7493e-189">Sudeste de Asia</span><span class="sxs-lookup"><span data-stu-id="7493e-189">South East Asia</span></span> | <span data-ttu-id="7493e-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="7493e-190">23.100.117.95</span></span> | <span data-ttu-id="7493e-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="7493e-191">104.43.15.0</span></span> |
| <span data-ttu-id="7493e-192">Norte del Reino Unido</span><span class="sxs-lookup"><span data-stu-id="7493e-192">UK North</span></span> | <span data-ttu-id="7493e-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="7493e-193">13.87.97.210</span></span> | |
| <span data-ttu-id="7493e-194">Sur de Reino Unido 1</span><span class="sxs-lookup"><span data-stu-id="7493e-194">UK South 1</span></span> | <span data-ttu-id="7493e-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="7493e-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="7493e-196">Sur del Reino Unido 2</span><span class="sxs-lookup"><span data-stu-id="7493e-196">UK South 2</span></span> | <span data-ttu-id="7493e-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="7493e-197">13.87.34.7</span></span> | |
| <span data-ttu-id="7493e-198">Oeste de Reino Unido</span><span class="sxs-lookup"><span data-stu-id="7493e-198">UK West</span></span> | <span data-ttu-id="7493e-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="7493e-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="7493e-200">Centro occidental de EE.UU.</span><span class="sxs-lookup"><span data-stu-id="7493e-200">West Central US</span></span> | <span data-ttu-id="7493e-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="7493e-201">13.78.145.25</span></span> | |
| <span data-ttu-id="7493e-202">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="7493e-202">West Europe</span></span> | <span data-ttu-id="7493e-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="7493e-203">191.237.232.75</span></span> | <span data-ttu-id="7493e-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="7493e-204">40.68.37.158</span></span> |
| <span data-ttu-id="7493e-205">Oeste de EE. UU. 1</span><span class="sxs-lookup"><span data-stu-id="7493e-205">West US 1</span></span> | <span data-ttu-id="7493e-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="7493e-206">23.99.34.75</span></span> | <span data-ttu-id="7493e-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="7493e-207">104.42.238.205</span></span> |
| <span data-ttu-id="7493e-208">Oeste de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="7493e-208">West US 2</span></span> | <span data-ttu-id="7493e-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="7493e-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="7493e-210">Cambio de la directiva de conexión de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="7493e-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="7493e-211">Hola toochange directiva de conexión de base de datos de SQL Azure para un servidor de base de datos de SQL Azure, use hello [API de REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="7493e-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="7493e-212">Si la directiva de conexión se establece demasiado**Proxy**, todo el flujo de paquetes a través de puerta de enlace de base de datos de SQL Azure Hola de red.</span><span class="sxs-lookup"><span data-stu-id="7493e-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="7493e-213">Para esta configuración, debe IP de puerta de enlace de tooallow tooonly saliente Hola base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7493e-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="7493e-214">El uso de la configuración de **proxy** ofrece más latencia que la de **redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="7493e-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="7493e-215">Si está configurando la directiva de conexión **redirigir**, todos los paquetes de red directamente fluyen toohello middleware proxy.</span><span class="sxs-lookup"><span data-stu-id="7493e-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="7493e-216">Para esta configuración, debe tooallow saliente toomultiple direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="7493e-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="7493e-217">Configuración de conexión de script toochange</span><span class="sxs-lookup"><span data-stu-id="7493e-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7493e-218">Este script requiere hello [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="7493e-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="7493e-219">Hola siguiente script de PowerShell muestra cómo toochange Hola directiva de conexión.</span><span class="sxs-lookup"><span data-stu-id="7493e-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="7493e-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7493e-220">Next steps</span></span>

- <span data-ttu-id="7493e-221">Para obtener información sobre cómo toochange Hola directiva de conexión de base de datos de SQL Azure para un servidor de base de datos de SQL Azure, consulte [Create o directiva de conexión del servidor de actualización utilizando Hola API de REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="7493e-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="7493e-222">Para obtener información sobre el comportamiento de conexión de Azure SQL Database para clientes que usan ADO.NET 4.5 o una versión posterior, vea [Puertos más allá de 1433 para ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="7493e-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="7493e-223">Para obtener información general sobre el desarrollo de aplicaciones, vea [Introducción al desarrollo de aplicaciones en SQL Database](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7493e-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>

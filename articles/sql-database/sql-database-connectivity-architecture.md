---
title: Arquitectura de conectividad de Azure SQL Database | Microsoft Docs
description: En este documento se explica la arquitectura de conectividad de Azure SQLDB, desde dentro o desde fuera de Azure.
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
ms.openlocfilehash: 8a1dd89c9e82483184ceb5d767190a5a5044265d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="8e12d-103">Arquitectura de conectividad de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="8e12d-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="8e12d-104">En este artículo se explica la arquitectura de conectividad de Azure SQL Database y cómo funcionan los distintos componentes para dirigir el tráfico a una instancia de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8e12d-104">This article explains the Azure SQL Database connectivity architecture and explains how the different components function to direct traffic to your instance of Azure SQL Database.</span></span> <span data-ttu-id="8e12d-105">La funcionalidad de estos componentes de la conectividad de Azure SQL Database consiste en dirigir el tráfico de red a la base de datos de Azure con clientes que se conectan desde dentro y desde fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e12d-105">These Azure SQL Database connectivity components function to direct network traffic to the Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="8e12d-106">En este artículo también se proporcionan ejemplos de script para cambiar cómo se establece la conectividad y, además, se incluyen consideraciones sobre la modificación de la configuración predeterminada de la conectividad.</span><span class="sxs-lookup"><span data-stu-id="8e12d-106">This article also provides script samples to change how connectivity occurs, and the considerations related to changing the default connectivity settings.</span></span> <span data-ttu-id="8e12d-107">Si le surge alguna pregunta después de leer este artículo, póngase en contacto con Dhruv en dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="8e12d-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="8e12d-108">Arquitectura de conectividad</span><span class="sxs-lookup"><span data-stu-id="8e12d-108">Connectivity architecture</span></span>

<span data-ttu-id="8e12d-109">En el siguiente diagrama se proporciona una descripción general de la arquitectura de conectividad de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8e12d-109">The following diagram provides a high-level overview of the Azure SQL Database connectivity architecture.</span></span> 

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="8e12d-111">En los pasos siguientes se describe cómo se establece una conexión a una base de datos SQL de Azure a través del equilibrador de carga de software (SLB) de Azure SQL Database y de la puerta de enlace de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8e12d-111">The following steps describe how a connection is established to an Azure SQL database through the Azure SQL Database software load-balancer (SLB) and the Azure SQL Database gateway.</span></span>

- <span data-ttu-id="8e12d-112">Los clientes, tanto desde dentro como desde fuera de Azure, se conectan a la SLB, que tiene una dirección IP pública y escucha en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="8e12d-112">Clients within Azure or outside of Azure connect to the SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="8e12d-113">El SLB dirige el tráfico a la puerta de enlace de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8e12d-113">The SLB directs traffic to the Azure SQL Database gateway.</span></span>
- <span data-ttu-id="8e12d-114">La puerta de enlace redirige el tráfico al middleware del proxy correcto.</span><span class="sxs-lookup"><span data-stu-id="8e12d-114">The gateway redirects the traffic to the correct proxy middleware.</span></span>
- <span data-ttu-id="8e12d-115">El middleware del proxy redirige el tráfico a la base de datos SQL de Azure adecuada.</span><span class="sxs-lookup"><span data-stu-id="8e12d-115">The proxy middleware redirects the traffic to the appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e12d-116">Cada uno de estos componentes integra protección frente a ataques de denegación de servicio distribuido (DDoS) en la red y en el nivel de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e12d-116">Each of these components has distributed denial of service (DDoS) protection built-in at the network and the app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="8e12d-117">Conectividad desde dentro de Azure</span><span class="sxs-lookup"><span data-stu-id="8e12d-117">Connectivity from within Azure</span></span>

<span data-ttu-id="8e12d-118">Si va a conectarse desde dentro de Azure, las conexiones tienen una directiva de conexión predeterminada basada en el **redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="8e12d-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="8e12d-119">Una directiva de **redireccionamiento** establece que las conexiones después de la sesión TCP se realicen a la base de datos SQL de Azure; a continuación, la sesión del cliente se redirige al middleware del proxy, pero se cambia la IP virtual de destino de la puerta de enlace de Azure SQL Database por la del middleware del proxy.</span><span class="sxs-lookup"><span data-stu-id="8e12d-119">A policy of **Redirect** means that connections after the TCP session is established to the Azure SQL database, the client session is then redirected to the proxy middleware with a change to the destination virtual IP from that of the Azure SQL Database gateway to that of the proxy middleware.</span></span> <span data-ttu-id="8e12d-120">Por lo tanto, todos los paquetes posteriores fluyen directamente a través del middleware del proxy, de tal forma que omiten la puerta de enlace de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8e12d-120">Thereafter, all subsequent packets flow directly via the proxy middleware, bypassing the Azure SQL Database gateway.</span></span> <span data-ttu-id="8e12d-121">En el siguiente diagrama, se ilustra este flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="8e12d-121">The following diagram illustrates this traffic flow.</span></span>

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="8e12d-123">Conectividad desde fuera de Azure</span><span class="sxs-lookup"><span data-stu-id="8e12d-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="8e12d-124">Si va a conectarse desde fuera de Azure, las conexiones tienen una directiva de conexión predeterminada basada en el **proxy**.</span><span class="sxs-lookup"><span data-stu-id="8e12d-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="8e12d-125">Una directiva de **proxy** establece que la sesión TCP se realice a través de la puerta de enlace de Azure SQL Database y que todos los paquetes posteriores fluyan a través de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8e12d-125">A policy of **Proxy** means that the TCP session is established via the Azure SQL Database gateway and all subsequent packets flow via the gateway.</span></span> <span data-ttu-id="8e12d-126">En el siguiente diagrama, se ilustra este flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="8e12d-126">The following diagram illustrates this traffic flow.</span></span>

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="8e12d-128">Direcciones IP de la puerta de enlace de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="8e12d-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="8e12d-129">Para conectarse a una base de datos SQL de Azure desde recursos locales, debe permitir el tráfico de red saliente a la puerta de enlace de Azure SQL Database en su región de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e12d-129">To connect to an Azure SQL database from on-premises resources, you need to allow outbound network traffic to the Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="8e12d-130">Las conexiones solo se establecen a través de la puerta de enlace al conectarse en modo de proxy, que es el valor predeterminado para conexiones desde recursos locales.</span><span class="sxs-lookup"><span data-stu-id="8e12d-130">Your connections only go via the gateway when connecting in Proxy mode, which is the default when connecting from on-premises resources.</span></span>

<span data-ttu-id="8e12d-131">En la tabla siguiente se enumeran las direcciones IP principales y secundarias de la puerta de enlace de Azure SQL Database para todas las regiones de datos.</span><span class="sxs-lookup"><span data-stu-id="8e12d-131">The following table lists the primary and secondary IPs of the Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="8e12d-132">En algunas regiones, hay dos direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="8e12d-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="8e12d-133">En estas regiones, la dirección IP principal es la dirección IP actual de la puerta de enlace y la dirección IP secundaria es una dirección IP de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="8e12d-133">In these regions, the primary IP address is the current IP address of the gateway and the second IP address is a failover IP address.</span></span> <span data-ttu-id="8e12d-134">La dirección de conmutación por error es la dirección a la que se puede mover el servidor para mantener la alta disponibilidad del servicio.</span><span class="sxs-lookup"><span data-stu-id="8e12d-134">The failover address is the address to which we might move your server to keep the service availability high.</span></span> <span data-ttu-id="8e12d-135">En estas regiones, se recomienda que permita el tráfico saliente a ambas direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="8e12d-135">For these regions, we recommend that you allow outbound to both the IP addresses.</span></span> <span data-ttu-id="8e12d-136">La dirección IP secundaria es propiedad de Microsoft y no escucha en ningún servicio hasta que Azure SQL Database la activa para aceptar conexiones.</span><span class="sxs-lookup"><span data-stu-id="8e12d-136">The second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database to accept connections.</span></span>

| <span data-ttu-id="8e12d-137">Nombre de región</span><span class="sxs-lookup"><span data-stu-id="8e12d-137">Region Name</span></span> | <span data-ttu-id="8e12d-138">Dirección IP principal</span><span class="sxs-lookup"><span data-stu-id="8e12d-138">Primary IP address</span></span> | <span data-ttu-id="8e12d-139">Dirección IP secundaria</span><span class="sxs-lookup"><span data-stu-id="8e12d-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="8e12d-140">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="8e12d-140">Australia East</span></span> | <span data-ttu-id="8e12d-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="8e12d-141">191.238.66.109</span></span> | <span data-ttu-id="8e12d-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="8e12d-142">13.75.149.87</span></span> |
| <span data-ttu-id="8e12d-143">Sudeste de Australia</span><span class="sxs-lookup"><span data-stu-id="8e12d-143">Australia South East</span></span> | <span data-ttu-id="8e12d-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="8e12d-144">191.239.192.109</span></span> | <span data-ttu-id="8e12d-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="8e12d-145">13.73.109.251</span></span> |
| <span data-ttu-id="8e12d-146">Sur de Brasil</span><span class="sxs-lookup"><span data-stu-id="8e12d-146">Brazil South</span></span> | <span data-ttu-id="8e12d-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="8e12d-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="8e12d-148">Centro de Canadá</span><span class="sxs-lookup"><span data-stu-id="8e12d-148">Canada Central</span></span> | <span data-ttu-id="8e12d-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="8e12d-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="8e12d-150">Este de Canadá</span><span class="sxs-lookup"><span data-stu-id="8e12d-150">Canada East</span></span> | <span data-ttu-id="8e12d-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="8e12d-151">40.86.226.166</span></span> | |
| <span data-ttu-id="8e12d-152">Central EE. UU.:</span><span class="sxs-lookup"><span data-stu-id="8e12d-152">Central US</span></span> | <span data-ttu-id="8e12d-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="8e12d-153">23.99.160.139</span></span> | <span data-ttu-id="8e12d-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="8e12d-154">13.67.215.62</span></span> |
| <span data-ttu-id="8e12d-155">Asia oriental</span><span class="sxs-lookup"><span data-stu-id="8e12d-155">East Asia</span></span> | <span data-ttu-id="8e12d-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="8e12d-156">191.234.2.139</span></span> | <span data-ttu-id="8e12d-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="8e12d-157">52.175.33.150</span></span> |
| <span data-ttu-id="8e12d-158">Este de EE. UU. 1</span><span class="sxs-lookup"><span data-stu-id="8e12d-158">East US 1</span></span> | <span data-ttu-id="8e12d-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="8e12d-159">191.238.6.43</span></span> | <span data-ttu-id="8e12d-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="8e12d-160">40.121.158.30</span></span> |
| <span data-ttu-id="8e12d-161">Este de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="8e12d-161">East US 2</span></span> | <span data-ttu-id="8e12d-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="8e12d-162">191.239.224.107</span></span> | <span data-ttu-id="8e12d-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="8e12d-163">40.79.84.180</span></span> |
| <span data-ttu-id="8e12d-164">India central</span><span class="sxs-lookup"><span data-stu-id="8e12d-164">India Central</span></span> | <span data-ttu-id="8e12d-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="8e12d-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="8e12d-166">Sur de India</span><span class="sxs-lookup"><span data-stu-id="8e12d-166">India South</span></span> | <span data-ttu-id="8e12d-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="8e12d-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="8e12d-168">India occidental</span><span class="sxs-lookup"><span data-stu-id="8e12d-168">India West</span></span> | <span data-ttu-id="8e12d-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="8e12d-169">104.211.160.80</span></span> | |
| <span data-ttu-id="8e12d-170">Este de Japón</span><span class="sxs-lookup"><span data-stu-id="8e12d-170">Japan East</span></span> | <span data-ttu-id="8e12d-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="8e12d-171">191.237.240.43</span></span> | <span data-ttu-id="8e12d-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="8e12d-172">13.78.61.196</span></span> |
| <span data-ttu-id="8e12d-173">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="8e12d-173">Japan West</span></span> | <span data-ttu-id="8e12d-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="8e12d-174">191.238.68.11</span></span> | <span data-ttu-id="8e12d-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="8e12d-175">104.214.148.156</span></span> |
| <span data-ttu-id="8e12d-176">Corea Central</span><span class="sxs-lookup"><span data-stu-id="8e12d-176">Korea Central</span></span> | <span data-ttu-id="8e12d-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="8e12d-177">52.231.32.42</span></span> | |
| <span data-ttu-id="8e12d-178">Corea del Sur</span><span class="sxs-lookup"><span data-stu-id="8e12d-178">Korea South</span></span> | <span data-ttu-id="8e12d-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="8e12d-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="8e12d-180">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="8e12d-180">North Central US</span></span> | <span data-ttu-id="8e12d-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="8e12d-181">23.98.55.75</span></span> | <span data-ttu-id="8e12d-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="8e12d-182">23.96.178.199</span></span> |
| <span data-ttu-id="8e12d-183">Europa del Norte</span><span class="sxs-lookup"><span data-stu-id="8e12d-183">North Europe</span></span> | <span data-ttu-id="8e12d-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="8e12d-184">191.235.193.75</span></span> | <span data-ttu-id="8e12d-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="8e12d-185">40.113.93.91</span></span> |
| <span data-ttu-id="8e12d-186">Centro-Sur de EE. UU</span><span class="sxs-lookup"><span data-stu-id="8e12d-186">South Central US</span></span> | <span data-ttu-id="8e12d-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="8e12d-187">23.98.162.75</span></span> | <span data-ttu-id="8e12d-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="8e12d-188">13.66.62.124</span></span> |
| <span data-ttu-id="8e12d-189">Sudeste de Asia</span><span class="sxs-lookup"><span data-stu-id="8e12d-189">South East Asia</span></span> | <span data-ttu-id="8e12d-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="8e12d-190">23.100.117.95</span></span> | <span data-ttu-id="8e12d-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="8e12d-191">104.43.15.0</span></span> |
| <span data-ttu-id="8e12d-192">Norte del Reino Unido</span><span class="sxs-lookup"><span data-stu-id="8e12d-192">UK North</span></span> | <span data-ttu-id="8e12d-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="8e12d-193">13.87.97.210</span></span> | |
| <span data-ttu-id="8e12d-194">Sur de Reino Unido 1</span><span class="sxs-lookup"><span data-stu-id="8e12d-194">UK South 1</span></span> | <span data-ttu-id="8e12d-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="8e12d-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="8e12d-196">Sur del Reino Unido 2</span><span class="sxs-lookup"><span data-stu-id="8e12d-196">UK South 2</span></span> | <span data-ttu-id="8e12d-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="8e12d-197">13.87.34.7</span></span> | |
| <span data-ttu-id="8e12d-198">Oeste de Reino Unido</span><span class="sxs-lookup"><span data-stu-id="8e12d-198">UK West</span></span> | <span data-ttu-id="8e12d-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="8e12d-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="8e12d-200">Centro occidental de EE.UU.</span><span class="sxs-lookup"><span data-stu-id="8e12d-200">West Central US</span></span> | <span data-ttu-id="8e12d-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="8e12d-201">13.78.145.25</span></span> | |
| <span data-ttu-id="8e12d-202">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="8e12d-202">West Europe</span></span> | <span data-ttu-id="8e12d-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="8e12d-203">191.237.232.75</span></span> | <span data-ttu-id="8e12d-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="8e12d-204">40.68.37.158</span></span> |
| <span data-ttu-id="8e12d-205">Oeste de EE. UU. 1</span><span class="sxs-lookup"><span data-stu-id="8e12d-205">West US 1</span></span> | <span data-ttu-id="8e12d-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="8e12d-206">23.99.34.75</span></span> | <span data-ttu-id="8e12d-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="8e12d-207">104.42.238.205</span></span> |
| <span data-ttu-id="8e12d-208">Oeste de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="8e12d-208">West US 2</span></span> | <span data-ttu-id="8e12d-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="8e12d-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="8e12d-210">Cambio de la directiva de conexión de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="8e12d-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="8e12d-211">Para cambiar la directiva de conexión de Azure SQL Database de un servidor de Azure SQL Database, use la [API de REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e12d-211">To change the Azure SQL Database connection policy for an Azure SQL Database server, use the [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="8e12d-212">Si la directiva de conexión se establece en **Proxy**, todos los paquetes de red fluyen a través de la puerta de enlace de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8e12d-212">If your connection policy is set to **Proxy**, all network packets flow via the Azure SQL Database gateway.</span></span> <span data-ttu-id="8e12d-213">Para esta configuración, debe permitir el tráfico saliente solo a la dirección IP de la puerta de enlace de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8e12d-213">For this setting, you need to allow outbound to only the Azure SQL Database gateway IP.</span></span> <span data-ttu-id="8e12d-214">El uso de la configuración de **proxy** ofrece más latencia que la de **redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="8e12d-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="8e12d-215">Si la configuración de la directiva de conexión está basada en el **redireccionamiento**, todos los paquetes de red fluyen directamente al proxy del middleware.</span><span class="sxs-lookup"><span data-stu-id="8e12d-215">If your connection policy is setting **Redirect**, all network packets flow directly to the middleware proxy.</span></span> <span data-ttu-id="8e12d-216">Para esta configuración, debe permitir el tráfico saliente a varias direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="8e12d-216">For this setting, you need to allow outbound to multiple IPs.</span></span> 

## <a name="script-to-change-connection-settings"></a><span data-ttu-id="8e12d-217">Script para cambiar la configuración de la conexión</span><span class="sxs-lookup"><span data-stu-id="8e12d-217">Script to change connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e12d-218">Este script requiere el [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8e12d-218">This script requires the [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="8e12d-219">El siguiente script de PowerShell muestra cómo cambiar la directiva de conexión.</span><span class="sxs-lookup"><span data-stu-id="8e12d-219">The following PowerShell script shows how to change the connection policy.</span></span>

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

#getting the current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting the property to ‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="8e12d-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e12d-220">Next steps</span></span>

- <span data-ttu-id="8e12d-221">Para obtener información sobre cómo cambiar la directiva de conexión de Azure SQL Database de un servidor de Azure SQL Database, vea [Creación o actualización de la directiva de conexión de un servidor mediante la API de REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e12d-221">For information on how to change the Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using the REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="8e12d-222">Para obtener información sobre el comportamiento de conexión de Azure SQL Database para clientes que usan ADO.NET 4.5 o una versión posterior, vea [Puertos más allá de 1433 para ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="8e12d-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="8e12d-223">Para obtener información general sobre el desarrollo de aplicaciones, vea [Introducción al desarrollo de aplicaciones en SQL Database](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e12d-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>

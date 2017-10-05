---
title: "Introducción a un escenario de recuperación ante desastres de Oracle en el entorno de Azure | Microsoft Docs"
description: "Un escenario de recuperación ante desastres para Oracle Database 12c en el entorno de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: f17ebb2b74cd7ad872f88483ed7cdb4f239ee069
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="d1591-103">Recuperación ante desastres para Oracle Database 12c en el entorno de Azure</span><span class="sxs-lookup"><span data-stu-id="d1591-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="d1591-104">Supuestos</span><span class="sxs-lookup"><span data-stu-id="d1591-104">Assumptions</span></span>

- <span data-ttu-id="d1591-105">Tiene conocimientos sobre el diseño de Oracle Data Guard y el entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="d1591-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="d1591-106">Objetivos</span><span class="sxs-lookup"><span data-stu-id="d1591-106">Goals</span></span>
- <span data-ttu-id="d1591-107">Diseñar la topología y configuración que satisfacen las necesidades de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="d1591-107">Design the topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="d1591-108">Escenario 1: sitios principal y de recuperación ante desastres en Azure</span><span class="sxs-lookup"><span data-stu-id="d1591-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="d1591-109">Un cliente tiene una instalación de base de datos de Oracle en el sitio principal.</span><span class="sxs-lookup"><span data-stu-id="d1591-109">A customer has an Oracle database set up on the primary site.</span></span> <span data-ttu-id="d1591-110">El sitio de recuperación ante desastres (DR) se encuentra en una región diferente.</span><span class="sxs-lookup"><span data-stu-id="d1591-110">A DR site is in a different region.</span></span> <span data-ttu-id="d1591-111">El cliente utiliza Oracle Data Guard para la recuperación rápida entre estos sitios.</span><span class="sxs-lookup"><span data-stu-id="d1591-111">The customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="d1591-112">El sitio principal tiene también una base de datos secundaria para informes y otros usos.</span><span class="sxs-lookup"><span data-stu-id="d1591-112">The primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="d1591-113">Topología</span><span class="sxs-lookup"><span data-stu-id="d1591-113">Topology</span></span>

<span data-ttu-id="d1591-114">A continuación, se muestra un resumen de la configuración de Azure:</span><span class="sxs-lookup"><span data-stu-id="d1591-114">Here is a summary of the Azure setup:</span></span>

- <span data-ttu-id="d1591-115">Dos sitios (un sitio principal y un sitio de recuperación ante desastres)</span><span class="sxs-lookup"><span data-stu-id="d1591-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="d1591-116">Dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="d1591-116">Two virtual networks</span></span>
- <span data-ttu-id="d1591-117">Dos bases de datos de Oracle con Data Guard (principal y en espera)</span><span class="sxs-lookup"><span data-stu-id="d1591-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="d1591-118">Dos bases de datos de Oracle con Golden Gate o Data Guard (solo para el sitio principal)</span><span class="sxs-lookup"><span data-stu-id="d1591-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="d1591-119">Dos servicios de aplicación, uno en el sitio principal y uno en el sitio de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="d1591-119">Two application services, one primary and one on the DR site</span></span>
- <span data-ttu-id="d1591-120">Un *conjunto de disponibilidad* que se usa para la base de datos y el servicio de aplicación en el sitio principal</span><span class="sxs-lookup"><span data-stu-id="d1591-120">An *availability set,* which is used for database and application service on the primary site</span></span>
- <span data-ttu-id="d1591-121">Un Jumpbox en cada sitio, que restringe el acceso a la red privada y solo permite el inicio de sesión al administrador</span><span class="sxs-lookup"><span data-stu-id="d1591-121">One jumpbox on each site, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="d1591-122">El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN en subredes independientes</span><span class="sxs-lookup"><span data-stu-id="d1591-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="d1591-123">El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos</span><span class="sxs-lookup"><span data-stu-id="d1591-123">NSG enforced on application and database subnets</span></span>

![Captura de pantalla de la página de la topología de recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="d1591-125">Escenario 2: sitio principal en ubicación local y sitio de recuperación ante desastres en Azure</span><span class="sxs-lookup"><span data-stu-id="d1591-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="d1591-126">Un cliente tiene una instalación de base de datos de Oracle en un sitio local (sitio principal).</span><span class="sxs-lookup"><span data-stu-id="d1591-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="d1591-127">Un sitio de recuperación ante desastres en Azure.</span><span class="sxs-lookup"><span data-stu-id="d1591-127">A DR site is on Azure.</span></span> <span data-ttu-id="d1591-128">Oracle Data Guard se usa para la recuperación rápida entre estos sitios.</span><span class="sxs-lookup"><span data-stu-id="d1591-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="d1591-129">El sitio principal tiene también una base de datos secundaria para informes y otros usos.</span><span class="sxs-lookup"><span data-stu-id="d1591-129">The primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="d1591-130">Existen dos enfoques para esta instalación.</span><span class="sxs-lookup"><span data-stu-id="d1591-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-the-firewall"></a><span data-ttu-id="d1591-131">Enfoque 1: conexiones directas entre el sitio local y Azure, lo que requiere abrir puertos TCP en el firewall</span><span class="sxs-lookup"><span data-stu-id="d1591-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on the firewall</span></span> 

<span data-ttu-id="d1591-132">No se recomiendan las conexiones directas porque exponen los puertos TCP al mundo exterior.</span><span class="sxs-lookup"><span data-stu-id="d1591-132">We don't recommend direct connections because they expose the TCP ports to the outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="d1591-133">Topología</span><span class="sxs-lookup"><span data-stu-id="d1591-133">Topology</span></span>

<span data-ttu-id="d1591-134">A continuación, se muestra un resumen de la configuración de Azure:</span><span class="sxs-lookup"><span data-stu-id="d1591-134">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="d1591-135">Un sitio de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="d1591-135">One DR site</span></span> 
- <span data-ttu-id="d1591-136">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="d1591-136">One virtual network</span></span>
- <span data-ttu-id="d1591-137">Una base de datos de Oracle con Data Guard (activo)</span><span class="sxs-lookup"><span data-stu-id="d1591-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="d1591-138">Un servicio de aplicación en el sitio de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="d1591-138">One application service on the DR site</span></span>
- <span data-ttu-id="d1591-139">Un Jumpbox, que restringe el acceso a la red privada y solo permite el inicio de sesión al administrador</span><span class="sxs-lookup"><span data-stu-id="d1591-139">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="d1591-140">El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN en subredes independientes</span><span class="sxs-lookup"><span data-stu-id="d1591-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="d1591-141">El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos</span><span class="sxs-lookup"><span data-stu-id="d1591-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="d1591-142">Una directiva o regla de NSG para permitir el tráfico entrante en el puerto TCP 1521 (o el definido por el usuario)</span><span class="sxs-lookup"><span data-stu-id="d1591-142">An NSG policy/rule to allow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="d1591-143">Una directiva o regla de NSG para restringir el acceso a la red virtual solo a la dirección o direcciones IP locales (base de datos o aplicación)</span><span class="sxs-lookup"><span data-stu-id="d1591-143">An NSG policy/rule to restrict only the IP address/addresses on-premises (DB or application) to access the virtual network</span></span>

![Captura de pantalla de la página de la topología de recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="d1591-145">Enfoque 2: VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="d1591-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="d1591-146">Un mejor enfoque consiste en el uso de una VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="d1591-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="d1591-147">Para más información acerca de cómo configurar una VPN, consulte [Creación de una red virtual con una conexión VPN de sitio a sitio mediante la CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="d1591-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="d1591-148">Topología</span><span class="sxs-lookup"><span data-stu-id="d1591-148">Topology</span></span>

<span data-ttu-id="d1591-149">A continuación, se muestra un resumen de la configuración de Azure:</span><span class="sxs-lookup"><span data-stu-id="d1591-149">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="d1591-150">Un sitio de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="d1591-150">One DR site</span></span> 
- <span data-ttu-id="d1591-151">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="d1591-151">One virtual network</span></span> 
- <span data-ttu-id="d1591-152">Una base de datos de Oracle con Data Guard (activo)</span><span class="sxs-lookup"><span data-stu-id="d1591-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="d1591-153">Un servicio de aplicación en el sitio de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="d1591-153">One application service on the DR site</span></span>
- <span data-ttu-id="d1591-154">Un Jumpbox, que restringe el acceso a la red privada y solo permite el inicio de sesión al administrador</span><span class="sxs-lookup"><span data-stu-id="d1591-154">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="d1591-155">El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN se encuentran en subredes independientes</span><span class="sxs-lookup"><span data-stu-id="d1591-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="d1591-156">El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos</span><span class="sxs-lookup"><span data-stu-id="d1591-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="d1591-157">Conexión VPN de sitio a sitio entre sistemas locales y Azure</span><span class="sxs-lookup"><span data-stu-id="d1591-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Captura de pantalla de la página de la topología de recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="d1591-159">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="d1591-159">Additional reading</span></span>

- [<span data-ttu-id="d1591-160">Diseño e implementación de una base de datos de Oracle en Azure</span><span class="sxs-lookup"><span data-stu-id="d1591-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="d1591-161">Configuración de Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="d1591-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="d1591-162">Configuración de Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="d1591-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="d1591-163">Copia de seguridad y recuperación de Oracle</span><span class="sxs-lookup"><span data-stu-id="d1591-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="d1591-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1591-164">Next steps</span></span>

- [<span data-ttu-id="d1591-165">Tutorial: Creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="d1591-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="d1591-166">Ejemplos de la CLI de Azure para implementación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d1591-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)

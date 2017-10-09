---
title: "aaaOverview de un escenario de recuperación ante desastres de Oracle en el entorno de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="70e03-103">Recuperación ante desastres para Oracle Database 12c en el entorno de Azure</span><span class="sxs-lookup"><span data-stu-id="70e03-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="70e03-104">Supuestos</span><span class="sxs-lookup"><span data-stu-id="70e03-104">Assumptions</span></span>

- <span data-ttu-id="70e03-105">Tiene conocimientos sobre el diseño de Oracle Data Guard y el entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="70e03-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="70e03-106">Objetivos</span><span class="sxs-lookup"><span data-stu-id="70e03-106">Goals</span></span>
- <span data-ttu-id="70e03-107">Diseñar la topología de Hola y configuración que satisfacen las necesidades de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="70e03-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="70e03-108">Escenario 1: sitios principal y de recuperación ante desastres en Azure</span><span class="sxs-lookup"><span data-stu-id="70e03-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="70e03-109">Un cliente tiene un Oracle base de datos establecido seguridad en el sitio principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="70e03-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="70e03-110">El sitio de recuperación ante desastres (DR) se encuentra en una región diferente.</span><span class="sxs-lookup"><span data-stu-id="70e03-110">A DR site is in a different region.</span></span> <span data-ttu-id="70e03-111">cliente de Hello usa a Oracle Data Guard para la recuperación rápida entre estos sitios.</span><span class="sxs-lookup"><span data-stu-id="70e03-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="70e03-112">sitio primario de Hello también tiene una base de datos secundaria para los informes y otros usos.</span><span class="sxs-lookup"><span data-stu-id="70e03-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="70e03-113">Topología</span><span class="sxs-lookup"><span data-stu-id="70e03-113">Topology</span></span>

<span data-ttu-id="70e03-114">Este es un resumen de hello el programa de instalación de Azure:</span><span class="sxs-lookup"><span data-stu-id="70e03-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="70e03-115">Dos sitios (un sitio principal y un sitio de recuperación ante desastres)</span><span class="sxs-lookup"><span data-stu-id="70e03-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="70e03-116">Dos redes virtuales</span><span class="sxs-lookup"><span data-stu-id="70e03-116">Two virtual networks</span></span>
- <span data-ttu-id="70e03-117">Dos bases de datos de Oracle con Data Guard (principal y en espera)</span><span class="sxs-lookup"><span data-stu-id="70e03-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="70e03-118">Dos bases de datos de Oracle con Golden Gate o Data Guard (solo para el sitio principal)</span><span class="sxs-lookup"><span data-stu-id="70e03-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="70e03-119">Dos de los servicios de aplicaciones, uno principal y otro en el sitio de recuperación ante desastres de Hola</span><span class="sxs-lookup"><span data-stu-id="70e03-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="70e03-120">Un *conjunto de disponibilidad,* que se usa para el servicio de base de datos y aplicaciones en el sitio principal de Hola</span><span class="sxs-lookup"><span data-stu-id="70e03-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="70e03-121">Uno jumpbox en cada sitio, lo que restringe la red privada de acceso toohello y solamente permite el inicio de sesión en un administrador</span><span class="sxs-lookup"><span data-stu-id="70e03-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="70e03-122">El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN en subredes independientes</span><span class="sxs-lookup"><span data-stu-id="70e03-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="70e03-123">El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos</span><span class="sxs-lookup"><span data-stu-id="70e03-123">NSG enforced on application and database subnets</span></span>

![Captura de pantalla de página de la topología de hello recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="70e03-125">Escenario 2: sitio principal en ubicación local y sitio de recuperación ante desastres en Azure</span><span class="sxs-lookup"><span data-stu-id="70e03-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="70e03-126">Un cliente tiene una instalación de base de datos de Oracle en un sitio local (sitio principal).</span><span class="sxs-lookup"><span data-stu-id="70e03-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="70e03-127">Un sitio de recuperación ante desastres en Azure.</span><span class="sxs-lookup"><span data-stu-id="70e03-127">A DR site is on Azure.</span></span> <span data-ttu-id="70e03-128">Oracle Data Guard se usa para la recuperación rápida entre estos sitios.</span><span class="sxs-lookup"><span data-stu-id="70e03-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="70e03-129">sitio primario de Hello también tiene una base de datos secundaria para los informes y otros usos.</span><span class="sxs-lookup"><span data-stu-id="70e03-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="70e03-130">Existen dos enfoques para esta instalación.</span><span class="sxs-lookup"><span data-stu-id="70e03-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="70e03-131">Enfoque 1: Conexiones directas entre local y Azure, la necesidad de abrir los puertos TCP en firewall de Hola</span><span class="sxs-lookup"><span data-stu-id="70e03-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="70e03-132">No se recomienda conexiones directas porque exponen toohello de puertos TCP de hello fuera del mundo.</span><span class="sxs-lookup"><span data-stu-id="70e03-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="70e03-133">Topología</span><span class="sxs-lookup"><span data-stu-id="70e03-133">Topology</span></span>

<span data-ttu-id="70e03-134">Aquí te mostramos un resumen de hello el programa de instalación de Azure:</span><span class="sxs-lookup"><span data-stu-id="70e03-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="70e03-135">Un sitio de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="70e03-135">One DR site</span></span> 
- <span data-ttu-id="70e03-136">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="70e03-136">One virtual network</span></span>
- <span data-ttu-id="70e03-137">Una base de datos de Oracle con Data Guard (activo)</span><span class="sxs-lookup"><span data-stu-id="70e03-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="70e03-138">Servicio de una aplicación en el sitio de recuperación ante desastres de Hola</span><span class="sxs-lookup"><span data-stu-id="70e03-138">One application service on hello DR site</span></span>
- <span data-ttu-id="70e03-139">Uno jumpbox, lo que restringe la red privada de acceso toohello y solamente permite el inicio de sesión en un administrador</span><span class="sxs-lookup"><span data-stu-id="70e03-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="70e03-140">El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN en subredes independientes</span><span class="sxs-lookup"><span data-stu-id="70e03-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="70e03-141">El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos</span><span class="sxs-lookup"><span data-stu-id="70e03-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="70e03-142">El puerto TCP 1521 (o un puerto definido por el usuario) de entrada de un tooallow de directiva o la regla NSG</span><span class="sxs-lookup"><span data-stu-id="70e03-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="70e03-143">Una NSG o la regla de directiva toorestrict solo Hola IP dirección/direcciones locales (base de datos o aplicación) tooaccess Hola red virtual</span><span class="sxs-lookup"><span data-stu-id="70e03-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Captura de pantalla de página de la topología de hello recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="70e03-145">Enfoque 2: VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="70e03-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="70e03-146">Un mejor enfoque consiste en el uso de una VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="70e03-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="70e03-147">Para más información acerca de cómo configurar una VPN, consulte [Creación de una red virtual con una conexión VPN de sitio a sitio mediante la CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="70e03-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="70e03-148">Topología</span><span class="sxs-lookup"><span data-stu-id="70e03-148">Topology</span></span>

<span data-ttu-id="70e03-149">Aquí te mostramos un resumen de hello el programa de instalación de Azure:</span><span class="sxs-lookup"><span data-stu-id="70e03-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="70e03-150">Un sitio de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="70e03-150">One DR site</span></span> 
- <span data-ttu-id="70e03-151">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="70e03-151">One virtual network</span></span> 
- <span data-ttu-id="70e03-152">Una base de datos de Oracle con Data Guard (activo)</span><span class="sxs-lookup"><span data-stu-id="70e03-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="70e03-153">Servicio de una aplicación en el sitio de recuperación ante desastres de Hola</span><span class="sxs-lookup"><span data-stu-id="70e03-153">One application service on hello DR site</span></span>
- <span data-ttu-id="70e03-154">Uno jumpbox, lo que restringe la red privada de acceso toohello y solamente permite el inicio de sesión en un administrador</span><span class="sxs-lookup"><span data-stu-id="70e03-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="70e03-155">El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN se encuentran en subredes independientes</span><span class="sxs-lookup"><span data-stu-id="70e03-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="70e03-156">El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos</span><span class="sxs-lookup"><span data-stu-id="70e03-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="70e03-157">Conexión VPN de sitio a sitio entre sistemas locales y Azure</span><span class="sxs-lookup"><span data-stu-id="70e03-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Captura de pantalla de página de la topología de hello recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="70e03-159">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="70e03-159">Additional reading</span></span>

- [<span data-ttu-id="70e03-160">Diseño e implementación de una base de datos de Oracle en Azure</span><span class="sxs-lookup"><span data-stu-id="70e03-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="70e03-161">Configuración de Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="70e03-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="70e03-162">Configuración de Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="70e03-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="70e03-163">Copia de seguridad y recuperación de Oracle</span><span class="sxs-lookup"><span data-stu-id="70e03-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="70e03-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="70e03-164">Next steps</span></span>

- [<span data-ttu-id="70e03-165">Tutorial: Creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="70e03-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="70e03-166">Ejemplos de la CLI de Azure para implementación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="70e03-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)

---
title: aaaExample tutorial de infraestructura de Azure | Documentos de Microsoft
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para implementar una infraestructura de ejemplo en Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="7f46e-103">Tutorial de la infraestructura de Azure de ejemplo para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="7f46e-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="7f46e-104">Este artículo le guía a través de la creación de una infraestructura de aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7f46e-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="7f46e-105">Se detallan diseñar una infraestructura de una tienda en línea simple que reúne todas las instrucciones de Hola y tomar decisiones sobre las convenciones de nomenclatura, conjuntos de disponibilidad, las redes virtuales y equilibradores de carga y la implementación real de sus máquinas virtuales (VM).</span><span class="sxs-lookup"><span data-stu-id="7f46e-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="7f46e-106">Carga de trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7f46e-106">Example workload</span></span>
<span data-ttu-id="7f46e-107">Adventure Works Cycles desea toobuild una aplicación de tienda en línea en Azure que consta de:</span><span class="sxs-lookup"><span data-stu-id="7f46e-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="7f46e-108">Dos servidores IIS que se ejecutan cliente hello front-end en un nivel de web</span><span class="sxs-lookup"><span data-stu-id="7f46e-108">Two IIS servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="7f46e-109">Dos servidores IIS que procesen datos y pedidos en un nivel de aplicación</span><span class="sxs-lookup"><span data-stu-id="7f46e-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="7f46e-110">Dos instancias de Microsoft SQL Server con grupos de disponibilidad AlwaysOn (dos servidores SQL Server y un testigo de mayoría de nodo) para almacenar datos de productos y pedidos en un nivel de base de datos</span><span class="sxs-lookup"><span data-stu-id="7f46e-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="7f46e-111">Dos controladores de dominio de Active Directory para los proveedores y las cuentas de cliente en un nivel de autenticación</span><span class="sxs-lookup"><span data-stu-id="7f46e-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="7f46e-112">Todos los servidores de Hola se encuentran en dos subredes:</span><span class="sxs-lookup"><span data-stu-id="7f46e-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="7f46e-113">una subred para servidores de hello web front-end</span><span class="sxs-lookup"><span data-stu-id="7f46e-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="7f46e-114">una subred de back-end para servidores de aplicaciones de hello, clúster de SQL y los controladores de dominio</span><span class="sxs-lookup"><span data-stu-id="7f46e-114">a back-end subnet for hello application servers, SQL cluster, and domain controllers</span></span>

![Diagrama de distintos niveles de infraestructura de aplicaciones](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="7f46e-116">Entrada segura tráfico web debe tener equilibrio de carga entre los servidores web de Hola mientras navega por los clientes de tienda en línea hello.</span><span class="sxs-lookup"><span data-stu-id="7f46e-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="7f46e-117">Orden de procesamiento de tráfico en forma de Hola de las solicitudes HTTP desde web Hola servidores deben estar equilibrados entre servidores de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f46e-117">Order processing traffic in hello form of HTTP requests from hello web servers must be balanced among hello application servers.</span></span> <span data-ttu-id="7f46e-118">Además, la infraestructura de Hola debe diseñarse para lograr alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="7f46e-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="7f46e-119">diseño de Hello resultante debe incorporar:</span><span class="sxs-lookup"><span data-stu-id="7f46e-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="7f46e-120">Una suscripción y una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="7f46e-120">An Azure subscription and account</span></span>
* <span data-ttu-id="7f46e-121">Un único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7f46e-121">A single resource group</span></span>
* <span data-ttu-id="7f46e-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="7f46e-122">Azure Managed Disks</span></span>
* <span data-ttu-id="7f46e-123">Una red virtual con dos subredes</span><span class="sxs-lookup"><span data-stu-id="7f46e-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="7f46e-124">Conjuntos de disponibilidad para hello las máquinas virtuales con una función similar</span><span class="sxs-lookup"><span data-stu-id="7f46e-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="7f46e-125">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7f46e-125">Virtual machines</span></span>

<span data-ttu-id="7f46e-126">Hola todos los anteriores seguir estas convenciones de nomenclaturas:</span><span class="sxs-lookup"><span data-stu-id="7f46e-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="7f46e-127">Adventure Works Cycles usa **[carga de trabajo de TI]-[ubicación]-[recurso de Azure]** como prefijo</span><span class="sxs-lookup"><span data-stu-id="7f46e-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="7f46e-128">En este ejemplo, "**azos**" (tienda en línea de Azure) se Hola nombre de cargas de trabajo de TI y "**usar**" (este de EE. 2) es la ubicación de Hola</span><span class="sxs-lookup"><span data-stu-id="7f46e-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="7f46e-129">Las redes virtuales usan AZOS-USE-VN**[número]**</span><span class="sxs-lookup"><span data-stu-id="7f46e-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="7f46e-130">Los conjuntos de disponibilidad usan azos-use-as-**[rol]**</span><span class="sxs-lookup"><span data-stu-id="7f46e-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="7f46e-131">Los nombres de máquinas virtuales usan azos-use-vm-**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="7f46e-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="7f46e-132">Suscripciones y cuentas de Azure</span><span class="sxs-lookup"><span data-stu-id="7f46e-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="7f46e-133">Adventure Works Cycles es con su suscripción de Enterprise, con el nombre Adventure Works Enterprise Subscription, tooprovide de facturación para esta carga de trabajo de TI.</span><span class="sxs-lookup"><span data-stu-id="7f46e-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="7f46e-134">Storage</span><span class="sxs-lookup"><span data-stu-id="7f46e-134">Storage</span></span>
<span data-ttu-id="7f46e-135">Adventure Works Cycles determina que deben usar Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="7f46e-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="7f46e-136">Al crear máquinas virtuales, se utilizan ambos niveles de almacenamiento disponible:</span><span class="sxs-lookup"><span data-stu-id="7f46e-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="7f46e-137">**Almacenamiento estándar** para servidores de hello web, servidores de aplicaciones y controladores de dominio y sus discos de datos.</span><span class="sxs-lookup"><span data-stu-id="7f46e-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="7f46e-138">**Almacenamiento Premium** para hello VM de SQL Server y sus discos de datos.</span><span class="sxs-lookup"><span data-stu-id="7f46e-138">**Premium storage** for hello SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="7f46e-139">Red virtual y subredes</span><span class="sxs-lookup"><span data-stu-id="7f46e-139">Virtual network and subnets</span></span>
<span data-ttu-id="7f46e-140">Red virtual de hello no necesite red local de conectividad en curso toohello Adventure ciclos de trabajo, decidió en una red virtual solo en la nube.</span><span class="sxs-lookup"><span data-stu-id="7f46e-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="7f46e-141">Crea una red virtual solo en la nube con hello después de la configuración mediante Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="7f46e-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="7f46e-142">Nombre: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="7f46e-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="7f46e-143">Ubicación: Este de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="7f46e-143">Location: East US 2</span></span>
* <span data-ttu-id="7f46e-144">Espacio de direcciones de red virtual: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="7f46e-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="7f46e-145">Primera subred:</span><span class="sxs-lookup"><span data-stu-id="7f46e-145">First subnet:</span></span>
  * <span data-ttu-id="7f46e-146">Nombre: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="7f46e-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="7f46e-147">Espacio de direcciones: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="7f46e-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="7f46e-148">Segunda subred:</span><span class="sxs-lookup"><span data-stu-id="7f46e-148">Second subnet:</span></span>
  * <span data-ttu-id="7f46e-149">Nombre: BackEnd</span><span class="sxs-lookup"><span data-stu-id="7f46e-149">Name: BackEnd</span></span>
  * <span data-ttu-id="7f46e-150">Espacio de direcciones: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="7f46e-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="7f46e-151">Conjuntos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="7f46e-151">Availability sets</span></span>
<span data-ttu-id="7f46e-152">toomaintain alta disponibilidad de los cuatro niveles de su tienda en línea, Adventure Works Cycles decidir sobre cuatro conjuntos de disponibilidad:</span><span class="sxs-lookup"><span data-stu-id="7f46e-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="7f46e-153">**use azos como web** para servidores web de Hola</span><span class="sxs-lookup"><span data-stu-id="7f46e-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="7f46e-154">**use azos como aplicación** hello en servidores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7f46e-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="7f46e-155">**uso de azos como sql** para hello servidores SQL Server</span><span class="sxs-lookup"><span data-stu-id="7f46e-155">**azos-use-as-sql** for hello SQL Servers</span></span>
* <span data-ttu-id="7f46e-156">**use azos como dc** Hola para controladores de dominio</span><span class="sxs-lookup"><span data-stu-id="7f46e-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="7f46e-157">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7f46e-157">Virtual machines</span></span>
<span data-ttu-id="7f46e-158">Adventure Works Cycles decidió Hola después de nombres para sus máquinas virtuales de Azure:</span><span class="sxs-lookup"><span data-stu-id="7f46e-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="7f46e-159">**azos-use-vm-web01** para el primer servidor de web Hola</span><span class="sxs-lookup"><span data-stu-id="7f46e-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="7f46e-160">**azos-use-vm-web02** para el segundo servidor de web Hola</span><span class="sxs-lookup"><span data-stu-id="7f46e-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="7f46e-161">**azos-use-vm-app01** Hola primer servidor de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7f46e-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="7f46e-162">**azos-use-vm-app02** Hola segundo servidor de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7f46e-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="7f46e-163">**azos-use-vm-sql01** para hello primer de SQL server en clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="7f46e-163">**azos-use-vm-sql01** for hello first SQL Server server in hello cluster</span></span>
* <span data-ttu-id="7f46e-164">**azos-use-vm-sql02** para hello segundo SQL server en clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="7f46e-164">**azos-use-vm-sql02** for hello second SQL Server server in hello cluster</span></span>
* <span data-ttu-id="7f46e-165">**azos-use-vm-dc01** Hola primer controlador de dominio</span><span class="sxs-lookup"><span data-stu-id="7f46e-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="7f46e-166">**azos-use-vm-dc02** Hola segundo controlador de dominio</span><span class="sxs-lookup"><span data-stu-id="7f46e-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="7f46e-167">Esta es la configuración resultante de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f46e-167">Here is hello resulting configuration.</span></span>

![Infraestructura de aplicaciones final implementada en Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="7f46e-169">Esta configuración incluye:</span><span class="sxs-lookup"><span data-stu-id="7f46e-169">This configuration incorporates:</span></span>

* <span data-ttu-id="7f46e-170">Una red virtual solo en la nube con dos subredes (FrontEnd y BackEnd)</span><span class="sxs-lookup"><span data-stu-id="7f46e-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="7f46e-171">Azure Managed Disks con discos Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="7f46e-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="7f46e-172">Cuatro conjuntos de disponibilidad, uno para cada nivel de tienda en línea hello</span><span class="sxs-lookup"><span data-stu-id="7f46e-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="7f46e-173">máquinas virtuales de Hola para los niveles de hello cuatro</span><span class="sxs-lookup"><span data-stu-id="7f46e-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="7f46e-174">Un conjunto de carga equilibrada externo para el tráfico web basada en HTTPS desde servidores web de hello Internet toohello</span><span class="sxs-lookup"><span data-stu-id="7f46e-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="7f46e-175">Una carga interna equilibrada conjunto para el tráfico web sin cifrar hello web servidores toohello desde servidores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7f46e-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="7f46e-176">Un único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7f46e-176">A single resource group</span></span>
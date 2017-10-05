---
title: Tutorial de la infraestructura de Azure de ejemplo | Microsoft Docs
description: "Obtenga información sobre las directrices clave de diseño e implementación para implementar una infraestructura de ejemplo en Azure."
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
ms.openlocfilehash: 84cefcdb85f1a3c753027e827abde010b461cda7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="a3c18-103">Tutorial de la infraestructura de Azure de ejemplo para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="a3c18-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="a3c18-104">Este artículo le guía a través de la creación de una infraestructura de aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a3c18-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="a3c18-105">Detallaremos el diseño de una infraestructura para una tienda en línea sencilla que reúna todas las directrices y decisiones relacionadas con las convenciones de nomenclatura, los conjuntos de disponibilidad, las redes virtuales, los equilibradores de carga y, realmente, la implementación de sus máquinas virtuales (VM).</span><span class="sxs-lookup"><span data-stu-id="a3c18-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="a3c18-106">Carga de trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a3c18-106">Example workload</span></span>
<span data-ttu-id="a3c18-107">Adventure Works Cycles desea crear una aplicación de la tienda en línea en Azure que conste de:</span><span class="sxs-lookup"><span data-stu-id="a3c18-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="a3c18-108">Dos servidores IIS que ejecuten el front-end de cliente en un nivel web</span><span class="sxs-lookup"><span data-stu-id="a3c18-108">Two IIS servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="a3c18-109">Dos servidores IIS que procesen datos y pedidos en un nivel de aplicación</span><span class="sxs-lookup"><span data-stu-id="a3c18-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="a3c18-110">Dos instancias de Microsoft SQL Server con grupos de disponibilidad AlwaysOn (dos servidores SQL Server y un testigo de mayoría de nodo) para almacenar datos de productos y pedidos en un nivel de base de datos</span><span class="sxs-lookup"><span data-stu-id="a3c18-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="a3c18-111">Dos controladores de dominio de Active Directory para los proveedores y las cuentas de cliente en un nivel de autenticación</span><span class="sxs-lookup"><span data-stu-id="a3c18-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="a3c18-112">Todos los servidores se encuentran en dos subredes:</span><span class="sxs-lookup"><span data-stu-id="a3c18-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="a3c18-113">una subred front-end para los servidores web</span><span class="sxs-lookup"><span data-stu-id="a3c18-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="a3c18-114">una subred back-end para los servidores de aplicaciones, un clúster de SQL y controladores de dominio</span><span class="sxs-lookup"><span data-stu-id="a3c18-114">a back-end subnet for the application servers, SQL cluster, and domain controllers</span></span>

![Diagrama de distintos niveles de infraestructura de aplicaciones](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="a3c18-116">El tráfico web seguro entrante debe ser de carga equilibrada entre los servidores web a medida que los clientes examinan la tienda en línea.</span><span class="sxs-lookup"><span data-stu-id="a3c18-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="a3c18-117">El tráfico de procesamiento de pedidos en forma de solicitudes HTTP procedente de los servidores web debe equilibrarse entre los servidores de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a3c18-117">Order processing traffic in the form of HTTP requests from the web servers must be balanced among the application servers.</span></span> <span data-ttu-id="a3c18-118">Además, la infraestructura debe diseñarse para alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="a3c18-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="a3c18-119">El diseño resultante incluirá:</span><span class="sxs-lookup"><span data-stu-id="a3c18-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="a3c18-120">Una suscripción y una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="a3c18-120">An Azure subscription and account</span></span>
* <span data-ttu-id="a3c18-121">Un único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a3c18-121">A single resource group</span></span>
* <span data-ttu-id="a3c18-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="a3c18-122">Azure Managed Disks</span></span>
* <span data-ttu-id="a3c18-123">Una red virtual con dos subredes</span><span class="sxs-lookup"><span data-stu-id="a3c18-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="a3c18-124">Conjuntos de disponibilidad para las máquinas virtuales con un rol similar</span><span class="sxs-lookup"><span data-stu-id="a3c18-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="a3c18-125">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a3c18-125">Virtual machines</span></span>

<span data-ttu-id="a3c18-126">Todo lo anterior seguirá estas convenciones de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="a3c18-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="a3c18-127">Adventure Works Cycles usa **[carga de trabajo de TI]-[ubicación]-[recurso de Azure]** como prefijo</span><span class="sxs-lookup"><span data-stu-id="a3c18-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="a3c18-128">En este ejemplo, "**azos**" (siglas en inglés de "tienda en línea de Azure") es el nombre de la carga de trabajo de TI y "**use**" (siglas en inglés de "este de EE. UU. 2") es la ubicación.</span><span class="sxs-lookup"><span data-stu-id="a3c18-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="a3c18-129">Las redes virtuales usan AZOS-USE-VN**[número]**</span><span class="sxs-lookup"><span data-stu-id="a3c18-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="a3c18-130">Los conjuntos de disponibilidad usan azos-use-as-**[rol]**</span><span class="sxs-lookup"><span data-stu-id="a3c18-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="a3c18-131">Los nombres de máquinas virtuales usan azos-use-vm-**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="a3c18-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="a3c18-132">Suscripciones y cuentas de Azure</span><span class="sxs-lookup"><span data-stu-id="a3c18-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="a3c18-133">Adventure Works Cycles usa la suscripción Enterprise, denominada Adventure Works Enterprise Subscription, para proporcionar la facturación de esta carga de trabajo de TI.</span><span class="sxs-lookup"><span data-stu-id="a3c18-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="a3c18-134">Almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a3c18-134">Storage</span></span>
<span data-ttu-id="a3c18-135">Adventure Works Cycles determina que deben usar Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="a3c18-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="a3c18-136">Al crear máquinas virtuales, se utilizan ambos niveles de almacenamiento disponible:</span><span class="sxs-lookup"><span data-stu-id="a3c18-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="a3c18-137">**Almacenamiento estándar** de los servidores web, los servidores de aplicaciones y los controladores de dominio y sus discos de datos.</span><span class="sxs-lookup"><span data-stu-id="a3c18-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="a3c18-138">**Premium Storage** de máquinas virtuales de SQL Server y sus discos de datos.</span><span class="sxs-lookup"><span data-stu-id="a3c18-138">**Premium storage** for the SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="a3c18-139">Red virtual y subredes</span><span class="sxs-lookup"><span data-stu-id="a3c18-139">Virtual network and subnets</span></span>
<span data-ttu-id="a3c18-140">Dado que la red virtual no necesita una conectividad continua con la red local de Adventure Work Cycles, la empresa optó por una red virtual solo en la nube.</span><span class="sxs-lookup"><span data-stu-id="a3c18-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="a3c18-141">Creó una red virtual solo en la nube con la siguiente configuración a través del Portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="a3c18-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="a3c18-142">Nombre: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="a3c18-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="a3c18-143">Ubicación: Este de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="a3c18-143">Location: East US 2</span></span>
* <span data-ttu-id="a3c18-144">Espacio de direcciones de red virtual: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="a3c18-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="a3c18-145">Primera subred:</span><span class="sxs-lookup"><span data-stu-id="a3c18-145">First subnet:</span></span>
  * <span data-ttu-id="a3c18-146">Nombre: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="a3c18-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="a3c18-147">Espacio de direcciones: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="a3c18-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="a3c18-148">Segunda subred:</span><span class="sxs-lookup"><span data-stu-id="a3c18-148">Second subnet:</span></span>
  * <span data-ttu-id="a3c18-149">Nombre: BackEnd</span><span class="sxs-lookup"><span data-stu-id="a3c18-149">Name: BackEnd</span></span>
  * <span data-ttu-id="a3c18-150">Espacio de direcciones: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="a3c18-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="a3c18-151">Conjuntos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="a3c18-151">Availability sets</span></span>
<span data-ttu-id="a3c18-152">Para mantener la alta disponibilidad de los cuatro niveles de su tienda en línea, Adventure Works Cycles optó por cuatro conjuntos de disponibilidad:</span><span class="sxs-lookup"><span data-stu-id="a3c18-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="a3c18-153">**azos-use-as-web** para los servidores web</span><span class="sxs-lookup"><span data-stu-id="a3c18-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="a3c18-154">**azos-use-as-app** para los servidores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a3c18-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="a3c18-155">**azos-use-as-sql** para los servidores SQL Server</span><span class="sxs-lookup"><span data-stu-id="a3c18-155">**azos-use-as-sql** for the SQL Servers</span></span>
* <span data-ttu-id="a3c18-156">**azos-use-as-dc** para los controladores de dominio</span><span class="sxs-lookup"><span data-stu-id="a3c18-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="a3c18-157">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a3c18-157">Virtual machines</span></span>
<span data-ttu-id="a3c18-158">Adventure Works Cycles decidió los siguientes nombres para sus máquinas virtuales de Azure:</span><span class="sxs-lookup"><span data-stu-id="a3c18-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="a3c18-159">**azos-use-vm-web01** para el primer servidor web</span><span class="sxs-lookup"><span data-stu-id="a3c18-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="a3c18-160">**azos-use-vm-web02** para el segundo servidor web</span><span class="sxs-lookup"><span data-stu-id="a3c18-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="a3c18-161">**azos-use-vm-app01** para el primer servidor de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a3c18-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="a3c18-162">**azos-use-vm-app02** para el segundo servidor de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a3c18-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="a3c18-163">**azos-use-vm-sql01** para el primer servidor SQL Server del clúster</span><span class="sxs-lookup"><span data-stu-id="a3c18-163">**azos-use-vm-sql01** for the first SQL Server server in the cluster</span></span>
* <span data-ttu-id="a3c18-164">**azos-use-vm-sql02** para el segundo servidor SQL Server del clúster</span><span class="sxs-lookup"><span data-stu-id="a3c18-164">**azos-use-vm-sql02** for the second SQL Server server in the cluster</span></span>
* <span data-ttu-id="a3c18-165">**azos-use-vm-dc01** para el primer controlador de dominio</span><span class="sxs-lookup"><span data-stu-id="a3c18-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="a3c18-166">**azos-use-vm-dc02** para el segundo controlador de dominio</span><span class="sxs-lookup"><span data-stu-id="a3c18-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="a3c18-167">Aquí está la configuración resultante.</span><span class="sxs-lookup"><span data-stu-id="a3c18-167">Here is the resulting configuration.</span></span>

![Infraestructura de aplicaciones final implementada en Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="a3c18-169">Esta configuración incluye:</span><span class="sxs-lookup"><span data-stu-id="a3c18-169">This configuration incorporates:</span></span>

* <span data-ttu-id="a3c18-170">Una red virtual solo en la nube con dos subredes (FrontEnd y BackEnd)</span><span class="sxs-lookup"><span data-stu-id="a3c18-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="a3c18-171">Azure Managed Disks con discos Standard y Premium</span><span class="sxs-lookup"><span data-stu-id="a3c18-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="a3c18-172">Cuatro conjuntos de disponibilidad, uno para cada nivel de la tienda en línea</span><span class="sxs-lookup"><span data-stu-id="a3c18-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="a3c18-173">Las máquinas virtuales para los cuatro niveles</span><span class="sxs-lookup"><span data-stu-id="a3c18-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="a3c18-174">Un conjunto externo de carga equilibrada para el tráfico web basado en HTTPS de Internet a los servidores web</span><span class="sxs-lookup"><span data-stu-id="a3c18-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="a3c18-175">Un conjunto interno de carga equilibrada para el tráfico web sin cifrar de los servidores web a los servidores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a3c18-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="a3c18-176">Un único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a3c18-176">A single resource group</span></span>
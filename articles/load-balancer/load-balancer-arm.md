---
title: Compatibilidad de Azure Resource Manager con Load Balancer | Microsoft Docs
description: Uso de PowerShell para el equilibrador de carga con Azure Resource Manager. Uso de plantillas para el equilibrador de carga
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="98157-104">Uso de la compatibilidad de Azure Resource Manager con Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="98157-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="98157-105">Azure Resource Manager es el marco de administración de servicios preferido en Azure.</span><span class="sxs-lookup"><span data-stu-id="98157-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="98157-106">Azure Load Balancer puede administrarse ahora mediante las herramientas y las API basadas en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="98157-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="98157-107">Conceptos</span><span class="sxs-lookup"><span data-stu-id="98157-107">Concepts</span></span>

<span data-ttu-id="98157-108">Con Resource Manager, Azure Load Balancer contiene los siguientes recursos secundarios:</span><span class="sxs-lookup"><span data-stu-id="98157-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="98157-109">Configuración de dirección IP front-end: un equilibrador de carga puede incluir una o varias direcciones IP front-end, conocidas también como IP virtuales (VIP).</span><span class="sxs-lookup"><span data-stu-id="98157-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="98157-110">Estas direcciones IP sirven como entrada para el tráfico.</span><span class="sxs-lookup"><span data-stu-id="98157-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="98157-111">Grupo de direcciones back-end: se trata de direcciones IP asociadas a las tarjetas de interfaz de red (NIC) de máquina virtual a las que se distribuirá la carga.</span><span class="sxs-lookup"><span data-stu-id="98157-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="98157-112">Reglas de equilibrio de carga: una propiedad de regla asigna una combinación dada de dirección IP front-end y puerto a un conjunto de combinaciones de direcciones IP back-end y puerto.</span><span class="sxs-lookup"><span data-stu-id="98157-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="98157-113">Un solo equilibrador de carga puede tener varias reglas de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="98157-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="98157-114">Cada regla tiene una combinación de una IP de front-end y un puerto y una IP de back-end asociados a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="98157-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="98157-115">Sondeos: los sondeos permiten realizar un seguimiento del estado de las instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="98157-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="98157-116">Si se produce un error en un sondeo de estado, la instancia de VM se sacará automáticamente de la rotación.</span><span class="sxs-lookup"><span data-stu-id="98157-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="98157-117">Reglas NAT entrantes: las reglas NAT que definen el tráfico entrante que fluye a través de la dirección IP front-end y se distribuye a la dirección IP back-end.</span><span class="sxs-lookup"><span data-stu-id="98157-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="98157-118">Plantillas de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="98157-118">Quickstart templates</span></span>

<span data-ttu-id="98157-119">El Administrador de recursos de Azure le permite aprovisionar sus aplicaciones mediante una plantilla declarativa.</span><span class="sxs-lookup"><span data-stu-id="98157-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="98157-120">En una plantilla, puede implementar varios servicios junto con sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="98157-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="98157-121">Use la misma plantilla para implementar su aplicación de forma repetida durante cada fase de su ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="98157-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="98157-122">Las plantillas pueden incluir definiciones de máquinas virtuales, redes virtuales, conjuntos de disponibilidad, interfaces de red (NIC), cuentas de almacenamiento, equilibradores de carga, grupos de seguridad de red y direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="98157-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="98157-123">Con las plantillas puede crear todo lo que necesita para una aplicación compleja.</span><span class="sxs-lookup"><span data-stu-id="98157-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="98157-124">El archivo de plantilla se puede proteger en el sistema de administración de contenidos para controlar versiones y colaborar.</span><span class="sxs-lookup"><span data-stu-id="98157-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="98157-125">Más información sobre las plantillas</span><span class="sxs-lookup"><span data-stu-id="98157-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="98157-126">Más información sobre los recursos de red</span><span class="sxs-lookup"><span data-stu-id="98157-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="98157-127">Las plantillas de inicio rápido que usan Azure Load Balancer se pueden encontrar en un [repositorio de GitHub](https://github.com/Azure/azure-quickstart-templates) que hospeda un conjunto de plantillas generadas por la comunidad.</span><span class="sxs-lookup"><span data-stu-id="98157-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="98157-128">Ejemplos de plantillas:</span><span class="sxs-lookup"><span data-stu-id="98157-128">Examples of templates:</span></span>

* [<span data-ttu-id="98157-129">Dos máquinas virtuales en un Equilibrador de carga y reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="98157-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="98157-130">Dos máquinas virtuales en una red virtual con un Equilibrador de carga interno y reglas del Equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="98157-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="98157-131">Dos máquinas virtuales en un Equilibrador de carga y configuración de reglas NAT en el Equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="98157-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="98157-132">Configuración del Equilibrador de carga de Azure con PowerShell o CLI</span><span class="sxs-lookup"><span data-stu-id="98157-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="98157-133">Introducción a los cmdlets de Azure Resource Manager, las herramientas de línea de comandos y las API de REST</span><span class="sxs-lookup"><span data-stu-id="98157-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="98157-134">[cmdlets de Redes de Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) pueden usarse para crear un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="98157-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="98157-135">Cómo crear un Equilibrador de carga mediante el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="98157-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="98157-136">Uso de CLI de Azure con el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="98157-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="98157-137">API de REST del Equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="98157-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="98157-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="98157-138">Next steps</span></span>

<span data-ttu-id="98157-139">También puede [empezar a crear un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento especifico del tráfico de red del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="98157-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="98157-140">Aprenda a administrar la [configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="98157-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="98157-141">Esto es importante cuando la aplicación necesita mantener las conexiones activas para servidores detrás de un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="98157-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>

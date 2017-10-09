---
title: compatibilidad con el Administrador de recursos para el equilibrador de carga aaaAzure | Documentos de Microsoft
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
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="ca3b1-104">Uso de la compatibilidad de Azure Resource Manager con Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="ca3b1-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="ca3b1-105">Administrador de recursos de Azure es el marco de trabajo de administración preferido de hello de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="ca3b1-106">Azure Load Balancer puede administrarse ahora mediante las herramientas y las API basadas en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="ca3b1-107">Conceptos</span><span class="sxs-lookup"><span data-stu-id="ca3b1-107">Concepts</span></span>

<span data-ttu-id="ca3b1-108">Con el Administrador de recursos, el equilibrador de carga de Azure contiene Hola recursos secundarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="ca3b1-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="ca3b1-109">Configuración de dirección IP front-end: un equilibrador de carga puede incluir una o varias direcciones IP front-end, conocidas también como IP virtuales (VIP).</span><span class="sxs-lookup"><span data-stu-id="ca3b1-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="ca3b1-110">Estas direcciones IP servir como entrada para el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="ca3b1-111">Grupo de direcciones de back-end: se trata de direcciones IP asociadas a la máquina virtual de Hola se distribuirá carga toowhich tarjeta de interfaz de red (NIC).</span><span class="sxs-lookup"><span data-stu-id="ca3b1-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="ca3b1-112">Reglas de equilibrio de carga: una propiedad de regla asigna una dirección IP determinada front-end y puerto conjunto tooa de combinación de direcciones IP de back-end y combinación de puerto.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="ca3b1-113">Un solo equilibrador de carga puede tener varias reglas de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="ca3b1-114">Cada regla tiene una combinación de una IP de front-end y un puerto y una IP de back-end asociados a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="ca3b1-115">Sondeos: sondeos permiten tookeep realizar un seguimiento del estado de Hola de instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="ca3b1-116">Si se produce un error en un sondeo de estado, instancia de máquina virtual de hello le llevará automáticamente fuera de la rotación.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="ca3b1-117">Las reglas NAT de entrada: las reglas NAT definir Hola tráfico entrante que fluyen a través de IP de front-end de Hola y distribuida toohello volver terminar IP.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="ca3b1-118">Plantillas de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="ca3b1-118">Quickstart templates</span></span>

<span data-ttu-id="ca3b1-119">Azure Resource Manager le permite tooprovision las aplicaciones utilizando una plantilla declarativa.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="ca3b1-120">En una plantilla, puede implementar varios servicios junto con sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="ca3b1-121">Usar hello mismo toorepeatedly plantilla implementar la aplicación durante cada fase del ciclo de vida de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="ca3b1-122">Las plantillas pueden incluir definiciones de máquinas virtuales, redes virtuales, conjuntos de disponibilidad, interfaces de red (NIC), cuentas de almacenamiento, equilibradores de carga, grupos de seguridad de red y direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="ca3b1-123">Con las plantillas puede crear todo lo que necesita para una aplicación compleja.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="ca3b1-124">archivo de plantilla de Hello pueda proteger en el sistema de administración de contenido para control de versiones y la colaboración.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="ca3b1-125">Más información sobre las plantillas</span><span class="sxs-lookup"><span data-stu-id="ca3b1-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="ca3b1-126">Más información sobre los recursos de red</span><span class="sxs-lookup"><span data-stu-id="ca3b1-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="ca3b1-127">Las plantillas de inicio rápido que usan Azure Load Balancer se pueden encontrar en un [repositorio de GitHub](https://github.com/Azure/azure-quickstart-templates) que hospeda un conjunto de plantillas generadas por la comunidad.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="ca3b1-128">Ejemplos de plantillas:</span><span class="sxs-lookup"><span data-stu-id="ca3b1-128">Examples of templates:</span></span>

* [<span data-ttu-id="ca3b1-129">Dos máquinas virtuales en un Equilibrador de carga y reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="ca3b1-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="ca3b1-130">Dos máquinas virtuales en una red virtual con un Equilibrador de carga interno y reglas del Equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="ca3b1-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="ca3b1-131">2 máquinas virtuales en un equilibrador de carga y configurar las reglas NAT en hello LB</span><span class="sxs-lookup"><span data-stu-id="ca3b1-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="ca3b1-132">Configuración del Equilibrador de carga de Azure con PowerShell o CLI</span><span class="sxs-lookup"><span data-stu-id="ca3b1-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="ca3b1-133">Introducción a los cmdlets de Azure Resource Manager, las herramientas de línea de comandos y las API de REST</span><span class="sxs-lookup"><span data-stu-id="ca3b1-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="ca3b1-134">[Cmdlets de redes de Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) puede ser toocreate usa un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="ca3b1-135">¿Cómo toocreate un equilibrador de carga con el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="ca3b1-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="ca3b1-136">Uso de hello CLI de Azure con administración de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="ca3b1-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="ca3b1-137">API de REST del Equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="ca3b1-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="ca3b1-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca3b1-138">Next steps</span></span>

<span data-ttu-id="ca3b1-139">También puede [empezar a crear un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento especifico del tráfico de red del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="ca3b1-140">Obtenga información acerca de cómo toomanage [inactivo de la configuración de tiempo de espera TCP para un equilibrador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="ca3b1-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="ca3b1-141">Esto es importante cuando la aplicación necesita que las conexiones de tookeep activo para servidores detrás de un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="ca3b1-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>

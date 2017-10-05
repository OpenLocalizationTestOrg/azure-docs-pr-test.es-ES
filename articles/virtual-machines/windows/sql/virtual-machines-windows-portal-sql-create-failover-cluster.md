---
title: 'FCI de SQL Server: Azure Virtual Machines | Microsoft Docs'
description: "En este artículo se explica cómo crear una instancia de clúster de conmutación por error de SQL Server en Azure Virtual Machines."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 439353b7d22fb7376049ea8e1433a8d5840d3e0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="3a089-103">Configuración de una instancia de clúster de conmutación por error de SQL Server en Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="3a089-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="3a089-104">En este artículo se explica cómo crear una instancia de clúster de conmutación por error (FCI) de SQL Server en Azure Virtual Machines con el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3a089-104">This article explains how to create a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="3a089-105">Esta solución usa [Espacios de almacenamiento directo \(S2D\) de Windows Server 2016 Datacenter Edition ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) como una SAN virtual de software que sincroniza el almacenamiento (discos de datos) entre los nodos (máquinas virtuales de Azure) de Windows Cluster.</span><span class="sxs-lookup"><span data-stu-id="3a089-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes the storage (data disks) between the nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="3a089-106">S2D es una novedad de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3a089-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="3a089-107">El siguiente diagrama muestra la solución completa en máquinas virtuales de Azure:</span><span class="sxs-lookup"><span data-stu-id="3a089-107">The following diagram shows the complete solution on Azure virtual machines:</span></span>

![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="3a089-109">El diagrama anterior muestra:</span><span class="sxs-lookup"><span data-stu-id="3a089-109">The preceding diagram shows:</span></span>

- <span data-ttu-id="3a089-110">Dos máquinas virtuales de Azure en un clúster de conmutación por error de Windows.</span><span class="sxs-lookup"><span data-stu-id="3a089-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="3a089-111">Cuando una máquina virtual está en un clúster de conmutación por error también se denomina un *nodo de clúster* o *nodos*.</span><span class="sxs-lookup"><span data-stu-id="3a089-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="3a089-112">Cada máquina virtual tiene dos, o más, discos de datos.</span><span class="sxs-lookup"><span data-stu-id="3a089-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="3a089-113">S2D sincroniza los datos del disco de datos y presenta el almacenamiento sincronizado como grupo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3a089-113">S2D synchronizes the data on the data disk and presents the synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="3a089-114">El grupo de almacenamiento presenta un volumen compartido de clúster (CSV) al clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="3a089-114">The storage pool presents a cluster shared volume (CSV) to the failover cluster.</span></span>
- <span data-ttu-id="3a089-115">El rol de clúster de FCI de SQL Server usa el CSV para las unidades de datos.</span><span class="sxs-lookup"><span data-stu-id="3a089-115">The SQL Server FCI cluster role uses the CSV for the data drives.</span></span>
- <span data-ttu-id="3a089-116">Un equilibrador de carga de Azure que almacene la dirección IP para la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-116">An Azure load balancer to hold the IP address for the SQL Server FCI.</span></span>
- <span data-ttu-id="3a089-117">Un conjunto de disponibilidad de Azure contiene todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="3a089-117">An Azure availability set holds all the resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="3a089-118">Todos los recursos de Azure que están en el diagrama se encuentran en el mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3a089-118">All Azure resources are in the diagram are in the same resource group.</span></span>

<span data-ttu-id="3a089-119">Para más información acerca de S2D, consulte [Espacios de almacenamiento directo \(S2D\) de Windows Server 2016 Datacenter Edition](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="3a089-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="3a089-120">S2D admite dos tipos de arquitecturas, convergidas e hiperconvergidas.</span><span class="sxs-lookup"><span data-stu-id="3a089-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="3a089-121">La arquitectura de este documento es hiperconvergida.</span><span class="sxs-lookup"><span data-stu-id="3a089-121">The architecture in this document is hyper-converged.</span></span> <span data-ttu-id="3a089-122">Las infraestructuras hiperconvergidas colocan el almacenamiento en los mismos servidores que hospedan la aplicación en clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-122">A hyper-converged infrastructure places the storage on the same servers that host the clustered application.</span></span> <span data-ttu-id="3a089-123">En esta arquitectura, el almacenamiento se realiza en cada nodo de FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-123">In this architecture, the storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="3a089-124">Plantilla de Azure de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3a089-124">Example Azure template</span></span>

<span data-ttu-id="3a089-125">Puede crear toda la solución en Azure a partir de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="3a089-125">You can create the entire solution in Azure from a template.</span></span> <span data-ttu-id="3a089-126">Un ejemplo de una plantilla está disponible en las [plantillas de inicio rápido de Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad) de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3a089-126">An example of a template is available in the GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="3a089-127">Este ejemplo no se ha diseñado para ninguna carga de trabajo específica ni se ha probado para ella.</span><span class="sxs-lookup"><span data-stu-id="3a089-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="3a089-128">Puede ejecutar la plantilla para crear una FCI de SQL Server con almacenamiento S2D conectado a su dominio.</span><span class="sxs-lookup"><span data-stu-id="3a089-128">You can run the template to create a SQL Server FCI with S2D storage connected to your domain.</span></span> <span data-ttu-id="3a089-129">Puede evaluar la plantilla y modificarla para adecuarla a sus fines.</span><span class="sxs-lookup"><span data-stu-id="3a089-129">You can evaluate the template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3a089-130">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3a089-130">Before you begin</span></span>

<span data-ttu-id="3a089-131">Antes de continuar, es preciso que sepa varias cosas y otras que deben estar en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3a089-131">There are a few things you need to know and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-to-know"></a><span data-ttu-id="3a089-132">Lo que necesita saber</span><span class="sxs-lookup"><span data-stu-id="3a089-132">What to know</span></span>
<span data-ttu-id="3a089-133">Debe estar familiarizado con el funcionamiento de las siguientes tecnologías:</span><span class="sxs-lookup"><span data-stu-id="3a089-133">You should have an operational understanding of the following technologies:</span></span>

- [<span data-ttu-id="3a089-134">Tecnologías de clúster de Windows</span><span class="sxs-lookup"><span data-stu-id="3a089-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="3a089-135">[Instancias del clúster de conmutación por error de SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a089-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="3a089-136">También debe tener conocimientos generales de las siguientes tecnologías:</span><span class="sxs-lookup"><span data-stu-id="3a089-136">Also, you should have a general understanding of the following technologies:</span></span>

- [<span data-ttu-id="3a089-137">Solución hiperconvergida con Espacios de almacenamiento directo en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3a089-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="3a089-138">Grupos de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="3a089-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-to-have"></a><span data-ttu-id="3a089-139">Lo que debe tener</span><span class="sxs-lookup"><span data-stu-id="3a089-139">What to have</span></span>

<span data-ttu-id="3a089-140">Para poder seguir las instrucciones de este artículo, debe tener:</span><span class="sxs-lookup"><span data-stu-id="3a089-140">Before following the instructions in this article, you should already have:</span></span>

- <span data-ttu-id="3a089-141">Una suscripción de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3a089-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="3a089-142">Un dominio de Windows en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a089-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="3a089-143">Una cuenta con permiso para crear objetos en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a089-143">An account with permission to create objects in the Azure virtual machine.</span></span>
- <span data-ttu-id="3a089-144">Una red virtual de Azure y una subred con espacio de direcciones IP suficiente para los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="3a089-144">An Azure virtual network and subnet with sufficient IP address space for the following components:</span></span>
   - <span data-ttu-id="3a089-145">Ambas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-145">Both virtual machines.</span></span>
   - <span data-ttu-id="3a089-146">La dirección IP del clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="3a089-146">The failover cluster IP address.</span></span>
   - <span data-ttu-id="3a089-147">Una dirección IP para cada FCI.</span><span class="sxs-lookup"><span data-stu-id="3a089-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="3a089-148">DNS configurado en la red de Azure que señala a los controladores de dominio.</span><span class="sxs-lookup"><span data-stu-id="3a089-148">DNS configured on the Azure Network, pointing to the domain controllers.</span></span>

<span data-ttu-id="3a089-149">Una vez que cumpla los requisitos previos, puede pasar a la creación de un clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="3a089-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="3a089-150">El primer paso es crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-150">The first step is to create the virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="3a089-151">Paso 1: Crear máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="3a089-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="3a089-152">Inicie sesión en [Azure Portal](http://portal.azure.com) con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="3a089-152">Log in to the [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="3a089-153">[Cree un conjunto de disponibilidad de Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="3a089-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="3a089-154">El conjunto de disponibilidad agrupa las máquinas virtuales en dominios de error y dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="3a089-154">The availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="3a089-155">Sirve para garantizar que la aplicación no resulta afectada por puntos únicos de error, como el conmutador de red o la fuente de alimentación de un conjunto de servidores.</span><span class="sxs-lookup"><span data-stu-id="3a089-155">The availability set makes sure that your application is not affected by single points of failure, like the network switch or the power unit of a rack of servers.</span></span>

   <span data-ttu-id="3a089-156">Si no ha creado el grupo de recursos para las máquinas virtuales, hágalo al crear un conjunto de disponibilidad de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a089-156">If you have not created the resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="3a089-157">Si va a usar Azure Portal para crear el conjunto de disponibilidad, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3a089-157">If you're using the Azure portal to create the availability set, do the following steps:</span></span>

   - <span data-ttu-id="3a089-158">En Azure Portal, haga clic en **+** para abrir Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3a089-158">In the Azure portal, click **+** to open the Azure Marketplace.</span></span> <span data-ttu-id="3a089-159">Busque **Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="3a089-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="3a089-160">Haga clic en **Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="3a089-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="3a089-161">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3a089-161">Click **Create**.</span></span>
   - <span data-ttu-id="3a089-162">En la hoja **Crear conjunto de disponibilidad**, configure los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="3a089-162">On the **Create availability set** blade, set the following values:</span></span>
      - <span data-ttu-id="3a089-163">**Nombre**: nombre del conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="3a089-163">**Name**: A name for the availability set.</span></span>
      - <span data-ttu-id="3a089-164">**Suscripción**: su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="3a089-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="3a089-165">**Grupo de recursos**: si desea utilizar un grupo existente, haga clic en **Usar existente** y seleccione el grupo en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="3a089-165">**Resource group**: If you want to use an existing group, click **Use existing** and select the group from the drop-down list.</span></span> <span data-ttu-id="3a089-166">De lo contrario, elija **Crear nuevo** y escriba el nombre del grupo.</span><span class="sxs-lookup"><span data-stu-id="3a089-166">Otherwise choose **Create New** and type a name for the group.</span></span>
      - <span data-ttu-id="3a089-167">**Ubicación**: establezca la ubicación en la que planea crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-167">**Location**: Set the location where you plan to create your virtual machines.</span></span>
      - <span data-ttu-id="3a089-168">**Dominios de error**: use el valor predeterminado (3).</span><span class="sxs-lookup"><span data-stu-id="3a089-168">**Fault domains**: Use the default (3).</span></span>
      - <span data-ttu-id="3a089-169">**Dominios de actualización**: use el valor predeterminado (5).</span><span class="sxs-lookup"><span data-stu-id="3a089-169">**Update domains**: Use the default (5).</span></span>
   - <span data-ttu-id="3a089-170">Haga clic en **Crear** para crear el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="3a089-170">Click **Create** to create the availability set.</span></span>

1. <span data-ttu-id="3a089-171">Cree las máquinas virtuales en el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="3a089-171">Create the virtual machines in the availability set.</span></span>

   <span data-ttu-id="3a089-172">Aprovisionar dos máquinas virtuales de SQL Server en el conjunto de disponibilidad de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a089-172">Provision two SQL Server virtual machines in the Azure availability set.</span></span> <span data-ttu-id="3a089-173">Para conocer las instrucciones, consulte [Aprovisionamiento de una máquina virtual de SQL Server en Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="3a089-173">For instructions, see [Provision a SQL Server virtual machine in the Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="3a089-174">Coloque ambas máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="3a089-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="3a089-175">En el mismo grupo de recursos de Azure en el que se encuentra su conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="3a089-175">In the same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="3a089-176">En la misma red que el controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="3a089-176">On the same network as your domain controller.</span></span>
   - <span data-ttu-id="3a089-177">En una subred con suficiente espacio de direcciones IP para ambas máquinas virtuales y todas las FCI que finalmente puede utilizar en este clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="3a089-178">En el conjunto de disponibilidad de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a089-178">In the Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="3a089-179">Una vez creada una máquina virtual el conjunto de disponibilidad no se puede establecer o cambiar.</span><span class="sxs-lookup"><span data-stu-id="3a089-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="3a089-180">Elija una imagen en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3a089-180">Choose an image from the Azure Marketplace.</span></span> <span data-ttu-id="3a089-181">Puede usar una imagen de Marketplace que incluya Windows Server y SQL Server, o solo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just the Windows Server.</span></span> <span data-ttu-id="3a089-182">Para más información, consulte [Información general de SQL Server en máquinas virtuales de Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3a089-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="3a089-183">Las imágenes oficiales de SQL Server de la galería de Azure incluyen una instancia de SQL Server instalada, más el software de instalación de SQL Server y la clave necesaria.</span><span class="sxs-lookup"><span data-stu-id="3a089-183">The official SQL Server images in the Azure Gallery include an installed SQL Server instance, plus the SQL Server installation software, and the required key.</span></span>

   <span data-ttu-id="3a089-184">Elija la imagen correcta en función de cómo desea pagar la licencia de SQL Server:</span><span class="sxs-lookup"><span data-stu-id="3a089-184">Choose the right image according to how you want to pay for the SQL Server license:</span></span>

   - <span data-ttu-id="3a089-185">**Pay per usage licensing** (Licencia de pago por uso): el costo por minuto de estas imágenes incluye la licencia de SQL Server:</span><span class="sxs-lookup"><span data-stu-id="3a089-185">**Pay per usage licensing**: The per-minute cost of these images includes the SQL Server licensing:</span></span>
      - <span data-ttu-id="3a089-186">**SQL Server 2016 Enterprise en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="3a089-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="3a089-187">**SQL Server 2016 Standard en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="3a089-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="3a089-188">**SQL Server 2016 Developer en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="3a089-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="3a089-189">**Traiga su propia licencia (BYOL)**</span><span class="sxs-lookup"><span data-stu-id="3a089-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="3a089-190">**{BYOL} SQL Server 2016 Enterprise en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="3a089-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="3a089-191">**{BYOL} SQL Server 2016 Standard en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="3a089-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="3a089-192">Después de crear la máquina virtual, quite la instancia de SQL Server independiente preinstalada.</span><span class="sxs-lookup"><span data-stu-id="3a089-192">After you create the virtual machine, remove the pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="3a089-193">Tras configurar el clúster de conmutación por error y S2D, tendrá que usar los medios de SQL Server preinstalado para crear la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-193">You will use the pre-installed SQL Server media to create the SQL Server FCI after you configure the failover cluster and S2D.</span></span>

   <span data-ttu-id="3a089-194">Como alternativa, puede utilizar imágenes de Azure Marketplace que solo tienen el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3a089-194">Alternatively, you can use Azure Marketplace images with just the operating system.</span></span> <span data-ttu-id="3a089-195">Elija una imagen de **Windows Server 2016 Datacenter** e instale la FCI de SQL Server después de configurar el clúster de conmutación por error y S2D.</span><span class="sxs-lookup"><span data-stu-id="3a089-195">Choose a **Windows Server 2016 Datacenter** image and install the SQL Server FCI after you configure the failover cluster and S2D.</span></span> <span data-ttu-id="3a089-196">Esta imagen no contiene los medios de instalación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="3a089-197">Coloque los medios de instalación en una ubicación en la que pueda ejecutar la instalación de SQL Server para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="3a089-197">Place the installation media in a location where you can run the SQL Server installation for each server.</span></span>

1. <span data-ttu-id="3a089-198">Una vez que Azure cree las máquinas virtuales, conéctese a cada una de ellas con RDP.</span><span class="sxs-lookup"><span data-stu-id="3a089-198">After Azure creates your virtual machines, connect to each virtual machine with RDP.</span></span>

   <span data-ttu-id="3a089-199">La primera vez que se conecte a una máquina virtual con RDP, el equipo le pregunta si desea permitir que este equipo se pueda detectar en la red.</span><span class="sxs-lookup"><span data-stu-id="3a089-199">When you first connect to a virtual machine with RDP, the computer asks if you want to allow this PC to be discoverable on the network.</span></span> <span data-ttu-id="3a089-200">Haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="3a089-200">Click **Yes**.</span></span>

1. <span data-ttu-id="3a089-201">Si utiliza una de las imágenes de máquina virtual basada en SQL Server, quite la instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-201">If you are using one of the SQL Server-based virtual machine images, remove the SQL Server instance.</span></span>

   - <span data-ttu-id="3a089-202">En **Programas y características**, haga clic con el botón derecho en **Microsoft SQL Server 2016 (64 bits)** y haga clic en **Desinstalar o cambiar**.</span><span class="sxs-lookup"><span data-stu-id="3a089-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="3a089-203">Haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="3a089-203">Click **Remove**.</span></span>
   - <span data-ttu-id="3a089-204">Seleccione la instancia predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3a089-204">Select the default instance.</span></span>
   - <span data-ttu-id="3a089-205">Quite todas las características en **Servicios de motor de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="3a089-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="3a089-206">No quite **Características compartidas**.</span><span class="sxs-lookup"><span data-stu-id="3a089-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="3a089-207">Vea la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="3a089-207">See the following picture:</span></span>

      ![Quitar características](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="3a089-209">Haga clic en **Siguiente** y, después, en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="3a089-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="3a089-210"><a name="ports"></a>Abra los puertos del firewall.</span><span class="sxs-lookup"><span data-stu-id="3a089-210"><a name="ports"></a>Open the firewall ports.</span></span>

   <span data-ttu-id="3a089-211">En cada máquina virtual, abra los siguientes puertos de Firewall de Windows.</span><span class="sxs-lookup"><span data-stu-id="3a089-211">On each virtual machine, open the following ports on the Windows Firewall.</span></span>

   | <span data-ttu-id="3a089-212">Propósito</span><span class="sxs-lookup"><span data-stu-id="3a089-212">Purpose</span></span> | <span data-ttu-id="3a089-213">Puerto TCP</span><span class="sxs-lookup"><span data-stu-id="3a089-213">TCP Port</span></span> | <span data-ttu-id="3a089-214">Notas</span><span class="sxs-lookup"><span data-stu-id="3a089-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="3a089-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3a089-215">SQL Server</span></span> | <span data-ttu-id="3a089-216">1433</span><span class="sxs-lookup"><span data-stu-id="3a089-216">1433</span></span> | <span data-ttu-id="3a089-217">Puerto normal para las instancias predeterminadas de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="3a089-218">Si usó una imagen de la galería, este puerto se abre automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3a089-218">If you used an image from the gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="3a089-219">Sondeo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="3a089-219">Health probe</span></span> | <span data-ttu-id="3a089-220">59999</span><span class="sxs-lookup"><span data-stu-id="3a089-220">59999</span></span> | <span data-ttu-id="3a089-221">Cualquier puerto TCP abierto.</span><span class="sxs-lookup"><span data-stu-id="3a089-221">Any open TCP port.</span></span> <span data-ttu-id="3a089-222">En un paso posterior, configure el [sondeo de mantenimiento](#probe) del equilibrador de carga y el clúster para usar este puerto.</span><span class="sxs-lookup"><span data-stu-id="3a089-222">In a later step, configure the load balancer [health probe](#probe) and the cluster to use this port.</span></span>  

1. <span data-ttu-id="3a089-223">Agregue almacenamiento a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a089-223">Add storage to the virtual machine.</span></span> <span data-ttu-id="3a089-224">Para más información, consulte [Almacenamiento premium: almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3a089-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="3a089-225">Ambas máquinas virtuales necesitan al menos dos discos de datos.</span><span class="sxs-lookup"><span data-stu-id="3a089-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="3a089-226">Conecte discos sin procesar (discos cuyo formato no es NTFS).</span><span class="sxs-lookup"><span data-stu-id="3a089-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="3a089-227">Si conecta discos con formato NTFS, solo puede habilitar S2D sin comprobación de la idoneidad del disco.</span><span class="sxs-lookup"><span data-stu-id="3a089-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="3a089-228">Conecte un mínimo de dos Premium Storage (discos SSD) a cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a089-228">Attach a minimum of two Premium Storage (SSD disks) to each VM.</span></span> <span data-ttu-id="3a089-229">Se recomienda usar, como mínimo, discos P30 (1 TB).</span><span class="sxs-lookup"><span data-stu-id="3a089-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="3a089-230">Establezca el almacenamiento en caché de host como **de solo lectura**.</span><span class="sxs-lookup"><span data-stu-id="3a089-230">Set host caching to **Read-only**.</span></span>

   <span data-ttu-id="3a089-231">La capacidad de almacenamiento que se utiliza en los entornos de producción depende de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3a089-231">The storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="3a089-232">Los valores que se describen en este artículo son para demostración y pruebas.</span><span class="sxs-lookup"><span data-stu-id="3a089-232">The values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="3a089-233">[Agregue las máquinas virtuales a un dominio preexistente](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="3a089-233">[Add the virtual machines to your pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="3a089-234">Después de crear y configurar las máquinas virtuales, puede configurar el clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="3a089-234">After the virtual machines are created and configured, you can configure the failover cluster.</span></span>

## <a name="step-2-configure-the-windows-failover-cluster-with-s2d"></a><span data-ttu-id="3a089-235">Paso 2: Configurar el clúster de conmutación por error de Windows con S2D</span><span class="sxs-lookup"><span data-stu-id="3a089-235">Step 2: Configure the Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="3a089-236">El siguiente paso es configurar el clúster de conmutación por error con S2D.</span><span class="sxs-lookup"><span data-stu-id="3a089-236">The next step is to configure the failover cluster with S2D.</span></span> <span data-ttu-id="3a089-237">En este paso, realizará los siguientes pasos secundarios:</span><span class="sxs-lookup"><span data-stu-id="3a089-237">In this step, you will do the following substeps:</span></span>

1. <span data-ttu-id="3a089-238">Agregue la característica Agrupación en clústeres de conmutación por error de Windows</span><span class="sxs-lookup"><span data-stu-id="3a089-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="3a089-239">Validación del clúster</span><span class="sxs-lookup"><span data-stu-id="3a089-239">Validate the cluster</span></span>
1. <span data-ttu-id="3a089-240">Creación del clúster de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="3a089-240">Create the failover cluster</span></span>
1. <span data-ttu-id="3a089-241">Cree el testigo en la nube</span><span class="sxs-lookup"><span data-stu-id="3a089-241">Create the cloud witness</span></span>
1. <span data-ttu-id="3a089-242">Agregue almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3a089-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="3a089-243">Agregue la característica Agrupación en clústeres de conmutación por error de Windows</span><span class="sxs-lookup"><span data-stu-id="3a089-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="3a089-244">Para empezar, conéctese a la primera máquina virtual con RDP mediante una cuenta de dominio que sea miembro de los administradores locales y tenga permisos para crear objetos en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3a089-244">To begin, connect to the first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions to create objects in Active Directory.</span></span> <span data-ttu-id="3a089-245">Utilice esta cuenta para el resto de la configuración.</span><span class="sxs-lookup"><span data-stu-id="3a089-245">Use this account for the rest of the configuration.</span></span>

1. <span data-ttu-id="3a089-246">[Agregue la característica Clústeres de conmutación por error a todas las máquinas virtuales](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="3a089-246">[Add Failover Clustering feature to each virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="3a089-247">Para instalar la característica Clústeres de conmutación por error desde la interfaz de usuario, realice los pasos siguientes en las dos máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-247">To install Failover Clustering feature from the UI, do the following steps on both virtual machines.</span></span>
   - <span data-ttu-id="3a089-248">En **Administrador del servidor**, haga clic en **Administrar** y, después, en **Agregar roles y características**.</span><span class="sxs-lookup"><span data-stu-id="3a089-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="3a089-249">En **Asistente para agregar roles y características**, haga clic en **Siguiente** hasta llegar a **Seleccionar características**.</span><span class="sxs-lookup"><span data-stu-id="3a089-249">In **Add Roles and Features Wizard**, click **Next** until you get to **Select Features**.</span></span>
   - <span data-ttu-id="3a089-250">En **Seleccionar características**, haga clic en **Clústeres de conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="3a089-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="3a089-251">Incluya todas las características y herramientas de administración requeridas.</span><span class="sxs-lookup"><span data-stu-id="3a089-251">Include all required features and the management tools.</span></span> <span data-ttu-id="3a089-252">Haga clic en **Agregar características**.</span><span class="sxs-lookup"><span data-stu-id="3a089-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="3a089-253">Haga clic en **Siguiente** y, después, en **Finalizar** para instalar las características.</span><span class="sxs-lookup"><span data-stu-id="3a089-253">Click **Next** and then click **Finish** to install the features.</span></span>

   <span data-ttu-id="3a089-254">Para instalar la característica Clústeres de conmutación por error con PowerShell, ejecute el siguiente script en una sesión de PowerShell de administrador de una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-254">To install the Failover Clustering feature with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="3a089-255">A modo de referencia, en los siguientes pasos se siguen las instrucciones del paso 3 de [Solución hiperconvergida con Espacios de almacenamiento directo en Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="3a089-255">For reference, the next steps follow the instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-the-cluster"></a><span data-ttu-id="3a089-256">Validación del clúster</span><span class="sxs-lookup"><span data-stu-id="3a089-256">Validate the cluster</span></span>

<span data-ttu-id="3a089-257">En esta guía se hace referencia a las instrucciones en [validar clúster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="3a089-257">This guide refers to instructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="3a089-258">Valide el clúster en la interfaz de usuario o con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a089-258">Validate the cluster in the UI or with PowerShell.</span></span>

<span data-ttu-id="3a089-259">Para validar el clúster con la interfaz de usuario, realice los pasos siguientes en una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-259">To validate the cluster with the UI, do the following steps from one of the virtual machines.</span></span>

1. <span data-ttu-id="3a089-260">En **Administrador del servidor**, haga clic en **Herramientas** y, después, en **Administrador de clústeres de conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="3a089-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="3a089-261">En **Administrador de clústeres de conmutación por error**, haga clic en **Acción** y, después, en **Validar configuración...**.</span><span class="sxs-lookup"><span data-stu-id="3a089-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="3a089-262">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a089-262">Click **Next**.</span></span>
1. <span data-ttu-id="3a089-263">En **Seleccionar servidores o un clúster**, escriba el nombre de ambas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-263">On **Select Servers or a Cluster**, type the name of both virtual machines.</span></span>
1. <span data-ttu-id="3a089-264">En **Opciones de pruebas**, elija **Ejecutar solo las pruebas que seleccione**.</span><span class="sxs-lookup"><span data-stu-id="3a089-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="3a089-265">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a089-265">Click **Next**.</span></span>
1. <span data-ttu-id="3a089-266">En **Selección de pruebas**, incluya todas las pruebas, excepto **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="3a089-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="3a089-267">Vea la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="3a089-267">See the following picture:</span></span>

   ![Pruebas de validación](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="3a089-269">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a089-269">Click **Next**.</span></span>
1. <span data-ttu-id="3a089-270">En **Confirmación**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a089-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="3a089-271">El **Asistente para validar una configuración** ejecuta las pruebas de validación.</span><span class="sxs-lookup"><span data-stu-id="3a089-271">The **Validate a Configuration Wizard** runs the validation tests.</span></span>

<span data-ttu-id="3a089-272">Para validar el clúster con PowerShell, ejecute el siguiente script en una sesión de PowerShell de administrador de una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-272">To validate the cluster with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="3a089-273">Después de validar el clúster, cree el clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="3a089-273">After you validate the cluster, create the failover cluster.</span></span>

### <a name="create-the-failover-cluster"></a><span data-ttu-id="3a089-274">Creación del clúster de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="3a089-274">Create the failover cluster</span></span>

<span data-ttu-id="3a089-275">Esta guía hace referencia a la [Creación del clúster de conmutación por error](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="3a089-275">This guide refers to [Create the failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="3a089-276">Para crear el clúster de conmutación por error, necesita:</span><span class="sxs-lookup"><span data-stu-id="3a089-276">To create the failover cluster, you need:</span></span>
- <span data-ttu-id="3a089-277">Los nombres de las máquinas virtuales que se convierten en nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-277">The names of the virtual machines that become the cluster nodes.</span></span>
- <span data-ttu-id="3a089-278">Un nombre para el clúster de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="3a089-278">A name for the failover cluster</span></span>
- <span data-ttu-id="3a089-279">Una dirección IP para el clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="3a089-279">An IP address for the failover cluster.</span></span> <span data-ttu-id="3a089-280">Puede usar una dirección IP que no se utilice en la misma red virtual de Azure y subred como nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-280">You can use an IP address that is not used on the same Azure virtual network and subnet as the cluster nodes.</span></span>

<span data-ttu-id="3a089-281">El siguiente PowerShell crea un clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="3a089-281">The following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="3a089-282">Actualice el script con los nombres de los nodos (los nombres de las máquinas virtuales) y una dirección IP disponible desde la red virtual de Azure:</span><span class="sxs-lookup"><span data-stu-id="3a089-282">Update the script with the names of the nodes (the virtual machine names) and an available IP address from the Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="3a089-283">Creación de un testigo en la nube</span><span class="sxs-lookup"><span data-stu-id="3a089-283">Create a cloud witness</span></span>

<span data-ttu-id="3a089-284">Testigo en la nube es un nuevo tipo de testigo de quórum de clúster almacenado en una instancia de Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="3a089-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="3a089-285">Esto elimina la necesidad de que una máquina virtual independiente hospede un recurso compartido testigo.</span><span class="sxs-lookup"><span data-stu-id="3a089-285">This removes the need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="3a089-286">[Cree un testigo en la nube para el clúster de conmutación por error](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="3a089-286">[Create a cloud witness for the failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="3a089-287">Cree un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="3a089-287">Create a blob container.</span></span>

1. <span data-ttu-id="3a089-288">Guarde las claves de acceso y la dirección URL del contenedor.</span><span class="sxs-lookup"><span data-stu-id="3a089-288">Save the access keys and the container URL.</span></span>

1. <span data-ttu-id="3a089-289">Configure el testigo de quórum de clúster del clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="3a089-289">Configure the failover cluster cluster quorum witness.</span></span> <span data-ttu-id="3a089-290">Vea, [Configuración del testigo de quórum en la interfaz de usuario]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="3a089-290">See, [Configure the quorum witness in the user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in the UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="3a089-291">Agregue almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3a089-291">Add storage</span></span>

<span data-ttu-id="3a089-292">Los discos de S2D deben estar vacío y no pueden tener particiones ni otros datos.</span><span class="sxs-lookup"><span data-stu-id="3a089-292">The disks for S2D need to be empty and without partitions or other data.</span></span> <span data-ttu-id="3a089-293">Para limpiar los discos siga [los pasos de esta guía](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="3a089-293">To clean disks follow [the steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="3a089-294">[Habilite Espacios de almacenamiento directo \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="3a089-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="3a089-295">El siguiente comando de PowerShell habilita los espacios de almacenamiento directo.</span><span class="sxs-lookup"><span data-stu-id="3a089-295">The following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="3a089-296">En **Administrador de clústeres de conmutación por error**, puede ver el grupo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3a089-296">In **Failover Cluster Manager**, you can now see the storage pool.</span></span>

1. <span data-ttu-id="3a089-297">[Cree un volumen](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="3a089-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="3a089-298">Una de las características de S2D es que crea automáticamente un grupo de almacenamiento cuando se habilita.</span><span class="sxs-lookup"><span data-stu-id="3a089-298">One of the features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="3a089-299">Ya está listo para crear un volumen.</span><span class="sxs-lookup"><span data-stu-id="3a089-299">You are now ready to create a volume.</span></span> <span data-ttu-id="3a089-300">El commandlet de PowerShell `New-Volume` automatiza el proceso de creación de volúmenes, lo que incluye la aplicación de formato, la adición al clúster y la creación de un volumen compartido de clúster (CSV).</span><span class="sxs-lookup"><span data-stu-id="3a089-300">The PowerShell commandlet `New-Volume` automates the volume creation process, including formatting, adding to the cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="3a089-301">En el ejemplo siguiente se crea un CSV de 800 gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="3a089-301">The following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="3a089-302">Una vez que se completa este comando, se monta un volumen de 800 GB como recurso del clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="3a089-303">El volumen está en `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="3a089-303">The volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="3a089-304">El siguiente diagrama muestra un volumen compartido de clúster con S2D:</span><span class="sxs-lookup"><span data-stu-id="3a089-304">The following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="3a089-306">Paso 3: Probar la conmutación por error del clúster de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="3a089-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="3a089-307">En Administrador de clústeres de conmutación por error, compruebe que puede mover el recurso de almacenamiento al otro nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-307">In Failover Cluster Manager, verify that you can move the storage resource to the other cluster node.</span></span> <span data-ttu-id="3a089-308">Si se puede conectar al clúster de conmutación por error con **Administrador de clústeres de conmutación por error** y mover el almacenamiento de un nodo al otro, está listo para configurar la FCI.</span><span class="sxs-lookup"><span data-stu-id="3a089-308">If you can connect to the failover cluster with **Failover Cluster Manager** and move the storage from one node to the other, you are ready to configure the FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="3a089-309">Paso 4: Crear la FCI de SQL Server</span><span class="sxs-lookup"><span data-stu-id="3a089-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="3a089-310">Después de haber configurado el clúster de conmutación por error y todos los componentes del clúster, incluido el almacenamiento, puede crear la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-310">After you have configured the failover cluster and all cluster components including storage, you can create the SQL Server FCI.</span></span>

1. <span data-ttu-id="3a089-311">Conéctese a la primera máquina virtual con RDP.</span><span class="sxs-lookup"><span data-stu-id="3a089-311">Connect to the first virtual machine with RDP.</span></span>

1. <span data-ttu-id="3a089-312">En **Administrador de clústeres de conmutación por error**, asegúrese de que todos los recursos principales de clúster estén en la primera máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a089-312">In **Failover Cluster Manager**, make sure all cluster core resources are on the first virtual machine.</span></span> <span data-ttu-id="3a089-313">Si es necesario, mueva todos los recursos a esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a089-313">If necessary, move all resources to this virtual machine.</span></span>

1. <span data-ttu-id="3a089-314">Localice los medios de instalación.</span><span class="sxs-lookup"><span data-stu-id="3a089-314">Locate the installation media.</span></span> <span data-ttu-id="3a089-315">Si la máquina virtual usa una de las imágenes de Azure Marketplace, los medios se encuentran en `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="3a089-315">If the virtual machine uses one of the Azure Marketplace images, the media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="3a089-316">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="3a089-316">Click **Setup**.</span></span>

1. <span data-ttu-id="3a089-317">En **Centro de instalación de SQL Server**, haga clic en **Instalación**.</span><span class="sxs-lookup"><span data-stu-id="3a089-317">In the **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="3a089-318">Haga clic en **Nueva instalación de clúster de conmutación por error de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3a089-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="3a089-319">Siga las instrucciones del asistente para instalar la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-319">Follow the instructions in the wizard to install the SQL Server FCI.</span></span>

   <span data-ttu-id="3a089-320">Es preciso que los directorios de datos de FCI estén en el almacenamiento en clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-320">The FCI data directories need to be on clustered storage.</span></span> <span data-ttu-id="3a089-321">Con S2D, no es un disco compartido, sino un punto de montaje a un volumen en cada servidor.</span><span class="sxs-lookup"><span data-stu-id="3a089-321">With S2D, it's not a shared disk, but a mount point to a volume on each server.</span></span> <span data-ttu-id="3a089-322">S2D sincroniza el volumen entre ambos nodos.</span><span class="sxs-lookup"><span data-stu-id="3a089-322">S2D synchronizes the volume between both nodes.</span></span> <span data-ttu-id="3a089-323">El volumen se presenta al clúster como un volumen compartido de clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-323">The volume is presented to the cluster as a cluster shared volume.</span></span> <span data-ttu-id="3a089-324">Utilice el punto de montaje de CSV para los directorios de datos.</span><span class="sxs-lookup"><span data-stu-id="3a089-324">Use the CSV mount point for the data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="3a089-326">Después de completar al asistente, el programa de instalación instalará una FCI de SQL Server en el primer nodo.</span><span class="sxs-lookup"><span data-stu-id="3a089-326">After you complete the wizard, Setup will install a SQL Server FCI on the first node.</span></span>

1. <span data-ttu-id="3a089-327">Una vez que el programa de instalación instale la FCI en el primer nodo, conéctese al segundo nodo con RDP.</span><span class="sxs-lookup"><span data-stu-id="3a089-327">After Setup successfully installs the FCI on the first node, connect to the second node with RDP.</span></span>

1. <span data-ttu-id="3a089-328">Abra **Centro de instalación de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3a089-328">Open the **SQL Server Installation Center**.</span></span> <span data-ttu-id="3a089-329">Haga clic en **Instalación**.</span><span class="sxs-lookup"><span data-stu-id="3a089-329">Click **Installation**.</span></span>

1. <span data-ttu-id="3a089-330">Haga clic en **Agregar nodo a clúster de conmutación por error de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3a089-330">Click **Add node to a SQL Server failover cluster**.</span></span> <span data-ttu-id="3a089-331">Siga las instrucciones del asistente para instalar el servidor de SQL Server y agregarlo a la FCI.</span><span class="sxs-lookup"><span data-stu-id="3a089-331">Follow the instructions in the wizard to install SQL server and add this server to the FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="3a089-332">Si usó una imagen de la galería de Azure Marketplace con SQL Server, las herramientas de SQL Server estaban incluidas en la imagen.</span><span class="sxs-lookup"><span data-stu-id="3a089-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with the image.</span></span> <span data-ttu-id="3a089-333">Si no usó esta imagen, instale las herramientas de SQL Server por separado.</span><span class="sxs-lookup"><span data-stu-id="3a089-333">If you did not use this image, install the SQL Server tools separately.</span></span> <span data-ttu-id="3a089-334">Consulte [Descarga de SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a089-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="3a089-335">Paso 5: Crear un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="3a089-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="3a089-336">En máquinas virtuales de Azure, los clústeres usan un equilibrador de carga para mantener una dirección IP que es preciso que esté en los nodos de clúster de uno en uno.</span><span class="sxs-lookup"><span data-stu-id="3a089-336">On Azure virtual machines, clusters use a load balancer to hold an IP address that needs to be on one cluster node at a time.</span></span> <span data-ttu-id="3a089-337">En esta solución, el equilibrador de carga que retiene la dirección IP para la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-337">In this solution, the load balancer holds the IP address for the SQL Server FCI.</span></span>

<span data-ttu-id="3a089-338">[Creación y configuración de un equilibrador de carga de Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="3a089-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="3a089-339">Creación del equilibrador de carga en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3a089-339">Create the load balancer in the Azure portal</span></span>

<span data-ttu-id="3a089-340">Para crear el equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="3a089-340">To create the load balancer:</span></span>

1. <span data-ttu-id="3a089-341">En Azure Portal, vaya al grupo de recursos con las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-341">In the Azure portal, go to the Resource Group with the virtual machines.</span></span>

1. <span data-ttu-id="3a089-342">Haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3a089-342">Click **+ Add**.</span></span> <span data-ttu-id="3a089-343">Busque **Equilibrador de carga** en Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3a089-343">Search the Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="3a089-344">Haga clic en **Equilibrador de carga**.</span><span class="sxs-lookup"><span data-stu-id="3a089-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="3a089-345">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3a089-345">Click **Create**.</span></span>

1. <span data-ttu-id="3a089-346">Configure el equilibrador de carga con:</span><span class="sxs-lookup"><span data-stu-id="3a089-346">Configure the load balancer with:</span></span>

   - <span data-ttu-id="3a089-347">**Nombre**: un nombre que identifica el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3a089-347">**Name**: A name that identifies the load balancer.</span></span>
   - <span data-ttu-id="3a089-348">**Tipo**: el equilibrador de carga puede ser público o privado.</span><span class="sxs-lookup"><span data-stu-id="3a089-348">**Type**: The load balancer can be either public or private.</span></span> <span data-ttu-id="3a089-349">A los equilibradores de carga privados se puede acceder desde la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="3a089-349">A private load balancer can be accessed from within the same VNET.</span></span> <span data-ttu-id="3a089-350">La mayoría de las aplicaciones de Azure pueden usar un equilibrador de carga privado.</span><span class="sxs-lookup"><span data-stu-id="3a089-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="3a089-351">Si la aplicación necesita acceder a SQL Server directamente a través de Internet, utilice un equilibrador de carga público.</span><span class="sxs-lookup"><span data-stu-id="3a089-351">If your application needs access to SQL Server directly over the Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="3a089-352">**Red virtual**: la misma red que la de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-352">**Virtual Network**: The same network as the virtual machines.</span></span>
   - <span data-ttu-id="3a089-353">**Subred**: la misma subred que la de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-353">**Subnet**: The same subnet as the virtual machines.</span></span>
   - <span data-ttu-id="3a089-354">**Dirección IP privada**: la misma dirección IP que asignó al recurso de red de clúster de la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-354">**Private IP address**: The same IP address that you assigned to the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="3a089-355">**Suscripción**: su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="3a089-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="3a089-356">**Grupo de recursos**: use el mismo grupo de recursos que las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-356">**Resource Group**: Use the same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="3a089-357">**Ubicación**: use la misma ubicación de Azure que las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a089-357">**Location**: Use the same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="3a089-358">Vea la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="3a089-358">See the following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-the-load-balancer-backend-pool"></a><span data-ttu-id="3a089-360">Configuración del grupo backend del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="3a089-360">Configure the load balancer backend pool</span></span>

1. <span data-ttu-id="3a089-361">Vuelva al grupo de recursos de Azure con las máquinas virtuales y busque el equilibrador de carga nuevo.</span><span class="sxs-lookup"><span data-stu-id="3a089-361">Return to the Azure Resource Group with the virtual machines and locate the new load balancer.</span></span> <span data-ttu-id="3a089-362">Es posible que tenga que actualizar la vista en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3a089-362">You may have to refresh the view on the Resource Group.</span></span> <span data-ttu-id="3a089-363">Haga clic en el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="3a089-363">Click the load balancer.</span></span>

1. <span data-ttu-id="3a089-364">En la hoja del equilibrador de carga, haga clic en **Grupos de back-end**.</span><span class="sxs-lookup"><span data-stu-id="3a089-364">On the load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="3a089-365">Haga clic en **+ Agregar** para agregar un grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="3a089-365">Click **+ Add** to add a backend pool.</span></span>

1. <span data-ttu-id="3a089-366">Escriba el nombre del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="3a089-366">Type a name for the backend pool.</span></span>

1. <span data-ttu-id="3a089-367">Haga clic en **Agregar una máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="3a089-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="3a089-368">En la hoja **Elegir máquinas virtuales**, haga clic en **Elegir un conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="3a089-368">On the **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="3a089-369">Elija que el conjunto de disponibilidad en el que colocó las máquinas virtuales de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-369">Choose the availability set that you placed the SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="3a089-370">En la hoja **Elegir máquinas virtuales**, haga clic en **Elegir las máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="3a089-370">On the **Choose virtual machines** blade, click **Choose the virtual machines**.</span></span>

   <span data-ttu-id="3a089-371">Azure Portal debe ser similar a lo que aparece en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="3a089-371">Your Azure portal should look like the following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="3a089-373">Haga clic en **Seleccionar** en la hoja **Elegir máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="3a089-373">Click **Select** on the **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="3a089-374">Haga clic en **Aceptar** dos veces.</span><span class="sxs-lookup"><span data-stu-id="3a089-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="3a089-375">Configuración de un sondeo de mantenimiento de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="3a089-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="3a089-376">En la hoja del equilibrador de carga, haga clic en **Health probes** (Sondeos de mantenimiento).</span><span class="sxs-lookup"><span data-stu-id="3a089-376">On the load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="3a089-377">Haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3a089-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="3a089-378">En la hoja **Add health probe** (Agregar sonda de mantenimiento), <a name="probe"></a>establezca los parámetros del sondeo de mantenimiento:</span><span class="sxs-lookup"><span data-stu-id="3a089-378">On the **Add health probe** blade, <a name="probe"></a>Set the health probe parameters:</span></span>

   - <span data-ttu-id="3a089-379">**Nombre**: el nombre del sondeo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="3a089-379">**Name**: A name for the health probe.</span></span>
   - <span data-ttu-id="3a089-380">**Protocolo**: TCP.</span><span class="sxs-lookup"><span data-stu-id="3a089-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="3a089-381">**Puerto**: se establece en un puerto TCP disponible.</span><span class="sxs-lookup"><span data-stu-id="3a089-381">**Port**: Set to an available TCP port.</span></span> <span data-ttu-id="3a089-382">Dicho puerto requiere un puerto de firewall abierto.</span><span class="sxs-lookup"><span data-stu-id="3a089-382">This port requires an open firewall port.</span></span> <span data-ttu-id="3a089-383">Use el [mismo puerto](#ports) que configuró para el sondeo de mantenimiento en el firewall.</span><span class="sxs-lookup"><span data-stu-id="3a089-383">Use the [same port](#ports) you set for the health probe at the firewall.</span></span>
   - <span data-ttu-id="3a089-384">**Intervalo**: 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="3a089-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="3a089-385">**Umbral incorrecto**: dos errores consecutivos.</span><span class="sxs-lookup"><span data-stu-id="3a089-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="3a089-386">Haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="3a089-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="3a089-387">Establecimiento de reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="3a089-387">Set load balancing rules</span></span>

1. <span data-ttu-id="3a089-388">En la hoja del equilibrador de carga, haga clic en **Reglas de equilibrio de carga**.</span><span class="sxs-lookup"><span data-stu-id="3a089-388">On the load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="3a089-389">Haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3a089-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="3a089-390">Establezca los parámetros de las reglas de equilibrio de carga:</span><span class="sxs-lookup"><span data-stu-id="3a089-390">Set the load balancing rules parameters:</span></span>

   - <span data-ttu-id="3a089-391">**Nombre**: nombre de las reglas de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="3a089-391">**Name**: A name for the load balancing rules.</span></span>
   - <span data-ttu-id="3a089-392">**Dirección IP de front-end**: use la dirección IP del recurso de red del clúster de la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-392">**Frontend IP address**: Use the IP address for the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="3a089-393">**Puerto**: establecido para el puerto TCP de la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-393">**Port**: Set for the SQL Server FCI TCP port.</span></span> <span data-ttu-id="3a089-394">El puerto de la instancia predeterminado es 1433.</span><span class="sxs-lookup"><span data-stu-id="3a089-394">The default instance port is 1433.</span></span>
   - <span data-ttu-id="3a089-395">**Puerto de back-end**: este valor utiliza el mismo puerto que el valor **Puerto** cuando se habilita **IP flotante (Direct Server Return)**.</span><span class="sxs-lookup"><span data-stu-id="3a089-395">**Backend port**: This value uses the same port as the **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="3a089-396">**Grupo back-end**: use el nombre del grupo back-end que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3a089-396">**Backend pool**: Use the backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="3a089-397">**Sondeo de mantenimiento**: utilice el sondeo de mantenimiento que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3a089-397">**Health probe**: Use the health probe that you configured earlier.</span></span>
   - <span data-ttu-id="3a089-398">**Persistencia de la sesión**: no.</span><span class="sxs-lookup"><span data-stu-id="3a089-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="3a089-399">**Tiempo de espera de inactividad (minutos)**: 4.</span><span class="sxs-lookup"><span data-stu-id="3a089-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="3a089-400">**IP flotante (Direct Server Return)**: habilitado</span><span class="sxs-lookup"><span data-stu-id="3a089-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="3a089-401">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3a089-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="3a089-402">Paso 6: Configurar el clúster para el sondeo</span><span class="sxs-lookup"><span data-stu-id="3a089-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="3a089-403">Establezca el parámetro del puerto de sondeo de clúster en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a089-403">Set the cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="3a089-404">Para establecer el parámetro del puerto de sondeo de clúster, actualice las variables del siguiente script desde su entorno.</span><span class="sxs-lookup"><span data-stu-id="3a089-404">To set the cluster probe port parameter, update variables in the following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "IP Address Resource Name" # the IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="3a089-405">Paso 7: Probar la conmutación por error de la FCI</span><span class="sxs-lookup"><span data-stu-id="3a089-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="3a089-406">Probar la conmutación por error de la FCI para validar la funcionalidad del clúster.</span><span class="sxs-lookup"><span data-stu-id="3a089-406">Test failover of the FCI to validate cluster functionality.</span></span> <span data-ttu-id="3a089-407">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3a089-407">Do the following steps:</span></span>

1. <span data-ttu-id="3a089-408">Conéctese a uno de los nodos de clúster de la FCI de SQL Server con RDP.</span><span class="sxs-lookup"><span data-stu-id="3a089-408">Connect to one of the SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="3a089-409">Abra el **Administrador de clústeres de conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="3a089-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="3a089-410">Haga clic en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="3a089-410">Click **Roles**.</span></span> <span data-ttu-id="3a089-411">Observe qué nodo posee el rol de FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-411">Notice which node owns the SQL Server FCI role.</span></span>

1. <span data-ttu-id="3a089-412">Haga clic con el botón derecho en el rol de FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-412">Right-click the SQL Server FCI role.</span></span>

1. <span data-ttu-id="3a089-413">Haga clic en **Mover** y, después, en **Mejor nodo posible**.</span><span class="sxs-lookup"><span data-stu-id="3a089-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="3a089-414">El **Administrador de clústeres de conmutación por error** muestra el rol y sus recursos pierden su conexión.</span><span class="sxs-lookup"><span data-stu-id="3a089-414">**Failover Cluster Manager** shows the role and its resources go offline.</span></span> <span data-ttu-id="3a089-415">Después, los recursos se mueven y vuelven a conectarse en el otro nodo.</span><span class="sxs-lookup"><span data-stu-id="3a089-415">The resources then move and come online on the other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="3a089-416">Comprobación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="3a089-416">Test connectivity</span></span>

<span data-ttu-id="3a089-417">Para probar la conectividad, inicie sesión en otra máquina virtual de la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="3a089-417">To test connectivity, log in to another virtual machine in the same virtual network.</span></span> <span data-ttu-id="3a089-418">Abra **SQL Server Management Studio** y conéctese al nombre de la FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a089-418">Open **SQL Server Management Studio** and connect to the SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="3a089-419">Si es necesario, puede [descargar SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a089-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="3a089-420">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="3a089-420">Limitations</span></span>
<span data-ttu-id="3a089-421">En las máquinas virtuales de Azure, Microsoft DTC (Coordinador de transacciones distribuidas) no se admite en las FCI, ya que el equilibrador de carga no admite el puerto de RPC.</span><span class="sxs-lookup"><span data-stu-id="3a089-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because the RPC port is not supported by the load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="3a089-422">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3a089-422">See Also</span></span>

[<span data-ttu-id="3a089-423">Instalación de S2D con escritorio remoto (Azure)</span><span class="sxs-lookup"><span data-stu-id="3a089-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="3a089-424">[Solución hiperconvergida con Espacios de almacenamiento directo en Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="3a089-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="3a089-425">Espacios de almacenamiento directo en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3a089-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="3a089-426">Compatibilidad de SQL Server con S2D</span><span class="sxs-lookup"><span data-stu-id="3a089-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)

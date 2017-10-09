---
title: "aaaSQL servidor FCI - máquinas virtuales de Azure | Documentos de Microsoft"
description: "Este artículo se explica cómo toocreate instancia de clúster de conmutación por error SQL Server en máquinas virtuales de Azure."
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
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="8f9fa-103">Configuración de una instancia de clúster de conmutación por error de SQL Server en Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="8f9fa-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="8f9fa-104">Este artículo explica cómo toocreate una conmutación por error SQL Server Cluster (FCI) de la instancia en máquinas virtuales de Azure en el modelo de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="8f9fa-105">Esta solución usa [espacios de almacenamiento directo de Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) como una SAN virtual basada en software que sincroniza el almacenamiento de hello (discos de datos) entre los nodos de hello (máquinas virtuales de Azure) en un Clúster de Windows.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="8f9fa-106">S2D es una novedad de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="8f9fa-107">Hello siguiente diagrama muestra la solución completa de hello en máquinas virtuales de Azure:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="8f9fa-109">Hola anterior diagrama muestra:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="8f9fa-110">Dos máquinas virtuales de Azure en un clúster de conmutación por error de Windows.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="8f9fa-111">Cuando una máquina virtual está en un clúster de conmutación por error también se denomina un *nodo de clúster* o *nodos*.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="8f9fa-112">Cada máquina virtual tiene dos, o más, discos de datos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="8f9fa-113">S2D sincroniza los datos de hello en disco de datos de Hola y presenta Hola sincronizado almacenamiento como un grupo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="8f9fa-114">grupo de almacenamiento de Hello presenta un clúster de conmutación por error de clúster volumen compartido (CSV) toohello.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="8f9fa-115">rol de clúster de SQL Server FCI Hello usa Hola CSV hello las unidades de datos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="8f9fa-116">Una carga de Azure equilibrador toohold Hola dirección IP para hello FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="8f9fa-117">Un conjunto de disponibilidad de Azure contiene todos los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="8f9fa-118">Todos los recursos de Azure están en el diagrama de hello en hello mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="8f9fa-119">Para más información acerca de S2D, consulte [Espacios de almacenamiento directo \(S2D\) de Windows Server 2016 Datacenter Edition](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="8f9fa-120">S2D admite dos tipos de arquitecturas, convergidas e hiperconvergidas.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="8f9fa-121">arquitectura de Hello en este documento es hiperconvergente.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="8f9fa-122">Un almacenamiento de hello hiperconvergente infraestructura lugares en Hola mismos servidores esa aplicación hello en clúster de host.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="8f9fa-123">En esta arquitectura, el almacenamiento de hello es en cada nodo de FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="8f9fa-124">Plantilla de Azure de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8f9fa-124">Example Azure template</span></span>

<span data-ttu-id="8f9fa-125">Puede crear toda la solución hello en Azure desde una plantilla.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="8f9fa-126">Un ejemplo de una plantilla está disponible en hello GitHub [plantillas de inicio rápido de Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="8f9fa-127">Este ejemplo no se ha diseñado para ninguna carga de trabajo específica ni se ha probado para ella.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="8f9fa-128">Puede ejecutar Hola plantilla toocreate una FCI de SQL Server con dominio de S2D almacenamiento tooyour conectado.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="8f9fa-129">Puede evaluar la plantilla de Hola y modificarlo para sus fines.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f9fa-130">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8f9fa-130">Before you begin</span></span>

<span data-ttu-id="8f9fa-131">Hay algunas cosas que debe tooknow y un par de cosas que necesita en su lugar antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="8f9fa-132">¿Qué tooknow</span><span class="sxs-lookup"><span data-stu-id="8f9fa-132">What tooknow</span></span>
<span data-ttu-id="8f9fa-133">Debe estar familiarizado operativa de hello siguientes tecnologías:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="8f9fa-134">Tecnologías de clúster de Windows</span><span class="sxs-lookup"><span data-stu-id="8f9fa-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="8f9fa-135">[Instancias del clúster de conmutación por error de SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="8f9fa-136">Además, debe tener un conocimiento general de hello siguientes tecnologías:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="8f9fa-137">Solución hiperconvergida con Espacios de almacenamiento directo en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8f9fa-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="8f9fa-138">Grupos de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="8f9fa-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="8f9fa-139">¿Qué toohave</span><span class="sxs-lookup"><span data-stu-id="8f9fa-139">What toohave</span></span>

<span data-ttu-id="8f9fa-140">Antes de seguir las instrucciones de hello en este artículo, ya debe tener:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="8f9fa-141">Una suscripción de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="8f9fa-142">Un dominio de Windows en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="8f9fa-143">Una cuenta con los objetos de máquina virtual de Azure hello toocreate permiso.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="8f9fa-144">Una red virtual de Azure y una subred con suficiente espacio de direcciones IP para saludo de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="8f9fa-145">Ambas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-145">Both virtual machines.</span></span>
   - <span data-ttu-id="8f9fa-146">dirección IP de clúster de conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="8f9fa-147">Una dirección IP para cada FCI.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="8f9fa-148">DNS configurado en la red de Azure, que señala a los controladores de dominio toohello Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="8f9fa-149">Una vez que cumpla los requisitos previos, puede pasar a la creación de un clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="8f9fa-150">Hola primer paso es máquinas virtuales de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="8f9fa-151">Paso 1: Crear máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="8f9fa-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="8f9fa-152">Inicie sesión en toohello [portal de Azure](http://portal.azure.com) con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="8f9fa-153">[Cree un conjunto de disponibilidad de Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="8f9fa-154">disponibilidad de Hello conjunto de máquinas virtuales de grupos entre dominios de error y dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="8f9fa-155">conjunto de disponibilidad de Hola se asegura de que la aplicación no se ve afectada por puntos únicos de error, como el conmutador de red de Hola o fuente de alimentación de Hola de un conjunto de servidores.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="8f9fa-156">Si no ha creado el grupo de recursos de Hola para las máquinas virtuales, hágalo cuando se crea un conjunto de disponibilidad de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="8f9fa-157">Si usas el conjunto de disponibilidad de hello toocreate portal Azure hello, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="8f9fa-158">Hola portal de Azure, haga clic en  **+**  tooopen hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="8f9fa-159">Busque **Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="8f9fa-160">Haga clic en **Conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="8f9fa-161">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-161">Click **Create**.</span></span>
   - <span data-ttu-id="8f9fa-162">En hello **crear conjunto de disponibilidad** hoja, Hola conjunto siguiente de valores:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="8f9fa-163">**Nombre**: un nombre para el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="8f9fa-164">**Suscripción**: su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="8f9fa-165">**Grupo de recursos**: si desea que toouse un grupo existente, haga clic en **utilizar existente** y grupo de hello seleccione de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="8f9fa-166">En caso contrario, elija **crear nuevo** y escriba un nombre para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="8f9fa-167">**Ubicación**: Establecer ubicación de Hola donde piensa toocreate las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="8f9fa-168">**Dominios de error**: usar Hola predeterminado (3).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="8f9fa-169">**Actualizar dominios**: usar Hola predeterminado (5).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="8f9fa-170">Haga clic en **crear** conjunto de disponibilidad de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="8f9fa-171">Crear máquinas virtuales de hello en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="8f9fa-172">Aprovisionar dos máquinas virtuales de SQL Server en el conjunto de disponibilidad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="8f9fa-173">Para obtener instrucciones, consulte [aprovisionar una máquina virtual de SQL Server en el portal de Azure hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="8f9fa-174">Coloque ambas máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="8f9fa-175">Hola mismo grupo de recursos de Azure que establezca su disponibilidad está en.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="8f9fa-176">En la misma red que el controlador de dominio de hello.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="8f9fa-177">En una subred con suficiente espacio de direcciones IP para ambas máquinas virtuales y todas las FCI que finalmente puede utilizar en este clúster.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="8f9fa-178">En el conjunto de disponibilidad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="8f9fa-179">Una vez creada una máquina virtual el conjunto de disponibilidad no se puede establecer o cambiar.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="8f9fa-180">Elija una imagen de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="8f9fa-181">Puede usar un mercado imagen con la que incluye Windows Server y SQL Server o simplemente hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="8f9fa-182">Para más información, consulte [Información general de SQL Server en máquinas virtuales de Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8f9fa-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="8f9fa-183">imágenes de SQL Server oficiales de Hola Hola Galería de Azure incluyen una instancia instalada de SQL Server, además de software de instalación de SQL Server de Hola y clave necesaria Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="8f9fa-184">Elija la imagen de la derecha Hola según toohow que desea toopay de licencia de SQL Server de hello:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="8f9fa-185">**Pago por uso de licencias**: Hola por minuto de estas imágenes comprenda Hola licencias de SQL Server:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="8f9fa-186">**SQL Server 2016 Enterprise en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="8f9fa-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="8f9fa-187">**SQL Server 2016 Standard en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="8f9fa-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="8f9fa-188">**SQL Server 2016 Developer en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="8f9fa-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="8f9fa-189">**Traiga su propia licencia (BYOL)**</span><span class="sxs-lookup"><span data-stu-id="8f9fa-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="8f9fa-190">**{BYOL} SQL Server 2016 Enterprise en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="8f9fa-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="8f9fa-191">**{BYOL} SQL Server 2016 Standard en Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="8f9fa-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="8f9fa-192">Después de crear la máquina virtual de hello, quitar instancia de SQL Server de hello previamente instalar de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="8f9fa-193">Después de configurar el clúster de conmutación por error de Hola y S2D utilizará Hola previamente instalado SQL Server media toocreate Hola FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="8f9fa-194">Como alternativa, puede utilizar imágenes de Azure Marketplace con solo el sistema de operativo Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="8f9fa-195">Elija un **Windows Server 2016 Datacenter** imagen e instalar Hola FCI de SQL Server después de configurar el clúster de conmutación por error de Hola y S2D.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="8f9fa-196">Esta imagen no contiene los medios de instalación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="8f9fa-197">Coloque los medios de instalación de hello en una ubicación donde puede ejecutar la instalación de SQL Server de Hola para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="8f9fa-198">Después de que Azure cree las máquinas virtuales, conectar máquinas virtuales de tooeach con RDP.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="8f9fa-199">Cuando se conecta primero tooa virtual machine con RDP, equipo de Hola le preguntará si desea tooallow esta toobe PC pueda detectarse en red Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="8f9fa-200">Haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-200">Click **Yes**.</span></span>

1. <span data-ttu-id="8f9fa-201">Si utilizas una de las imágenes de máquina virtual basada en SQL Server de hello, quitar instancia de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="8f9fa-202">En **Programas y características**, haga clic con el botón derecho en **Microsoft SQL Server 2016 (64 bits)** y haga clic en **Desinstalar o cambiar**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="8f9fa-203">Haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-203">Click **Remove**.</span></span>
   - <span data-ttu-id="8f9fa-204">Seleccione la instancia predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-204">Select hello default instance.</span></span>
   - <span data-ttu-id="8f9fa-205">Quite todas las características en **Servicios de motor de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="8f9fa-206">No quite **Características compartidas**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="8f9fa-207">Vea Hola después de imagen:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-207">See hello following picture:</span></span>

      ![Quitar características](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="8f9fa-209">Haga clic en **Siguiente** y, después, en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="8f9fa-210"><a name="ports"></a>Abrir puertos del firewall Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="8f9fa-211">En cada máquina virtual, abra Hola después de puertos en Firewall de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="8f9fa-212">Propósito</span><span class="sxs-lookup"><span data-stu-id="8f9fa-212">Purpose</span></span> | <span data-ttu-id="8f9fa-213">Puerto TCP</span><span class="sxs-lookup"><span data-stu-id="8f9fa-213">TCP Port</span></span> | <span data-ttu-id="8f9fa-214">Notas</span><span class="sxs-lookup"><span data-stu-id="8f9fa-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="8f9fa-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f9fa-215">SQL Server</span></span> | <span data-ttu-id="8f9fa-216">1433</span><span class="sxs-lookup"><span data-stu-id="8f9fa-216">1433</span></span> | <span data-ttu-id="8f9fa-217">Puerto normal para las instancias predeterminadas de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="8f9fa-218">Si utiliza una imagen de galería de hello, este puerto se abre automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="8f9fa-219">Sondeo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="8f9fa-219">Health probe</span></span> | <span data-ttu-id="8f9fa-220">59999</span><span class="sxs-lookup"><span data-stu-id="8f9fa-220">59999</span></span> | <span data-ttu-id="8f9fa-221">Cualquier puerto TCP abierto.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-221">Any open TCP port.</span></span> <span data-ttu-id="8f9fa-222">En un paso posterior, configure el equilibrador de carga de hello [sondeo de estado](#probe) y Hola toouse de clúster en este puerto.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="8f9fa-223">Agregar máquina virtual de almacenamiento toohello.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="8f9fa-224">Para más información, consulte [Almacenamiento premium: almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="8f9fa-225">Ambas máquinas virtuales necesitan al menos dos discos de datos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="8f9fa-226">Conecte discos sin procesar (discos cuyo formato no es NTFS).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="8f9fa-227">Si conecta discos con formato NTFS, solo puede habilitar S2D sin comprobación de la idoneidad del disco.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="8f9fa-228">Adjuntar un mínimo de dos tooeach de almacenamiento Premium (discos SSD) máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="8f9fa-229">Se recomienda usar, como mínimo, discos P30 (1 TB).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="8f9fa-230">Host de conjunto de almacenamiento en caché demasiado**de sólo lectura**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="8f9fa-231">capacidad de almacenamiento de Hello que usar en entornos de producción depende de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="8f9fa-232">los valores de Hello descritos en este artículo son para la demostración y pruebas.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="8f9fa-233">[Agregar dominio preexistente de hello máquinas virtuales tooyour](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="8f9fa-234">Después de hello las máquinas virtuales se crean y configuran, puede configurar el clúster de conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="8f9fa-235">Paso 2: Configurar el clúster de conmutación por error de Windows hello con S2D</span><span class="sxs-lookup"><span data-stu-id="8f9fa-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="8f9fa-236">Hola siguiente paso es clúster de conmutación por error de hello tooconfigure con S2D.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="8f9fa-237">En este paso, realizará Hola siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="8f9fa-238">Agregue la característica Agrupación en clústeres de conmutación por error de Windows</span><span class="sxs-lookup"><span data-stu-id="8f9fa-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="8f9fa-239">Validar clúster Hola</span><span class="sxs-lookup"><span data-stu-id="8f9fa-239">Validate hello cluster</span></span>
1. <span data-ttu-id="8f9fa-240">Crear el clúster de conmutación por error de Hola</span><span class="sxs-lookup"><span data-stu-id="8f9fa-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="8f9fa-241">Crear el testigo de hello en la nube</span><span class="sxs-lookup"><span data-stu-id="8f9fa-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="8f9fa-242">Agregue almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8f9fa-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="8f9fa-243">Agregue la característica Agrupación en clústeres de conmutación por error de Windows</span><span class="sxs-lookup"><span data-stu-id="8f9fa-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="8f9fa-244">toobegin, conectar la máquina virtual de la primera toohello con RDP con una cuenta de dominio que es miembro de los administradores locales y tiene objetos de toocreate de permisos en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="8f9fa-245">Utilice esta cuenta para el resto de Hola de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="8f9fa-246">[Agregar máquina virtual tooeach característica de agrupación en clústeres de conmutación por error](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="8f9fa-247">Hola tooinstall característica de agrupación en clústeres de conmutación por error de hello interfaz de usuario, siga los pasos en ambas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="8f9fa-248">En **Administrador del servidor**, haga clic en **Administrar** y, después, en **Agregar roles y características**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="8f9fa-249">En **agregar Roles y características Asistente**, haga clic en **siguiente** hasta llegar demasiado**seleccionar características**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="8f9fa-250">En **Seleccionar características**, haga clic en **Clústeres de conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="8f9fa-251">Incluye todas las características necesarias y herramientas de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="8f9fa-252">Haga clic en **Agregar características**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="8f9fa-253">Haga clic en **siguiente** y, a continuación, haga clic en **finalizar** características de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="8f9fa-254">tooinstall Hola agrupación en clústeres de conmutación por error característica con PowerShell, ejecute hello siguiente secuencia de comandos desde una sesión de PowerShell de administrador en una de las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="8f9fa-255">Como referencia, los pasos siguientes de Hola siguen instrucciones de hello en el paso 3 de [solución convergente Hyper mediante espacios de almacenamiento directo en Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="8f9fa-256">Validar clúster Hola</span><span class="sxs-lookup"><span data-stu-id="8f9fa-256">Validate hello cluster</span></span>

<span data-ttu-id="8f9fa-257">Esta guía hace referencia tooinstructions en [validar clúster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="8f9fa-258">Validación de clúster de Hola Hola interfaz de usuario o con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="8f9fa-259">clúster de hello toovalidate con interfaz de usuario, hello Hola siguiendo los pasos de una de las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="8f9fa-260">En **Administrador del servidor**, haga clic en **Herramientas** y, después, en **Administrador de clústeres de conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="8f9fa-261">En **Administrador de clústeres de conmutación por error**, haga clic en **Acción** y, después, en **Validar configuración...**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="8f9fa-262">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-262">Click **Next**.</span></span>
1. <span data-ttu-id="8f9fa-263">En **seleccionar servidores o un clúster de**, nombre de tipo hello de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="8f9fa-264">En **Opciones de pruebas**, elija **Ejecutar solo las pruebas que seleccione**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="8f9fa-265">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-265">Click **Next**.</span></span>
1. <span data-ttu-id="8f9fa-266">En **Selección de pruebas**, incluya todas las pruebas, excepto **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="8f9fa-267">Vea Hola después de imagen:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-267">See hello following picture:</span></span>

   ![Pruebas de validación](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="8f9fa-269">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-269">Click **Next**.</span></span>
1. <span data-ttu-id="8f9fa-270">En **Confirmación**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="8f9fa-271">Hola **validar un asistente de configuración** Hola de ejecuciones de pruebas de validación.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="8f9fa-272">clúster de hello toovalidate con PowerShell, ejecute hello siguiente secuencia de comandos desde una sesión de PowerShell de administrador en una de las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="8f9fa-273">Después de validar clúster hello, crear el clúster de conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="8f9fa-274">Crear el clúster de conmutación por error de Hola</span><span class="sxs-lookup"><span data-stu-id="8f9fa-274">Create hello failover cluster</span></span>

<span data-ttu-id="8f9fa-275">Esta guía hace referencia demasiado[crear clúster de conmutación por error de hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="8f9fa-276">clúster de conmutación por error de hello toocreate, necesita:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="8f9fa-277">nombres de Hola de máquinas virtuales de Hola que pasan a ser nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="8f9fa-278">Un nombre para el clúster de conmutación por error de Hola</span><span class="sxs-lookup"><span data-stu-id="8f9fa-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="8f9fa-279">Una dirección IP de clúster de conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="8f9fa-280">Puede usar una dirección IP que no se utiliza en hello misma red virtual y subred como Hola nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="8f9fa-281">Hola después de PowerShell crea un clúster de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="8f9fa-282">Actualizar script de Hola con nombres de Hola de nodos de hello (nombres de máquina virtual de hello) y una dirección IP disponible de hello red virtual de Azure:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="8f9fa-283">Creación de un testigo en la nube</span><span class="sxs-lookup"><span data-stu-id="8f9fa-283">Create a cloud witness</span></span>

<span data-ttu-id="8f9fa-284">Testigo en la nube es un nuevo tipo de testigo de quórum de clúster almacenado en una instancia de Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="8f9fa-285">Esto elimina la necesidad de Hola de una máquina virtual independiente hospeda un testigo de recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="8f9fa-286">[Crear un testigo en la nube para clúster de conmutación por error de hello](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="8f9fa-287">Cree un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-287">Create a blob container.</span></span>

1. <span data-ttu-id="8f9fa-288">Guardar las claves de acceso de Hola y Hola dirección URL del contenedor.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="8f9fa-289">Configurar a testigo de quórum de clúster de clúster de conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="8f9fa-290">Ver, [configurar testigo de quórum de hello en la interfaz de usuario de hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) en la interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="8f9fa-291">Agregue almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8f9fa-291">Add storage</span></span>

<span data-ttu-id="8f9fa-292">es necesario que los discos de Hola para S2D toobe vacía y sin particiones u otros datos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="8f9fa-293">siguen discos tooclean [Hola los pasos de esta guía](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="8f9fa-294">[Habilite Espacios de almacenamiento directo \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="8f9fa-295">Hola después PowerShell permite espacios de almacenamiento directos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="8f9fa-296">En **Administrador de clústeres de conmutación por error**, ahora puede ver el grupo de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="8f9fa-297">[Cree un volumen](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="8f9fa-298">Una de las características de Hola de S2D es que crea automáticamente un grupo de almacenamiento cuando se habilita.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="8f9fa-299">Ya estás listo toocreate un volumen.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="8f9fa-300">Hola PowerShell commandlet `New-Volume` automatiza el proceso de creación de volumen de hello, como el formato, Agregar clúster toohello y creación de un volumen compartido de clúster (CSV).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="8f9fa-301">Hola de ejemplo siguiente crea un 800 gigabyte (GB) CSV.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="8f9fa-302">Una vez que se completa este comando, se monta un volumen de 800 GB como recurso del clúster.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="8f9fa-303">volumen de Hello es en `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="8f9fa-304">Hola siguiente diagrama muestra un volumen compartido de clúster con S2D:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="8f9fa-306">Paso 3: Probar la conmutación por error del clúster de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="8f9fa-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="8f9fa-307">En el Administrador de clústeres de conmutación por error, compruebe que puede mover toohello de recursos de almacenamiento de hello otro nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="8f9fa-308">Si se puede conectar clúster de conmutación por error de toohello con **Administrador de clústeres de conmutación por error** y mover el almacenamiento de Hola desde un nodo toohello otros, está listo tooconfigure Hola FCI.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="8f9fa-309">Paso 4: Crear la FCI de SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f9fa-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="8f9fa-310">Después de haber configurado el clúster de conmutación por error de Hola y todos los componentes de clúster, incluido el almacenamiento, puede crear Hola FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="8f9fa-311">Conecte la máquina virtual de la primera toohello con RDP.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="8f9fa-312">En **Administrador de clústeres de conmutación por error**, asegúrese de que todos los recursos principales de clúster estén en la máquina virtual de primera Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="8f9fa-313">Si es necesario, mueva la máquina virtual de todos los recursos toothis.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="8f9fa-314">Busque los medios de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-314">Locate hello installation media.</span></span> <span data-ttu-id="8f9fa-315">Si máquina virtual de hello utiliza una de las imágenes de Azure Marketplace de hello, se encuentra en medio de hello `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="8f9fa-316">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-316">Click **Setup**.</span></span>

1. <span data-ttu-id="8f9fa-317">Hola **centro de instalación de SQL Server**, haga clic en **instalación**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="8f9fa-318">Haga clic en **Nueva instalación de clúster de conmutación por error de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="8f9fa-319">Siga las instrucciones de Hola Hola Hola de tooinstall Asistente FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="8f9fa-320">directorios de datos de Hello FCI necesitan toobe en almacenamiento en clúster.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="8f9fa-321">Con S2D, no es un disco compartido, pero un volumen de tooa de punto de montaje en cada servidor.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="8f9fa-322">S2D sincroniza volumen Hola entre ambos nodos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="8f9fa-323">volumen de Hola se presenta toohello clúster como un volumen compartido de clúster.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="8f9fa-324">Utilizar el punto de montaje CSV de hello en los directorios de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="8f9fa-326">Después de completar al Asistente de hello, el programa de instalación instalará una FCI de SQL Server en el primer nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="8f9fa-327">Después de que el programa de instalación instala correctamente Hola FCI en el primer nodo de hello, conecte toohello segundo nodo con RDP.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="8f9fa-328">Abra hello **centro de instalación de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="8f9fa-329">Haga clic en **Instalación**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-329">Click **Installation**.</span></span>

1. <span data-ttu-id="8f9fa-330">Haga clic en **clúster de conmutación por error de SQL Server de agregar nodos tooa**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="8f9fa-331">Siga las instrucciones de hello en SQL server de hello Asistente tooinstall y agregue este toohello servidor FCI.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="8f9fa-332">Si usa una imagen de la Galería de Azure Marketplace con SQL Server, herramientas de SQL Server se incluían en la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="8f9fa-333">Si no usó esta imagen, instalar herramientas de SQL Server de Hola por separado.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="8f9fa-334">Consulte [Descarga de SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="8f9fa-335">Paso 5: Crear un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="8f9fa-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="8f9fa-336">En máquinas virtuales de Azure, los clústeres usen un toohold de equilibrador de carga de una dirección IP que necesita toobe en un nodo de clúster en un momento.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="8f9fa-337">En esta solución, el equilibrador de carga de hello contiene dirección IP Hola Hola FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="8f9fa-338">[Creación y configuración de un equilibrador de carga de Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="8f9fa-339">Crear el equilibrador de carga de Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8f9fa-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="8f9fa-340">equilibrador de carga de Hola toocreate:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="8f9fa-341">Hola portal de Azure, vaya toohello grupo de recursos con máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="8f9fa-342">Haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-342">Click **+ Add**.</span></span> <span data-ttu-id="8f9fa-343">Hola de búsqueda Marketplace para **equilibrador de carga**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="8f9fa-344">Haga clic en **Equilibrador de carga**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="8f9fa-345">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-345">Click **Create**.</span></span>

1. <span data-ttu-id="8f9fa-346">Configure el equilibrador de carga de hello con:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="8f9fa-347">**Nombre**: un nombre que identifique el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="8f9fa-348">**Tipo de**: equilibrador de carga de hello puede ser público o privado.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="8f9fa-349">Puede tener acceso a un equilibrador de carga privada desde Hola misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="8f9fa-350">La mayoría de las aplicaciones de Azure pueden usar un equilibrador de carga privado.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="8f9fa-351">Si la aplicación necesita acceso tooSQL Server directamente a través de Internet de hello, use un equilibrador de carga pública.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="8f9fa-352">**Red virtual**: Hola misma red que las máquinas virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="8f9fa-353">**Subred**: Hola la misma subred que hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="8f9fa-354">**La dirección IP privada**: Hola la misma dirección IP que ha asignado el recurso de red de clústeres de toohello FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="8f9fa-355">**Suscripción**: su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="8f9fa-356">**Grupo de recursos**: Use Hola mismo grupo de recursos que las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="8f9fa-357">**Ubicación**: Use Hola misma ubicación de Azure como las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="8f9fa-358">Vea Hola después de imagen:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="8f9fa-360">Configurar grupo de back-end de equilibradores de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="8f9fa-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="8f9fa-361">Devolver toohello grupo de recursos de Azure con máquinas virtuales de Hola y busque el equilibrador de carga nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="8f9fa-362">Es posible que tenga la vista de hello toorefresh en hello grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="8f9fa-363">Haga clic en el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="8f9fa-364">En la hoja de equilibrador de carga de hello, haga clic en **grupos back-end**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="8f9fa-365">Haga clic en **+ agregar** tooadd un grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="8f9fa-366">Escriba un nombre para el grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="8f9fa-367">Haga clic en **Agregar una máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="8f9fa-368">En hello **elegir máquinas virtuales** hoja, haga clic en **elegir un conjunto de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="8f9fa-369">Elija que coloquen máquinas de virtuales de SQL Server de hello en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="8f9fa-370">En hello **elegir máquinas virtuales** hoja, haga clic en **elegir máquinas virtuales de hello**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="8f9fa-371">El portal de Azure debe ser similar Hola después de imagen:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="8f9fa-373">Haga clic en **seleccione** en hello **elegir máquinas virtuales** hoja.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="8f9fa-374">Haga clic en **Aceptar** dos veces.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="8f9fa-375">Configuración de un sondeo de mantenimiento de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="8f9fa-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="8f9fa-376">En la hoja de equilibrador de carga de hello, haga clic en **sondeos de estado**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="8f9fa-377">Haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="8f9fa-378">En hello **sondeo de estado del complemento** hoja, <a name="probe"> </a>establecer parámetros de sondeo de estado de hello:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="8f9fa-379">**Nombre**: un nombre para el sondeo de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="8f9fa-380">**Protocolo**: TCP.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="8f9fa-381">**Puerto**: establecer tooan puertos TCP disponibles.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="8f9fa-382">Dicho puerto requiere un puerto de firewall abierto.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-382">This port requires an open firewall port.</span></span> <span data-ttu-id="8f9fa-383">Hola de uso [mismo puerto](#ports) se establece para el sondeo de estado de hello en firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="8f9fa-384">**Intervalo**: 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="8f9fa-385">**Umbral incorrecto**: dos errores consecutivos.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="8f9fa-386">Haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="8f9fa-387">Establecimiento de reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="8f9fa-387">Set load balancing rules</span></span>

1. <span data-ttu-id="8f9fa-388">En la hoja de equilibrador de carga de hello, haga clic en **reglas de equilibrio de carga**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="8f9fa-389">Haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="8f9fa-390">Establecer parámetros de reglas de equilibrio de carga de hello:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="8f9fa-391">**Nombre**: un nombre para las reglas de equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="8f9fa-392">**Dirección IP de Frontend**: Use una dirección IP Hola para hello recurso de red de clústeres de SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="8f9fa-393">**Puerto**: establecer para el puerto TCP de SQL Server FCI Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="8f9fa-394">puerto de instancia de Hello predeterminado es 1433.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="8f9fa-395">**Puerto de back-end**: este valor usa Hola mismo número de puerto como hello **puerto** valor cuando se habilita el **IP flotante (direct server devuelto)**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="8f9fa-396">**Grupo back-end**: nombre de grupo de back-end de Hola de uso que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="8f9fa-397">**Sondeo de estado**: sondeo de estado de Hola de uso que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="8f9fa-398">**Persistencia de la sesión**: no.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="8f9fa-399">**Tiempo de espera de inactividad (minutos)**: 4.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="8f9fa-400">**IP flotante (Direct Server Return)**: habilitado</span><span class="sxs-lookup"><span data-stu-id="8f9fa-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="8f9fa-401">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="8f9fa-402">Paso 6: Configurar el clúster para el sondeo</span><span class="sxs-lookup"><span data-stu-id="8f9fa-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="8f9fa-403">Establecer el parámetro de puerto de sondeo de clúster de hello en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="8f9fa-404">tooset Hola parámetro de puerto de sondeo de clúster, actualice las variables Hola siguiente secuencia de comandos de su entorno.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="8f9fa-405">Paso 7: Probar la conmutación por error de la FCI</span><span class="sxs-lookup"><span data-stu-id="8f9fa-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="8f9fa-406">Probar la conmutación por error de hello funcionalidad de clústeres de toovalidate FCI.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="8f9fa-407">Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f9fa-407">Do hello following steps:</span></span>

1. <span data-ttu-id="8f9fa-408">Conecte tooone de nodos de clúster de SQL Server FCI Hola con RDP.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="8f9fa-409">Abra el **Administrador de clústeres de conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="8f9fa-410">Haga clic en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-410">Click **Roles**.</span></span> <span data-ttu-id="8f9fa-411">Observe qué nodo posee el rol de SQL Server FCI de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="8f9fa-412">Haga clic en el rol de hello FCI de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="8f9fa-413">Haga clic en **Mover** y, después, en **Mejor nodo posible**.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="8f9fa-414">**El Administrador de clústeres de conmutación por error** muestra Hola rol y sus recursos se ponen sin conexión.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="8f9fa-415">Hello recursos, a continuación, mover y ponerse en línea hello en otro nodo.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="8f9fa-416">Comprobación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="8f9fa-416">Test connectivity</span></span>

<span data-ttu-id="8f9fa-417">conectividad tootest de registro en la máquina virtual de tooanother Hola misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="8f9fa-418">Abra **SQL Server Management Studio** y nombre de SQL Server FCI toohello connect.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="8f9fa-419">Si es necesario, puede [descargar SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="8f9fa-420">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="8f9fa-420">Limitations</span></span>
<span data-ttu-id="8f9fa-421">En máquinas virtuales de Azure, Coordinador de transacciones distribuidas de Microsoft (DTC) no se admite en fci porque Hola puerto RPC no es compatible con el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f9fa-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="8f9fa-422">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8f9fa-422">See Also</span></span>

[<span data-ttu-id="8f9fa-423">Instalación de S2D con escritorio remoto (Azure)</span><span class="sxs-lookup"><span data-stu-id="8f9fa-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="8f9fa-424">[Solución hiperconvergida con Espacios de almacenamiento directo en Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="8f9fa-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="8f9fa-425">Espacios de almacenamiento directo en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8f9fa-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="8f9fa-426">Compatibilidad de SQL Server con S2D</span><span class="sxs-lookup"><span data-stu-id="8f9fa-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)

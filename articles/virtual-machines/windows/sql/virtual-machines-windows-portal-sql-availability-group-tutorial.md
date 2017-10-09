---
title: "Tutorial de grupos de disponibilidad de servidor - máquinas virtuales de Azure - aaaSQL | Documentos de Microsoft"
description: "Este tutorial se muestra cómo toocreate un SQL Server grupo de disponibilidad AlwaysOn en máquinas virtuales de Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="f0322-103">Configuración manual de grupos de disponibilidad AlwaysOn en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="f0322-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="f0322-104">Este tutorial se muestra cómo toocreate un SQL Server grupo de disponibilidad AlwaysOn en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="f0322-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="f0322-105">todo el tutorial Hola crea un grupo de disponibilidad con una réplica de base de datos en dos servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="f0322-106">**Estimación del tiempo**: tarda unos 30 minutos toocomplete una vez que se cumplen los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="f0322-107">diagrama de Hello muestra lo que crea en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="f0322-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f0322-109">Prerequisites</span></span>

<span data-ttu-id="f0322-110">tutorial de Hola se da por supuesto que tiene conocimientos básicos de SQL Server siempre grupos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f0322-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="f0322-111">Para más información, consulte [Información general de los grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0322-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="f0322-112">Hello tabla siguiente enumeran los requisitos previos de Hola que necesita toocomplete antes de iniciar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="f0322-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="f0322-113">Requisito</span><span class="sxs-lookup"><span data-stu-id="f0322-113">Requirement</span></span> |<span data-ttu-id="f0322-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="f0322-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="f0322-116">Dos servidores SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0322-116">Two SQL Servers</span></span> | <span data-ttu-id="f0322-117">- En un conjunto de disponibilidad de Azure</span><span class="sxs-lookup"><span data-stu-id="f0322-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="f0322-118">- En un solo dominio</span><span class="sxs-lookup"><span data-stu-id="f0322-118">- In a single domain</span></span> <br/> <span data-ttu-id="f0322-119">- Con la característica Clústeres de conmutación por error instalada</span><span class="sxs-lookup"><span data-stu-id="f0322-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="f0322-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="f0322-121">Windows Server</span></span> | <span data-ttu-id="f0322-122">Recurso compartido de archivos para testigo de clúster</span><span class="sxs-lookup"><span data-stu-id="f0322-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="f0322-124">Cuenta de servicio de SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0322-124">SQL Server service account</span></span> | <span data-ttu-id="f0322-125">Cuenta de dominio</span><span class="sxs-lookup"><span data-stu-id="f0322-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="f0322-127">Cuenta de servicio Agente SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0322-127">SQL Server Agent service account</span></span> | <span data-ttu-id="f0322-128">Cuenta de dominio</span><span class="sxs-lookup"><span data-stu-id="f0322-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="f0322-130">Puertos de firewall abiertos</span><span class="sxs-lookup"><span data-stu-id="f0322-130">Firewall ports open</span></span> | <span data-ttu-id="f0322-131">- SQL Server: **1433** para la instancia predeterminada</span><span class="sxs-lookup"><span data-stu-id="f0322-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="f0322-132">- Punto de conexión de reflejo de la base de datos: **5022** o cualquier puerto disponible</span><span class="sxs-lookup"><span data-stu-id="f0322-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="f0322-133">- Sondeo de Azure Load Balancer: **59999** o cualquier puerto disponible</span><span class="sxs-lookup"><span data-stu-id="f0322-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="f0322-135">Agregar característica Clústeres de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="f0322-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="f0322-136">Ambos servidores SQL Server necesitan esta característica</span><span class="sxs-lookup"><span data-stu-id="f0322-136">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="f0322-138">Cuenta de dominio de la instalación</span><span class="sxs-lookup"><span data-stu-id="f0322-138">Installation domain account</span></span> | <span data-ttu-id="f0322-139">- Administrador local en cada servidor SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0322-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="f0322-140">- Miembro del rol fijo del servidor sysadmin de SQL Server para cada instancia de SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0322-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="f0322-141">Antes de comenzar el tutorial de hello, necesita demasiado[completar los requisitos previos para la creación de grupos de disponibilidad AlwaysOn en máquinas virtuales Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="f0322-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="f0322-142">Si estos requisitos previos ya se ha completado, puede saltar demasiado[crear clúster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="f0322-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="f0322-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Crear clúster Hola</span><span class="sxs-lookup"><span data-stu-id="f0322-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="f0322-144">Después de Hola se completan los requisitos previos, Hola primer paso es toocreate un clúster de conmutación por error de Windows Server que incluye dos servidores SQL Server y un servidor testigo.</span><span class="sxs-lookup"><span data-stu-id="f0322-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="f0322-145">RDP toohello primer servidor de SQL Server con una cuenta de dominio que es un administrador de servidores SQL Server y servidor de testigo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="f0322-146">Si ha seguido hello [documento de requisitos previos](virtual-machines-windows-portal-sql-availability-group-prereq.md), crea una cuenta llamada **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="f0322-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="f0322-147">Utilice esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="f0322-147">Use this account.</span></span>

2. <span data-ttu-id="f0322-148">Hola **el administrador del servidor** panel, seleccione **herramientas**y, a continuación, haga clic en **Administrador de clústeres de conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="f0322-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="f0322-149">En el panel izquierdo de hello, haga clic en **Administrador de clústeres de conmutación por error**y, a continuación, haga clic en **crear un clúster de**.</span><span class="sxs-lookup"><span data-stu-id="f0322-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="f0322-150">![Crear clúster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="f0322-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="f0322-151">En el Asistente para crear clúster de Hola, cree un clúster de un nodo recorriendo las páginas Hola con la configuración de hello en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="f0322-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="f0322-152">Page</span><span class="sxs-lookup"><span data-stu-id="f0322-152">Page</span></span> | <span data-ttu-id="f0322-153">Configuración</span><span class="sxs-lookup"><span data-stu-id="f0322-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="f0322-154">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f0322-154">Before You Begin</span></span> |<span data-ttu-id="f0322-155">Usar predeterminados</span><span class="sxs-lookup"><span data-stu-id="f0322-155">Use defaults</span></span> |
   | <span data-ttu-id="f0322-156">Seleccionar servidores</span><span class="sxs-lookup"><span data-stu-id="f0322-156">Select Servers</span></span> |<span data-ttu-id="f0322-157">Hola de tipo nombre del primer servidor SQL Server en **escriba el nombre de servidor** y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="f0322-158">Advertencia de validación</span><span class="sxs-lookup"><span data-stu-id="f0322-158">Validation Warning</span></span> |<span data-ttu-id="f0322-159">Seleccione **no. no requieren soporte técnico de Microsoft para este clúster y, por tanto, no desea validación de hello toorun las pruebas. Al hacer clic en siguiente, continuar con la creación de clúster de hello**.</span><span class="sxs-lookup"><span data-stu-id="f0322-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="f0322-160">Punto de acceso para administrar Hola clúster</span><span class="sxs-lookup"><span data-stu-id="f0322-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="f0322-161">Escriba un nombre de clúster, por ejemplo **SQLAGCluster1** en **Nombre del clúster**.</span><span class="sxs-lookup"><span data-stu-id="f0322-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="f0322-162">Confirmación</span><span class="sxs-lookup"><span data-stu-id="f0322-162">Confirmation</span></span> |<span data-ttu-id="f0322-163">Use los valores predeterminados a menos que use Espacios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f0322-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="f0322-164">Vea la nota de Hola que sigue a esta tabla.</span><span class="sxs-lookup"><span data-stu-id="f0322-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="f0322-165">Establecer la dirección IP del clúster Hola</span><span class="sxs-lookup"><span data-stu-id="f0322-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="f0322-166">En **Administrador de clústeres de conmutación por error**, desplácese hacia abajo demasiado**recursos principales de clúster** y expanda detalles del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="f0322-167">Debería ver dos hello **nombre** hello y **dirección IP** recursos de hello **error** estado.</span><span class="sxs-lookup"><span data-stu-id="f0322-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="f0322-168">Hello recurso de dirección IP no se puede poner en conexión clúster Hola se asigna Hola igual de direcciones IP como máquina de hello propiamente dicha, por lo tanto, es una dirección duplicada.</span><span class="sxs-lookup"><span data-stu-id="f0322-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="f0322-169">Hola contextual error **dirección IP** recurso y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="f0322-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Propiedades de clúster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="f0322-171">Seleccione **dirección IP estática** y especifique una dirección de subred donde hello SQL Server en el cuadro de texto de dirección de hello disponible.</span><span class="sxs-lookup"><span data-stu-id="f0322-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="f0322-172">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="f0322-173">Hola **recursos principales de clúster** sección, haga clic en el nombre de clúster y haga clic en **poner en conexión**.</span><span class="sxs-lookup"><span data-stu-id="f0322-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="f0322-174">Después espere hasta que ambos recursos estén en línea.</span><span class="sxs-lookup"><span data-stu-id="f0322-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="f0322-175">Cuando el recurso de nombre de clúster de Hola se pone en línea, actualiza el servidor de DC de hello con una nueva cuenta de equipo de AD.</span><span class="sxs-lookup"><span data-stu-id="f0322-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="f0322-176">Utilice este hello toorun de cuenta de AD más tarde el servicio de clúster del grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f0322-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="f0322-177"><a name="addNode"></a>Agregar Hola otro toocluster de SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0322-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="f0322-178">Agregar Hola otro clúster de SQL Server toohello.</span><span class="sxs-lookup"><span data-stu-id="f0322-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="f0322-179">En el árbol del explorador de hello, haga clic en el clúster de Hola y haga clic en **agregar nodo**.</span><span class="sxs-lookup"><span data-stu-id="f0322-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Agregar nodo toohello clúster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="f0322-181">Hola **Asistente para agregar nodos**, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="f0322-182">Hola **seleccionar servidores** página, agregue Hola segundo servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="f0322-183">Nombre del servidor de tipo hello en **escriba el nombre de servidor** y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="f0322-184">Cuando haya terminado, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="f0322-185">Hola **advertencia de validación** página, haga clic en **No** (en un escenario de producción debería realizar pruebas de validación de hello).</span><span class="sxs-lookup"><span data-stu-id="f0322-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="f0322-186">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="f0322-187">Hola **confirmación** página si usa espacios de almacenamiento, desactive Hola casilla **agregar todo el almacenamiento apto toohello clúster.**</span><span class="sxs-lookup"><span data-stu-id="f0322-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Agregar nodo de confirmación](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="f0322-189">Si utiliza espacios de almacenamiento y no desactive **agregar todo el almacenamiento apto toohello clúster**, Windows separa los discos virtuales de Hola durante el proceso de agrupación en clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="f0322-190">Como resultado, que no aparecen en el Administrador de discos o en el explorador hasta que se quiten los espacios de almacenamiento de Hola de clúster de Hola y volver a adjuntar con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0322-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="f0322-191">Espacios de almacenamiento agrupa varios discos en grupos de toostorage.</span><span class="sxs-lookup"><span data-stu-id="f0322-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="f0322-192">Para obtener más información, consulte el artículo sobre [espacios de almacenamiento](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="f0322-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="f0322-193">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-193">Click **Next**.</span></span>

1. <span data-ttu-id="f0322-194">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="f0322-194">Click **Finish**.</span></span>

   <span data-ttu-id="f0322-195">El Administrador de clústeres de conmutación por error se muestra que el clúster tiene un nuevo nodo y las listas en hello **nodos** contenedor.</span><span class="sxs-lookup"><span data-stu-id="f0322-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="f0322-196">Cerrar sesión de escritorio remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="f0322-197">Agregar un recurso compartido de cuórum de clúster</span><span class="sxs-lookup"><span data-stu-id="f0322-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="f0322-198">En este ejemplo, clúster de Windows hello utiliza un toocreate de recurso compartido de archivo un quórum de clúster.</span><span class="sxs-lookup"><span data-stu-id="f0322-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="f0322-199">Este tutorial utiliza un cuórum de mayoría de recurso compartido de archivos y nodo.</span><span class="sxs-lookup"><span data-stu-id="f0322-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="f0322-200">Para más información, consulte [Descripción de las configuraciones de cuórum en un clúster de conmutación por error](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0322-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="f0322-201">Conectar el servidor de miembro de testigo de recurso compartido de archivos de toohello con una sesión de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="f0322-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="f0322-202">En **Administrador del servidor**, haga clic en **Herramientas**.</span><span class="sxs-lookup"><span data-stu-id="f0322-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="f0322-203">Abra **Administración de equipos**.</span><span class="sxs-lookup"><span data-stu-id="f0322-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="f0322-204">Haga clic en **Carpetas compartidas**.</span><span class="sxs-lookup"><span data-stu-id="f0322-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="f0322-205">Haga clic con el botón derecho en **Recursos compartidos** y, a continuación, haga clic en **Nuevo recurso compartido...**</span><span class="sxs-lookup"><span data-stu-id="f0322-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="f0322-207">Use **crear un Asistente para carpetas compartidas** toocreate un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="f0322-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="f0322-208">En **ruta de acceso de carpeta**, haga clic en **examinar** y busque o cree una ruta de acceso de carpeta compartida de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="f0322-209">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-209">Click **Next**.</span></span>

1. <span data-ttu-id="f0322-210">En **nombre, descripción y configuración** Compruebe el nombre del recurso compartido de Hola y ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="f0322-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="f0322-211">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-211">Click **Next**.</span></span>

1. <span data-ttu-id="f0322-212">En **Permisos de la carpeta compartida**, establezca **Personalizar permisos**.</span><span class="sxs-lookup"><span data-stu-id="f0322-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="f0322-213">Clic en **Personalizado...**</span><span class="sxs-lookup"><span data-stu-id="f0322-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="f0322-214">En **Personalizar permisos**, haga clic en **Agregar...**</span><span class="sxs-lookup"><span data-stu-id="f0322-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="f0322-215">Asegúrese de que ese clúster de Hola Hola cuenta usada toocreate tiene control total.</span><span class="sxs-lookup"><span data-stu-id="f0322-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="f0322-217">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-217">Click **OK**.</span></span>

1. <span data-ttu-id="f0322-218">En **Permisos de la carpeta compartida**, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="f0322-219">Haga clic de nuevo en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="f0322-220">Cierre la sesión de servidor hello</span><span class="sxs-lookup"><span data-stu-id="f0322-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="f0322-221">Configuración del cuórum de clúster</span><span class="sxs-lookup"><span data-stu-id="f0322-221">Configure cluster quorum</span></span>

<span data-ttu-id="f0322-222">A continuación, establezca el quórum del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="f0322-223">Conectar toohello primer nodo del clúster con Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="f0322-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="f0322-224">En **Administrador de clústeres de conmutación por error**, haga clic en el clúster de hello, seleccione demasiado**más acciones**y haga clic en **configurar opciones de quórum de clúster...** .</span><span class="sxs-lookup"><span data-stu-id="f0322-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="f0322-226">En **Asistente para configurar quórum de clúster**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="f0322-227">En **seleccionar la opción de configuración de quórum**, elija **seleccionar testigo de quórum de hello**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="f0322-228">En **Seleccionar el testigo de quórum**, haga clic en **Configurar un testigo de recurso compartido de archivos**.</span><span class="sxs-lookup"><span data-stu-id="f0322-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="f0322-229">Windows Server 2016 admite un testigo en la nube.</span><span class="sxs-lookup"><span data-stu-id="f0322-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="f0322-230">Si elige este tipo de testigo, no necesita ningún testigo de recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="f0322-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="f0322-231">Para más información, consulte [Implementación de un testigo en la nube para un clúster de conmutación por error](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="f0322-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="f0322-232">Este tutorial usa un testigo de recurso compartido de archivos, que es compatible con los sistemas operativos anteriores.</span><span class="sxs-lookup"><span data-stu-id="f0322-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="f0322-233">En **testigo del recurso compartido de archivo de configuración**, ruta de acceso de tipo hello para el recurso compartido de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="f0322-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="f0322-234">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-234">Click **Next**.</span></span>

1. <span data-ttu-id="f0322-235">Compruebe la configuración de hello en **confirmación**.</span><span class="sxs-lookup"><span data-stu-id="f0322-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="f0322-236">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-236">Click **Next**.</span></span>

1. <span data-ttu-id="f0322-237">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="f0322-237">Click **Finish**.</span></span>

<span data-ttu-id="f0322-238">recursos principales de clúster Hola se configuran con un testigo de recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="f0322-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="f0322-239">Habilitación de grupos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="f0322-239">Enable Availability Groups</span></span>

<span data-ttu-id="f0322-240">A continuación, habilite hello **grupos de disponibilidad AlwaysOn** característica.</span><span class="sxs-lookup"><span data-stu-id="f0322-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="f0322-241">Siga estos pasos para ambos servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="f0322-242">De hello **iniciar** pantalla, inicie **Administrador de configuración de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f0322-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="f0322-243">En el árbol del explorador de hello, haga clic en **Services de SQL Server**, a continuación, haga clic en hello **SQL Server (MSSQLSERVER)** de servicio y haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="f0322-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="f0322-244">Haga clic en hello **alta disponibilidad de AlwaysOn** y, después, seleccione **habilitar los grupos de disponibilidad AlwaysOn**, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f0322-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Habilitación de grupos de disponibilidad AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="f0322-246">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f0322-246">Click **Apply**.</span></span> <span data-ttu-id="f0322-247">Haga clic en **Aceptar** en el cuadro de diálogo emergente de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="f0322-248">Reinicie el servicio de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="f0322-249">Repita estos pasos en hello en otro servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="f0322-250">Crear una base de datos en hello primer servidor SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0322-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="f0322-251">Archivo RDP de inicio hello toohello primer servidor de SQL Server con un dominio de la cuenta que es miembro de sysadmin rol fijo de servidor.</span><span class="sxs-lookup"><span data-stu-id="f0322-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="f0322-252">Abra SQL Server Management Studio y conéctese toohello primer servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="f0322-253">En el **Explorador de objetos**, haga clic con el botón derecho en **Bases de datos** y luego en **Nueva base de datos**.</span><span class="sxs-lookup"><span data-stu-id="f0322-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="f0322-254">En **Nombre de base de datos**, escriba **MyDB1** y después haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="f0322-255"><a name="backupshare"></a> Creación de un recurso compartido de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="f0322-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="f0322-256">En Hola el primer servidor de SQL Server en **el administrador del servidor**, haga clic en **herramientas**.</span><span class="sxs-lookup"><span data-stu-id="f0322-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="f0322-257">Abra **Administración de equipos**.</span><span class="sxs-lookup"><span data-stu-id="f0322-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="f0322-258">Haga clic en **Carpetas compartidas**.</span><span class="sxs-lookup"><span data-stu-id="f0322-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="f0322-259">Haga clic con el botón derecho en **Recursos compartidos** y, a continuación, haga clic en **Nuevo recurso compartido...**</span><span class="sxs-lookup"><span data-stu-id="f0322-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="f0322-261">Use **crear un Asistente para carpetas compartidas** toocreate un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="f0322-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="f0322-262">En **ruta de acceso de carpeta**, haga clic en **examinar** y busque o cree una ruta de acceso de carpeta compartida de hello base de datos copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f0322-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="f0322-263">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-263">Click **Next**.</span></span>

1. <span data-ttu-id="f0322-264">En **nombre, descripción y configuración** Compruebe el nombre del recurso compartido de Hola y ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="f0322-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="f0322-265">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-265">Click **Next**.</span></span>

1. <span data-ttu-id="f0322-266">En **Permisos de la carpeta compartida**, establezca **Personalizar permisos**.</span><span class="sxs-lookup"><span data-stu-id="f0322-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="f0322-267">Clic en **Personalizado...**</span><span class="sxs-lookup"><span data-stu-id="f0322-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="f0322-268">En **Personalizar permisos**, haga clic en **Agregar...**</span><span class="sxs-lookup"><span data-stu-id="f0322-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="f0322-269">Asegúrese de que Hola SQL Server y Agente SQL Server las cuentas de servicio para ambos servidores tienen control total.</span><span class="sxs-lookup"><span data-stu-id="f0322-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="f0322-271">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-271">Click **OK**.</span></span>

1. <span data-ttu-id="f0322-272">En **Permisos de la carpeta compartida**, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="f0322-273">Haga clic de nuevo en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="f0322-274">Realizar copia de seguridad de base de datos de hello una completa</span><span class="sxs-lookup"><span data-stu-id="f0322-274">Take a full backup of hello database</span></span>

<span data-ttu-id="f0322-275">Necesita tooback seguridad Hola nueva base de datos tooinitialize Hola cadena de registros.</span><span class="sxs-lookup"><span data-stu-id="f0322-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="f0322-276">Si no se realiza una copia de seguridad de base de datos nueva hello, no pueden incluirse en un grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f0322-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="f0322-277">En **Explorador de objetos**, haga clic en la base de datos de hello, seleccione demasiado**tareas...** , haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="f0322-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="f0322-278">Haga clic en **Aceptar** tootake una ubicación de copia de seguridad de toohello de copia de seguridad completa de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f0322-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="f0322-279">Crear grupo de disponibilidad de hello</span><span class="sxs-lookup"><span data-stu-id="f0322-279">Create hello Availability Group</span></span>
<span data-ttu-id="f0322-280">Ya estás listo tooconfigure un grupo de disponibilidad mediante Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="f0322-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="f0322-281">Crear una base de datos en hello primer servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="f0322-282">Realice una copia de seguridad completa y una copia de seguridad del registro de transacciones de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="f0322-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="f0322-283">Hola de restauración completa y toohello de las copias de seguridad de registro segundo SQL Server con hello **NORECOVERY** opción</span><span class="sxs-lookup"><span data-stu-id="f0322-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="f0322-284">Crear grupo de disponibilidad de hello (**AG1**) con réplicas secundarias legibles, confirmación sincrónica y conmutación automática por error</span><span class="sxs-lookup"><span data-stu-id="f0322-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="f0322-285">Crear grupo de disponibilidad de hello:</span><span class="sxs-lookup"><span data-stu-id="f0322-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="f0322-286">En la sesión de escritorio remoto toohello primer servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="f0322-287">En el **Explorador de objetos** de SSMS, haga clic con el botón derecho en **Alta disponibilidad de AlwaysOn** y en **Asistente para nuevo grupo de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="f0322-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Iniciar el Asistente para nuevo grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="f0322-289">Hola **Introducción** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="f0322-290">Hola **especificar el nombre de grupo de disponibilidad** página, escriba un nombre para hello grupo de disponibilidad, por ejemplo **AG1**, en **nombre del grupo de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="f0322-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="f0322-291">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-291">Click **Next**.</span></span>

    ![Asistente para nuevo grupo de disponibilidad, especificar el nombre del grupo](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="f0322-293">Hola **seleccionar bases de datos** , seleccione la base de datos y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f0322-294">base de datos de Hello cumple los requisitos previos de Hola para un grupo de disponibilidad dado que ha realizado al menos una copia de seguridad completa en la réplica principal pretendida de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Asistente para nuevo grupo de disponibilidad, seleccionar bases de datos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="f0322-296">Hola **especificar réplicas** página, haga clic en **agregar una réplica**.</span><span class="sxs-lookup"><span data-stu-id="f0322-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Asistente para nuevo grupo de disponibilidad, especificar réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="f0322-298">Hola **conectar tooServer** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0322-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="f0322-299">Nombre del tipo hello del segundo servidor de hello en **nombre del servidor**.</span><span class="sxs-lookup"><span data-stu-id="f0322-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="f0322-300">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-300">Click **Connect**.</span></span>

   <span data-ttu-id="f0322-301">Nuevo en hello **especificar réplicas** página, ahora debería ver segundo servidor de hello enumerado en **réplicas de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="f0322-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="f0322-302">Configurar réplicas de hello como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="f0322-302">Configure hello replicas as follows.</span></span>

   ![Asistente para nuevo grupo de disponibilidad, especificar réplicas (completo)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="f0322-304">Haga clic en **extremos** toosee de base de datos de hello extremo de reflejo para este grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f0322-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="f0322-305">Hola uso mismo número de puerto que usó al configurar hello [regla de firewall para los puntos de conexión de creación de reflejo de la base de datos](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="f0322-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Asistente para nuevo grupo de disponibilidad, seleccionar sincronización de datos iniciales](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="f0322-307">Hola **seleccionar sincronización de datos iniciales** , seleccione **completa** y especifique una ubicación de red compartida.</span><span class="sxs-lookup"><span data-stu-id="f0322-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="f0322-308">Para la ubicación de hello, usar hello [recurso compartido de copia de seguridad que creaste](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="f0322-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="f0322-309">En el ejemplo de Hola fue así, **\\\\\<primer servidor SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="f0322-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="f0322-310">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f0322-311">Sincronización completa toma una copia de seguridad completa de base de datos de hello en la primera instancia de SQL Server de Hola y restaurarlo toohello segunda instancia.</span><span class="sxs-lookup"><span data-stu-id="f0322-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="f0322-312">Para bases de datos grandes, no se recomienda la sincronización completa porque puede llevar mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="f0322-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="f0322-313">Puede reducir este tiempo manualmente tomando una copia de seguridad de base de datos de Hola y restaurarlo con `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="f0322-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="f0322-314">Si ya se restaure la base de datos de hello con `NO RECOVERY` en hello segundo SQL Server antes de configurar el grupo de disponibilidad de hello, elija **solo unión**.</span><span class="sxs-lookup"><span data-stu-id="f0322-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="f0322-315">Elija si desea que copia de seguridad de hello tootake después de configurar el grupo de disponibilidad de hello, **omitir la sincronización de datos inicial**.</span><span class="sxs-lookup"><span data-stu-id="f0322-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Asistente para nuevo grupo de disponibilidad, seleccionar sincronización de datos iniciales](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="f0322-317">Hola **validación** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f0322-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="f0322-318">Esta página debería ser similar toohello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="f0322-318">This page should look similar toohello following image:</span></span>

    ![Asistente para nuevo grupo de disponibilidad, validación](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="f0322-320">Hay una advertencia para la configuración de agente de escucha de hello porque no ha configurado un agente de escucha del grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f0322-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="f0322-321">Puede omitir esta advertencia porque en máquinas virtuales de Azure crear agente de escucha de hello después de crear el equilibrador de carga de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="f0322-322">Hola **resumen** página, haga clic en **finalizar**, a continuación, espere mientras el Asistente de hello configura Hola nuevo grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f0322-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="f0322-323">Hola **progreso** página, puede hacer clic en **detalles más** tooview Hola detallada progreso.</span><span class="sxs-lookup"><span data-stu-id="f0322-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="f0322-324">Una vez que haya finalizado el Asistente de hello, inspeccionar hello **resultados** tooverify de página que Hola grupo de disponibilidad se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="f0322-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Asistente para nuevo grupo de disponibilidad, resultados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="f0322-326">Haga clic en **cerrar** Asistente de hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="f0322-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="f0322-327">Hola de comprobación de grupo de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="f0322-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="f0322-328">En el **Explorador de objetos**, expanda **Alta disponibilidad de AlwaysOn** y después expanda **Grupos de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="f0322-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="f0322-329">Ahora debería ver Hola nuevo grupo de disponibilidad de este contenedor.</span><span class="sxs-lookup"><span data-stu-id="f0322-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="f0322-330">Haga clic en grupo de disponibilidad de Hola y haga clic en **Mostrar panel**.</span><span class="sxs-lookup"><span data-stu-id="f0322-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![Mostrar panel de grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="f0322-332">Su **panel AlwaysOn** debe tener un aspecto similar toothis.</span><span class="sxs-lookup"><span data-stu-id="f0322-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![Panel de grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="f0322-334">Puede ver réplicas hello, modo de conmutación por error de Hola de cada estado de sincronización hello y de réplica.</span><span class="sxs-lookup"><span data-stu-id="f0322-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="f0322-335">En **Administrador de clústeres de conmutación por error**, haga clic en el clúster.</span><span class="sxs-lookup"><span data-stu-id="f0322-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="f0322-336">Seleccione **Roles**.</span><span class="sxs-lookup"><span data-stu-id="f0322-336">Select **Roles**.</span></span> <span data-ttu-id="f0322-337">nombre de grupo de disponibilidad de Hello utilizado es un rol en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="f0322-338">Ese grupo de disponibilidad no tiene una dirección IP para las conexiones de cliente porque no ha configurado un agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="f0322-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="f0322-339">Después de crear un equilibrador de carga de Azure que va a configurar el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![Grupo de disponibilidad en el administrador de clústeres de conmutación por error.](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="f0322-341">No intente toofail sobre Hola grupo de disponibilidad desde el Administrador de clústeres de conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="f0322-342">Todas las operaciones de conmutación por error deben realizarse desde el **Panel AlwaysOn** de SSMS.</span><span class="sxs-lookup"><span data-stu-id="f0322-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="f0322-343">Para obtener más información, consulte [restricciones sobre el uso Hola Administrador de clústeres de conmutación por error con grupos de disponibilidad](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0322-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="f0322-344">En este punto, tiene un grupo de disponibilidad con réplicas en dos instancias de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="f0322-345">Puede mover Hola grupo de disponibilidad entre instancias.</span><span class="sxs-lookup"><span data-stu-id="f0322-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="f0322-346">No se puede conectar toohello grupo de disponibilidad aún porque no tiene un agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="f0322-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="f0322-347">En máquinas virtuales de Azure, el agente de escucha de hello requiere un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="f0322-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="f0322-348">Hola siguiente paso es toocreate equilibrador de carga de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="f0322-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="f0322-349">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="f0322-349">Create an Azure load balancer</span></span>

<span data-ttu-id="f0322-350">En Azure Virtual Machines, un grupo de disponibilidad de SQL Server necesita un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="f0322-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="f0322-351">equilibrador de carga de Hello contiene la dirección IP de hello para el agente de escucha del grupo de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="f0322-352">En esta sección se resume cómo toocreate Hola equilibrador de carga de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f0322-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="f0322-353">Hola portal de Azure, vaya toohello grupo de recursos donde los servidores SQL Server y haga clic en **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="f0322-354">Busque **Equilibrador de carga**.</span><span class="sxs-lookup"><span data-stu-id="f0322-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="f0322-355">Elegir el equilibrador de carga de hello publicado por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f0322-355">Choose hello load balancer published by Microsoft.</span></span>

   ![Grupo de disponibilidad en el administrador de clústeres de conmutación por error.](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="f0322-357">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f0322-357">Click **Create**.</span></span>
3. <span data-ttu-id="f0322-358">Configurar Hola parámetros para el equilibrador de carga de hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="f0322-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="f0322-359">Configuración</span><span class="sxs-lookup"><span data-stu-id="f0322-359">Setting</span></span> | <span data-ttu-id="f0322-360">Campo</span><span class="sxs-lookup"><span data-stu-id="f0322-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="f0322-361">**Name**</span><span class="sxs-lookup"><span data-stu-id="f0322-361">**Name**</span></span> |<span data-ttu-id="f0322-362">Usar un nombre de texto para el equilibrador de carga de hello, por ejemplo **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="f0322-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="f0322-363">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="f0322-363">**Type**</span></span> |<span data-ttu-id="f0322-364">Interno</span><span class="sxs-lookup"><span data-stu-id="f0322-364">Internal</span></span> |
   | <span data-ttu-id="f0322-365">**Red virtual**</span><span class="sxs-lookup"><span data-stu-id="f0322-365">**Virtual network**</span></span> |<span data-ttu-id="f0322-366">Usar el nombre de Hola de hello red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="f0322-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="f0322-367">**Subred**</span><span class="sxs-lookup"><span data-stu-id="f0322-367">**Subnet**</span></span> |<span data-ttu-id="f0322-368">Usar el nombre de Hola de subred de Hola que Hola máquina virtual está en.</span><span class="sxs-lookup"><span data-stu-id="f0322-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="f0322-369">**Asignación de dirección IP**</span><span class="sxs-lookup"><span data-stu-id="f0322-369">**IP address assignment**</span></span> |<span data-ttu-id="f0322-370">Estática</span><span class="sxs-lookup"><span data-stu-id="f0322-370">Static</span></span> |
   | <span data-ttu-id="f0322-371">**Dirección IP**</span><span class="sxs-lookup"><span data-stu-id="f0322-371">**IP address**</span></span> |<span data-ttu-id="f0322-372">Use una dirección disponible en la subred.</span><span class="sxs-lookup"><span data-stu-id="f0322-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="f0322-373">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="f0322-373">**Subscription**</span></span> |<span data-ttu-id="f0322-374">Use Hola misma suscripción que la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="f0322-375">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="f0322-375">**Location**</span></span> |<span data-ttu-id="f0322-376">Use Hola misma ubicación que la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="f0322-377">Hola portal de Azure, hoja debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="f0322-377">hello Azure portal blade should look like this:</span></span>

   ![Cree un equilibrador de carga](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="f0322-379">Haga clic en **crear**, equilibrador de carga de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="f0322-380">equilibrador de carga de hello tooconfigure, deberá toocreate un grupo back-end, un sondeo, conjunto Hola equilibrio de carga y reglas.</span><span class="sxs-lookup"><span data-stu-id="f0322-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="f0322-381">Haga lo siguiente en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f0322-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="f0322-382">Agregar grupo de back-end</span><span class="sxs-lookup"><span data-stu-id="f0322-382">Add backend pool</span></span>

1. <span data-ttu-id="f0322-383">Hola portal de Azure, vaya tooyour grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f0322-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="f0322-384">Puede que tenga el equilibrador de carga de toorefresh Hola vista toosee Hola recién creado.</span><span class="sxs-lookup"><span data-stu-id="f0322-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Buscar equilibrador de carga en el grupo de recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="f0322-386">Haga clic en el equilibrador de carga de hello, haga clic en **grupos back-end**y haga clic en **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="f0322-387">Configure el grupo de back-end de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="f0322-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="f0322-388">Configuración</span><span class="sxs-lookup"><span data-stu-id="f0322-388">Setting</span></span> | <span data-ttu-id="f0322-389">Descripción</span><span class="sxs-lookup"><span data-stu-id="f0322-389">Description</span></span> | <span data-ttu-id="f0322-390">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f0322-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="f0322-391">**Name**</span><span class="sxs-lookup"><span data-stu-id="f0322-391">**Name**</span></span> | <span data-ttu-id="f0322-392">Escribir un nombre de texto</span><span class="sxs-lookup"><span data-stu-id="f0322-392">Type a text name</span></span> | <span data-ttu-id="f0322-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="f0322-393">SQLLBBE</span></span>
   | <span data-ttu-id="f0322-394">**Asociado a**</span><span class="sxs-lookup"><span data-stu-id="f0322-394">**Associated to**</span></span> | <span data-ttu-id="f0322-395">Elegir de la lista</span><span class="sxs-lookup"><span data-stu-id="f0322-395">Pick from list</span></span> | <span data-ttu-id="f0322-396">Conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="f0322-396">Availability set</span></span>
   | <span data-ttu-id="f0322-397">**El conjunto de disponibilidad**</span><span class="sxs-lookup"><span data-stu-id="f0322-397">**Availability set**</span></span> | <span data-ttu-id="f0322-398">Usar un nombre de conjunto de disponibilidad de Hola que la VM de SQL Server se encuentran en</span><span class="sxs-lookup"><span data-stu-id="f0322-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="f0322-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="f0322-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="f0322-400">**Máquinas virtuales**</span><span class="sxs-lookup"><span data-stu-id="f0322-400">**Virtual machines**</span></span> |<span data-ttu-id="f0322-401">Hola dos nombres de VM de Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0322-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="f0322-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="f0322-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="f0322-403">Nombre del tipo hello para el grupo de servidores de hello back-end.</span><span class="sxs-lookup"><span data-stu-id="f0322-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="f0322-404">Haga clic en **+ Agregar máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="f0322-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="f0322-405">Para un conjunto de disponibilidad de hello, elija disponibilidad Hola establece ese Hola servidores SQL Server están en.</span><span class="sxs-lookup"><span data-stu-id="f0322-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="f0322-406">Para máquinas virtuales, incluir tanto de hello servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="f0322-407">No incluya el servidor de testigo de recurso compartido de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="f0322-408">Haga clic en **Aceptar** grupo back-end de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="f0322-409">Sondeo de Hola de conjunto</span><span class="sxs-lookup"><span data-stu-id="f0322-409">Set hello probe</span></span>

1. <span data-ttu-id="f0322-410">Haga clic en el equilibrador de carga de hello, haga clic en **sondeos de estado**y haga clic en **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="f0322-411">Establecer sondeo de estado de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="f0322-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="f0322-412">Configuración</span><span class="sxs-lookup"><span data-stu-id="f0322-412">Setting</span></span> | <span data-ttu-id="f0322-413">Descripción</span><span class="sxs-lookup"><span data-stu-id="f0322-413">Description</span></span> | <span data-ttu-id="f0322-414">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f0322-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="f0322-415">**Name**</span><span class="sxs-lookup"><span data-stu-id="f0322-415">**Name**</span></span> | <span data-ttu-id="f0322-416">Texto</span><span class="sxs-lookup"><span data-stu-id="f0322-416">Text</span></span> | <span data-ttu-id="f0322-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="f0322-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="f0322-418">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="f0322-418">**Protocol**</span></span> | <span data-ttu-id="f0322-419">Elija TCP</span><span class="sxs-lookup"><span data-stu-id="f0322-419">Choose TCP</span></span> | <span data-ttu-id="f0322-420">TCP</span><span class="sxs-lookup"><span data-stu-id="f0322-420">TCP</span></span> |
   | <span data-ttu-id="f0322-421">**Puerto**</span><span class="sxs-lookup"><span data-stu-id="f0322-421">**Port**</span></span> | <span data-ttu-id="f0322-422">Cualquier puerto no utilizado</span><span class="sxs-lookup"><span data-stu-id="f0322-422">Any unused port</span></span> | <span data-ttu-id="f0322-423">59999</span><span class="sxs-lookup"><span data-stu-id="f0322-423">59999</span></span> |
   | <span data-ttu-id="f0322-424">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="f0322-424">**Interval**</span></span>  | <span data-ttu-id="f0322-425">los intentos de cantidad de Hola de tiempo entre el sondeo en segundos</span><span class="sxs-lookup"><span data-stu-id="f0322-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="f0322-426">5</span><span class="sxs-lookup"><span data-stu-id="f0322-426">5</span></span> |
   | <span data-ttu-id="f0322-427">**Umbral incorrecto**</span><span class="sxs-lookup"><span data-stu-id="f0322-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="f0322-428">Hola número de errores de sondeo consecutivos que debe realizarse para una toobe de máquina virtual que se considera incorrecto</span><span class="sxs-lookup"><span data-stu-id="f0322-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="f0322-429">2</span><span class="sxs-lookup"><span data-stu-id="f0322-429">2</span></span> |

1. <span data-ttu-id="f0322-430">Haga clic en **Aceptar** sondeo de estado de tooset Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="f0322-431">Establecer reglas de equilibrio de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="f0322-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="f0322-432">Haga clic en el equilibrador de carga de hello, haga clic en **reglas de equilibrio de carga**y haga clic en **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="f0322-433">Establecer como se indica a continuación de las reglas de equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="f0322-434">Configuración</span><span class="sxs-lookup"><span data-stu-id="f0322-434">Setting</span></span> | <span data-ttu-id="f0322-435">Descripción</span><span class="sxs-lookup"><span data-stu-id="f0322-435">Description</span></span> | <span data-ttu-id="f0322-436">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f0322-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="f0322-437">**Name**</span><span class="sxs-lookup"><span data-stu-id="f0322-437">**Name**</span></span> | <span data-ttu-id="f0322-438">Texto</span><span class="sxs-lookup"><span data-stu-id="f0322-438">Text</span></span> | <span data-ttu-id="f0322-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="f0322-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="f0322-440">**Frontend IP address** (Dirección IP de front-end)</span><span class="sxs-lookup"><span data-stu-id="f0322-440">**Frontend IP address**</span></span> | <span data-ttu-id="f0322-441">Elija una dirección</span><span class="sxs-lookup"><span data-stu-id="f0322-441">Choose an address</span></span> |<span data-ttu-id="f0322-442">Usar una dirección Hola que creó cuando creó el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="f0322-443">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="f0322-443">**Protocol**</span></span> | <span data-ttu-id="f0322-444">Elija TCP</span><span class="sxs-lookup"><span data-stu-id="f0322-444">Choose TCP</span></span> |<span data-ttu-id="f0322-445">TCP</span><span class="sxs-lookup"><span data-stu-id="f0322-445">TCP</span></span> |
   | <span data-ttu-id="f0322-446">**Puerto**</span><span class="sxs-lookup"><span data-stu-id="f0322-446">**Port**</span></span> | <span data-ttu-id="f0322-447">Usar el puerto de hello para la instancia de SQL Server de Hola</span><span class="sxs-lookup"><span data-stu-id="f0322-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="f0322-448">1433</span><span class="sxs-lookup"><span data-stu-id="f0322-448">1433</span></span> |
   | <span data-ttu-id="f0322-449">**Puerto back-end**</span><span class="sxs-lookup"><span data-stu-id="f0322-449">**Backend Port**</span></span> | <span data-ttu-id="f0322-450">Este campo no se utiliza cuando la IP flotante está establecida para Direct Server Return</span><span class="sxs-lookup"><span data-stu-id="f0322-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="f0322-451">1433</span><span class="sxs-lookup"><span data-stu-id="f0322-451">1433</span></span> |
   | <span data-ttu-id="f0322-452">**Sondeo**</span><span class="sxs-lookup"><span data-stu-id="f0322-452">**Probe**</span></span> |<span data-ttu-id="f0322-453">nombre de Hola que especificó para la sonda de Hola</span><span class="sxs-lookup"><span data-stu-id="f0322-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="f0322-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="f0322-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="f0322-455">**Persistencia de la sesión**</span><span class="sxs-lookup"><span data-stu-id="f0322-455">**Session Persistence**</span></span> | <span data-ttu-id="f0322-456">Lista desplegable</span><span class="sxs-lookup"><span data-stu-id="f0322-456">Drop down list</span></span> | <span data-ttu-id="f0322-457">**None**</span><span class="sxs-lookup"><span data-stu-id="f0322-457">**None**</span></span> |
   | <span data-ttu-id="f0322-458">**Tiempo de espera de inactividad**</span><span class="sxs-lookup"><span data-stu-id="f0322-458">**Idle Timeout**</span></span> | <span data-ttu-id="f0322-459">Tookeep minutos abrir una conexión TCP</span><span class="sxs-lookup"><span data-stu-id="f0322-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="f0322-460">4</span><span class="sxs-lookup"><span data-stu-id="f0322-460">4</span></span> |
   | <span data-ttu-id="f0322-461">**IP flotante (Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="f0322-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="f0322-462">Enabled</span><span class="sxs-lookup"><span data-stu-id="f0322-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="f0322-463">Direct Server Return se establece durante la creación.</span><span class="sxs-lookup"><span data-stu-id="f0322-463">Direct server return is set during creation.</span></span> <span data-ttu-id="f0322-464">No se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="f0322-464">It cannot be changed.</span></span>

1. <span data-ttu-id="f0322-465">Haga clic en **Aceptar** equilibrio de carga de tooset Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="f0322-466"><a name="configure-listener"></a>Configurar el agente de escucha de Hola</span><span class="sxs-lookup"><span data-stu-id="f0322-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="f0322-467">Hola toodo de lo siguiente es un agente de escucha de grupo de disponibilidad en el clúster de conmutación por error de hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="f0322-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f0322-468">Este tutorial muestra cómo se direccionan toocreate un agente de escucha único - con una IP de ILB.</span><span class="sxs-lookup"><span data-stu-id="f0322-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="f0322-469">toocreate uno o varios agentes de escucha con una o varias direcciones IP, consulte [equilibrador de carga y el agente de escucha de Create Availability Group | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0322-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="f0322-470">Configuración del puerto del agente de escucha</span><span class="sxs-lookup"><span data-stu-id="f0322-470">Set listener port</span></span>

<span data-ttu-id="f0322-471">En SQL Server Management Studio, establezca el puerto de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="f0322-472">Inicie SQL Server Management Studio y conéctese toohello de réplica principal.</span><span class="sxs-lookup"><span data-stu-id="f0322-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="f0322-473">Navegue demasiado**alta disponibilidad de AlwaysOn** | **grupos de disponibilidad** | **los agentes de escucha del grupo de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="f0322-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="f0322-474">Ahora debería ver el nombre de agente de escucha de Hola que creó en el Administrador de clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="f0322-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="f0322-475">Haga clic en nombre de agente de escucha de Hola y haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="f0322-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="f0322-476">Hola **puerto** , especifique el número de puerto de hello para el agente de escucha del grupo de disponibilidad de hello mediante el uso de hello $EndpointPort que usó anteriormente (1433 pasaba Hola valor predeterminado), a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f0322-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="f0322-477">Ahora tiene un grupo de disponibilidad de SQL Server en Azure Virtual Machines que se ejecuta en el modo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f0322-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="f0322-478">Toolistener de conexión de prueba</span><span class="sxs-lookup"><span data-stu-id="f0322-478">Test connection toolistener</span></span>

<span data-ttu-id="f0322-479">conexión de Hola tootest:</span><span class="sxs-lookup"><span data-stu-id="f0322-479">tootest hello connection:</span></span>

1. <span data-ttu-id="f0322-480">RDP tooa SQL Server que se encuentra en hello mismo virtual de red, pero no no réplica Hola propio.</span><span class="sxs-lookup"><span data-stu-id="f0322-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="f0322-481">Puede usar Hola a otro servidor SQL Server en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="f0322-482">Use **sqlcmd** conexión de utilidad tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="f0322-483">Por ejemplo, Establece la siguiente secuencia de comandos de hello un **sqlcmd** réplica principal de conexión toohello a través de agente de escucha de hello con autenticación de Windows:</span><span class="sxs-lookup"><span data-stu-id="f0322-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="f0322-484">Si el agente de escucha de hello usa un puerto distinto de hello predeterminado (1433) de puerto, especifique el puerto hello en la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0322-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="f0322-485">Por ejemplo, hello siguiente comando sqlcmd conecta tooa escucha en el puerto 1435:</span><span class="sxs-lookup"><span data-stu-id="f0322-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="f0322-486">Hola conexión SQLCMD conecta automáticamente toowhichever instancia de réplica principal de Hola de hosts de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="f0322-487">Asegúrese de que especifica el puerto de hello está abierto en firewall de Hola de ambos servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0322-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="f0322-488">Ambos servidores requieren una regla de entrada para el puerto TCP que usa hello.</span><span class="sxs-lookup"><span data-stu-id="f0322-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="f0322-489">Consulte [Agregar o editar regla de firewall](http://technet.microsoft.com/library/cc753558.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="f0322-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="f0322-490">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f0322-490">Next steps</span></span>

- <span data-ttu-id="f0322-491">[Agregar un equilibrador de carga de tooa de dirección IP para un segundo grupo de disponibilidad](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="f0322-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>

---
title: "Administración de clústeres de HDInsight unidos a dominio - Azure | Microsoft Docs"
description: "Aprenda a administrar clústeres de HDInsight unidos a dominio"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 9b56ce6cc5bdd3b8d48d047751e978cad08598e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="13b15-103">Administración de clústeres de HDInsight unidos a dominio (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="13b15-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="13b15-104">Conozca los usuarios y los roles de HDInsight unido a un dominio y cómo administrar clústeres de HDInsight unidos a dominio.</span><span class="sxs-lookup"><span data-stu-id="13b15-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="13b15-105">Usuarios de clústeres de HDInsight unidos a dominio</span><span class="sxs-lookup"><span data-stu-id="13b15-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="13b15-106">Un clúster de HDInsight que no está unido a un dominio tiene dos cuentas de usuario que se crean durante la creación del clúster:</span><span class="sxs-lookup"><span data-stu-id="13b15-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="13b15-107">**Administrador de Ambari**: esta cuenta es también conocida como *usuario de Hadoop* o *usuario de HTTP*.</span><span class="sxs-lookup"><span data-stu-id="13b15-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="13b15-108">Esta cuenta puede usarse para iniciar sesión en Ambari en https://&lt;nombreDeClúster >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="13b15-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="13b15-109">También puede usarse para ejecutar consultas en vistas de Ambari, ejecutar trabajos mediante herramientas externas (es decir, PowerShell, Templeton, Visual Studio) y autenticarse con el controlador ODBC de Hive y herramientas de BI (es decir, Excel, PowerBI o Tableau).</span><span class="sxs-lookup"><span data-stu-id="13b15-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="13b15-110">**Usuario de SSH**: esta cuenta se puede usar con SSH y permite ejecutar comandos de sudo.</span><span class="sxs-lookup"><span data-stu-id="13b15-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="13b15-111">Tiene privilegios raíz a las máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="13b15-111">It has root privileges to the Linux VMs.</span></span>

<span data-ttu-id="13b15-112">Un clúster de HDInsight unido a dominio tiene tres nuevos usuarios además de administrador de Ambari y usuario de SSH.</span><span class="sxs-lookup"><span data-stu-id="13b15-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span></span>

* <span data-ttu-id="13b15-113">**Administrador de Ranger**: esta cuenta es la cuenta de administrador local de Apache Ranger.</span><span class="sxs-lookup"><span data-stu-id="13b15-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="13b15-114">No es un usuario de dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13b15-114">It is not an active directory domain user.</span></span> <span data-ttu-id="13b15-115">Esta cuenta se puede usar para configurar directivas y crear otros administradores de usuarios o administradores delegados (para que esos usuarios puedan administrar directivas).</span><span class="sxs-lookup"><span data-stu-id="13b15-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="13b15-116">De forma predeterminada, el nombre de usuario es *admin* y la contraseña es la misma que la contraseña de administrador de Ambari.</span><span class="sxs-lookup"><span data-stu-id="13b15-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="13b15-117">En la página de configuración de Ranger se puede actualizar la contraseña.</span><span class="sxs-lookup"><span data-stu-id="13b15-117">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="13b15-118">**Usuario de dominio administrador de clúster**: esta cuenta es un usuario de dominio de Active Directory designado como administrador de clúster de Hadoop, por ejemplo Ambari y Ranger.</span><span class="sxs-lookup"><span data-stu-id="13b15-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="13b15-119">Se deben proporcionar las credenciales del usuario durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="13b15-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="13b15-120">Este usuario tiene los privilegios siguientes:</span><span class="sxs-lookup"><span data-stu-id="13b15-120">This user has the following privileges:</span></span>

  * <span data-ttu-id="13b15-121">Unir máquinas al dominio y colocarlas en la unidad organizativa que especifique durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="13b15-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="13b15-122">Crear entidades de servicio dentro de la unidad organizativa que especifique durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="13b15-122">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="13b15-123">Crear entradas de DNS inversas.</span><span class="sxs-lookup"><span data-stu-id="13b15-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="13b15-124">Tenga en cuenta que los demás usuarios de AD también tienen estos privilegios.</span><span class="sxs-lookup"><span data-stu-id="13b15-124">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="13b15-125">Hay algunos puntos de conexión en el clúster (por ejemplo, Templeton) que no están administrados por Ranger, de ahí que no sean seguros.</span><span class="sxs-lookup"><span data-stu-id="13b15-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="13b15-126">Estos puntos de conexión están bloqueados para todos los usuarios excepto para el usuario de dominio administrador del clúster.</span><span class="sxs-lookup"><span data-stu-id="13b15-126">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="13b15-127">**Normal**: durante la creación del clúster, puede proporcionar varios grupos de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13b15-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="13b15-128">Los usuarios de estos grupos se sincronizarán con Ranger y Ambari.</span><span class="sxs-lookup"><span data-stu-id="13b15-128">The users in these groups will be synced to Ranger and Ambari.</span></span> <span data-ttu-id="13b15-129">Estos usuarios son usuarios de dominio y solo tendrán acceso a los puntos de conexión administrados por Ranger (por ejemplo, Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="13b15-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="13b15-130">Todas las directivas y la auditoría de RBAC serán aplicable a estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="13b15-130">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="13b15-131">Roles de clústeres de HDInsight unidos a dominio</span><span class="sxs-lookup"><span data-stu-id="13b15-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="13b15-132">Los clústeres de HDInsight unidos a un dominio tienen los siguientes roles:</span><span class="sxs-lookup"><span data-stu-id="13b15-132">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="13b15-133">Administrador de clústeres</span><span class="sxs-lookup"><span data-stu-id="13b15-133">Cluster Administrator</span></span>
* <span data-ttu-id="13b15-134">Operador de clústeres</span><span class="sxs-lookup"><span data-stu-id="13b15-134">Cluster Operator</span></span>
* <span data-ttu-id="13b15-135">Administrador de servicios</span><span class="sxs-lookup"><span data-stu-id="13b15-135">Service Administrator</span></span>
* <span data-ttu-id="13b15-136">Operador de servicio</span><span class="sxs-lookup"><span data-stu-id="13b15-136">Service Operator</span></span>
* <span data-ttu-id="13b15-137">Usuario del clúster</span><span class="sxs-lookup"><span data-stu-id="13b15-137">Cluster User</span></span>

<span data-ttu-id="13b15-138">**Para ver los permisos de estos roles:**</span><span class="sxs-lookup"><span data-stu-id="13b15-138">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="13b15-139">Abra la interfaz de usuario de administración de Ambari.</span><span class="sxs-lookup"><span data-stu-id="13b15-139">Open the Ambari Management UI.</span></span>  <span data-ttu-id="13b15-140">Consulte [Abrir la interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="13b15-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="13b15-141">En el menú de la izquierda, haga clic en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="13b15-141">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="13b15-142">Haga clic en el signo de interrogación azul para ver los permisos:</span><span class="sxs-lookup"><span data-stu-id="13b15-142">Click the blue question mark to see the permissions:</span></span>

    ![Permisos de roles de HDInsight unidos a dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="13b15-144">Abrir la interfaz de usuario de administración de Ambari</span><span class="sxs-lookup"><span data-stu-id="13b15-144">Open the Ambari Management UI</span></span>
1. <span data-ttu-id="13b15-145">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13b15-145">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="13b15-146">Abra el clúster de HDInsight en una hoja.</span><span class="sxs-lookup"><span data-stu-id="13b15-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="13b15-147">Consulte [Enumeración y visualización de clústeres](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="13b15-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="13b15-148">Haga clic en **Panel** en el menú superior para abrir Ambari.</span><span class="sxs-lookup"><span data-stu-id="13b15-148">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="13b15-149">Inicie sesión en Ambari con el nombre de usuario y la contraseña de dominio de administrador del clúster:</span><span class="sxs-lookup"><span data-stu-id="13b15-149">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="13b15-150">Haga clic en el menú desplegable **Administrador** de la esquina superior derecha y luego haga clic en **Administrar Ambari**.</span><span class="sxs-lookup"><span data-stu-id="13b15-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![Administración de Ambari para HDInsight unido a un dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="13b15-152">La interfaz de usuario tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="13b15-152">The UI looks like:</span></span>

    ![IU de administración de Ambari para HDInsight unido a dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="13b15-154">Enumeración de los usuarios de dominio sincronizados desde Active Directory</span><span class="sxs-lookup"><span data-stu-id="13b15-154">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="13b15-155">Abra la interfaz de usuario de administración de Ambari.</span><span class="sxs-lookup"><span data-stu-id="13b15-155">Open the Ambari Management UI.</span></span>  <span data-ttu-id="13b15-156">Consulte [Abrir la interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="13b15-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="13b15-157">En el menú de la izquierda, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="13b15-157">From the left menu, click **Users**.</span></span> <span data-ttu-id="13b15-158">Verá todos los usuarios sincronizados desde Active Directory con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13b15-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![IU de administración de Ambari para HDInsight unido a dominio: enumeración de usuarios](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="13b15-160">Enumeración de los grupos de dominios sincronizados desde Active Directory</span><span class="sxs-lookup"><span data-stu-id="13b15-160">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="13b15-161">Abra la interfaz de usuario de administración de Ambari.</span><span class="sxs-lookup"><span data-stu-id="13b15-161">Open the Ambari Management UI.</span></span>  <span data-ttu-id="13b15-162">Consulte [Abrir la interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="13b15-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="13b15-163">En el menú de la izquierda, haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="13b15-163">From the left menu, click **Groups**.</span></span> <span data-ttu-id="13b15-164">Verá todos los grupos sincronizados desde Active Directory con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="13b15-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![IU de administración de Ambari para HDInsight unido a dominio: enumeración de grupos](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="13b15-166">Configuración de permisos de vistas de Hive</span><span class="sxs-lookup"><span data-stu-id="13b15-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="13b15-167">Abra la interfaz de usuario de administración de Ambari.</span><span class="sxs-lookup"><span data-stu-id="13b15-167">Open the Ambari Management UI.</span></span>  <span data-ttu-id="13b15-168">Consulte [Abrir la interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="13b15-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="13b15-169">En el menú de la izquierda, haga clic en **Vistas**.</span><span class="sxs-lookup"><span data-stu-id="13b15-169">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="13b15-170">Haga clic en **HIVE** para mostrar los detalles.</span><span class="sxs-lookup"><span data-stu-id="13b15-170">Click **HIVE** to show the details.</span></span>

    ![IU de administración de Ambari para HDInsight unido a dominio: vistas de Hive](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="13b15-172">Haga clic en el vínculo **Vista de Hive** para configurar vistas de Hive.</span><span class="sxs-lookup"><span data-stu-id="13b15-172">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="13b15-173">Desplácese hacia abajo hasta la sección **Permisos**.</span><span class="sxs-lookup"><span data-stu-id="13b15-173">Scroll down to the **Permissions** section.</span></span>

    ![IU de administración de Ambari para HDInsight unido a dominio: vistas de Hive, configuración de permisos](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="13b15-175">Haga clic en **Agregar usuario** o **Agregar grupo**, y especifique los usuarios o grupos que pueden usar vistas de Hive.</span><span class="sxs-lookup"><span data-stu-id="13b15-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="13b15-176">Configuración de usuarios para los roles</span><span class="sxs-lookup"><span data-stu-id="13b15-176">Configure users for the roles</span></span>
 <span data-ttu-id="13b15-177">Para ver una lista de roles y sus permisos, consulte [Roles de clústeres de HDInsight unidos a dominio](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="13b15-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="13b15-178">Abra la interfaz de usuario de administración de Ambari.</span><span class="sxs-lookup"><span data-stu-id="13b15-178">Open the Ambari Management UI.</span></span>  <span data-ttu-id="13b15-179">Consulte [Abrir la interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="13b15-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="13b15-180">En el menú de la izquierda, haga clic en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="13b15-180">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="13b15-181">Haga clic en **Agregar usuario** o **Agregar grupo** para asignar usuarios y grupos a roles diferentes.</span><span class="sxs-lookup"><span data-stu-id="13b15-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13b15-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13b15-182">Next steps</span></span>
* <span data-ttu-id="13b15-183">Para configurar un clúster de HDInsight unido a dominio, consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).</span><span class="sxs-lookup"><span data-stu-id="13b15-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="13b15-184">Para configurar directivas de Hive y ejecución de consultas de Hive, consulte [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configuración de directivas de los clústeres de HDInsight unidos a dominio).</span><span class="sxs-lookup"><span data-stu-id="13b15-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="13b15-185">Para ejecutar consultas de Hive mediante SSH en clústeres de HDInsight unidos a un dominio, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="13b15-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>

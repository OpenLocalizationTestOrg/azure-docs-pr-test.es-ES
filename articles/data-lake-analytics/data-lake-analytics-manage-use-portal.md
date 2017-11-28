---
title: "Administración de Azure Data Lake Analytics con el portal de Azure | Microsoft Docs"
description: "Aprenda a administrar cuentas, orígenes de datos, usuarios y trabajos de Análisis de Data Lake."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e49d1a0e0ccc6567d0a6841817667717ff5dba76
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-the-azure-portal"></a><span data-ttu-id="0ec72-103">Administración de Azure Data Lake Analytics con el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0ec72-103">Manage Azure Data Lake Analytics by using the Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="0ec72-104">Aprenda a administrar cuentas, orígenes de datos, usuarios y trabajos de Azure Data Lake Analytics mediante el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec72-104">Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using the Azure portal.</span></span> <span data-ttu-id="0ec72-105">Para ver los temas de administración sobre el uso de otras herramientas, haga clic en una pestaña de la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="0ec72-105">To see management topics about using other tools, click a tab at the top of the page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="0ec72-106">Administración de cuentas de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ec72-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="0ec72-107">Crear una cuenta</span><span class="sxs-lookup"><span data-stu-id="0ec72-107">Create an account</span></span>

1. <span data-ttu-id="0ec72-108">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ec72-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0ec72-109">Haga clic en **Nuevo** > **Inteligencia y análisis** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="0ec72-110">Seleccione los valores de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0ec72-110">Select values for the following items:</span></span> 
   1. <span data-ttu-id="0ec72-111">**Nombre**: nombre de la cuenta de Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-111">**Name**: The name of the Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="0ec72-112">**Suscripción**: suscripción de Azure usada para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-112">**Subscription**: The Azure subscription used for the account.</span></span>
   3. <span data-ttu-id="0ec72-113">**Grupo de recursos**: grupo de recursos de Azure en el que se va a crear la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-113">**Resource Group**: The Azure resource group in which to create the account.</span></span> 
   4. <span data-ttu-id="0ec72-114">**Ubicación**: centro de datos de Azure para la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-114">**Location**: The Azure datacenter for the Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="0ec72-115">**Data Lake Store**: almacén predeterminado que se va a usar para la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-115">**Data Lake Store**: The default store to be used for the Data Lake Analytics account.</span></span> <span data-ttu-id="0ec72-116">Las cuentas de Azure Data Lake Store y de Data Lake Analytics deben estar en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="0ec72-116">The Azure Data Lake Store account and the Data Lake Analytics account must be in the same location.</span></span>
4. <span data-ttu-id="0ec72-117">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="0ec72-118">Eliminar una cuenta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ec72-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="0ec72-119">Para eliminar una cuenta de Data Lake Analytics, elimine la cuenta de Data Lake Store predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0ec72-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="0ec72-120">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-120">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-121">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-121">Click **Delete**.</span></span>
3. <span data-ttu-id="0ec72-122">Escriba el nombre de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-122">Type the account name.</span></span>
4. <span data-ttu-id="0ec72-123">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="0ec72-124">Administración de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="0ec72-124">Manage data sources</span></span>

<span data-ttu-id="0ec72-125">Data Lake Analytics admite los siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="0ec72-125">Data Lake Analytics supports the following data sources:</span></span>

* <span data-ttu-id="0ec72-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0ec72-126">Data Lake Store</span></span>
* <span data-ttu-id="0ec72-127">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="0ec72-127">Azure Storage</span></span>

<span data-ttu-id="0ec72-128">Puede usar el explorador de datos para examinar los orígenes de datos y realizar operaciones básicas de administración de archivos.</span><span class="sxs-lookup"><span data-stu-id="0ec72-128">You can use Data Explorer to browse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="0ec72-129">Agregar un origen de datos</span><span class="sxs-lookup"><span data-stu-id="0ec72-129">Add a data source</span></span>

1. <span data-ttu-id="0ec72-130">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-130">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-131">Haga clic en **Orígenes de datos**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="0ec72-132">Haga clic en **Agregar origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="0ec72-133">Para agregar una cuenta de Data Lake Store, necesita el nombre de la cuenta y acceso a ella para poder realizar consultas.</span><span class="sxs-lookup"><span data-stu-id="0ec72-133">To add a Data Lake Store account, you need the account name and access to the account to be able to query it.</span></span>
   * <span data-ttu-id="0ec72-134">Para agregar Azure Blob Storage, necesita la cuenta y la clave de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0ec72-134">To add Azure Blob storage, you need the storage account and the account key.</span></span> <span data-ttu-id="0ec72-135">Para encontrarlas, vaya a la cuenta de almacenamiento en el portal.</span><span class="sxs-lookup"><span data-stu-id="0ec72-135">To find them, go to the storage account in the portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="0ec72-136">Configurar reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="0ec72-136">Set up firewall rules</span></span>

<span data-ttu-id="0ec72-137">Puede usar Data Lake Analytics para bloquear aún más el acceso a la cuenta de Data Lake Analytics en el nivel de red.</span><span class="sxs-lookup"><span data-stu-id="0ec72-137">You can use Data Lake Analytics to further lock down access to your Data Lake Analytics account at the network level.</span></span> <span data-ttu-id="0ec72-138">Puede habilitar un firewall, especificar una dirección IP o definir un intervalo de direcciones IP para los clientes de confianza.</span><span class="sxs-lookup"><span data-stu-id="0ec72-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="0ec72-139">Una vez habilitadas estas medidas, solo los clientes con direcciones IP del intervalo definido pueden conectarse al almacén.</span><span class="sxs-lookup"><span data-stu-id="0ec72-139">After you enable these measures, only clients that have the IP addresses within the defined range can connect to the store.</span></span>

<span data-ttu-id="0ec72-140">Si otros servicios de Azure, como Azure Data Factory o las máquinas virtuales, se conectan a la cuenta de Data Lake Analytics, asegúrese de que **Permitir los servicios de Azure** esté **Activado**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-140">If other Azure services, like Azure Data Factory or VMs, connect to the Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="0ec72-141">Configurar una regla de firewall</span><span class="sxs-lookup"><span data-stu-id="0ec72-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="0ec72-142">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-142">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-143">En el menú de la izquierda, haga clic en **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-143">On the menu on the left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="0ec72-144">Agregar un nuevo usuario</span><span class="sxs-lookup"><span data-stu-id="0ec72-144">Add a new user</span></span>

<span data-ttu-id="0ec72-145">Puede usar el **Asistente para agregar usuario** para aprovisionar fácilmente nuevos usuarios de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0ec72-145">You can use the **Add User Wizard** to easily provision new Data Lake users.</span></span>

1. <span data-ttu-id="0ec72-146">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-146">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-147">A la izquierda, en **Introducción**, haga clic en **Asistente para agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-147">On the left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="0ec72-148">Seleccione un usuario y luego haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="0ec72-149">Seleccione un rol y luego haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="0ec72-150">Para configurar un nuevo desarrollador que use Azure Data Lake, seleccione el rol **Desarrollador de Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-150">To set up a new developer to use Azure Data Lake, select the **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="0ec72-151">Seleccione las listas de control de acceso (ACL) para las bases de datos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0ec72-151">Select the access control lists (ACLs) for the U-SQL databases.</span></span> <span data-ttu-id="0ec72-152">Cuando esté satisfecho con las opciones seleccionadas, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="0ec72-153">Seleccione las ACL para los archivos.</span><span class="sxs-lookup"><span data-stu-id="0ec72-153">Select the ACLs for files.</span></span> <span data-ttu-id="0ec72-154">Para el almacén predeterminado, no cambie las ACL de la carpeta raíz "/" ni de la carpeta /system.</span><span class="sxs-lookup"><span data-stu-id="0ec72-154">For the default store, don't change the ACLs for the root folder "/" and for the /system folder.</span></span> <span data-ttu-id="0ec72-155">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-155">Click **Select**.</span></span>
7. <span data-ttu-id="0ec72-156">Revise todos los cambios seleccionados y luego haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="0ec72-157">Al finalizar el asistente, haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-157">When the wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="0ec72-158">Administrar el control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="0ec72-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="0ec72-159">Al igual que otros servicios de Azure, puede usar el control de acceso basado en roles (RBAC) para controlar cómo interactúan los usuarios con el servicio.</span><span class="sxs-lookup"><span data-stu-id="0ec72-159">Like other Azure services, you can use Role-Based Access Control (RBAC) to control how users interact with the service.</span></span>

<span data-ttu-id="0ec72-160">Los roles estándar de RBAC tienen las siguientes capacidades:</span><span class="sxs-lookup"><span data-stu-id="0ec72-160">The standard RBAC roles have the following capabilities:</span></span>
* <span data-ttu-id="0ec72-161">**Propietario**: puede enviar, supervisar y cancelar trabajos de cualquier usuario y configurar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="0ec72-162">**Colaborador**: puede enviar, supervisar y cancelar trabajos de cualquier usuario y configurar la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="0ec72-163">**Lector**: puede supervisar trabajos.</span><span class="sxs-lookup"><span data-stu-id="0ec72-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="0ec72-164">Emplee el rol de desarrollador de Data Lake Analytics para permitir que los desarrolladores de U-SQL usen el servicio Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-164">Use the Data Lake Analytics Developer role to enable U-SQL developers to use the Data Lake Analytics service.</span></span> <span data-ttu-id="0ec72-165">Puede usar el rol de desarrollador de Data Lake Analytics para:</span><span class="sxs-lookup"><span data-stu-id="0ec72-165">You can use the Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="0ec72-166">Enviar trabajos.</span><span class="sxs-lookup"><span data-stu-id="0ec72-166">Submit jobs.</span></span>
* <span data-ttu-id="0ec72-167">Supervisar el estado y el progreso de los trabajos enviados por cualquier usuario.</span><span class="sxs-lookup"><span data-stu-id="0ec72-167">Monitor job status and the progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="0ec72-168">Ver los scripts de U-SQL de los trabajos enviados por cualquier usuario.</span><span class="sxs-lookup"><span data-stu-id="0ec72-168">See the U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="0ec72-169">Cancelar solo sus propios trabajos.</span><span class="sxs-lookup"><span data-stu-id="0ec72-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-to-a-data-lake-analytics-account"></a><span data-ttu-id="0ec72-170">Agregar usuarios o grupos de seguridad a una cuenta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ec72-170">Add users or security groups to a Data Lake Analytics account</span></span>

1. <span data-ttu-id="0ec72-171">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-171">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-172">Haga clic en **Control de acceso (IAM)** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="0ec72-173">Seleccione un rol.</span><span class="sxs-lookup"><span data-stu-id="0ec72-173">Select a role.</span></span>
4. <span data-ttu-id="0ec72-174">Agregue un usuario.</span><span class="sxs-lookup"><span data-stu-id="0ec72-174">Add a user.</span></span>
5. <span data-ttu-id="0ec72-175">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="0ec72-176">Si un usuario o un grupo de seguridad necesita enviar trabajos, también necesita permiso en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0ec72-176">If a user or a security group needs to submit jobs, they also need permission on the store account.</span></span> <span data-ttu-id="0ec72-177">Para más información, vea [Secure data stored in Data Lake Store (Protección de datos almacenados en Data Lake Store)](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="0ec72-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="0ec72-178">Trabajos de administración</span><span class="sxs-lookup"><span data-stu-id="0ec72-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="0ec72-179">Enviar un trabajo</span><span class="sxs-lookup"><span data-stu-id="0ec72-179">Submit a job</span></span>

1. <span data-ttu-id="0ec72-180">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-180">In the Azure portal, go to your Data Lake Analytics account.</span></span>

2. <span data-ttu-id="0ec72-181">Haga clic en **Nuevo trabajo**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-181">Click **New Job**.</span></span> <span data-ttu-id="0ec72-182">Para cada trabajo, configure:</span><span class="sxs-lookup"><span data-stu-id="0ec72-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="0ec72-183">**Nombre del trabajo**: nombre del trabajo.</span><span class="sxs-lookup"><span data-stu-id="0ec72-183">**Job Name**: The name of the job.</span></span>
    2. <span data-ttu-id="0ec72-184">**Prioridad**: los números más bajos tienen mayor prioridad.</span><span class="sxs-lookup"><span data-stu-id="0ec72-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="0ec72-185">Si hay dos trabajos en cola, se ejecuta primero el que tenga un valor de prioridad más bajo.</span><span class="sxs-lookup"><span data-stu-id="0ec72-185">If two jobs are queued, the one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="0ec72-186">**Paralelismo**: número máximo de procesos de cálculo que se van a reservar para este trabajo.</span><span class="sxs-lookup"><span data-stu-id="0ec72-186">**Parallelism**: The maximum number of compute processes to reserve for this job.</span></span>

3. <span data-ttu-id="0ec72-187">Haga clic en **Enviar trabajo**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="0ec72-188">Supervisión de trabajos</span><span class="sxs-lookup"><span data-stu-id="0ec72-188">Monitor jobs</span></span>

1. <span data-ttu-id="0ec72-189">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-189">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-190">Haga clic en **Ver todos los trabajos**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-190">Click **View All Jobs**.</span></span> <span data-ttu-id="0ec72-191">Se muestra una lista de todos los trabajos activos y finalizados recientemente en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-191">A list of all the active and recently finished jobs in the account is shown.</span></span>
3. <span data-ttu-id="0ec72-192">De forma opcional, haga clic en **Filtrar** para encontrar los trabajos por los valores **Intervalo de tiempo**, **Nombre del trabajo** y **Autor**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-192">Optionally, click **Filter** to help you find the jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="0ec72-193">Supervisión de trabajos de canalización</span><span class="sxs-lookup"><span data-stu-id="0ec72-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="0ec72-194">Los trabajos que forman parte de un trabajo de canalización actúan juntos, normalmente de forma secuencial, para lograr un escenario concreto.</span><span class="sxs-lookup"><span data-stu-id="0ec72-194">Jobs that are part of a pipeline work together, usually sequentially, to accomplish a specific scenario.</span></span> <span data-ttu-id="0ec72-195">Por ejemplo, puede tener una canalización que limpia, extrae, transforma y agrega el uso para información del cliente.</span><span class="sxs-lookup"><span data-stu-id="0ec72-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="0ec72-196">Los trabajos de canalización se identifican mediante la propiedad "Pipeline" al enviar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="0ec72-196">Pipeline jobs are identified using the "Pipeline" property when the job was submitted.</span></span> <span data-ttu-id="0ec72-197">En los trabajos programados con ADF V2 esta propiedad se rellena de forma automática.</span><span class="sxs-lookup"><span data-stu-id="0ec72-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="0ec72-198">Para ver una lista de trabajos de U-SQL que forman parte de canalizaciones:</span><span class="sxs-lookup"><span data-stu-id="0ec72-198">To view a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="0ec72-199">En Azure Portal, vaya a las cuentas de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-199">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="0ec72-200">Haga clic en **Información de trabajos**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-200">Click **Job Insights**.</span></span> <span data-ttu-id="0ec72-201">La pestaña "Todos los trabajos" aparece de forma predeterminada y muestra una lista de trabajos en ejecución, en cola y finalizados.</span><span class="sxs-lookup"><span data-stu-id="0ec72-201">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="0ec72-202">Haga clic en la pestaña **Trabajos de canalización**. Se muestra una lista de trabajos de canalización junto con estadísticas agregadas de cada canalización.</span><span class="sxs-lookup"><span data-stu-id="0ec72-202">Click the **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="0ec72-203">Supervisión de trabajos periódicos</span><span class="sxs-lookup"><span data-stu-id="0ec72-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="0ec72-204">Un trabajo periódico es aquel que tiene la misma lógica de negocios pero usa distintos datos de entrada cada vez que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-204">A recurring job is one that has the same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="0ec72-205">Lo ideal sería que los trabajos periódicos siempre fueran correctos y tuvieran un tiempo de ejecución relativamente estable; la supervisión de estos comportamientos ayuda a garantizar que el trabajo sea correcto.</span><span class="sxs-lookup"><span data-stu-id="0ec72-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure the job is healthy.</span></span> <span data-ttu-id="0ec72-206">Los trabajos periódicos se identifican mediante la propiedad "Recurrence".</span><span class="sxs-lookup"><span data-stu-id="0ec72-206">Recurring jobs are identified using the "Recurrence" property.</span></span> <span data-ttu-id="0ec72-207">En los trabajos programados con ADF V2 esta propiedad se rellena de forma automática.</span><span class="sxs-lookup"><span data-stu-id="0ec72-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="0ec72-208">Para ver una lista de trabajos de U-SQL que son periódicos:</span><span class="sxs-lookup"><span data-stu-id="0ec72-208">To view a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="0ec72-209">En Azure Portal, vaya a las cuentas de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-209">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="0ec72-210">Haga clic en **Información de trabajos**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-210">Click **Job Insights**.</span></span> <span data-ttu-id="0ec72-211">La pestaña "Todos los trabajos" aparece de forma predeterminada y muestra una lista de trabajos en ejecución, en cola y finalizados.</span><span class="sxs-lookup"><span data-stu-id="0ec72-211">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="0ec72-212">Haga clic en la pestaña **Trabajos periódicos**. Se muestra una lista de trabajos periódicos junto con estadísticas agregadas de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="0ec72-212">Click the **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="0ec72-213">Administración de directivas</span><span class="sxs-lookup"><span data-stu-id="0ec72-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="0ec72-214">Directivas de nivel de cuenta</span><span class="sxs-lookup"><span data-stu-id="0ec72-214">Account-level policies</span></span>

<span data-ttu-id="0ec72-215">Estas directivas se aplican a todos los trabajos de una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-215">These policies apply to all jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="0ec72-216">Número máximo de unidades de análisis en una cuenta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ec72-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="0ec72-217">Una directiva controla el número total de unidades de análisis (AU) que puede usar la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-217">A policy controls the total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="0ec72-218">De forma predeterminada, el valor se establece en 250.</span><span class="sxs-lookup"><span data-stu-id="0ec72-218">By default, the value is set to 250.</span></span> <span data-ttu-id="0ec72-219">Por ejemplo, si este valor está establecido en 250 unidades, puede tener un trabajo en ejecución con 250 unidades asignadas o 10 trabajos en ejecución con 25 unidades cada uno.</span><span class="sxs-lookup"><span data-stu-id="0ec72-219">For example, if this value is set to 250 AUs, you can have one job running with 250 AUs assigned to it, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="0ec72-220">Los trabajos adicionales que se envían se ponen en cola hasta que finalizan los trabajos en ejecución.</span><span class="sxs-lookup"><span data-stu-id="0ec72-220">Additional jobs that are submitted are queued until the running jobs are finished.</span></span> <span data-ttu-id="0ec72-221">Cuando terminan los trabajos en ejecución, se liberan unidades de análisis para la ejecución de los trabajos en cola.</span><span class="sxs-lookup"><span data-stu-id="0ec72-221">When running jobs are finished, AUs are freed up for the queued jobs to run.</span></span>

<span data-ttu-id="0ec72-222">Para cambiar el número de unidades de análisis de la cuenta de Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="0ec72-222">To change the number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="0ec72-223">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-223">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-224">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-224">Click **Properties**.</span></span>
3. <span data-ttu-id="0ec72-225">En **Número de AU máximo**, mueva el control deslizante para seleccionar un valor o escríbalo en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0ec72-225">Under **Maximum AUs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="0ec72-226">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="0ec72-227">Si necesita más unidades de análisis que el valor predeterminado (250), haga clic en **Ayuda y soporte técnico** en el portal para enviar una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="0ec72-227">If you need more than the default (250) AUs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="0ec72-228">Es posible aumentar el número de unidades de análisis disponibles en la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-228">The number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="0ec72-229">Número máximo de trabajos que se pueden ejecutar simultáneamente</span><span class="sxs-lookup"><span data-stu-id="0ec72-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="0ec72-230">Una directiva controla cuántos trabajos pueden ejecutarse al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="0ec72-230">A policy controls how many jobs can run at the same time.</span></span> <span data-ttu-id="0ec72-231">De forma predeterminada, este valor se establece en 20.</span><span class="sxs-lookup"><span data-stu-id="0ec72-231">By default, this value is set to 20.</span></span> <span data-ttu-id="0ec72-232">Si Data Lake Analytics tiene unidades de análisis disponibles, los trabajos nuevos se programan para ejecutarse de inmediato hasta que el número total de trabajos en ejecución alcanza el valor de esta directiva.</span><span class="sxs-lookup"><span data-stu-id="0ec72-232">If your Data Lake Analytics has AUs available, new jobs are scheduled to run immediately until the total number of running jobs reaches the value of this policy.</span></span> <span data-ttu-id="0ec72-233">Cuando se alcanza el número máximo de trabajos que se pueden ejecutar al mismo tiempo, los trabajos posteriores se ponen en cola en orden de prioridad hasta que finalizan uno o varios de los trabajos que están en ejecución (según la disponibilidad de unidades de análisis).</span><span class="sxs-lookup"><span data-stu-id="0ec72-233">When you reach the maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="0ec72-234">Para cambiar el número de trabajos que se pueden ejecutar simultáneamente:</span><span class="sxs-lookup"><span data-stu-id="0ec72-234">To change the number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="0ec72-235">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-235">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-236">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-236">Click **Properties**.</span></span>
3. <span data-ttu-id="0ec72-237">En **Número máximo de trabajos en ejecución**, mueva el control deslizante para seleccionar un valor o escríbalo en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0ec72-237">Under **Maximum Number of Running Jobs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="0ec72-238">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="0ec72-239">Si necesita ejecutar más que el número predeterminado de trabajos (20), en el portal, haga clic en **Ayuda y soporte técnico** para enviar una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="0ec72-239">If you need to run more than the default (20) number of jobs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="0ec72-240">Es posible aumentar el número de trabajos que se pueden ejecutar al mismo tiempo en la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-240">The number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-to-keep-job-metadata-and-resources"></a><span data-ttu-id="0ec72-241">Periodo de conservación de metadatos de trabajo y recursos</span><span class="sxs-lookup"><span data-stu-id="0ec72-241">How long to keep job metadata and resources</span></span> 
<span data-ttu-id="0ec72-242">Cuando los usuarios ejecutan trabajos de U-SQL, el servicio Data Lake Analytics conserva todos los archivos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0ec72-242">When your users run U-SQL jobs, the Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="0ec72-243">Los archivos relacionados incluyen el script de U-SQL, los archivos DLL a los que se hace referencia en el script de U-SQL, los recursos compilados y las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="0ec72-243">Related files include the U-SQL script, the DLL files referenced in the U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="0ec72-244">Los archivos están en la carpeta /system/ de la cuenta predeterminada de Azure Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="0ec72-244">The files are in the /system/ folder of the default Azure Data Lake Storage account.</span></span> <span data-ttu-id="0ec72-245">Esta directiva controla durante cuánto tiempo se almacenan estos recursos antes de su eliminación automática (el valor predeterminado es 30 días).</span><span class="sxs-lookup"><span data-stu-id="0ec72-245">This policy controls how long these resources are stored before they are automatically deleted (the default is 30 days).</span></span> <span data-ttu-id="0ec72-246">Puede usar estos archivos para la depuración y para la optimización de rendimiento de los trabajos que se vayan a volver a ejecutar en el futuro.</span><span class="sxs-lookup"><span data-stu-id="0ec72-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in the future.</span></span>

<span data-ttu-id="0ec72-247">Para cambiar el periodo de conservación de metadatos de trabajo y recursos:</span><span class="sxs-lookup"><span data-stu-id="0ec72-247">To change how long to keep job metadata and resources:</span></span>

1. <span data-ttu-id="0ec72-248">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-248">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-249">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-249">Click **Properties**.</span></span>
3. <span data-ttu-id="0ec72-250">En **Días durante los que se conservarán las consultas de trabajo**, mueva el control deslizante para seleccionar un valor o escríbalo en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0ec72-250">Under **Days to Retain Job Queries**, move the slider to select a value, or enter the value in the text box.</span></span>  
4. <span data-ttu-id="0ec72-251">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="0ec72-252">Directivas de nivel de trabajo</span><span class="sxs-lookup"><span data-stu-id="0ec72-252">Job-level policies</span></span>
<span data-ttu-id="0ec72-253">Con las directivas de nivel de trabajo, puede controlar las unidades de análisis máximas y la prioridad máxima que los usuarios individuales (o los miembros de grupos de seguridad concretos) pueden establecer en los trabajos que envían.</span><span class="sxs-lookup"><span data-stu-id="0ec72-253">With job-level policies, you can control the maximum AUs and the maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="0ec72-254">Esto permite controlar los costos en que incurren los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0ec72-254">This lets you control the costs incurred by users.</span></span> <span data-ttu-id="0ec72-255">También permite controlar el efecto que los trabajos programados podrían tener en los trabajos de producción de alta prioridad que se ejecutan en la misma cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-255">It also lets you control the effect that scheduled jobs might have on high-priority production jobs that are running in the same Data Lake Analytics account.</span></span>

<span data-ttu-id="0ec72-256">Data Lake Analytics tiene dos directivas que se pueden establecer en el nivel de trabajo:</span><span class="sxs-lookup"><span data-stu-id="0ec72-256">Data Lake Analytics has two policies that you can set at the job level:</span></span>

* <span data-ttu-id="0ec72-257">**Límite de AU por trabajo**: los usuarios solo pueden enviar trabajos que tengan como máximo este número de unidades de análisis.</span><span class="sxs-lookup"><span data-stu-id="0ec72-257">**AU limit per job**: Users can only submit jobs that have up to this number of AUs.</span></span> <span data-ttu-id="0ec72-258">De forma predeterminada, este límite es el mismo que el límite máximo de unidades de análisis de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-258">By default, this limit is the same as the maximum AU limit for the account.</span></span>
* <span data-ttu-id="0ec72-259">**Prioridad**: los usuarios solo pueden enviar trabajos con una prioridad inferior o igual a este valor.</span><span class="sxs-lookup"><span data-stu-id="0ec72-259">**Priority**: Users can only submit jobs that have a priority lower than or equal to this value.</span></span> <span data-ttu-id="0ec72-260">Tenga en cuenta que un número mayor significa una prioridad más baja.</span><span class="sxs-lookup"><span data-stu-id="0ec72-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="0ec72-261">De forma predeterminada, se establece en 1, que es la prioridad más alta posible.</span><span class="sxs-lookup"><span data-stu-id="0ec72-261">By default, this is set to 1, which is the highest possible priority.</span></span>

<span data-ttu-id="0ec72-262">Hay una directiva predeterminada establecida en cada cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-262">There is a default policy set on every account.</span></span> <span data-ttu-id="0ec72-263">La directiva predeterminada se aplica a todos los usuarios de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0ec72-263">The default policy applies to all users of the account.</span></span> <span data-ttu-id="0ec72-264">Puede establecer directivas adicionales para usuarios y grupos concretos.</span><span class="sxs-lookup"><span data-stu-id="0ec72-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="0ec72-265">Las directivas de nivel de cuenta y las directivas de nivel de trabajo se aplican de forma simultánea.</span><span class="sxs-lookup"><span data-stu-id="0ec72-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="0ec72-266">Agregar una directiva para un usuario o grupo concreto</span><span class="sxs-lookup"><span data-stu-id="0ec72-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="0ec72-267">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-267">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-268">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-268">Click **Properties**.</span></span>
3. <span data-ttu-id="0ec72-269">En **Límites del envío de trabajos**, haga clic en el botón **Agregar directiva**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-269">Under **Job Submission Limits**, click the **Add Policy** button.</span></span> <span data-ttu-id="0ec72-270">Luego, seleccione o escriba los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="0ec72-270">Then, select or enter the following settings:</span></span>
    1. <span data-ttu-id="0ec72-271">**Nombre de la directiva de cálculo**: escriba un nombre de directiva que le recuerde su propósito.</span><span class="sxs-lookup"><span data-stu-id="0ec72-271">**Compute Policy Name**: Enter a policy name, to remind you of the purpose of the policy.</span></span>
    2. <span data-ttu-id="0ec72-272">**Seleccionar usuario o grupo**: seleccione el usuario o grupo al que se aplica esta directiva.</span><span class="sxs-lookup"><span data-stu-id="0ec72-272">**Select User or Group**: Select the user or group this policy applies to.</span></span>
    3. <span data-ttu-id="0ec72-273">**Establezca el límite de AU del trabajo**: establezca el límite de unidades de análisis que se aplica al usuario o grupo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="0ec72-273">**Set the Job AU Limit**: Set the AU limit that applies to the selected user or group.</span></span>
    4. <span data-ttu-id="0ec72-274">**Establezca el límite de prioridad**: establezca el límite de prioridad que se aplica al usuario o grupo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="0ec72-274">**Set the Priority Limit**: Set the priority limit that applies to the selected user or group.</span></span>

4. <span data-ttu-id="0ec72-275">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-275">Click **Ok**.</span></span>

5. <span data-ttu-id="0ec72-276">La nueva directiva aparece en la tabla de directivas **Predeterminado** de **Límites del envío de trabajos**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-276">The new policy is listed in the **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="0ec72-277">Eliminar o editar una directiva existente</span><span class="sxs-lookup"><span data-stu-id="0ec72-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="0ec72-278">En Azure Portal, vaya a la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ec72-278">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0ec72-279">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="0ec72-279">Click **Properties**.</span></span>
3. <span data-ttu-id="0ec72-280">En **Límites del envío de trabajos**, busque la directiva que quiere editar.</span><span class="sxs-lookup"><span data-stu-id="0ec72-280">Under **Job Submission Limits**, find the policy you want to edit.</span></span>
4.  <span data-ttu-id="0ec72-281">Para ver las opciones **Eliminar** y **Editar**, en la columna situada más a la derecha de la tabla, haga clic en **...** .</span><span class="sxs-lookup"><span data-stu-id="0ec72-281">To see the **Delete** and **Edit** options, in the rightmost column of the table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="0ec72-282">Recursos adicionales para directivas de trabajo</span><span class="sxs-lookup"><span data-stu-id="0ec72-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="0ec72-283">Entrada de blog de información general sobre directivas</span><span class="sxs-lookup"><span data-stu-id="0ec72-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="0ec72-284">Entrada de blog sobre directivas de nivel de cuenta</span><span class="sxs-lookup"><span data-stu-id="0ec72-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="0ec72-285">Entrada de blog sobre directivas de nivel de trabajo</span><span class="sxs-lookup"><span data-stu-id="0ec72-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="0ec72-286">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ec72-286">Next steps</span></span>

* [<span data-ttu-id="0ec72-287">Información general de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ec72-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="0ec72-288">Introducción al uso de Azure Portal por parte de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ec72-288">Get started with Data Lake Analytics by using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* <span data-ttu-id="0ec72-289">[Manage Azure Data Lake Analytics by using Azure PowerShell](data-lake-analytics-manage-use-powershell.md) (Administración de Azure Data Lake Analytics mediante Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0ec72-289">[Manage Azure Data Lake Analytics by using Azure PowerShell](data-lake-analytics-manage-use-powershell.md)</span></span>


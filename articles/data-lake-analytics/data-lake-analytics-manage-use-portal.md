---
title: "aaaManage análisis de Data Lake de Azure mediante el uso de Hola portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage cuentas de análisis de Data Lake, datos de orígenes, los usuarios y trabajos."
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
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="810f5-103">Administrar el análisis de Azure Data Lake mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="810f5-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="810f5-104">Obtenga información acerca de cómo las cuentas de análisis de Azure Data Lake toomanage, orígenes de datos de cuenta, los usuarios y trabajos mediante el uso de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="810f5-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="810f5-105">temas de administración de toosee sobre el uso de otras herramientas, haga clic en una pestaña de la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="810f5-106">Administración de cuentas de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="810f5-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="810f5-107">Crear una cuenta</span><span class="sxs-lookup"><span data-stu-id="810f5-107">Create an account</span></span>

1. <span data-ttu-id="810f5-108">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="810f5-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="810f5-109">Haga clic en **Nuevo** > **Inteligencia y análisis** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="810f5-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="810f5-110">Seleccione los valores de hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="810f5-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="810f5-111">**Nombre**: nombre de Hola de hello cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="810f5-112">**Suscripción**: Hola suscripción de Azure usada para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="810f5-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="810f5-113">**Grupo de recursos**: grupo de recursos de Azure de hello en qué cuenta de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="810f5-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="810f5-114">**Ubicación**: Hola centro de datos de Azure para la cuenta de análisis de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="810f5-115">**Almacén de Data Lake**: Hola toobe de almacén predeterminado utilizado por cuenta de análisis de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="810f5-116">cuenta de almacén de Azure Data Lake de Hola y Hola cuenta debe estar en el análisis de Data Lake Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="810f5-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="810f5-117">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="810f5-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="810f5-118">Eliminar una cuenta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="810f5-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="810f5-119">Para eliminar una cuenta de Data Lake Analytics, elimine la cuenta de Data Lake Store predeterminada.</span><span class="sxs-lookup"><span data-stu-id="810f5-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="810f5-120">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-121">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-121">Click **Delete**.</span></span>
3. <span data-ttu-id="810f5-122">Nombre de cuenta de hello de tipo.</span><span class="sxs-lookup"><span data-stu-id="810f5-122">Type hello account name.</span></span>
4. <span data-ttu-id="810f5-123">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="810f5-124">Administración de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="810f5-124">Manage data sources</span></span>

<span data-ttu-id="810f5-125">Análisis de Data Lake admite Hola siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="810f5-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="810f5-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="810f5-126">Data Lake Store</span></span>
* <span data-ttu-id="810f5-127">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="810f5-127">Azure Storage</span></span>

<span data-ttu-id="810f5-128">Puede usar orígenes de datos de toobrowse de explorador de datos y realizar operaciones de administración básica de archivos.</span><span class="sxs-lookup"><span data-stu-id="810f5-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="810f5-129">Agregar un origen de datos</span><span class="sxs-lookup"><span data-stu-id="810f5-129">Add a data source</span></span>

1. <span data-ttu-id="810f5-130">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-131">Haga clic en **Orígenes de datos**.</span><span class="sxs-lookup"><span data-stu-id="810f5-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="810f5-132">Haga clic en **Agregar origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="810f5-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="810f5-133">tooadd una cuenta de almacén de Data Lake, necesita cuenta de hello toohello de acceso y nombre de la cuenta tooquery de toobe capaz de él.</span><span class="sxs-lookup"><span data-stu-id="810f5-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="810f5-134">tooadd almacenamiento de blobs de Azure, necesitará cuenta de almacenamiento de Hola y clave de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="810f5-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="810f5-135">toofind toohello de éstos, vaya cuenta de almacenamiento en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="810f5-136">Configurar reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="810f5-136">Set up firewall rules</span></span>

<span data-ttu-id="810f5-137">Puede usar análisis de Data Lake toofurther bloquear acceso tooyour cuenta de análisis de Data Lake Hola a nivel de red.</span><span class="sxs-lookup"><span data-stu-id="810f5-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="810f5-138">Puede habilitar un firewall, especificar una dirección IP o definir un intervalo de direcciones IP para los clientes de confianza.</span><span class="sxs-lookup"><span data-stu-id="810f5-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="810f5-139">Después de habilitar estas medidas, solo los clientes que tengan direcciones IP de hello en el intervalo de hello definido pueden conectarse toohello almacén.</span><span class="sxs-lookup"><span data-stu-id="810f5-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="810f5-140">Si otros servicios de Azure, como Data Factory de Azure o máquinas virtuales, conectan la cuenta de análisis de Data Lake toohello, asegúrese de que **permitir servicios de Azure** está activado **en**.</span><span class="sxs-lookup"><span data-stu-id="810f5-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="810f5-141">Configurar una regla de firewall</span><span class="sxs-lookup"><span data-stu-id="810f5-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="810f5-142">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-143">En el menú de Hola Hola izquierda, haga clic en **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="810f5-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="810f5-144">Agregar un nuevo usuario</span><span class="sxs-lookup"><span data-stu-id="810f5-144">Add a new user</span></span>

<span data-ttu-id="810f5-145">Puede usar hello **Asistente para agregar usuarios** tooeasily aprovisionar nuevos usuarios de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="810f5-146">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-147">En hello izquierdo, bajo **Introducción**, haga clic en **Asistente para agregar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="810f5-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="810f5-148">Seleccione un usuario y luego haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="810f5-149">Seleccione un rol y luego haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="810f5-150">tooset seguridad un nuevo toouse de desarrollador Azure Data Lake, seleccione hello **para desarrolladores de análisis de datos Lake** rol.</span><span class="sxs-lookup"><span data-stu-id="810f5-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="810f5-151">Seleccione las listas de control de acceso (ACL) de Hola para bases de datos de SQL U Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="810f5-152">Cuando esté satisfecho con las opciones seleccionadas, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="810f5-153">Seleccione Hola ACL para los archivos.</span><span class="sxs-lookup"><span data-stu-id="810f5-153">Select hello ACLs for files.</span></span> <span data-ttu-id="810f5-154">Para el almacén predeterminado de hello, no cambie las ACL de hello para la carpeta raíz de Hola "/" y para la carpeta de Hola/sistema.</span><span class="sxs-lookup"><span data-stu-id="810f5-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="810f5-155">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-155">Click **Select**.</span></span>
7. <span data-ttu-id="810f5-156">Revise todos los cambios seleccionados y luego haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="810f5-157">Cuando finalice el Asistente de hello, haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="810f5-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="810f5-158">Administrar el control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="810f5-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="810f5-159">Al igual que otros servicios de Azure, puede usar toocontrol de Control de acceso basado en roles (RBAC) cómo los usuarios interactúan con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="810f5-160">los roles RBAC estándares de Hello tienen Hola siguientes capacidades:</span><span class="sxs-lookup"><span data-stu-id="810f5-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="810f5-161">**Propietario**: puede enviar trabajos, supervise los trabajos, Cancelar trabajos de todos los usuarios y configurar la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="810f5-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="810f5-162">**Colaborador**: puede enviar trabajos, supervise los trabajos, Cancelar trabajos de todos los usuarios y configurar la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="810f5-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="810f5-163">**Lector**: puede supervisar trabajos.</span><span class="sxs-lookup"><span data-stu-id="810f5-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="810f5-164">Usar Hola para desarrolladores de análisis de datos Lake tooenable U-SQL a los desarrolladores toouse Hola análisis de Data Lake servicio de función.</span><span class="sxs-lookup"><span data-stu-id="810f5-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="810f5-165">Puede usar papel de los desarrolladores de análisis de datos Lake Hola para:</span><span class="sxs-lookup"><span data-stu-id="810f5-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="810f5-166">Enviar trabajos.</span><span class="sxs-lookup"><span data-stu-id="810f5-166">Submit jobs.</span></span>
* <span data-ttu-id="810f5-167">Supervisar el progreso del trabajo hello y estado de los trabajos enviados por cualquier usuario.</span><span class="sxs-lookup"><span data-stu-id="810f5-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="810f5-168">Vea las secuencias de comandos SQL U Hola de trabajos enviados por cualquier usuario.</span><span class="sxs-lookup"><span data-stu-id="810f5-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="810f5-169">Cancelar solo sus propios trabajos.</span><span class="sxs-lookup"><span data-stu-id="810f5-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="810f5-170">Agregar usuarios o grupos de seguridad tooa cuenta de análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="810f5-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="810f5-171">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-172">Haga clic en **Control de acceso (IAM)** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="810f5-173">Seleccione un rol.</span><span class="sxs-lookup"><span data-stu-id="810f5-173">Select a role.</span></span>
4. <span data-ttu-id="810f5-174">Agregue un usuario.</span><span class="sxs-lookup"><span data-stu-id="810f5-174">Add a user.</span></span>
5. <span data-ttu-id="810f5-175">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="810f5-176">Si un usuario o un grupo de seguridad necesita toosubmit trabajos, también necesitan el permiso en la cuenta de la tienda de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="810f5-177">Para más información, vea [Secure data stored in Data Lake Store (Protección de datos almacenados en Data Lake Store)](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="810f5-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="810f5-178">Trabajos de administración</span><span class="sxs-lookup"><span data-stu-id="810f5-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="810f5-179">Enviar un trabajo</span><span class="sxs-lookup"><span data-stu-id="810f5-179">Submit a job</span></span>

1. <span data-ttu-id="810f5-180">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="810f5-181">Haga clic en **Nuevo trabajo**.</span><span class="sxs-lookup"><span data-stu-id="810f5-181">Click **New Job**.</span></span> <span data-ttu-id="810f5-182">Para cada trabajo, configure:</span><span class="sxs-lookup"><span data-stu-id="810f5-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="810f5-183">**Nombre del trabajo**: nombre de hello del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="810f5-184">**Prioridad**: los números más bajos tienen mayor prioridad.</span><span class="sxs-lookup"><span data-stu-id="810f5-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="810f5-185">Si se ponen en cola dos trabajos, Hola con un valor de prioridad inferior se ejecuta primero.</span><span class="sxs-lookup"><span data-stu-id="810f5-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="810f5-186">**Paralelismo**: número máximo de Hola de cálculo procesa tooreserve para este trabajo.</span><span class="sxs-lookup"><span data-stu-id="810f5-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="810f5-187">Haga clic en **Enviar trabajo**.</span><span class="sxs-lookup"><span data-stu-id="810f5-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="810f5-188">Supervisión de trabajos</span><span class="sxs-lookup"><span data-stu-id="810f5-188">Monitor jobs</span></span>

1. <span data-ttu-id="810f5-189">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-190">Haga clic en **Ver todos los trabajos**.</span><span class="sxs-lookup"><span data-stu-id="810f5-190">Click **View All Jobs**.</span></span> <span data-ttu-id="810f5-191">Se muestra una lista de todos los trabajos activas y finalizadas recientemente de hello en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="810f5-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="810f5-192">Si lo desea, haga clic en **filtro** toohelp buscar trabajos Hola por **intervalo de tiempo**, **nombre del trabajo**, y **autor** valores.</span><span class="sxs-lookup"><span data-stu-id="810f5-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="810f5-193">Supervisión de trabajos de canalización</span><span class="sxs-lookup"><span data-stu-id="810f5-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="810f5-194">Trabajos que forman parte de una canalización funcionan juntos, normalmente secuencialmente, tooaccomplish un escenario concreto.</span><span class="sxs-lookup"><span data-stu-id="810f5-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="810f5-195">Por ejemplo, puede tener una canalización que limpia, extrae, transforma y agrega el uso para información del cliente.</span><span class="sxs-lookup"><span data-stu-id="810f5-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="810f5-196">Trabajos de canalización se identifican mediante la propiedad de la "Canalización" hello cuando se envió el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="810f5-197">En los trabajos programados con ADF V2 esta propiedad se rellena de forma automática.</span><span class="sxs-lookup"><span data-stu-id="810f5-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="810f5-198">tooview una lista de trabajos de SQL U que forman parte de las canalizaciones:</span><span class="sxs-lookup"><span data-stu-id="810f5-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="810f5-199">Hola portal de Azure, vaya cuentas de análisis de Data Lake tooyour.</span><span class="sxs-lookup"><span data-stu-id="810f5-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="810f5-200">Haga clic en **Información de trabajos**.</span><span class="sxs-lookup"><span data-stu-id="810f5-200">Click **Job Insights**.</span></span> <span data-ttu-id="810f5-201">Hola que se establecerá pestaña "Todos los trabajos" que muestra una lista de ejecución, en cola y había finalizado trabajos.</span><span class="sxs-lookup"><span data-stu-id="810f5-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="810f5-202">Haga clic en hello **trabajos de canalización** ficha. Se muestra una lista de trabajos de canalización junto con estadísticas agregadas de cada canalización.</span><span class="sxs-lookup"><span data-stu-id="810f5-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="810f5-203">Supervisión de trabajos periódicos</span><span class="sxs-lookup"><span data-stu-id="810f5-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="810f5-204">Un trabajo periódico es aquel que tiene Hola misma lógica de negocios pero usa los datos de entrada diferente cada vez que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="810f5-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="810f5-205">Idealmente, los trabajos recurrentes deberían siempre correctamente y tener tiempo de ejecución relativamente estable; supervisión de estos comportamientos servirán para asegurarse del trabajo de hello es correcto.</span><span class="sxs-lookup"><span data-stu-id="810f5-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="810f5-206">Los trabajos recurrentes se identifican mediante la propiedad de "Recurrence" Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="810f5-207">En los trabajos programados con ADF V2 esta propiedad se rellena de forma automática.</span><span class="sxs-lookup"><span data-stu-id="810f5-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="810f5-208">tooview una lista de trabajos U SQL que son periódicos:</span><span class="sxs-lookup"><span data-stu-id="810f5-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="810f5-209">Hola portal de Azure, vaya cuentas de análisis de Data Lake tooyour.</span><span class="sxs-lookup"><span data-stu-id="810f5-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="810f5-210">Haga clic en **Información de trabajos**.</span><span class="sxs-lookup"><span data-stu-id="810f5-210">Click **Job Insights**.</span></span> <span data-ttu-id="810f5-211">Hola que se establecerá pestaña "Todos los trabajos" que muestra una lista de ejecución, en cola y había finalizado trabajos.</span><span class="sxs-lookup"><span data-stu-id="810f5-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="810f5-212">Haga clic en hello **trabajos recurrentes** ficha. Se muestra una lista de trabajos periódicos junto con estadísticas agregadas de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="810f5-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="810f5-213">Administración de directivas</span><span class="sxs-lookup"><span data-stu-id="810f5-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="810f5-214">Directivas de nivel de cuenta</span><span class="sxs-lookup"><span data-stu-id="810f5-214">Account-level policies</span></span>

<span data-ttu-id="810f5-215">Estas directivas aplican tooall trabajos en una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="810f5-216">Número máximo de unidades de análisis en una cuenta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="810f5-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="810f5-217">Una directiva controla el número total de Hola de unidades de análisis (AUs) puede usar su cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="810f5-218">De forma predeterminada, el valor de Hola se establece too250.</span><span class="sxs-lookup"><span data-stu-id="810f5-218">By default, hello value is set too250.</span></span> <span data-ttu-id="810f5-219">Por ejemplo, si este valor se establece too250 AUs, puede tener un trabajo en ejecución con 250 tooit AUs asignados o 10 trabajos que se ejecutan con 25 AUs cada.</span><span class="sxs-lookup"><span data-stu-id="810f5-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="810f5-220">Trabajos adicionales que se envían se ponen en cola hasta que finalicen los trabajos en ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="810f5-221">Cuando haya terminado de trabajos en ejecución, AUs se liberen para hello en cola trabajos toorun.</span><span class="sxs-lookup"><span data-stu-id="810f5-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="810f5-222">número de hello toochange de AUs para su cuenta de análisis de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="810f5-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="810f5-223">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-224">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="810f5-224">Click **Properties**.</span></span>
3. <span data-ttu-id="810f5-225">En **AUs máximo**, mover el control deslizante de hello tooselect un valor o escriba el valor de hello en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="810f5-226">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="810f5-227">Si necesita más de Hola predeterminado (250) AUs, en el portal de hello, haga clic en **+ compatibilidad con la Ayuda** toosubmit una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="810f5-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="810f5-228">puede aumentar el número de Hola de AUs disponibles en su cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="810f5-229">Número máximo de trabajos que se pueden ejecutar simultáneamente</span><span class="sxs-lookup"><span data-stu-id="810f5-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="810f5-230">Una directiva controla cuántos trabajos pueden ejecutar en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="810f5-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="810f5-231">De forma predeterminada, este valor se establece too20.</span><span class="sxs-lookup"><span data-stu-id="810f5-231">By default, this value is set too20.</span></span> <span data-ttu-id="810f5-232">Si el análisis de Data Lake tiene AUs disponibles, nuevos trabajos son toorun programada inmediatamente hasta el número total de Hola de trabajos en ejecución alcanza el valor de Hola de esta directiva.</span><span class="sxs-lookup"><span data-stu-id="810f5-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="810f5-233">Cuando se alcanza el número máximo de Hola de trabajos que se pueden ejecutar simultáneamente, se ponen en cola en los trabajos posteriores en orden de prioridad hasta que se completen uno o varios trabajos en ejecución (según la disponibilidad de Australia).</span><span class="sxs-lookup"><span data-stu-id="810f5-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="810f5-234">número de hello toochange de trabajos que se pueden ejecutar simultáneamente:</span><span class="sxs-lookup"><span data-stu-id="810f5-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="810f5-235">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-236">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="810f5-236">Click **Properties**.</span></span>
3. <span data-ttu-id="810f5-237">En **máximo el número de trabajos ejecuta**, mover el control deslizante de hello tooselect un valor o escriba el valor de hello en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="810f5-238">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="810f5-239">Si necesita más de Hola predeterminada (20) número de trabajos, en el portal de hello, haga clic en el toorun **+ compatibilidad con la Ayuda** toosubmit una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="810f5-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="810f5-240">puede aumentar el número de Hola de trabajos que se pueden ejecutar simultáneamente en su cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="810f5-241">¿Cuánto tiempo tookeep metadatos de trabajo y recursos</span><span class="sxs-lookup"><span data-stu-id="810f5-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="810f5-242">Cuando los usuarios ejecuten trabajos SQL U, Hola servicio de análisis de Data Lake conserva todos los archivos relacionados.</span><span class="sxs-lookup"><span data-stu-id="810f5-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="810f5-243">Archivos relacionados incluyen script de Hola U-SQL, archivos DLL de hello hace referencia en el script de Hola U-SQL, recursos compilados y estadísticas.</span><span class="sxs-lookup"><span data-stu-id="810f5-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="810f5-244">archivos de Hello están en carpeta de /system/ Hola de cuenta de almacenamiento de Azure datos Lake Hola predeterminada.</span><span class="sxs-lookup"><span data-stu-id="810f5-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="810f5-245">Esta directiva controla cuánto tiempo se almacenan estos recursos antes de que se eliminen automáticamente (valor predeterminado de hello es 30 días).</span><span class="sxs-lookup"><span data-stu-id="810f5-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="810f5-246">Puede utilizar estos archivos para la depuración y para la optimización de rendimiento de trabajos que podrá volver a ejecutar en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="810f5-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="810f5-247">toochange cuánto tookeep metadatos de trabajo y recursos:</span><span class="sxs-lookup"><span data-stu-id="810f5-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="810f5-248">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-249">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="810f5-249">Click **Properties**.</span></span>
3. <span data-ttu-id="810f5-250">En **tooRetain días trabajo consulta**, mover el control deslizante de hello tooselect un valor o escriba el valor de hello en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="810f5-251">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="810f5-252">Directivas de nivel de trabajo</span><span class="sxs-lookup"><span data-stu-id="810f5-252">Job-level policies</span></span>
<span data-ttu-id="810f5-253">Con las directivas de nivel de trabajo, puede controlar Hola AUs máximos y Hola máxima prioridad que los usuarios individuales (o los miembros de grupos de seguridad específicos) pueden establecer en trabajos que envíen ellos mismos.</span><span class="sxs-lookup"><span data-stu-id="810f5-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="810f5-254">Esto permite controlar los costos de hello producidos por los usuarios.</span><span class="sxs-lookup"><span data-stu-id="810f5-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="810f5-255">También le permite podría tener efecto de Hola de control que los trabajos programados en alta prioridad los trabajos de producción que se ejecutan en Hola la misma cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="810f5-256">Análisis de Data Lake tiene dos directivas que se pueden establecer en el nivel de trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="810f5-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="810f5-257">**Límite de AU por trabajo**: los usuarios sólo pueden enviar los trabajos que tienen un número de toothis de Australia.</span><span class="sxs-lookup"><span data-stu-id="810f5-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="810f5-258">De forma predeterminada, este límite es Hola mismo Hola Australia el límite máximo para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="810f5-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="810f5-259">**Prioridad**: los usuarios sólo pueden enviar los trabajos que tienen un valor de prioridad toothis menores o iguales.</span><span class="sxs-lookup"><span data-stu-id="810f5-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="810f5-260">Tenga en cuenta que un número mayor significa una prioridad más baja.</span><span class="sxs-lookup"><span data-stu-id="810f5-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="810f5-261">De forma predeterminada, se establece too1, que es la prioridad más alta posible de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="810f5-262">Hay una directiva predeterminada establecida en cada cuenta.</span><span class="sxs-lookup"><span data-stu-id="810f5-262">There is a default policy set on every account.</span></span> <span data-ttu-id="810f5-263">directiva predeterminada de Hola aplica a los usuarios de tooall de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="810f5-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="810f5-264">Puede establecer directivas adicionales para usuarios y grupos concretos.</span><span class="sxs-lookup"><span data-stu-id="810f5-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="810f5-265">Las directivas de nivel de cuenta y las directivas de nivel de trabajo se aplican de forma simultánea.</span><span class="sxs-lookup"><span data-stu-id="810f5-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="810f5-266">Agregar una directiva para un usuario o grupo concreto</span><span class="sxs-lookup"><span data-stu-id="810f5-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="810f5-267">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-268">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="810f5-268">Click **Properties**.</span></span>
3. <span data-ttu-id="810f5-269">En **límites de envío de trabajos**, haga clic en hello **Agregar directiva** botón.</span><span class="sxs-lookup"><span data-stu-id="810f5-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="810f5-270">A continuación, seleccione o escriba Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="810f5-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="810f5-271">**Nombre de la directiva de proceso**: escriba un nombre de directiva, tooremind de propósito de Hola de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="810f5-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="810f5-272">**Seleccione usuario o grupo**: Seleccione usuario de Hola o grupo al que se aplica esta directiva.</span><span class="sxs-lookup"><span data-stu-id="810f5-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="810f5-273">**Establecer Hola trabajo Australia límite**: conjunto Hola Australia se aplica un límite toohello selecciona usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="810f5-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="810f5-274">**Establecer límite de prioridad de Hola**: conjunto Hola prioridad se aplica un límite toohello selecciona usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="810f5-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="810f5-275">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="810f5-275">Click **Ok**.</span></span>

5. <span data-ttu-id="810f5-276">Hola nueva directiva se muestra en hello **predeterminado** en directiva de tabla **límites de envío de trabajos**.</span><span class="sxs-lookup"><span data-stu-id="810f5-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="810f5-277">Eliminar o editar una directiva existente</span><span class="sxs-lookup"><span data-stu-id="810f5-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="810f5-278">Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="810f5-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="810f5-279">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="810f5-279">Click **Properties**.</span></span>
3. <span data-ttu-id="810f5-280">En **límites de envío de trabajos**, directiva de Hola de búsqueda que desee tooedit.</span><span class="sxs-lookup"><span data-stu-id="810f5-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="810f5-281">Hola toosee **eliminar** y **editar** haga clic en Opciones, en la columna situada más a Hola de tabla de hello, **...** .</span><span class="sxs-lookup"><span data-stu-id="810f5-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="810f5-282">Recursos adicionales para directivas de trabajo</span><span class="sxs-lookup"><span data-stu-id="810f5-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="810f5-283">Entrada de blog de información general sobre directivas</span><span class="sxs-lookup"><span data-stu-id="810f5-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="810f5-284">Entrada de blog sobre directivas de nivel de cuenta</span><span class="sxs-lookup"><span data-stu-id="810f5-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="810f5-285">Entrada de blog sobre directivas de nivel de trabajo</span><span class="sxs-lookup"><span data-stu-id="810f5-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="810f5-286">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="810f5-286">Next steps</span></span>

* [<span data-ttu-id="810f5-287">Información general de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="810f5-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="810f5-288">Empezar a trabajar con análisis de Data Lake utilizando Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="810f5-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* <span data-ttu-id="810f5-289">[Manage Azure Data Lake Analytics by using Azure PowerShell](data-lake-analytics-manage-use-powershell.md) (Administración de Azure Data Lake Analytics mediante Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="810f5-289">[Manage Azure Data Lake Analytics by using Azure PowerShell](data-lake-analytics-manage-use-powershell.md)</span></span>


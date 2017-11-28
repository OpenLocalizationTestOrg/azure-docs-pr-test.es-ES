---
title: "aaaSet la configuración de replicación para Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo la replicación de tooorchestrate de toodeploy Site Recovery, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V en VMM nubes tooAzure."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="74b9a-103">Administrar la directiva de replicación para VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="74b9a-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="74b9a-104">Creación de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="74b9a-104">Create a replication policy</span></span>

1. <span data-ttu-id="74b9a-105">Seleccione **Administrar** > **Infraestructura de Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="74b9a-106">Seleccione **Directivas de replicación** en **Para VMware y máquinas físicas**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="74b9a-107">Seleccione **+Directiva de replicación**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-107">Select **+Replication policy**.</span></span>

    ![Creación de la directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="74b9a-109">Escriba el nombre de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="74b9a-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="74b9a-110">En **umbral de RPO**, especifique el límite RPO de Hola.</span><span class="sxs-lookup"><span data-stu-id="74b9a-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="74b9a-111">Se generarán alertas cuando la replicación continua supera este límite.</span><span class="sxs-lookup"><span data-stu-id="74b9a-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="74b9a-112">En **retención de punto de recuperación**, especifique (en horas) Hola duración del período de retención de Hola para cada punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="74b9a-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="74b9a-113">Equipos protegidos pueden ser recuperado tooany punto dentro de un período de retención.</span><span class="sxs-lookup"><span data-stu-id="74b9a-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="74b9a-114">Horas de too24 de retención es compatible con almacenamiento replicado toopremium de máquinas.</span><span class="sxs-lookup"><span data-stu-id="74b9a-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="74b9a-115">Horas de too72 de retención es compatible con almacenamiento replicado toostandard de máquinas.</span><span class="sxs-lookup"><span data-stu-id="74b9a-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="74b9a-116">Se crea automáticamente una directiva de replicación para la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="74b9a-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="74b9a-117">En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (en minutos) con la que se crearán puntos de recuperación que contengan las instantáneas coherentes con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="74b9a-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="74b9a-118">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-118">Click **OK**.</span></span> <span data-ttu-id="74b9a-119">Directiva de Hello debe crearse en 30 segundos de too60.</span><span class="sxs-lookup"><span data-stu-id="74b9a-119">hello policy should be created in 30 too60 seconds.</span></span>

![Generación de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="74b9a-121">Asociación de un servidor de configuración con una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="74b9a-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="74b9a-122">Elija toowhich de directiva de replicación de hello desea que el servidor de configuración de tooassociate Hola.</span><span class="sxs-lookup"><span data-stu-id="74b9a-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="74b9a-123">Haga clic en **Asociar**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-123">Click **Associate**.</span></span>
<span data-ttu-id="74b9a-124">![Asociación de servidor de configuración](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="74b9a-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="74b9a-125">Seleccionar servidor de configuración de hello en lista de Hola de servidores.</span><span class="sxs-lookup"><span data-stu-id="74b9a-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="74b9a-126">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-126">Click **OK**.</span></span> <span data-ttu-id="74b9a-127">servidor de configuración de Hello debe asociará un tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="74b9a-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Asociación del servidor de configuración](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="74b9a-129">Edición de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="74b9a-129">Edit a replication policy</span></span>
1. <span data-ttu-id="74b9a-130">Elija la directiva de replicación de hello para el que desea tooedit configuración de replicación.</span><span class="sxs-lookup"><span data-stu-id="74b9a-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="74b9a-131">![Edición de una directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="74b9a-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="74b9a-132">Haga clic en **Edit Settings**(Editar configuración).</span><span class="sxs-lookup"><span data-stu-id="74b9a-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="74b9a-133">![Edición de la configuración de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="74b9a-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="74b9a-134">Cambiar la configuración de hello en función de sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="74b9a-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="74b9a-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-135">Click **Save**.</span></span> <span data-ttu-id="74b9a-136">Directiva de Hello debe guardarse en dos minutos toofive, dependiendo de cuántas máquinas virtuales están utilizando esa directiva de replicación.</span><span class="sxs-lookup"><span data-stu-id="74b9a-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Guardado de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="74b9a-138">Desasociación de un servidor de configuración de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="74b9a-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="74b9a-139">Elija toowhich de directiva de replicación de hello desea que el servidor de configuración de tooassociate Hola.</span><span class="sxs-lookup"><span data-stu-id="74b9a-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="74b9a-140">Haga clic en **Desasociar**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="74b9a-141">Seleccionar servidor de configuración de hello en lista de Hola de servidores.</span><span class="sxs-lookup"><span data-stu-id="74b9a-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="74b9a-142">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-142">Click **OK**.</span></span> <span data-ttu-id="74b9a-143">servidor de configuración de Hello debe puede desasociar en un tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="74b9a-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="74b9a-144">No se puede anular la asociación de un servidor de configuración si hay al menos un elemento replicado mediante la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="74b9a-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="74b9a-145">Asegúrese de que no hay elementos replicados mediante la directiva de hello antes de anular la asociación de servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="74b9a-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="74b9a-146">Eliminación de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="74b9a-146">Delete a replication policy</span></span>

1. <span data-ttu-id="74b9a-147">Elija la directiva de replicación de Hola que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="74b9a-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="74b9a-148">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="74b9a-148">Click **Delete**.</span></span> <span data-ttu-id="74b9a-149">Directiva de Hello debe eliminarse en 30 segundos de too60.</span><span class="sxs-lookup"><span data-stu-id="74b9a-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="74b9a-150">No se puede eliminar una directiva de replicación, si existe al menos una configuración servidor asociado tooit.</span><span class="sxs-lookup"><span data-stu-id="74b9a-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="74b9a-151">Asegúrese de que no hay elementos replicados mediante la directiva de Hola y delete que Hola a todos los asociados servidores de configuración antes de eliminar la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="74b9a-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>

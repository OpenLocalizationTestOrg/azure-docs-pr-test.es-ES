---
title: "Configuración de la replicación en Azure Site Recovery | Microsoft Docs"
description: "Describe cómo implementar Site Recovery para orquestar la replicación, la conmutación por error y la recuperación, en Azure, de máquinas virtuales de Hyper-V que están en nubes de VMM."
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
ms.openlocfilehash: 73a1f19177f23441f5f7165cf2bc92ba85e62aa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-replication-policy-for-vmware-to-azure"></a><span data-ttu-id="c07aa-103">Administración de una directiva de replicación de VMware en Azure</span><span class="sxs-lookup"><span data-stu-id="c07aa-103">Manage replication policy for VMware to Azure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="c07aa-104">Creación de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="c07aa-104">Create a replication policy</span></span>

1. <span data-ttu-id="c07aa-105">Seleccione **Administrar** > **Infraestructura de Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="c07aa-106">Seleccione **Directivas de replicación** en **Para VMware y máquinas físicas**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="c07aa-107">Seleccione **+Directiva de replicación**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-107">Select **+Replication policy**.</span></span>

    ![Creación de la directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="c07aa-109">Escriba el nombre de la directiva.</span><span class="sxs-lookup"><span data-stu-id="c07aa-109">Enter the policy name.</span></span>

5. <span data-ttu-id="c07aa-110">En **Umbral de RPO**, especifique el límite de RPO.</span><span class="sxs-lookup"><span data-stu-id="c07aa-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="c07aa-111">Se generarán alertas cuando la replicación continua supera este límite.</span><span class="sxs-lookup"><span data-stu-id="c07aa-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="c07aa-112">En **Retención de punto de recuperación**, especifique (en horas) la duración del período de retención para cada punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="c07aa-112">In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point.</span></span> <span data-ttu-id="c07aa-113">Las máquinas protegidas se pueden recuperar en cualquier punto dentro de un período de retención.</span><span class="sxs-lookup"><span data-stu-id="c07aa-113">Protected machines can be recovered to any point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c07aa-114">Se admite una retención de hasta 24 horas para máquinas replicadas en Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="c07aa-114">Up to 24 hours of retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="c07aa-115">Se admite una retención de hasta 72 horas para máquinas replicadas en almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="c07aa-115">Up to 72 hours of retention is supported for machines replicated to standard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c07aa-116">Se crea automáticamente una directiva de replicación para la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="c07aa-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="c07aa-117">En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (en minutos) con la que se crearán puntos de recuperación que contengan las instantáneas coherentes con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c07aa-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="c07aa-118">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-118">Click **OK**.</span></span> <span data-ttu-id="c07aa-119">La directiva debe demorar entre 30 y 60 segundos en crearse.</span><span class="sxs-lookup"><span data-stu-id="c07aa-119">The policy should be created in 30 to 60 seconds.</span></span>

![Generación de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="c07aa-121">Asociación de un servidor de configuración con una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="c07aa-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="c07aa-122">Elija la directiva de replicación a la que desea asociar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="c07aa-122">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="c07aa-123">Haga clic en **Asociar**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-123">Click **Associate**.</span></span>
<span data-ttu-id="c07aa-124">![Asociación de servidor de configuración](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="c07aa-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="c07aa-125">Seleccione el servidor de configuración en la lista de servidores.</span><span class="sxs-lookup"><span data-stu-id="c07aa-125">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="c07aa-126">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-126">Click **OK**.</span></span> <span data-ttu-id="c07aa-127">El servidor de configuración debería demorar entre uno y dos minutos en asociarse.</span><span class="sxs-lookup"><span data-stu-id="c07aa-127">The configuration server should be associated in one to two minutes.</span></span>

![Asociación del servidor de configuración](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="c07aa-129">Edición de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="c07aa-129">Edit a replication policy</span></span>
1. <span data-ttu-id="c07aa-130">Elija la directiva de replicación cuya configuración desee editar.</span><span class="sxs-lookup"><span data-stu-id="c07aa-130">Choose the replication policy for which you want to edit replication settings.</span></span>
<span data-ttu-id="c07aa-131">![Edición de una directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="c07aa-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="c07aa-132">Haga clic en **Edit Settings**(Editar configuración).</span><span class="sxs-lookup"><span data-stu-id="c07aa-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="c07aa-133">![Edición de la configuración de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="c07aa-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="c07aa-134">Cambie la configuración para ajustarla a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="c07aa-134">Change the settings based on your need.</span></span>
4. <span data-ttu-id="c07aa-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-135">Click **Save**.</span></span> <span data-ttu-id="c07aa-136">La directiva debería demorar entre dos y cinco minutos en guardarse, en función del número de máquinas virtuales que la usen.</span><span class="sxs-lookup"><span data-stu-id="c07aa-136">The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.</span></span>

![Guardado de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="c07aa-138">Desasociación de un servidor de configuración de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="c07aa-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="c07aa-139">Elija la directiva de replicación a la que desea asociar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="c07aa-139">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="c07aa-140">Haga clic en **Desasociar**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="c07aa-141">Seleccione el servidor de configuración en la lista de servidores.</span><span class="sxs-lookup"><span data-stu-id="c07aa-141">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="c07aa-142">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-142">Click **OK**.</span></span> <span data-ttu-id="c07aa-143">El servidor de configuración debería demorar entre uno y dos minutos en desasociarse.</span><span class="sxs-lookup"><span data-stu-id="c07aa-143">The configuration server should be dissociated in one to two minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c07aa-144">Un servidor de configuración no se puede desasociar si hay al menos un elemento replicado que use la directiva.</span><span class="sxs-lookup"><span data-stu-id="c07aa-144">You cannot dissociate a configuration server if there is at least one replicated item using the policy.</span></span> <span data-ttu-id="c07aa-145">Asegúrese de que no hay elementos replicados que usen la directiva antes de desasociar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="c07aa-145">Make sure there are no replicated items using the policy before you dissociate the configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="c07aa-146">Eliminación de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="c07aa-146">Delete a replication policy</span></span>

1. <span data-ttu-id="c07aa-147">Elija la directiva de replicación que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="c07aa-147">Choose the replication policy that you want to delete.</span></span>
2. <span data-ttu-id="c07aa-148">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c07aa-148">Click **Delete**.</span></span> <span data-ttu-id="c07aa-149">La directiva debería demorar entre 30 y 60 segundos en eliminarse.</span><span class="sxs-lookup"><span data-stu-id="c07aa-149">The policy should be deleted in 30 to 60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c07aa-150">Una directiva de replicación no se puede eliminar si tiene al menos un servidor de configuración asociado.</span><span class="sxs-lookup"><span data-stu-id="c07aa-150">You cannot delete a replication policy if it has at least one configuration server associated to it.</span></span> <span data-ttu-id="c07aa-151">Asegúrese de que no hay elementos replicados que usen la directiva y elimine todos los servidores de configuración asociados antes de eliminar la directiva.</span><span class="sxs-lookup"><span data-stu-id="c07aa-151">Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.</span></span>

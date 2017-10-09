---
title: "aaaBack el almacén de copia de seguridad de tooa clásico implementado máquinas virtuales de Azure | Documentos de Microsoft"
description: "Detectar, registrar y realizar copias de seguridad de las máquinas virtuales con estos procedimientos de copia de seguridad de máquinas virtuales de Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "copia de seguridad de máquinas virtuales; hacer copia de seguridad de máquinas virtuales; recuperación ante desastres y copia de seguridad; copia de seguridad de vm"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="fa0d2-104">Copia de seguridad de máquinas virtuales de Azure (Portal clásico)</span><span class="sxs-lookup"><span data-stu-id="fa0d2-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa0d2-105">Copia el almacén de servicios de máquinas virtuales tooRecovery</span><span class="sxs-lookup"><span data-stu-id="fa0d2-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="fa0d2-106">Realizar copias de las máquinas virtuales tooBackup almacén</span><span class="sxs-lookup"><span data-stu-id="fa0d2-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="fa0d2-107">En este artículo se proporciona procedimientos de Hola para copia de seguridad de un almacén de copia de seguridad de tooa implementado clásico máquina virtual de Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="fa0d2-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="fa0d2-108">Hay algunas tareas que necesita tootake símbolo inglés care de antes de hacer copias de seguridad una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="fa0d2-109">Si aún no ha hecho Hola completa, por lo que [requisitos previos](backup-azure-vms-prepare.md) tooprepare el entorno para realizar copias de seguridad de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="fa0d2-110">Para obtener más información, vea los artículos de hello en [planear la infraestructura de copia de seguridad de máquina virtual en Azure](backup-azure-vms-introduction.md) y [máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="fa0d2-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="fa0d2-111">Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fa0d2-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fa0d2-112">Un almacén de Copia de seguridad solo puede proteger máquinas virtuales con implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="fa0d2-113">No puede proteger máquinas virtuales con implementación mediante Resource Manager con un almacén de Copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="fa0d2-114">Vea [copia de seguridad el almacén de servicios de máquinas virtuales tooRecovery](backup-azure-arm-vms.md) para obtener más información sobre cómo trabajar con servicios de recuperación de los almacenes de credenciales.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="fa0d2-115">La realización de copias de seguridad de máquinas virtuales de Azure consta tres pasos principales:</span><span class="sxs-lookup"><span data-stu-id="fa0d2-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Tooback de tres pasos de una VM de IaaS de Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="fa0d2-117">La copia de seguridad de máquinas virtuales es un proceso local.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="fa0d2-118">No se puede realizar copias de seguridad de máquinas virtuales en un almacén de copia de seguridad de tooa región en otra región.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="fa0d2-119">Por lo tanto, debe crear un almacén de copia de seguridad en cada región de Azure donde estén las máquinas virtuales de las que se realizará una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="fa0d2-120">A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="fa0d2-121">Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="fa0d2-122">Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="fa0d2-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="fa0d2-123">Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="fa0d2-124">Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="fa0d2-125">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="fa0d2-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="fa0d2-126">Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="fa0d2-127">No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="fa0d2-128">En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="fa0d2-129">Paso 1: Detección de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="fa0d2-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="fa0d2-130">tooensure cualquier nueva suscripción toohello agregada de máquinas virtuales (VM) se identifican antes de registrar, ejecute el proceso de detección de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="fa0d2-131">Hola procesar consultas Azure para la lista de Hola de máquinas virtuales de suscripción de hello, junto con información adicional como el nombre del servicio de nube de Hola y región Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="fa0d2-132">Inicie sesión en toohello [portal clásico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="fa0d2-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="fa0d2-133">En la lista de hello de servicios de Azure, haga clic en **servicios de recuperación** tooopen lista de Hola de almacenes de copia de seguridad y recuperación del sitio.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="fa0d2-134">![Abrir lista de almacenes](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="fa0d2-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="fa0d2-135">En lista de Hola de almacenes de copia de seguridad, seleccione hello tooback de almacén de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="fa0d2-136">Si se trata de un nuevo portal de Hola de almacén abre toohello **inicio rápido** página.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![Abrir menú de elementos registrados](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="fa0d2-138">Si previamente se ha configurado el almacén de hello, portal de hello abre el menú de toohello usado más recientemente.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="fa0d2-139">Menú de almacén de hello (al principio de Hola de página de hello), haga clic en **elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![Abrir menú de elementos registrados](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="fa0d2-141">De hello **tipo** menú, seleccione **Máquina Virtual de Azure**.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="fa0d2-143">Haga clic en **DISCOVER** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="fa0d2-144">![Botón Detectar](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="fa0d2-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="fa0d2-145">proceso de detección de Hello puede tardar unos minutos mientras se se tabulan hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="fa0d2-146">Hay una notificación en la parte inferior de Hola de pantalla de bienvenida que le permite saber que se está ejecutando el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Detectar máquinas virtuales](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="fa0d2-148">notificación de Hello cambia cuando se complete el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="fa0d2-149">Si el proceso de detección de hello no encontró hello las máquinas virtuales, asegúrese en primer lugar que existen hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="fa0d2-150">Si existen hello las máquinas virtuales, asegúrese de hello las máquinas virtuales están en Hola misma región que el almacén de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="fa0d2-151">Si las máquinas virtuales de hello existen y están en Hola la misma región, asegúrese de que Hello las máquinas virtuales ya no están registrados tooa el almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="fa0d2-152">Si una máquina virtual es el almacén de copia de seguridad tooa asignado no es almacenes de copia de seguridad de tooother toobe disponibles asignado.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![Detección realizada](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="fa0d2-154">Una vez que ha detectado elementos nuevos de hello, vaya tooStep 2 y registre las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="fa0d2-155">Paso 2: Registro de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="fa0d2-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="fa0d2-156">Registrar un tooassociate de máquina virtual de Azure con hello servicio de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="fa0d2-157">El registro suele ser una actividad que solo se realiza una vez.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="fa0d2-158">Navegar por el almacén de copia de seguridad toohello en **servicios de recuperación** en Hola portal de Azure y, a continuación, haga clic en **elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="fa0d2-159">Seleccione **Máquina Virtual de Azure** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="fa0d2-161">Haga clic en **registrar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="fa0d2-162">![Botón Registrar](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="fa0d2-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="fa0d2-163">Hola **registrar elementos** menú contextual, seleccione hello las máquinas virtuales que desea tooregister.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="fa0d2-164">Si hay dos o más máquinas virtuales con Hola mismo nombre, utilice toodistinguish de servicio de nube Hola entre ellos.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="fa0d2-165">Se pueden registrar varias máquinas virtuales al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="fa0d2-166">Se crea un trabajo para cada máquina virtual que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="fa0d2-167">Haga clic en **ver trabajo** en hello notificación toogo toohello **trabajos** página.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Registrar trabajo](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="fa0d2-169">máquina virtual de Hola también aparece en la lista de Hola de los elementos registrados, junto con el estado de Hola de operación de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Registrando estado 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="fa0d2-171">Cuando se completa la operación de hello, estado de hello cambia hello tooreflect *registrado* estado.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Registrando estado 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="fa0d2-173">Paso 3: Protección de las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="fa0d2-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="fa0d2-174">Ahora puede configurar una directiva de copia de seguridad y retención de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="fa0d2-175">Se pueden proteger varias máquinas virtuales en una sola acción de protección.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="fa0d2-176">Almacenes de copia de seguridad de Azure creados después de mayo de 2015 vienen con una directiva predeterminada integrada en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="fa0d2-177">Esta directiva predeterminada viene con un período de retención predeterminado de 30 días y una programación de copia de seguridad diaria.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="fa0d2-178">Navegar por el almacén de copia de seguridad toohello en **servicios de recuperación** en Hola portal de Azure y, a continuación, haga clic en **elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="fa0d2-179">Seleccione **Máquina Virtual de Azure** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Seleccionar carga de trabajo en el portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="fa0d2-181">Haga clic en **proteger** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="fa0d2-182">Hola **Asistente para proteger elementos** aparece.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="fa0d2-183">Asistente de Hello solo muestra las máquinas virtuales que están registradas y no protegidas.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="fa0d2-184">Seleccione hello las máquinas virtuales que desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="fa0d2-185">Si hay dos o más máquinas virtuales con Hola mismo nombre, utilice toodistinguish de servicio de nube Hola entre las máquinas virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="fa0d2-186">Puede proteger varias máquinas virtuales al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Configuración de protección a escala](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="fa0d2-188">Elija un **programar copia de seguridad** tooback las máquinas virtuales de Hola que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="fa0d2-189">Puede seleccionar una directiva de un conjunto existente o definir una nueva.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="fa0d2-190">Cada directiva de copia de seguridad puede tener asociadas varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="fa0d2-191">Sin embargo, máquina virtual de hello solo puede estar asociado a una directiva en un momento determinado en tiempo.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Protección mediante nueva directiva](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="fa0d2-193">Una directiva de copia de seguridad incluye un esquema de retención de copias de seguridad programada de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="fa0d2-194">Si selecciona una directiva de copia de seguridad existente, no se puede modificar opciones de retención de hello en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="fa0d2-195">Elija un **duración de retención** tooassociate con copias de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![Protección con retención flexible](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="fa0d2-197">Directiva de retención especifica Hola período de tiempo para almacenar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="fa0d2-198">Puede especificar las directivas de retención diferentes en función de cuando se realizó la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="fa0d2-199">Por ejemplo, un punto de copia de seguridad diario (que sirve como punto de recuperación operativo) podría conservarse durante 90 días.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="fa0d2-200">En comparación, un punto de copia de seguridad realizado al final de Hola de cada trimestre (por motivos de auditoría) puede necesitar toobe conservan por varios meses o años.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="fa0d2-202">En esta imagen de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fa0d2-202">In this example image:</span></span>

   * <span data-ttu-id="fa0d2-203">**Directiva de retención diaria**: las copias de seguridad realizadas diariamente se almacenan durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="fa0d2-204">**Directiva de retención semanal**: las copias de seguridad realizadas cada domingo se conservan durante 104 semanas.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="fa0d2-205">**Directiva de retención mensual**: copias de seguridad realizadas en hello último domingo de cada mes se conservan durante 120 meses.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="fa0d2-206">**Directiva de retención anual**: se conservan las copias de seguridad realizadas en hello primer domingo de cada enero de 99 años.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="fa0d2-207">Un trabajo se crea la directiva de protección de tooconfigure hello y asociar directiva de toothat Hola máquinas virtuales para cada máquina virtual que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="fa0d2-208">lista de hello tooview de **configurar la protección** trabajos, desde el menú de almacenes de hello, haga clic en **trabajos** y seleccione **configurar la protección** de hello **operación**  filtro.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![Configurar trabajo de protección](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="fa0d2-210">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="fa0d2-210">Initial backup</span></span>
<span data-ttu-id="fa0d2-211">Una vez que la máquina virtual de hello está protegida con una directiva, muestra en hello **elementos protegidos** ficha con el estado de Hola de *Protected - (pendiente de copia de seguridad inicial)*.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="fa0d2-212">De forma predeterminada, copia de seguridad programada Hola primer es hello *copia de seguridad inicial*.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="fa0d2-213">tootrigger Hola copia de seguridad inicial inmediatamente después de configurar la protección:</span><span class="sxs-lookup"><span data-stu-id="fa0d2-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="fa0d2-214">Final de Hola de hello **elementos protegidos** página, haga clic en **copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="fa0d2-215">Hola servicio copia de seguridad de Azure crea un trabajo de copia de seguridad para la operación de copia de seguridad inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="fa0d2-216">Haga clic en hello **trabajos** lista de pestañas tooview Hola de trabajos.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Copia de seguridad en curso](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="fa0d2-218">Durante la operación de copia de seguridad de hello, Hola servicio copia de seguridad de Azure emite una extensión de copia de seguridad de toohello de comando en cada máquina virtual de tooflush todos los trabajos de escritura y toman una instantánea coherente.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="fa0d2-219">Cuando finalice la copia de seguridad inicial de hello, estado de Hola de máquina virtual de Hola Hola **elementos protegidos** ficha es *Protected*.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="fa0d2-221">Visualización de los detalles y el estado de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="fa0d2-221">Viewing backup status and details</span></span>
<span data-ttu-id="fa0d2-222">Una vez protegido, recuento de máquinas virtuales de hello también aumenta en hello **panel** resumen de la página.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="fa0d2-223">Hola **panel** página también muestra el número de Hola de trabajos de hello últimas 24 horas que estaban *correcta*, tienen *no se pudo*y son *en curso*.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="fa0d2-224">En hello **trabajos** , utilice hello **estado**, **operación**, o **de** y **a** toofilter de menús trabajos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![Estado de la copia de seguridad en la página Panel](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="fa0d2-226">Los valores en el panel de Hola se actualizan una vez cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="fa0d2-227">Solución de errores</span><span class="sxs-lookup"><span data-stu-id="fa0d2-227">Troubleshooting errors</span></span>
<span data-ttu-id="fa0d2-228">Si surgen problemas durante la copia de seguridad de la máquina virtual, mirar hello [artículo de solución de problemas de VM](backup-azure-vms-troubleshoot.md) para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="fa0d2-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa0d2-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fa0d2-229">Next steps</span></span>
* [<span data-ttu-id="fa0d2-230">Administración y supervisión de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fa0d2-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="fa0d2-231">Restauración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fa0d2-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)

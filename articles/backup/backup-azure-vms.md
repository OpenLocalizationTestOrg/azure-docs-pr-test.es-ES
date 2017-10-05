---
title: "Copia de seguridad de máquinas virtuales de Azure con implementación clásica en un almacén de copia de seguridad | Microsoft Docs"
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
ms.openlocfilehash: e1da8bce96078a43c656f84005cefc8bbe81c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="fecf3-104">Copia de seguridad de máquinas virtuales de Azure (Portal clásico)</span><span class="sxs-lookup"><span data-stu-id="fecf3-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fecf3-105">Copia de seguridad de VM en el almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="fecf3-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="fecf3-106">Copia de seguridad de VM en el almacén de Copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="fecf3-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="fecf3-107">Este artículo proporciona los procedimientos para realizar una copia de seguridad de una máquina virtual de Azure con implementación clásica en un almacén de Copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-107">This article provides the procedures for backing up a Classic-deployed Azure virtual machine (VM) to a Backup vault.</span></span> <span data-ttu-id="fecf3-108">Hay algunas tareas que es necesario tener en cuenta antes de poder realizar una copia de seguridad de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="fecf3-108">There are a few tasks you need to take care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="fecf3-109">Si aún no lo ha hecho, complete los [requisitos previos](backup-azure-vms-prepare.md) para preparar el entorno para realizar copias de seguridad de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fecf3-109">If you haven't already done so, complete the [prerequisites](backup-azure-vms-prepare.md) to prepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="fecf3-110">Para más información, consulte los artículos acerca de cómo [planear la infraestructura de copia de seguridad de máquinas virtuales en Azure](backup-azure-vms-introduction.md) y acerca de [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="fecf3-110">For additional information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="fecf3-111">Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fecf3-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fecf3-112">Un almacén de Copia de seguridad solo puede proteger máquinas virtuales con implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="fecf3-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="fecf3-113">No puede proteger máquinas virtuales con implementación mediante Resource Manager con un almacén de Copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="fecf3-114">Consulte [Copia de seguridad de VM en el almacén de servicios de recuperación](backup-azure-arm-vms.md) para más información sobre cómo trabajar con almacenes de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="fecf3-114">See [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="fecf3-115">La realización de copias de seguridad de máquinas virtuales de Azure consta tres pasos principales:</span><span class="sxs-lookup"><span data-stu-id="fecf3-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Tres pasos para realizar una copia de seguridad de una máquina virtual de IaaS](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="fecf3-117">La copia de seguridad de máquinas virtuales es un proceso local.</span><span class="sxs-lookup"><span data-stu-id="fecf3-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="fecf3-118">No puede realizar copias de seguridad de máquinas virtuales de una región en un almacén de copia de seguridad de otra región.</span><span class="sxs-lookup"><span data-stu-id="fecf3-118">You cannot back up virtual machines in one region to a backup vault in another region.</span></span> <span data-ttu-id="fecf3-119">Por lo tanto, debe crear un almacén de copia de seguridad en cada región de Azure donde estén las máquinas virtuales de las que se realizará una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="fecf3-120">A partir de marzo de 2017, ya no podrá usar el portal clásico para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="fecf3-120">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="fecf3-121">Ahora puede actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="fecf3-121">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="fecf3-122">Para más información, consulte el artículo [Actualización de un almacén de Backup a un almacén de Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="fecf3-122">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="fecf3-123">Microsoft anima a actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="fecf3-123">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="fecf3-124">A partir del 15 de octubre de 2017, no podrá usar PowerShell para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="fecf3-124">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="fecf3-125">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="fecf3-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="fecf3-126">Todos los almacenes de Backup restantes se actualizarán automáticamente a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="fecf3-126">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="fecf3-127">No podrá acceder a los datos de copia de seguridad en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="fecf3-127">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="fecf3-128">En su lugar, utilice Azure Portal para tener acceso a los datos de copia de seguridad en los almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="fecf3-128">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="fecf3-129">Paso 1: Detección de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="fecf3-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="fecf3-130">Para asegurarse de identificar antes del registro todas las máquinas virtuales nuevas agregadas a la suscripción, ejecute el proceso de detección.</span><span class="sxs-lookup"><span data-stu-id="fecf3-130">To ensure any new virtual machines (VMs) added to the subscription are identified before registering, run the discovery process.</span></span> <span data-ttu-id="fecf3-131">El proceso consulta a Azure la lista de máquinas virtuales incluidas en la suscripción, junto con información adicional, por ejemplo, el nombre del servicio en la nube y la región.</span><span class="sxs-lookup"><span data-stu-id="fecf3-131">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="fecf3-132">Inicie sesión en el [Portal clásico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="fecf3-132">Sign in to the [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="fecf3-133">En la lista de servicios de Azure, haga clic en **Recovery Services** para abrir la lista de almacenes de Backup y Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fecf3-133">In the list of Azure services, click **Recovery Services** to open the list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="fecf3-134">![Abrir lista de almacenes](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="fecf3-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="fecf3-135">En la lista de almacenes de copia de seguridad, seleccione el almacén de copia de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fecf3-135">In the list of Backup vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="fecf3-136">Si se trata de un nuevo almacén, el portal se abre en la página **Inicio rápido** .</span><span class="sxs-lookup"><span data-stu-id="fecf3-136">If this is a new vault the portal opens to the **Quick Start** page.</span></span>

    ![Abrir menú de elementos registrados](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="fecf3-138">Si el almacén se ha configurado previamente, el portal se abrirá en el último menú usado.</span><span class="sxs-lookup"><span data-stu-id="fecf3-138">If the vault has previously been configured, the portal opens to the most recently used menu.</span></span>
4. <span data-ttu-id="fecf3-139">En el menú del almacén (en la parte superior de la página), haga clic en **Elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="fecf3-139">From the vault menu (at the top of the page), click **Registered Items**.</span></span>

    ![Abrir menú de elementos registrados](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="fecf3-141">En el menú **Tipo**, seleccione **Máquina virtual de Azure**.</span><span class="sxs-lookup"><span data-stu-id="fecf3-141">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="fecf3-143">Haga clic en **DETECTAR** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="fecf3-143">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="fecf3-144">![Botón Detectar](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="fecf3-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="fecf3-145">El proceso de detección puede tardar unos minutos mientras se tabulan las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fecf3-145">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="fecf3-146">Hay una notificación en la parte inferior de la pantalla que informa de que el proceso se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="fecf3-146">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Detectar máquinas virtuales](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="fecf3-148">La notificación cambia cuando el proceso se completa.</span><span class="sxs-lookup"><span data-stu-id="fecf3-148">The notification changes when the process is complete.</span></span> <span data-ttu-id="fecf3-149">Si el proceso de detección no encontró las máquinas virtuales, primero asegúrese de que existan las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fecf3-149">If the discovery process did not find the virtual machines, first ensure the VMs exist.</span></span> <span data-ttu-id="fecf3-150">Si efectivamente es así, asegúrese de que las máquinas virtuales están en la misma región que el almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-150">If the VMs exist, ensure the VMs are in the same region as the backup vault.</span></span> <span data-ttu-id="fecf3-151">Si las máquinas virtuales existen y están en la misma región, asegúrese de que no están registradas en un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-151">If the VMs exist and are in the same region, ensure the VMs are not already registered to a backup vault.</span></span> <span data-ttu-id="fecf3-152">Si se asigna una máquina virtual a un almacén de copia de seguridad, no será posible asignarla a otros almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-152">If a VM is assigned to a backup vault it is not available to be assigned to other backup vaults.</span></span>

    ![Detección realizada](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="fecf3-154">Una vez que haya encontrado los nuevos elementos, vaya al paso 2 y registre las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fecf3-154">Once you have discovered the new items, go to Step 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="fecf3-155">Paso 2: Registro de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="fecf3-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="fecf3-156">Se registra una máquina virtual de Azure para asociarla con el servicio Copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="fecf3-156">You register an Azure virtual machine to associate it with the Azure Backup service.</span></span> <span data-ttu-id="fecf3-157">El registro suele ser una actividad que solo se realiza una vez.</span><span class="sxs-lookup"><span data-stu-id="fecf3-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="fecf3-158">Navegue al almacén de copia de seguridad de **Recovery Services** en Azure Portal y haga clic en **Elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="fecf3-158">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="fecf3-159">Seleccione **Máquina virtual de Azure** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="fecf3-159">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="fecf3-161">Haga clic en **REGISTRAR** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="fecf3-161">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="fecf3-162">![Botón Registrar](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="fecf3-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="fecf3-163">En el menú contextual **Elementos registrados** , seleccione las máquinas virtuales que desea registrar.</span><span class="sxs-lookup"><span data-stu-id="fecf3-163">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span> <span data-ttu-id="fecf3-164">Si hay dos o más máquinas virtuales con el mismo nombre, use el servicio en la nube para distinguirlas.</span><span class="sxs-lookup"><span data-stu-id="fecf3-164">If there are two or more virtual machines with the same name, use the cloud service to distinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="fecf3-165">Se pueden registrar varias máquinas virtuales al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="fecf3-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="fecf3-166">Se crea un trabajo para cada máquina virtual que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="fecf3-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="fecf3-167">Haga clic en **Ver trabajo** en la notificación para ir a la página **Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="fecf3-167">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Registrar trabajo](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="fecf3-169">La máquina virtual también aparece en la lista de elementos registrados junto con el estado de la operación de registro.</span><span class="sxs-lookup"><span data-stu-id="fecf3-169">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Registrando estado 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="fecf3-171">Una vez completada la operación, el estado cambia a *registrado* .</span><span class="sxs-lookup"><span data-stu-id="fecf3-171">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Registrando estado 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="fecf3-173">Paso 3: Protección de las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="fecf3-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="fecf3-174">Ahora puede configurar una directiva de retención y copia de seguridad para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fecf3-174">Now you can set up a backup and retention policy for the virtual machine.</span></span> <span data-ttu-id="fecf3-175">Se pueden proteger varias máquinas virtuales en una sola acción de protección.</span><span class="sxs-lookup"><span data-stu-id="fecf3-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="fecf3-176">Los almacenes de Copia de seguridad de Azure creados después de mayo de 2015 incluyen una directiva predeterminada integrada en el almacén.</span><span class="sxs-lookup"><span data-stu-id="fecf3-176">Azure Backup vaults created after May 2015 come with a default policy built into the vault.</span></span> <span data-ttu-id="fecf3-177">Esta directiva predeterminada viene con un período de retención predeterminado de 30 días y una programación de copia de seguridad diaria.</span><span class="sxs-lookup"><span data-stu-id="fecf3-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="fecf3-178">Navegue al almacén de copia de seguridad de **Recovery Services** en Azure Portal y haga clic en **Elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="fecf3-178">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="fecf3-179">Seleccione **Máquina virtual de Azure** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="fecf3-179">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Seleccionar carga de trabajo en el portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="fecf3-181">Haga clic en **PROTEGER** , en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="fecf3-181">Click **PROTECT** at the bottom of the page.</span></span>

    <span data-ttu-id="fecf3-182">Se abrirá el **Asistente para protección de elementos** .</span><span class="sxs-lookup"><span data-stu-id="fecf3-182">The **Protect Items wizard** appears.</span></span> <span data-ttu-id="fecf3-183">El asistente solo muestra las máquinas virtuales que están registradas y que no están protegidas.</span><span class="sxs-lookup"><span data-stu-id="fecf3-183">The wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="fecf3-184">Seleccione las máquinas virtuales que desee proteger.</span><span class="sxs-lookup"><span data-stu-id="fecf3-184">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="fecf3-185">Si hay dos o más máquinas virtuales con el mismo nombre, use el servicio en la nube para distinguir las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fecf3-185">If there are two or more virtual machines with the same name, use the cloud service to distinguish between the virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="fecf3-186">Puede proteger varias máquinas virtuales al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="fecf3-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Configuración de protección a escala](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="fecf3-188">Elija una **programación de copia de seguridad** para hacer una copia de seguridad de las máquinas virtuales que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="fecf3-188">Choose a **backup schedule** to back up the virtual machines that you've selected.</span></span> <span data-ttu-id="fecf3-189">Puede seleccionar una directiva de un conjunto existente o definir una nueva.</span><span class="sxs-lookup"><span data-stu-id="fecf3-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="fecf3-190">Cada directiva de copia de seguridad puede tener asociadas varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fecf3-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="fecf3-191">Sin embargo, la máquina virtual solo se puede asociar con una directiva en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="fecf3-191">However, the virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Protección mediante nueva directiva](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="fecf3-193">Una directiva de copia de seguridad incluye un esquema de retención de las copias de seguridad programadas.</span><span class="sxs-lookup"><span data-stu-id="fecf3-193">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="fecf3-194">Si selecciona una directiva de copia de seguridad existente, no podrá modificar las opciones de retención en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="fecf3-194">If you select an existing backup policy, you cannot modify the retention options in the next step.</span></span>
   >
   >

5. <span data-ttu-id="fecf3-195">Elija un **intervalo de retención** para asociarlo a las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-195">Choose a **retention range** to associate with the backups.</span></span>

    ![Protección con retención flexible](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="fecf3-197">La directiva de retención especifica el período de tiempo que se almacena una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-197">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="fecf3-198">Puede especificar directivas de retención diferentes en función de cuándo se realizó la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fecf3-198">You can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="fecf3-199">Por ejemplo, un punto de copia de seguridad diario (que sirve como punto de recuperación operativo) podría conservarse durante 90 días.</span><span class="sxs-lookup"><span data-stu-id="fecf3-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="fecf3-200">En comparación, un punto de copia de seguridad realizado al final de cada trimestre (con fines de auditoría) podría tener que conservarse durante muchos meses o años.</span><span class="sxs-lookup"><span data-stu-id="fecf3-200">In comparison, a backup point taken at the end of each quarter (for audit purposes) may need to be preserved for many months or years.</span></span>

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="fecf3-202">En esta imagen de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fecf3-202">In this example image:</span></span>

   * <span data-ttu-id="fecf3-203">**Directiva de retención diaria**: las copias de seguridad realizadas diariamente se almacenan durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="fecf3-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="fecf3-204">**Directiva de retención semanal**: las copias de seguridad realizadas cada domingo se conservan durante 104 semanas.</span><span class="sxs-lookup"><span data-stu-id="fecf3-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="fecf3-205">**Directiva de retención mensual**: las copias de seguridad realizadas el último domingo de cada mes se conservan durante 120 meses.</span><span class="sxs-lookup"><span data-stu-id="fecf3-205">**Monthly retention policy**: Backups taken on the last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="fecf3-206">**Directiva de retención anual**: las copias de seguridad realizadas el primer domingo de cada mes de enero se conservan durante 99 años.</span><span class="sxs-lookup"><span data-stu-id="fecf3-206">**Yearly retention policy**: Backups taken on the first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="fecf3-207">Se crea un trabajo para configurar la directiva de protección y asociar a esa directiva cada máquina virtual que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="fecf3-207">A job is created to configure the protection policy and associate the virtual machines to that policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="fecf3-208">Para ver la lista de los trabajos de **Configurar la protección**, en el menú de almacenes, haga clic en **Trabajos** y seleccione **Configurar la protección** en el filtro **Operación**.</span><span class="sxs-lookup"><span data-stu-id="fecf3-208">To view the list of **Configure Protection** jobs, from the vaults menu, click **Jobs** and select **Configure Protection** from the **Operation** filter.</span></span>

    ![Configurar trabajo de protección](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="fecf3-210">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="fecf3-210">Initial backup</span></span>
<span data-ttu-id="fecf3-211">Una vez que la máquina virtual está protegida con una directiva, aparecerá en la pestaña **Elementos protegidos** y tendrá un estado *Protegido (copia de seguridad inicial pendiente)*.</span><span class="sxs-lookup"><span data-stu-id="fecf3-211">Once the virtual machine is protected with a policy, it shows up under the **Protected Items** tab with the status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="fecf3-212">De forma predeterminada, la primera copia de seguridad programada es la *copia de seguridad inicial*.</span><span class="sxs-lookup"><span data-stu-id="fecf3-212">By default, the first scheduled backup is the *initial backup*.</span></span>

<span data-ttu-id="fecf3-213">Para desencadenar la copia de seguridad inicial inmediatamente después de configurar la protección:</span><span class="sxs-lookup"><span data-stu-id="fecf3-213">To trigger the initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="fecf3-214">En la parte inferior de la página **Elementos protegidos**, haga clic en **Realizar copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="fecf3-214">At the bottom of the **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="fecf3-215">El servicio Copia de seguridad de Azure crea un trabajo de copia de seguridad para la operación de copia de seguridad inicial.</span><span class="sxs-lookup"><span data-stu-id="fecf3-215">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="fecf3-216">Haga clic en la pestaña **Trabajos** para ver la lista de los trabajos.</span><span class="sxs-lookup"><span data-stu-id="fecf3-216">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Copia de seguridad en curso](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="fecf3-218">Durante la operación de copia de seguridad, el servicio Copia de seguridad de Azure emite un comando a la extensión de copia de seguridad en cada máquina virtual para vaciar todos los trabajos de escritura y tomar una instantánea coherente.</span><span class="sxs-lookup"><span data-stu-id="fecf3-218">During the backup operation, the Azure Backup service issues a command to the backup extension in each virtual machine to flush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="fecf3-219">Cuando finalice la copia de seguridad inicial, el estado de la máquina virtual en la pestaña **Elementos protegidos** será *Protegido*.</span><span class="sxs-lookup"><span data-stu-id="fecf3-219">When the initial backup finishes, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="fecf3-221">Visualización de los detalles y el estado de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="fecf3-221">Viewing backup status and details</span></span>
<span data-ttu-id="fecf3-222">Una vez protegidas, el recuento de máquinas virtuales también aumenta en el resumen de la página **Panel** .</span><span class="sxs-lookup"><span data-stu-id="fecf3-222">Once protected, the virtual machine count also increases in the **Dashboard** page summary.</span></span> <span data-ttu-id="fecf3-223">La página **Panel** también muestra el número de trabajos de las últimas 24 horas que se realizaron *correctamente*, los que causaron un *error* y los que están *en curso*.</span><span class="sxs-lookup"><span data-stu-id="fecf3-223">The **Dashboard** page also shows the number of jobs from the last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="fecf3-224">En la página **Trabajos**, use los menús **Estado**, **Operación** o **Desde** y **Hasta** para filtrar los trabajos.</span><span class="sxs-lookup"><span data-stu-id="fecf3-224">On the **Jobs** page, use the **Status**, **Operation**, or **From** and **To** menus to filter the jobs.</span></span>

![Estado de la copia de seguridad en la página Panel](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="fecf3-226">Los valores indicados en el panel se actualizan cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="fecf3-226">Values in the dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="fecf3-227">Solución de errores</span><span class="sxs-lookup"><span data-stu-id="fecf3-227">Troubleshooting errors</span></span>
<span data-ttu-id="fecf3-228">Si surgen problemas al realizar la copia de seguridad de la máquina virtual, consulte el artículo [Solución de problemas de copia de seguridad de máquinas virtuales de Azure](backup-azure-vms-troubleshoot.md) para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="fecf3-228">If you run into issues while backing up your virtual machine, look at the [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fecf3-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fecf3-229">Next steps</span></span>
* [<span data-ttu-id="fecf3-230">Administración y supervisión de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fecf3-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="fecf3-231">Restauración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fecf3-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)

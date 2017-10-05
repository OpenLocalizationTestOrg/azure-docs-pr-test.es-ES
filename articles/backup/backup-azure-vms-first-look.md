---
title: "Primer vistazo: copia de seguridad de máquinas virtuales de Azure con un almacén de copia de seguridad | Microsoft Docs"
description: "Use el portal clásico para hacer copia de seguridad de las máquinas virtuales de Azure en un almacén de Backup. En este tutorial se explican todas las fases, que incluyen la creación del almacén de Backup, el registro de las máquinas virtuales, la creación de directivas de copia de seguridad y la ejecución del trabajo inicial de copia de seguridad."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="f34b2-104">Primer contacto: copia de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="f34b2-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f34b2-105">Protección de máquinas virtuales con un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="f34b2-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="f34b2-106">Protección de máquinas virtuales con un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="f34b2-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="f34b2-107">Este tutorial le guiará por los pasos para crear copias de seguridad de una máquina virtual de Azure en un almacén de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="f34b2-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="f34b2-108">En este artículo se describe el modelo de implementación clásica o de Service Manager para la creación de copias de seguridad de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f34b2-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="f34b2-109">Los siguientes pasos se aplican únicamente a los almacenes de Backup creados en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="f34b2-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="f34b2-110">Microsoft recomienda usar el modelo de Resource Manager para nuevas implementaciones.</span><span class="sxs-lookup"><span data-stu-id="f34b2-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="f34b2-111">Si está interesado en la realización de una copia de seguridad de una máquina virtual en un almacén de Recovery Services que pertenece a un grupo de recursos, consulte [Primer análisis: copia de seguridad de máquinas virtuales con ARM en un almacén de Recovery Services](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f34b2-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="f34b2-112">Para completar correctamente este tutorial, se deben cumplir estos requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="f34b2-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="f34b2-113">Ha creado una máquina virtual en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f34b2-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="f34b2-114">La máquina virtual tiene conectividad a las direcciones IP públicas de Azure.</span><span class="sxs-lookup"><span data-stu-id="f34b2-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="f34b2-115">Para más información, consulte [Conectividad de red](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="f34b2-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="f34b2-116">Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f34b2-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f34b2-117">El uso de este tutorial está destinado a máquinas virtuales creadas en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="f34b2-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="f34b2-118">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="f34b2-118">Create a backup vault</span></span>
<span data-ttu-id="f34b2-119">Un almacén de copia de seguridad es una entidad que almacena todas las copias de seguridad y los puntos de recuperación creados con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="f34b2-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="f34b2-120">El almacén de copia de seguridad contiene también las directivas de copia de seguridad que se aplican a las máquinas virtuales cuya copia de seguridad se está realizando.</span><span class="sxs-lookup"><span data-stu-id="f34b2-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f34b2-121">A partir de marzo de 2017, ya no podrá usar el portal clásico para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="f34b2-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="f34b2-122">Puede actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f34b2-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="f34b2-123">Para más información, consulte el artículo [Actualización de un almacén de Backup a un almacén de Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="f34b2-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="f34b2-124">Microsoft anima a actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f34b2-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="f34b2-125">A partir del 15 de octubre de 2017, no podrá usar PowerShell para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="f34b2-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="f34b2-126">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="f34b2-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="f34b2-127">Todos los almacenes de Backup restantes se actualizarán automáticamente a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f34b2-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="f34b2-128">No podrá acceder a los datos de copia de seguridad en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="f34b2-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="f34b2-129">En su lugar, utilice Azure Portal para tener acceso a los datos de copia de seguridad en los almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f34b2-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="f34b2-130">Detección y registro de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="f34b2-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="f34b2-131">Antes de registrar la máquina virtual con un almacén, ejecute el proceso de detección para identificar nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f34b2-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="f34b2-132">Este proceso devuelve una lista de las máquinas virtuales incluidas en la suscripción, junto con información adicional; por ejemplo, el nombre del servicio en la nube y la región.</span><span class="sxs-lookup"><span data-stu-id="f34b2-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="f34b2-133">Inicie sesión en el [Portal de Azure clásico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="f34b2-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="f34b2-134">En el Portal de Azure clásico, haga clic en **Recovery Services** para abrir la lista de almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f34b2-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="f34b2-135">![Seleccionar carga de trabajo](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="f34b2-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="f34b2-136">En la lista de almacenes de copia de seguridad, seleccione el almacén de copia de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f34b2-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="f34b2-137">Cuando seleccione el almacén, este se abrirá en la página **Inicio rápido**</span><span class="sxs-lookup"><span data-stu-id="f34b2-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="f34b2-138">En el menú del almacén, haga clic en **Elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="f34b2-138">From the vault menu, click **Registered Items**.</span></span>

    ![Seleccionar carga de trabajo](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="f34b2-140">En el menú **Tipo**, seleccione **Máquina virtual de Azure**.</span><span class="sxs-lookup"><span data-stu-id="f34b2-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="f34b2-142">Haga clic en **DETECTAR** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="f34b2-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="f34b2-143">![Botón Detectar](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="f34b2-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="f34b2-144">El proceso de detección puede tardar unos minutos mientras se tabulan las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f34b2-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="f34b2-145">Hay una notificación en la parte inferior de la pantalla que informa de que el proceso se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="f34b2-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Detectar máquinas virtuales](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="f34b2-147">La notificación cambia cuando el proceso se completa.</span><span class="sxs-lookup"><span data-stu-id="f34b2-147">The notification changes when the process is complete.</span></span>

    ![Detección realizada](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="f34b2-149">Haga clic en **REGISTRAR** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="f34b2-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="f34b2-150">![Botón Registrar](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="f34b2-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="f34b2-151">En el menú contextual **Elementos registrados** , seleccione las máquinas virtuales que desea registrar.</span><span class="sxs-lookup"><span data-stu-id="f34b2-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="f34b2-152">Se pueden registrar varias máquinas virtuales al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="f34b2-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="f34b2-153">Se crea un trabajo para cada máquina virtual que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="f34b2-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="f34b2-154">Haga clic en **Ver trabajo** en la notificación para ir a la página **Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="f34b2-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Registrar trabajo](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="f34b2-156">La máquina virtual también aparece en la lista de elementos registrados junto con el estado de la operación de registro.</span><span class="sxs-lookup"><span data-stu-id="f34b2-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Registrando estado 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="f34b2-158">Una vez completada la operación, el estado cambia a *registrado* .</span><span class="sxs-lookup"><span data-stu-id="f34b2-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Registrando estado 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="f34b2-160">Instale el agente de máquina virtual en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f34b2-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="f34b2-161">El agente de máquina virtual de Azure se debe instalar en la máquina virtual de Azure para que funcione la extensión de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f34b2-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="f34b2-162">Si la máquina virtual se creó desde la galería de Azure, el agente de máquina virtual ya está presente en la máquina virtual; puede pasar directamente a la [protección de las máquinas virtuales](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="f34b2-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="f34b2-163">Si la máquina virtual se migra desde un centro de datos local, es probable que no tenga instalado el agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f34b2-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="f34b2-164">Debe instalar al agente de máquina virtual en la máquina virtual antes de continuar con su protección.</span><span class="sxs-lookup"><span data-stu-id="f34b2-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="f34b2-165">Para más información sobre cómo instalar el agente de máquina virtual, consulte la [sección Agente de máquina virtual del artículo Copia de seguridad de máquinas virtuales](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="f34b2-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="f34b2-166">Creación de la directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="f34b2-166">Create the backup policy</span></span>
<span data-ttu-id="f34b2-167">Antes de desencadenar el trabajo de copia de seguridad inicial, establezca la programación de cuándo se van a realizar las instantáneas de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f34b2-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="f34b2-168">La programación de cuándo se realizan las instantáneas de copia de seguridad y el período de tiempo durante el que se conservan dichas instantáneas, forman la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f34b2-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="f34b2-169">La información de retención se basa en un esquema de rotación abuelo-padre-hijo (GFS) para las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f34b2-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="f34b2-170">Navegue al almacén de copia de seguridad en **Recovery Services** en el Portal de Azure clásico y haga clic en **Elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="f34b2-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="f34b2-171">Seleccione **Máquina virtual de Azure** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="f34b2-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Seleccionar carga de trabajo en el portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="f34b2-173">Haga clic en **PROTEGER** , en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="f34b2-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="f34b2-174">![Haga clic en Proteger](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="f34b2-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="f34b2-175">Aparece el **Asistente para la protección de elementos** , que enumera *solo* las máquinas virtuales que están registradas y no protegidas.</span><span class="sxs-lookup"><span data-stu-id="f34b2-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configuración de protección a escala](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="f34b2-177">Seleccione las máquinas virtuales que desee proteger.</span><span class="sxs-lookup"><span data-stu-id="f34b2-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="f34b2-178">Si hay dos o más máquinas virtuales con el mismo nombre, use el servicio en la nube para distinguirlas.</span><span class="sxs-lookup"><span data-stu-id="f34b2-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="f34b2-179">En el menú **Configurar la protección** , seleccione una directiva existente o cree una nueva para proteger las máquinas virtuales que ha identificado.</span><span class="sxs-lookup"><span data-stu-id="f34b2-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="f34b2-180">Los nuevos almacenes de copia de seguridad tienen una directiva predeterminada asociada con el almacén.</span><span class="sxs-lookup"><span data-stu-id="f34b2-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="f34b2-181">Esta directiva realiza una instantáneas diaria cada noche que se conserva durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="f34b2-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="f34b2-182">Cada directiva de copia de seguridad puede tener asociadas varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f34b2-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="f34b2-183">Sin embargo, la máquina virtual solo se puede asociar con una directiva cada vez.</span><span class="sxs-lookup"><span data-stu-id="f34b2-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![Protección mediante nueva directiva](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="f34b2-185">Una directiva de copia de seguridad incluye un esquema de retención de las copias de seguridad programadas.</span><span class="sxs-lookup"><span data-stu-id="f34b2-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="f34b2-186">Si selecciona una directiva de copia de seguridad existente, no podrá modificar las opciones de retención en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="f34b2-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="f34b2-187">En **Duración de retención** , defina el ámbito diario, semanal, mensual y anual de los puntos de copia de seguridad específicos.</span><span class="sxs-lookup"><span data-stu-id="f34b2-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="f34b2-189">La directiva de retención especifica el período de tiempo que se almacena una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f34b2-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="f34b2-190">Puede especificar directivas de retención diferentes en función de cuándo se realizó la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f34b2-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="f34b2-191">Haga clic en **Trabajos** para ver la lista de trabajos de **Configurar protección**.</span><span class="sxs-lookup"><span data-stu-id="f34b2-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![Configurar trabajo de protección](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="f34b2-193">Ahora que ha establecido la directiva, vaya al paso siguiente y ejecute la copia de seguridad inicial.</span><span class="sxs-lookup"><span data-stu-id="f34b2-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="f34b2-194">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="f34b2-194">Initial backup</span></span>
<span data-ttu-id="f34b2-195">Una vez que una máquina virtual se ha protegido con una directiva, dicha relación se puede ver en la pestaña **Elementos protegidos** . Hasta que se realiza la copia de seguridad inicial, en **Estado de protección** se muestra el valor **Protegido (copia de seguridad inicial pendiente)**.</span><span class="sxs-lookup"><span data-stu-id="f34b2-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="f34b2-196">De forma predeterminada, la primera copia de seguridad programada es la *copia de seguridad inicial*.</span><span class="sxs-lookup"><span data-stu-id="f34b2-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![Copia de seguridad pendiente](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="f34b2-198">Para empezar con la copia de seguridad inicial de forma inmediata:</span><span class="sxs-lookup"><span data-stu-id="f34b2-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="f34b2-199">En la página **Elementos protegidos**, haga clic en **Realizar copia de seguridad ahora** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="f34b2-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="f34b2-200">![Icono Realizar copia de seguridad ahora](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="f34b2-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="f34b2-201">El servicio Copia de seguridad de Azure crea un trabajo de copia de seguridad para la operación de copia de seguridad inicial.</span><span class="sxs-lookup"><span data-stu-id="f34b2-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="f34b2-202">Haga clic en la pestaña **Trabajos** para ver la lista de los trabajos.</span><span class="sxs-lookup"><span data-stu-id="f34b2-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Copia de seguridad en curso](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="f34b2-204">Una vez completada la copia de seguridad inicial, el estado de la máquina virtual en la pestaña **Elementos protegidos** es *Protegido*.</span><span class="sxs-lookup"><span data-stu-id="f34b2-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="f34b2-206">La copia de seguridad de máquinas virtuales es un proceso local.</span><span class="sxs-lookup"><span data-stu-id="f34b2-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="f34b2-207">No puede realizar copias de seguridad de máquinas virtuales desde una región hasta un almacén de copia de seguridad de otra región.</span><span class="sxs-lookup"><span data-stu-id="f34b2-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="f34b2-208">Por lo tanto, para cada región de Azure que tiene máquinas virtuales que necesiten una copia de seguridad, debe crearse al menos un almacén de copia de seguridad en esa región.</span><span class="sxs-lookup"><span data-stu-id="f34b2-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="f34b2-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f34b2-209">Next steps</span></span>
<span data-ttu-id="f34b2-210">Una vez que se ha copiado correctamente una máquina virtual, hay varios pasos que pueden ser de interés.</span><span class="sxs-lookup"><span data-stu-id="f34b2-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="f34b2-211">El paso más lógico sería familiarizarse con la restauración de datos en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f34b2-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="f34b2-212">Sin embargo, hay tareas de administración que le ayudarán a entender cómo mantener seguros los datos y minimizar los costos.</span><span class="sxs-lookup"><span data-stu-id="f34b2-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="f34b2-213">Administración y supervisión de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f34b2-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="f34b2-214">Restauración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="f34b2-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="f34b2-215">Guía de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="f34b2-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="f34b2-216">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="f34b2-216">Questions?</span></span>
<span data-ttu-id="f34b2-217">Si tiene alguna pregunta o hay alguna característica que le gustaría que se incluyera, [envíenos sus comentarios](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="f34b2-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

---
title: "Primer vistazo: copia de seguridad de máquinas virtuales de Azure con un almacén de copia de seguridad | Microsoft Docs"
description: "Utilice tooback portal clásico de hello el almacén de copia de seguridad de máquinas virtuales de Azure tooa. Este tutorial le explica todas las fases incluidas crear almacén de copia de seguridad de hello, registrar máquinas virtuales de hello, creación de directiva de copia de seguridad y ejecuta el trabajo de copia de seguridad inicial de Hola."
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
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="00446-104">Primer contacto: copia de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="00446-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00446-105">Protección de máquinas virtuales con un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="00446-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="00446-106">Protección de máquinas virtuales con un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="00446-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="00446-107">Este tutorial le guiará por los pasos de Hola para copia de seguridad de un almacén de copia de seguridad de máquina virtual (VM) Azure tooa en Azure.</span><span class="sxs-lookup"><span data-stu-id="00446-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="00446-108">Este artículo describe el modelo clásico de Hola o modelo de implementación de Service Manager, para realizar copias de seguridad de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="00446-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="00446-109">Hello pasos siguientes aplican solo los almacenes de tooBackup creados en portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="00446-110">Microsoft recomienda utilizar el modelo de administrador de recursos de Hola para nuevas implementaciones.</span><span class="sxs-lookup"><span data-stu-id="00446-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="00446-111">Si está interesado en copia de seguridad de un almacén de servicios de recuperación de tooa VM que pertenezca tooa grupo de recursos, consulte [primer vistazo: proteger las máquinas virtuales con un almacén de servicios de recuperación](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="00446-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="00446-112">toosuccessfully completar siguiente Hola tutorial, deben existir en estos requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="00446-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="00446-113">Ha creado una máquina virtual en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="00446-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="00446-114">Hola VM tiene direcciones IP públicas de conectividad tooAzure.</span><span class="sxs-lookup"><span data-stu-id="00446-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="00446-115">Para más información, consulte [Conectividad de red](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="00446-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="00446-116">Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="00446-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="00446-117">Este tutorial es para su uso con las máquinas virtuales creadas en portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="00446-118">Creación de un almacén de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="00446-118">Create a backup vault</span></span>
<span data-ttu-id="00446-119">Un almacén de copia de seguridad es una entidad que almacena todas las copias de seguridad de Hola y puntos de recuperación que se han creado con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="00446-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="00446-120">almacén de copia de seguridad de Hello también contiene las directivas de copia de seguridad de hello son máquinas virtuales de toohello aplicado haciendo copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="00446-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00446-121">A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.</span><span class="sxs-lookup"><span data-stu-id="00446-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="00446-122">Puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="00446-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="00446-123">Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="00446-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="00446-124">Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="00446-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="00446-125">Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00446-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="00446-126">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="00446-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="00446-127">Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="00446-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="00446-128">No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="00446-129">En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="00446-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="00446-130">Detección y registro de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="00446-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="00446-131">Antes de registrar Hola VM a un almacén, ejecute tooidentify de proceso de detección de hello las nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="00446-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="00446-132">Esto devuelve una lista de máquinas virtuales en la suscripción de hello, junto con información adicional como el nombre del servicio de nube de Hola y región Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="00446-133">Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="00446-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="00446-134">Hola portal de Azure clásico, haga clic en **servicios de recuperación** tooopen lista de Hola de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="00446-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="00446-135">![Seleccionar carga de trabajo](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="00446-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="00446-136">En lista de Hola de almacenes de credenciales, seleccione hello tooback de almacén de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00446-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="00446-137">Cuando se selecciona el almacén, se abre en hello **inicio rápido** página</span><span class="sxs-lookup"><span data-stu-id="00446-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="00446-138">En el menú de almacén de hello, haga clic en **elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="00446-138">From hello vault menu, click **Registered Items**.</span></span>

    ![Seleccionar carga de trabajo](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="00446-140">De hello **tipo** menú, seleccione **Máquina Virtual de Azure**.</span><span class="sxs-lookup"><span data-stu-id="00446-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="00446-142">Haga clic en **DISCOVER** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="00446-143">![Botón Detectar](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="00446-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="00446-144">proceso de detección de Hello puede tardar unos minutos mientras se se tabulan hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="00446-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="00446-145">Hay una notificación en la parte inferior de Hola de pantalla de bienvenida que le permite saber que se está ejecutando el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Detectar máquinas virtuales](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="00446-147">notificación de Hello cambia cuando se complete el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-147">hello notification changes when hello process is complete.</span></span>

    ![Detección realizada](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="00446-149">Haga clic en **registrar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="00446-150">![Botón Registrar](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="00446-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="00446-151">Hola **registrar elementos** menú contextual, seleccione hello las máquinas virtuales que desea tooregister.</span><span class="sxs-lookup"><span data-stu-id="00446-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="00446-152">Se pueden registrar varias máquinas virtuales al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="00446-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="00446-153">Se crea un trabajo para cada máquina virtual que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="00446-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="00446-154">Haga clic en **ver trabajo** en hello notificación toogo toohello **trabajos** página.</span><span class="sxs-lookup"><span data-stu-id="00446-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Registrar trabajo](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="00446-156">máquina virtual de Hola también aparece en la lista de Hola de los elementos registrados, junto con el estado de Hola de operación de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="00446-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Registrando estado 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="00446-158">Cuando se completa la operación de hello, estado de hello cambia hello tooreflect *registrado* estado.</span><span class="sxs-lookup"><span data-stu-id="00446-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Registrando estado 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="00446-160">Instalar agente de máquina virtual de hello en la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="00446-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="00446-161">Hello Azure VM Agent debe instalarse en la máquina virtual de Azure para toowork de extensión de copia de seguridad de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="00446-162">Si la máquina virtual se creó desde Hola Galería de Azure, Hola agente de máquina virtual ya está presente en hello VM; puede omitir demasiado[protege las máquinas virtuales](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="00446-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="00446-163">Si la máquina virtual se migra desde un centro de datos local, Hola VM probablemente no tiene Hola instalado el agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00446-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="00446-164">Debe instalar Hola agente de máquina virtual en la máquina virtual de hello antes de Hola de tooprotect continuar máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00446-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="00446-165">Para obtener pasos detallados acerca de cómo instalar hello agente de máquina virtual, vea hello [sección de agente de máquina virtual de artículo de máquinas virtuales de copia de seguridad de hello](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="00446-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="00446-166">Crear directiva de copia de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="00446-166">Create hello backup policy</span></span>
<span data-ttu-id="00446-167">Antes de desencadenar el trabajo de copia de seguridad inicial de hello, establecer la programación de hello cuando se realizan las instantáneas de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="00446-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="00446-168">programación de Hello cuando se toman las instantáneas de copia de seguridad; Hola tiempo de esas instantáneas conservan, son directiva de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="00446-169">información de retención de Hola se basa en el esquema de rotación de copia de seguridad de su Abuelo-padre-hijo.</span><span class="sxs-lookup"><span data-stu-id="00446-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="00446-170">Navegar por el almacén de copia de seguridad toohello en **servicios de recuperación** en Hola portal de Azure clásico y haga clic en **elementos registrados**.</span><span class="sxs-lookup"><span data-stu-id="00446-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="00446-171">Seleccione **Máquina Virtual de Azure** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Seleccionar carga de trabajo en el portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="00446-173">Haga clic en **proteger** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="00446-174">![Haga clic en Proteger](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="00446-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="00446-175">Hola **Asistente para proteger elementos** aparece y muestra *sólo* máquinas virtuales que están registradas y no protegidas.</span><span class="sxs-lookup"><span data-stu-id="00446-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configuración de protección a escala](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="00446-177">Seleccione hello las máquinas virtuales que desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="00446-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="00446-178">Si hay dos o más máquinas virtuales con hello mismo nombre, use hello toodistinguish de servicio en la nube entre las máquinas virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="00446-179">En hello **configurar la protección** menú Seleccione una directiva existente o cree una nueva tooprotect directiva máquinas virtuales de Hola que identificó.</span><span class="sxs-lookup"><span data-stu-id="00446-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="00446-180">Nuevos almacenes de copia de seguridad tienen una directiva predeterminada asociada con el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="00446-181">Esta directiva tiene un diario de instantáneas cada noche e instantánea diaria Hola se conserva durante 30 días.</span><span class="sxs-lookup"><span data-stu-id="00446-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="00446-182">Cada directiva de copia de seguridad puede tener asociadas varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="00446-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="00446-183">Sin embargo, Hola máquina virtual puede estar solo asociado a una directiva a la vez.</span><span class="sxs-lookup"><span data-stu-id="00446-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![Protección mediante nueva directiva](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="00446-185">Una directiva de copia de seguridad incluye un esquema de retención de copias de seguridad programada de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="00446-186">Si selecciona una directiva de copia de seguridad existente, será opciones de retención no se puede toomodify hello en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="00446-187">En **duración de retención** definir Hola ámbito diaria, semanal, mensual y anual de puntos de copia de seguridad específicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="00446-189">Directiva de retención especifica Hola período de tiempo para almacenar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="00446-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="00446-190">Puede especificar las directivas de retención diferentes en función de cuando se realizó la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="00446-191">Haga clic en **trabajos** lista de hello tooview de **configurar la protección** trabajos.</span><span class="sxs-lookup"><span data-stu-id="00446-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![Configurar trabajo de protección](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="00446-193">Ahora que ha establecido la directiva de Hola, vaya toohello siguiente paso y ejecutar copia de seguridad inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="00446-194">Copia de seguridad inicial</span><span class="sxs-lookup"><span data-stu-id="00446-194">Initial backup</span></span>
<span data-ttu-id="00446-195">Una vez que una máquina virtual se ha protegido con una directiva, puede ver esa relación en hello **elementos protegidos** ficha. Hasta que la copia de seguridad inicial de Hola se produce, hello **el estado de protección** se muestra como **Protected - (pendiente de copia de seguridad inicial)**.</span><span class="sxs-lookup"><span data-stu-id="00446-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="00446-196">De forma predeterminada, copia de seguridad programada Hola primer es hello *copia de seguridad inicial*.</span><span class="sxs-lookup"><span data-stu-id="00446-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![Copia de seguridad pendiente](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="00446-198">toostart Hola copia de seguridad inicial ahora:</span><span class="sxs-lookup"><span data-stu-id="00446-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="00446-199">En hello **elementos protegidos** página, haga clic en **copia de seguridad ahora** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="00446-200">![Icono Realizar copia de seguridad ahora](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="00446-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="00446-201">Hola servicio copia de seguridad de Azure crea un trabajo de copia de seguridad para la operación de copia de seguridad inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="00446-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="00446-202">Haga clic en hello **trabajos** lista de pestañas tooview Hola de trabajos.</span><span class="sxs-lookup"><span data-stu-id="00446-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Copia de seguridad en curso](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="00446-204">Cuando la copia de seguridad inicial está completa, el estado de Hola de máquina virtual de Hola Hola **elementos protegidos** ficha es *Protected*.</span><span class="sxs-lookup"><span data-stu-id="00446-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="00446-206">La copia de seguridad de máquinas virtuales es un proceso local.</span><span class="sxs-lookup"><span data-stu-id="00446-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="00446-207">No puede hacer copia de seguridad de máquinas virtuales desde un almacén de copia de seguridad de tooa región en otra región.</span><span class="sxs-lookup"><span data-stu-id="00446-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="00446-208">Por lo tanto, para cada región de Azure que tiene máquinas virtuales que necesitan toobe copia de seguridad, al menos un almacén de copia de seguridad debe crearse en dicha región.</span><span class="sxs-lookup"><span data-stu-id="00446-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="00446-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="00446-209">Next steps</span></span>
<span data-ttu-id="00446-210">Una vez que se ha copiado correctamente una máquina virtual, hay varios pasos que pueden ser de interés.</span><span class="sxs-lookup"><span data-stu-id="00446-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="00446-211">paso más lógica Hello es toofamiliarize usted mismo con la restauración de datos tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="00446-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="00446-212">Sin embargo, hay tareas de administración que le ayudará a entender cómo tookeep los datos seguros y minimizar los costes.</span><span class="sxs-lookup"><span data-stu-id="00446-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="00446-213">Administración y supervisión de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="00446-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="00446-214">Restauración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="00446-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="00446-215">Guía de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="00446-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="00446-216">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="00446-216">Questions?</span></span>
<span data-ttu-id="00446-217">Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="00446-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

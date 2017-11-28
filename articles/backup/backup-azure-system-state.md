---
title: aaaBack una tooAzure de estado de sistema de Windows | Documentos de Microsoft
description: "Obtenga información acerca de tooback el estado de sistema de Hola de Windows Server o tooAzure de equipos de Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "¿Cómo toobackup; ¿Cómo tooback; las carpetas y archivos de copia de seguridad"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="15fdf-104">Copias de seguridad del estado del sistema de Windows en la implementación de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="15fdf-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="15fdf-105">Este artículo explica cómo tooback el sistema de Windows Server estado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="15fdf-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="15fdf-106">Es un tutorial toowalk previsto le guían a través de los conceptos básicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="15fdf-107">Si desea más información acerca de la copia de seguridad de Azure tooknow, lea esta [Introducción](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="15fdf-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="15fdf-108">Si no tiene una suscripción de Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) que le permita acceder a todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="15fdf-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="15fdf-109">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="15fdf-109">Create a recovery services vault</span></span>
<span data-ttu-id="15fdf-110">tooback seguridad de archivos y carpetas, deberá toocreate un almacén de servicios de recuperación de la región de Hola donde desea toostore Hola datos.</span><span class="sxs-lookup"><span data-stu-id="15fdf-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="15fdf-111">También debe toodetermine cómo desea que su almacenamiento replicado.</span><span class="sxs-lookup"><span data-stu-id="15fdf-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="15fdf-112">toocreate un almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="15fdf-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="15fdf-113">Si aún no lo ha hecho, inicie sesión en toohello [Portal de Azure](https://portal.azure.com/) con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="15fdf-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="15fdf-114">En el menú del concentrador hello, haga clic en **más servicios** y en la lista de Hola de recursos, escriba **servicios de recuperación** y haga clic en **servicios de recuperación de los almacenes de credenciales**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="15fdf-116">Si no hay almacenes de servicios de recuperación de la suscripción de hello, se enumeran los almacenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="15fdf-117">En hello **servicios de recuperación de los almacenes de credenciales** menú, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="15fdf-119">Servicios de recuperación de Hello del almacén se abre de hoja, que le pide que tooprovide una **nombre**, **suscripción**, **grupo de recursos**, y **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creación del almacén de Recovery Services, paso 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="15fdf-121">Para **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="15fdf-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="15fdf-122">nombre de Hello debe toobe único para hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="15fdf-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="15fdf-123">Escriba un nombre que tenga entre 2 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="15fdf-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="15fdf-124">Debe comenzar por una letra y solo puede contener letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="15fdf-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="15fdf-125">Hola **suscripción** sección, usar Hola menú desplegable toochoose hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="15fdf-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="15fdf-126">Si usa una sola suscripción, que aparece de la suscripción y puede omitir el paso siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="15fdf-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="15fdf-127">Si no está seguro de qué toouse de suscripción, utilice Hola predeterminado (o sugiere) suscripción.</span><span class="sxs-lookup"><span data-stu-id="15fdf-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="15fdf-128">Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="15fdf-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="15fdf-129">Hola **grupo de recursos** sección:</span><span class="sxs-lookup"><span data-stu-id="15fdf-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="15fdf-130">Seleccione **crear nuevo** si desea que toocreate un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="15fdf-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="15fdf-131">O</span><span class="sxs-lookup"><span data-stu-id="15fdf-131">Or</span></span>
    * <span data-ttu-id="15fdf-132">Seleccione **utilizar existente** y haga clic en hello menú desplegable toosee Hola disponible lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="15fdf-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="15fdf-133">Para obtener información completa sobre los grupos de recursos, vea hello [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15fdf-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="15fdf-134">Haga clic en **ubicación** región geográfica de tooselect hello para el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="15fdf-135">Esta opción determina dónde se envían los datos de copia de seguridad de región geográfica Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="15fdf-136">En la parte inferior de Hola de hoja de almacén de servicios de recuperación de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="15fdf-137">Puede tardar varios minutos para hello que toobe creado del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="15fdf-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="15fdf-138">Supervisar las notificaciones de estado de hello en el área superior derecha de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="15fdf-139">Una vez creado el almacén, aparece en la lista de Hola de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="15fdf-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="15fdf-140">Si no ve el almacén pasados unos minutos, haga clic en **Refresh** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="15fdf-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Clic en el botón Refresh (Actualizar)](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="15fdf-142">Una vez que vea el almacén en la lista de Hola de almacenes de servicios de recuperación, son redundancia de almacenamiento de hello tooset listo.</span><span class="sxs-lookup"><span data-stu-id="15fdf-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="15fdf-143">Establecer la redundancia de almacenamiento para el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="15fdf-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="15fdf-144">Cuando se crea un almacén de servicios de recuperación, asegúrese de redundancia de almacenamiento está configurado Hola que quieras.</span><span class="sxs-lookup"><span data-stu-id="15fdf-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="15fdf-145">De hello **servicios de recuperación de los almacenes de credenciales** hoja, haga clic en nuevo almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Seleccione el nuevo almacén de Hola de lista de Hola de almacén de servicios de recuperación](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="15fdf-147">Cuando se selecciona el almacén de hello, Hola **del almacén de servicios de recuperación** permite delimitar hoja y hoja de configuración de hello (*que tiene el nombre de Hola de almacén de hello en la parte superior de hello*) y hoja de detalles de almacén de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="15fdf-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Configuración de almacenamiento de vista Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="15fdf-149">En la hoja de configuración del nuevo almacén de hello, hello tooscroll de desplazamiento vertical hacia abajo toohello sección administrar y haga clic en **infraestructura de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="15fdf-150">se abre la hoja de la infraestructura de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="15fdf-151">En la hoja de la infraestructura de copia de seguridad de hello, haga clic en **configuración de copia de seguridad** tooopen hello **configuración de copia de seguridad** hoja.</span><span class="sxs-lookup"><span data-stu-id="15fdf-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Establecer configuración de almacenamiento de Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="15fdf-153">Elija la opción de replicación de almacenamiento apropiada de hello para el almacén.</span><span class="sxs-lookup"><span data-stu-id="15fdf-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![opciones de configuración de almacenamiento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="15fdf-155">De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="15fdf-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="15fdf-156">Si utiliza Azure como un punto de conexión de almacenamiento principal de copia de seguridad, continúe toouse **con redundancia geográfica**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="15fdf-157">Si no utiliza Azure como un punto de conexión de almacenamiento de copia de seguridad principal, a continuación, elija **localmente redundante**, lo que reduce los costos de almacenamiento de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="15fdf-158">En esta página de [información general sobre la redundancia del almacenamiento](../storage/common/storage-redundancy.md) encontrará más información sobre las opciones de almacenamiento con [redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="15fdf-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="15fdf-159">Ahora que ha creado un almacén, configúrelo para realizar copias de seguridad del estado del sistema de Windows.</span><span class="sxs-lookup"><span data-stu-id="15fdf-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="15fdf-160">Configurar el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="15fdf-160">Configure hello vault</span></span>
1. <span data-ttu-id="15fdf-161">Hola hoja de almacén de servicios de recuperación (hello para el almacén de que acaba de crear), en la sección de introducción de hello en, haga clic en **copia de seguridad**, a continuación, en hello **Introducción a la copia de seguridad** hoja, seleccione  **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="15fdf-163">Hola **objetivo de copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="15fdf-163">hello **Backup Goal** blade opens.</span></span>

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="15fdf-165">De hello **donde se está ejecutando la carga de trabajo?** menú desplegable, seleccione **local**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="15fdf-166">Elija **Local** ya que su equipo Windows o Windows Server es una máquina física que no está en Azure.</span><span class="sxs-lookup"><span data-stu-id="15fdf-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="15fdf-167">De hello **especifique qué desea toobackup?** menú, seleccione **estado del sistema**y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![Configuración de archivos y carpetas](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="15fdf-169">Después de hacer clic en Aceptar, aparece una marca siguiente demasiado**objetivo de copia de seguridad**, hello y **preparar infraestructura** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="15fdf-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Objetivo de copia de seguridad configurado, a continuación, prepare la infraestructura](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="15fdf-171">En hello **preparar infraestructura** hoja, haga clic en **descargar agente para Windows Server o cliente de Windows**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="15fdf-173">Si usa Windows Server esencial, a continuación, elija a agente de hello toodownload para Windows Server esenciales.</span><span class="sxs-lookup"><span data-stu-id="15fdf-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="15fdf-174">Un menú emergente le pide que toorun o guardar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="15fdf-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Cuadro de diálogo de MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="15fdf-176">En el menú emergente de descarga de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="15fdf-177">De forma predeterminada, Hola **MARSagentinstaller.exe** archivo se guarda la carpeta de descargas de tooyour.</span><span class="sxs-lookup"><span data-stu-id="15fdf-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="15fdf-178">Cuando se completa el instalador de hello, verá una ventana emergente que pregunta si desea que el instalador de toorun hello, o Abrir carpeta Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="15fdf-180">No es necesario a tooinstall agente de hello todavía.</span><span class="sxs-lookup"><span data-stu-id="15fdf-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="15fdf-181">Puede instalar a agente de hello después de haber descargado las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="15fdf-182">En hello **preparar infraestructura** hoja, haga clic en **descargar**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![descargar las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="15fdf-184">carpeta de descargas de tooyour de descarga de las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="15fdf-185">Después de que las credenciales de almacén de hello termine la descarga, verá una ventana emergente que pregunta si desea tooopen o guardar las credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="15fdf-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-186">Click **Save**.</span></span> <span data-ttu-id="15fdf-187">Si hace clic en accidentalmente **abiertos**, permitir que el cuadro de diálogo de Hola que trata las credenciales de almacén de hello tooopen, producirá un error.</span><span class="sxs-lookup"><span data-stu-id="15fdf-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="15fdf-188">No se puede abrir las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="15fdf-189">Continúe toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="15fdf-189">Proceed toohello next step.</span></span> <span data-ttu-id="15fdf-190">las credenciales de almacén de Hola están en la carpeta de descargas de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![finalizó la descarga de las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="15fdf-192">Instalar y registrar el agente de Hola</span><span class="sxs-lookup"><span data-stu-id="15fdf-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="15fdf-193">Habilitar copia de seguridad a través del portal de Azure Hola todavía no está disponible.</span><span class="sxs-lookup"><span data-stu-id="15fdf-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="15fdf-194">Utilice tooback de agente de servicios de recuperación de Microsoft Azure Hola el estado de sistema de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="15fdf-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="15fdf-195">Busque y haga doble clic en hello **MARSagentinstaller.exe** desde la carpeta de descargas de hello (u otra ubicación de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="15fdf-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="15fdf-196">instalador de Hello proporciona una serie de mensajes cuando extrae, instala y registra el agente de servicios de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![ejecutar las credenciales del instalador del agente de Recovery Services](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="15fdf-198">Asistente para la instalación de Microsoft Azure Recovery Services agente de hello completa.</span><span class="sxs-lookup"><span data-stu-id="15fdf-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="15fdf-199">Asistente de hello toocomplete, debe:</span><span class="sxs-lookup"><span data-stu-id="15fdf-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="15fdf-200">Elegir una ubicación para la carpeta de instalación y de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="15fdf-201">Proporcionar la proxy información al servidor si usa un toohello de tooconnect de servidor proxy internet.</span><span class="sxs-lookup"><span data-stu-id="15fdf-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="15fdf-202">Si usa un servidor proxy autenticado, escriba los detalles de nombre y contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="15fdf-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="15fdf-203">Proporcione las credenciales de almacén de hello descargado</span><span class="sxs-lookup"><span data-stu-id="15fdf-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="15fdf-204">Guarde la frase de contraseña de cifrado de hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="15fdf-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="15fdf-205">Si pierde u olvida la frase de contraseña de hello, Microsoft no puede ayudar a recuperar datos de copia de seguridad de saludo.</span><span class="sxs-lookup"><span data-stu-id="15fdf-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="15fdf-206">Guarde el archivo hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="15fdf-206">Save hello file in a secure location.</span></span> <span data-ttu-id="15fdf-207">Es necesario toorestore una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="15fdf-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="15fdf-208">Ahora está instalado el agente de Hola y su equipo es el almacén de toohello registrados.</span><span class="sxs-lookup"><span data-stu-id="15fdf-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="15fdf-209">Está listo tooconfigure y programar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="15fdf-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="15fdf-210">Copia de seguridad del estado del sistema de Windows Server (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="15fdf-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="15fdf-211">copia de seguridad inicial de Hello incluye tres tareas:</span><span class="sxs-lookup"><span data-stu-id="15fdf-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="15fdf-212">Habilitar la copia de seguridad de estado de sistema con hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="15fdf-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="15fdf-213">Programar copias de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="15fdf-213">Schedule hello backup</span></span>
* <span data-ttu-id="15fdf-214">Realizar una copia de archivos y carpetas de hello primera vez</span><span class="sxs-lookup"><span data-stu-id="15fdf-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="15fdf-215">toocomplete Hola copia de seguridad inicial, agente de servicios de recuperación de Microsoft Azure Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="15fdf-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="15fdf-216">tooenable de copia de seguridad de estado del sistema con el agente de copia de seguridad de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="15fdf-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="15fdf-217">En una sesión de PowerShell, ejecute hello después de motor de copia de seguridad de Azure de comando toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="15fdf-218">Abra Hola del registro de Windows.</span><span class="sxs-lookup"><span data-stu-id="15fdf-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="15fdf-219">Agregar Hola después de la clave del registro con hello especificado valor DWord.</span><span class="sxs-lookup"><span data-stu-id="15fdf-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="15fdf-220">Ruta de acceso del Registro</span><span class="sxs-lookup"><span data-stu-id="15fdf-220">Registry path</span></span> | <span data-ttu-id="15fdf-221">Clave del Registro</span><span class="sxs-lookup"><span data-stu-id="15fdf-221">Registry key</span></span> | <span data-ttu-id="15fdf-222">Valor DWord</span><span class="sxs-lookup"><span data-stu-id="15fdf-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="15fdf-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="15fdf-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="15fdf-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="15fdf-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="15fdf-225">2</span><span class="sxs-lookup"><span data-stu-id="15fdf-225">2</span></span> |

4. <span data-ttu-id="15fdf-226">Reinicie el motor de copia de seguridad de hello ejecutando el siguiente comando en un símbolo del sistema con privilegios elevados de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="15fdf-227">trabajo de copia de seguridad de hello tooschedule</span><span class="sxs-lookup"><span data-stu-id="15fdf-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="15fdf-228">Abra el agente de servicios de recuperación de Microsoft Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="15fdf-229">Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.</span><span class="sxs-lookup"><span data-stu-id="15fdf-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Iniciar el agente de servicios de recuperación de Azure de Hola](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="15fdf-231">En el agente de servicios de recuperación de hello, haga clic en **programar copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Programación de una copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="15fdf-233">En hello Introducción a la página de hello Asistente para la programación de copia de seguridad, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="15fdf-234">En la página de tooBackup de seleccionar elementos de hello, haga clic en **agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="15fdf-235">Seleccione **Estado del sistema** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="15fdf-236">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-236">Click **Next**.</span></span>

7. <span data-ttu-id="15fdf-237">Hello programación de copia de seguridad de estado del sistema y de retención se establece automáticamente tooback seguridad de todos los domingos a 9:00 P.M., hora local, y se establece el período de retención de hello too60 días.</span><span class="sxs-lookup"><span data-stu-id="15fdf-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="15fdf-238">La directiva de retención y copia de seguridad del estado del sistema se configura automáticamente.</span><span class="sxs-lookup"><span data-stu-id="15fdf-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="15fdf-239">Si hace una copia archivos y carpetas además toohello Windows Server System State, especifique la única directiva de copia de seguridad y retención de Hola para copias de seguridad de archivos de Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="15fdf-240">En la página de confirmación de hello, revise la información de hello y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="15fdf-241">Cuando finalice el Asistente de hello, crear la programación de copia de seguridad de hello, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="15fdf-242">tooback el estado de sistema de Windows Server para hello primera vez</span><span class="sxs-lookup"><span data-stu-id="15fdf-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="15fdf-243">Asegúrese de que no hay actualizaciones pendientes para Windows Server que requieran un reinicio.</span><span class="sxs-lookup"><span data-stu-id="15fdf-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="15fdf-244">En el agente de servicios de recuperación de hello, haga clic en **Back Up Now** toocomplete Hola inicial de la propagación a través de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Copia de seguridad de Windows Server ahora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="15fdf-246">En la página de confirmación de hello, revise la configuración Hola que Hola a ahora Asistente de Back Up usará tooback máquina Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="15fdf-247">Luego, haga clic en **Crear copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="15fdf-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="15fdf-248">Haga clic en **cerrar** Asistente de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="15fdf-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="15fdf-249">Si cierra al Asistente de hello antes de que finalice el proceso de copia de seguridad de hello, Asistente Hola continúa toorun en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="15fdf-250">Si hace una copia archivos y carpetas en el servidor, además toohello Windows Server System State, Asistente de copia de seguridad ahora Hola realizará solo una copia de archivos.</span><span class="sxs-lookup"><span data-stu-id="15fdf-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="15fdf-251">tooperform un estado del sistema ad hoc realizar copias de seguridad, Hola de uso siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="15fdf-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="15fdf-252">Una vez completada la copia de seguridad inicial de hello, Hola **ha completado el trabajo** estado aparece en la consola de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![IR completado](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="15fdf-254">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="15fdf-254">Frequently asked questions</span></span>

<span data-ttu-id="15fdf-255">Hello siguientes preguntas y respuestas proporcionan información complementaria.</span><span class="sxs-lookup"><span data-stu-id="15fdf-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="15fdf-256">¿Cuál es el volumen de almacenamiento provisional de Hola?</span><span class="sxs-lookup"><span data-stu-id="15fdf-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="15fdf-257">Hola volumen de almacenamiento provisional representa ubicación intermedia Hola donde hello disponible de forma nativa, copias de seguridad de Windows Server crea etapas en hello copia de seguridad de estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="15fdf-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="15fdf-258">Agente de copia de seguridad de Azure, a continuación, comprime y cifra esta copia de seguridad intermedio y envía que esta a través de secure toohello de protocolo HTTPS configurado el almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="15fdf-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="15fdf-259">**Se recomienda que establecer Hola volumen de almacenamiento provisional en un volumen sin sistema operativo Windows. Si observa problemas con las copias de seguridad de estado de sistema, comprobando ubicación Hola de su volumen de almacenamiento provisional es el primer paso de solución de problemas Hola.**</span><span class="sxs-lookup"><span data-stu-id="15fdf-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="15fdf-260">¿Cómo se puede cambiar Hola ruta de acceso de volumen de almacenamiento provisional especificada en el agente de copia de seguridad de Azure de hello?</span><span class="sxs-lookup"><span data-stu-id="15fdf-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="15fdf-261">Hola volumen de almacenamiento provisional se encuentra en la carpeta de caché de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="15fdf-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="15fdf-262">toochange esta ubicación, Hola de uso siguiente comando (en un símbolo del sistema con privilegios elevados):</span><span class="sxs-lookup"><span data-stu-id="15fdf-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="15fdf-263">A continuación, actualice Hola siguiendo las entradas del registro con la carpeta Hola ruta toohello nuevo volumen de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="15fdf-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="15fdf-264">Ruta de acceso del Registro</span><span class="sxs-lookup"><span data-stu-id="15fdf-264">Registry path</span></span>|<span data-ttu-id="15fdf-265">Clave del Registro</span><span class="sxs-lookup"><span data-stu-id="15fdf-265">Registry key</span></span>|<span data-ttu-id="15fdf-266">Valor</span><span class="sxs-lookup"><span data-stu-id="15fdf-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="15fdf-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="15fdf-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="15fdf-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="15fdf-268">SSBStagingPath</span></span> | <span data-ttu-id="15fdf-269">nueva ubicación del volumen de almacenamiento provisional</span><span class="sxs-lookup"><span data-stu-id="15fdf-269">new staging volume location</span></span> |

<span data-ttu-id="15fdf-270">Hola ruta de acceso de almacenamiento provisional distingue mayúsculas de minúsculas y debe ser Hola exacta mismo mayúsculas y minúsculas como lo que existe en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="15fdf-271">Una vez que cambie la ruta de acceso del volumen de almacenamiento provisional de hello, reinicie el motor de copia de seguridad de hello:</span><span class="sxs-lookup"><span data-stu-id="15fdf-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="15fdf-272">toopick ruta de acceso de hello cambiado, agente de servicios de recuperación de Microsoft Azure Hola abierto y desencadenador una copia de seguridad ad hoc de estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="15fdf-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="15fdf-273">¿Por qué es el estado de sistema de hello tiempo predeterminado de retención establecido too60 días?</span><span class="sxs-lookup"><span data-stu-id="15fdf-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="15fdf-274">vida útil de Hola de una copia de seguridad de estado del sistema es Hola igual a la configuración de hello, "tombstone lifetime" para el rol de Windows Server Active Directory Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="15fdf-275">valor predeterminado de Hello para la entrada de duración de objetos de desecho de hello es de 60 días.</span><span class="sxs-lookup"><span data-stu-id="15fdf-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="15fdf-276">Este valor se puede establecer en el objeto de configuración del servicio de directorio (NTDS) Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="15fdf-277">¿Cómo cambio predeterminado Hola copia de seguridad y directiva de retención para el estado del sistema?</span><span class="sxs-lookup"><span data-stu-id="15fdf-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="15fdf-278">predeterminado de hello toochange copia de seguridad y directiva de retención para el estado del sistema:</span><span class="sxs-lookup"><span data-stu-id="15fdf-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="15fdf-279">Detenga el motor de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-279">Stop hello Backup engine.</span></span> <span data-ttu-id="15fdf-280">Ejecute hello siguiente comando desde un símbolo del sistema con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="15fdf-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="15fdf-281">Agregar o actualizar Hola siguientes entradas de la clave del registro en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Backup\Config\CloudBackupProvider de Azure.</span><span class="sxs-lookup"><span data-stu-id="15fdf-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="15fdf-282">Nombre en el Registro</span><span class="sxs-lookup"><span data-stu-id="15fdf-282">Registry Name</span></span>|<span data-ttu-id="15fdf-283">Descripción</span><span class="sxs-lookup"><span data-stu-id="15fdf-283">Description</span></span>|<span data-ttu-id="15fdf-284">Valor</span><span class="sxs-lookup"><span data-stu-id="15fdf-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="15fdf-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="15fdf-285">SSBScheduleTime</span></span>|<span data-ttu-id="15fdf-286">Utiliza el tiempo de hello tooconfigure de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="15fdf-287">El valor predeterminado es 9 p. m. (hora local).</span><span class="sxs-lookup"><span data-stu-id="15fdf-287">Default is 9PM local time.</span></span>|<span data-ttu-id="15fdf-288">DWord: Formato HHMM (decimal), por ejemplo 2130 para 9:30 p. m. (hora local)</span><span class="sxs-lookup"><span data-stu-id="15fdf-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="15fdf-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="15fdf-289">SSBScheduleDays</span></span>|<span data-ttu-id="15fdf-290">Especificar los días de hello tooconfigure usado cuando debe realizarse la copia de seguridad de estado del sistema en hello tiempo.</span><span class="sxs-lookup"><span data-stu-id="15fdf-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="15fdf-291">Dígitos individuales especifican los días de la semana de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="15fdf-292">0 representa el domingo, 1 es el lunes y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="15fdf-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="15fdf-293">El día predeterminado para hacer la copia de seguridad es el domingo.</span><span class="sxs-lookup"><span data-stu-id="15fdf-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="15fdf-294">DWord: días de copia de seguridad de hello semana toorun (decimal), por ejemplo 1230 programa copias de seguridad en el lunes, el martes, el miércoles y el domingo.</span><span class="sxs-lookup"><span data-stu-id="15fdf-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="15fdf-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="15fdf-295">SSBRetentionDays</span></span>|<span data-ttu-id="15fdf-296">Tooconfigure usado Hola días tooretain copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="15fdf-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="15fdf-297">El valor predeterminado es 60.</span><span class="sxs-lookup"><span data-stu-id="15fdf-297">Default value is 60.</span></span> <span data-ttu-id="15fdf-298">El valor máximo permitido es 180.</span><span class="sxs-lookup"><span data-stu-id="15fdf-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="15fdf-299">DWord: Días tooretain copia de seguridad (decimal).</span><span class="sxs-lookup"><span data-stu-id="15fdf-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="15fdf-300">Usar hello después de motor de copia de seguridad de comando toorestart Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="15fdf-301">Abra el agente de servicios de recuperación de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="15fdf-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="15fdf-302">Haga clic en **programar copias de seguridad** y, a continuación, haga clic en **siguiente** hasta que vea cambios Hola reflejados.</span><span class="sxs-lookup"><span data-stu-id="15fdf-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="15fdf-303">Haga clic en **finalizar** cambios de hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="15fdf-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="15fdf-304">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="15fdf-304">Questions?</span></span>
<span data-ttu-id="15fdf-305">Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="15fdf-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15fdf-306">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15fdf-306">Next steps</span></span>
* <span data-ttu-id="15fdf-307">Obtenga más información acerca de cómo [realizar copias de seguridad de máquinas Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="15fdf-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="15fdf-308">Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="15fdf-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="15fdf-309">Si necesita toorestore una copia de seguridad, use este artículo demasiado[restaurar archivos tooa Windows máquina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="15fdf-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>

---
title: aaaBack la tooAzure de archivos y carpetas de Windows (Administrador de recursos) | Documentos de Microsoft
description: "Obtenga información acerca de tooback una tooAzure de archivos y carpetas de Windows en una implementación de administrador de recursos."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "¿Cómo toobackup; ¿Cómo tooback; las carpetas y archivos de copia de seguridad"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="7098e-104">Primer análisis: Copia de seguridad de archivos y carpetas en la implementación de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7098e-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="7098e-105">Este artículo se explica cómo tooback su servidor de Windows (o equipo de Windows) tooAzure de archivos y carpetas mediante una implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="7098e-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="7098e-106">Es un tutorial toowalk previsto le guían a través de los conceptos básicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="7098e-107">Si desea tooget iniciado mediante copia de seguridad de Azure, está en un lugar incorrecto Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="7098e-108">Si desea más información acerca de la copia de seguridad de Azure tooknow, lea esta [Introducción](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="7098e-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="7098e-109">Si no tiene una suscripción de Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) que le permita acceder a todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="7098e-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="7098e-110">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="7098e-110">Create a recovery services vault</span></span>
<span data-ttu-id="7098e-111">tooback seguridad de archivos y carpetas, deberá toocreate un almacén de servicios de recuperación de la región de Hola donde desea toostore Hola datos.</span><span class="sxs-lookup"><span data-stu-id="7098e-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="7098e-112">También debe toodetermine cómo desea que su almacenamiento replicado.</span><span class="sxs-lookup"><span data-stu-id="7098e-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="7098e-113">toocreate un almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="7098e-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="7098e-114">Si aún no lo ha hecho, inicie sesión en toohello [Portal de Azure](https://portal.azure.com/) con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7098e-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="7098e-115">En el menú del concentrador hello, haga clic en **más servicios** y en la lista de Hola de recursos, escriba **servicios de recuperación** y haga clic en **servicios de recuperación de los almacenes de credenciales**.</span><span class="sxs-lookup"><span data-stu-id="7098e-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="7098e-117">Si no hay almacenes de servicios de recuperación de la suscripción de hello, se enumeran los almacenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="7098e-118">En hello **servicios de recuperación de los almacenes de credenciales** menú, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="7098e-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="7098e-120">Servicios de recuperación de Hello del almacén se abre de hoja, que le pide que tooprovide una **nombre**, **suscripción**, **grupo de recursos**, y **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="7098e-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creación del almacén de Recovery Services, paso 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="7098e-122">Para **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="7098e-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="7098e-123">nombre de Hello debe toobe único para hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7098e-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="7098e-124">Escriba un nombre que tenga entre 2 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7098e-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="7098e-125">Debe comenzar por una letra y solo puede contener letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="7098e-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="7098e-126">Hola **suscripción** sección, usar Hola menú desplegable toochoose hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7098e-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="7098e-127">Si usa una sola suscripción, que aparece de la suscripción y puede omitir el paso siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="7098e-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="7098e-128">Si no está seguro de qué toouse de suscripción, utilice Hola predeterminado (o sugiere) suscripción.</span><span class="sxs-lookup"><span data-stu-id="7098e-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="7098e-129">Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7098e-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="7098e-130">Hola **grupo de recursos** sección:</span><span class="sxs-lookup"><span data-stu-id="7098e-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="7098e-131">Seleccione **crear nuevo** si desea que toocreate un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7098e-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="7098e-132">O</span><span class="sxs-lookup"><span data-stu-id="7098e-132">Or</span></span>
    * <span data-ttu-id="7098e-133">Seleccione **utilizar existente** y haga clic en hello menú desplegable toosee Hola disponible lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="7098e-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="7098e-134">Para obtener información completa sobre los grupos de recursos, vea hello [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7098e-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="7098e-135">Haga clic en **ubicación** región geográfica de tooselect hello para el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="7098e-136">Esta opción determina dónde se envían los datos de copia de seguridad de región geográfica Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="7098e-137">En la parte inferior de Hola de hoja de almacén de servicios de recuperación de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="7098e-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="7098e-138">Puede tardar varios minutos para hello que toobe creado del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="7098e-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="7098e-139">Supervisar las notificaciones de estado de hello en el área superior derecha de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="7098e-140">Una vez creado el almacén, aparece en la lista de Hola de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="7098e-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="7098e-141">Si no ve el almacén pasados unos minutos, haga clic en **Refresh** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="7098e-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Clic en el botón Refresh (Actualizar)](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="7098e-143">Una vez que vea el almacén en la lista de Hola de almacenes de servicios de recuperación, son redundancia de almacenamiento de hello tooset listo.</span><span class="sxs-lookup"><span data-stu-id="7098e-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="7098e-144">Establecer la redundancia de almacenamiento para el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="7098e-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="7098e-145">Cuando se crea un almacén de servicios de recuperación, asegúrese de redundancia de almacenamiento está configurado Hola que quieras.</span><span class="sxs-lookup"><span data-stu-id="7098e-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="7098e-146">De hello **servicios de recuperación de los almacenes de credenciales** hoja, haga clic en nuevo almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Seleccione el nuevo almacén de Hola de lista de Hola de almacén de servicios de recuperación](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="7098e-148">Cuando se selecciona el almacén de hello, Hola **del almacén de servicios de recuperación** permite delimitar hoja y hoja de configuración de hello (*que tiene el nombre de Hola de almacén de hello en la parte superior de hello*) y hoja de detalles de almacén de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="7098e-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Configuración de almacenamiento de vista Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="7098e-150">En la hoja de configuración del nuevo almacén de hello, hello tooscroll de desplazamiento vertical hacia abajo toohello sección administrar y haga clic en **infraestructura de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="7098e-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="7098e-151">se abre la hoja de la infraestructura de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="7098e-152">En la hoja de la infraestructura de copia de seguridad de hello, haga clic en **configuración de copia de seguridad** tooopen hello **configuración de copia de seguridad** hoja.</span><span class="sxs-lookup"><span data-stu-id="7098e-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Establecer configuración de almacenamiento de Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="7098e-154">Elija la opción de replicación de almacenamiento apropiada de hello para el almacén.</span><span class="sxs-lookup"><span data-stu-id="7098e-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![opciones de configuración de almacenamiento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="7098e-156">De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="7098e-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="7098e-157">Si utiliza Azure como un punto de conexión de almacenamiento principal de copia de seguridad, continúe toouse **con redundancia geográfica**.</span><span class="sxs-lookup"><span data-stu-id="7098e-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="7098e-158">Si no utiliza Azure como un punto de conexión de almacenamiento de copia de seguridad principal, a continuación, elija **localmente redundante**, lo que reduce los costos de almacenamiento de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="7098e-159">En esta página de [información general sobre la redundancia del almacenamiento](../storage/common/storage-redundancy.md) encontrará más información sobre las opciones de almacenamiento con [redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="7098e-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="7098e-160">Ahora que ha creado un almacén, configúrelo para realizar copias de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="7098e-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="7098e-161">Configurar el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="7098e-161">Configure hello vault</span></span>
1. <span data-ttu-id="7098e-162">Hola hoja de almacén de servicios de recuperación (hello para el almacén de que acaba de crear), en la sección de introducción de hello en, haga clic en **copia de seguridad**, a continuación, en hello **Introducción a la copia de seguridad** hoja, seleccione  **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="7098e-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="7098e-164">Hola **objetivo de copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="7098e-164">hello **Backup Goal** blade opens.</span></span>

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="7098e-166">De hello **donde se está ejecutando la carga de trabajo?** menú desplegable, seleccione **local**.</span><span class="sxs-lookup"><span data-stu-id="7098e-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="7098e-167">Elija **Local** ya que su equipo Windows o Windows Server es una máquina física que no está en Azure.</span><span class="sxs-lookup"><span data-stu-id="7098e-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="7098e-168">De hello **especifique qué desea toobackup?** menú, seleccione **archivos y carpetas**y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7098e-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Configuración de archivos y carpetas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="7098e-170">Después de hacer clic en Aceptar, aparece una marca siguiente demasiado**objetivo de copia de seguridad**, hello y **preparar infraestructura** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="7098e-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Objetivo de copia de seguridad configurado, a continuación, prepare la infraestructura](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="7098e-172">En hello **preparar infraestructura** hoja, haga clic en **descargar agente para Windows Server o cliente de Windows**.</span><span class="sxs-lookup"><span data-stu-id="7098e-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="7098e-174">Si usa Windows Server esencial, a continuación, elija a agente de hello toodownload para Windows Server esenciales.</span><span class="sxs-lookup"><span data-stu-id="7098e-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="7098e-175">Un menú emergente le pide que toorun o guardar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="7098e-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Cuadro de diálogo de MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="7098e-177">En el menú emergente de descarga de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="7098e-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="7098e-178">De forma predeterminada, Hola **MARSagentinstaller.exe** archivo se guarda la carpeta de descargas de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7098e-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="7098e-179">Cuando se completa el instalador de hello, verá una ventana emergente que pregunta si desea que el instalador de toorun hello, o Abrir carpeta Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="7098e-181">No es necesario a tooinstall agente de hello todavía.</span><span class="sxs-lookup"><span data-stu-id="7098e-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="7098e-182">Puede instalar a agente de hello después de haber descargado las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="7098e-183">En hello **preparar infraestructura** hoja, haga clic en **descargar**.</span><span class="sxs-lookup"><span data-stu-id="7098e-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![descargar las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="7098e-185">carpeta de descargas de tooyour de descarga de las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="7098e-186">Después de que las credenciales de almacén de hello termine la descarga, verá una ventana emergente que pregunta si desea tooopen o guardar las credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="7098e-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7098e-187">Click **Save**.</span></span> <span data-ttu-id="7098e-188">Si hace clic en accidentalmente **abiertos**, permitir que el cuadro de diálogo de Hola que trata las credenciales de almacén de hello tooopen, producirá un error.</span><span class="sxs-lookup"><span data-stu-id="7098e-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="7098e-189">No se puede abrir las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="7098e-190">Continúe toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="7098e-190">Proceed toohello next step.</span></span> <span data-ttu-id="7098e-191">las credenciales de almacén de Hola están en la carpeta de descargas de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![finalizó la descarga de las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="7098e-193">Instalar y registrar el agente de Hola</span><span class="sxs-lookup"><span data-stu-id="7098e-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="7098e-194">Habilitar copia de seguridad a través del portal de Azure Hola todavía no está disponible.</span><span class="sxs-lookup"><span data-stu-id="7098e-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="7098e-195">Utilice tooback de agente de servicios de recuperación de Microsoft Azure Hola seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="7098e-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="7098e-196">Busque y haga doble clic en hello **MARSagentinstaller.exe** desde la carpeta de descargas de hello (u otra ubicación de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="7098e-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="7098e-197">instalador de Hello proporciona una serie de mensajes cuando extrae, instala y registra el agente de servicios de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![ejecutar las credenciales del instalador del agente de Recovery Services](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="7098e-199">Asistente para la instalación de Microsoft Azure Recovery Services agente de hello completa.</span><span class="sxs-lookup"><span data-stu-id="7098e-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="7098e-200">Asistente de hello toocomplete, debe:</span><span class="sxs-lookup"><span data-stu-id="7098e-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="7098e-201">Elegir una ubicación para la carpeta de instalación y de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="7098e-202">Proporcionar la proxy información al servidor si usa un toohello de tooconnect de servidor proxy internet.</span><span class="sxs-lookup"><span data-stu-id="7098e-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="7098e-203">Si usa un servidor proxy autenticado, escriba los detalles de nombre y contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="7098e-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="7098e-204">Proporcione las credenciales de almacén de hello descargado</span><span class="sxs-lookup"><span data-stu-id="7098e-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="7098e-205">Guarde la frase de contraseña de cifrado de hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="7098e-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7098e-206">Si pierde u olvida la frase de contraseña de hello, Microsoft no puede ayudar a recuperar datos de copia de seguridad de saludo.</span><span class="sxs-lookup"><span data-stu-id="7098e-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="7098e-207">Guarde el archivo hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="7098e-207">Save hello file in a secure location.</span></span> <span data-ttu-id="7098e-208">Es necesario toorestore una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7098e-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="7098e-209">Ahora está instalado el agente de Hola y su equipo es el almacén de toohello registrados.</span><span class="sxs-lookup"><span data-stu-id="7098e-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="7098e-210">Está listo tooconfigure y programar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7098e-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="7098e-211">Requisitos de conectividad y de red</span><span class="sxs-lookup"><span data-stu-id="7098e-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="7098e-212">Si el máquina/proxy ha limitado el acceso a internet, asegúrese de que la configuración de firewall en hello mcahine/proxy es hello tooallow configurado las siguientes direcciones URL:</span><span class="sxs-lookup"><span data-stu-id="7098e-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="7098e-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="7098e-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="7098e-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="7098e-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="7098e-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="7098e-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="7098e-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="7098e-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="7098e-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="7098e-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="7098e-218">Realización de copias de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="7098e-218">Back up your files and folders</span></span>
<span data-ttu-id="7098e-219">copia de seguridad inicial de Hello incluye dos tareas fundamentales:</span><span class="sxs-lookup"><span data-stu-id="7098e-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="7098e-220">Programar copias de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="7098e-220">Schedule hello backup</span></span>
* <span data-ttu-id="7098e-221">Realizar una copia de archivos y carpetas de hello primera vez</span><span class="sxs-lookup"><span data-stu-id="7098e-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="7098e-222">toocomplete Hola copia de seguridad inicial, agente de servicios de recuperación de Microsoft Azure Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="7098e-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="7098e-223">trabajo de copia de seguridad de hello tooschedule</span><span class="sxs-lookup"><span data-stu-id="7098e-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="7098e-224">Abra el agente de servicios de recuperación de Microsoft Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="7098e-225">Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.</span><span class="sxs-lookup"><span data-stu-id="7098e-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Iniciar el agente de servicios de recuperación de Azure de Hola](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="7098e-227">En el agente de servicios de recuperación de hello, haga clic en **programar copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="7098e-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Programación de una copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="7098e-229">En hello Introducción a la página de hello Asistente para la programación de copia de seguridad, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7098e-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="7098e-230">En la página de tooBackup de seleccionar elementos de hello, haga clic en **agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="7098e-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="7098e-231">Seleccionar archivos de Hola y las carpetas que desea tooback seguridad y, a continuación, haga clic en **bien**.</span><span class="sxs-lookup"><span data-stu-id="7098e-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="7098e-232">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7098e-232">Click **Next**.</span></span>
7. <span data-ttu-id="7098e-233">En hello **especificar una programación de copia de seguridad** página, especifique hello **programar copia de seguridad** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7098e-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="7098e-234">Puede programar copias de seguridad diarias (con una frecuencia máxima de tres veces al día) o semanales.</span><span class="sxs-lookup"><span data-stu-id="7098e-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="7098e-236">Para obtener más información acerca de cómo toospecify Hola programar copia de seguridad, vea el artículo de hello [tooreplace utilice Azure Backup su infraestructura de cinta](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="7098e-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="7098e-237">En hello **Seleccionar directiva de retención** página, seleccione hello **directiva de retención** para copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="7098e-238">Directiva de retención de Hello especifica cuánto tiempo se almacenan los datos de copia de seguridad de saludo.</span><span class="sxs-lookup"><span data-stu-id="7098e-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="7098e-239">En vez de especificar una "directiva" para todos los puntos de copia de seguridad, puede especificar las directivas de retención diferente en función de cuando se produce la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="7098e-240">Puede modificar toomeet de directivas de retención diaria, semanal, mensual y anual de hello sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="7098e-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="7098e-241">En la página Elegir tipo de copia de seguridad inicial de hello, elija el tipo de copia de seguridad inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="7098e-242">Deje la opción de hello **automáticamente a través de la red de hello** seleccionada y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7098e-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="7098e-243">Hacer copias de seguridad automáticamente a través de red de hello, o puede realizar una copia sin conexión.</span><span class="sxs-lookup"><span data-stu-id="7098e-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="7098e-244">resto de Hola de este artículo describe proceso Hola para realizar copias de seguridad automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7098e-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="7098e-245">Si lo prefiere toodo una copia de seguridad sin conexión, revise el artículo de hello [flujo de trabajo de copia de seguridad sin conexión en copia de seguridad de Azure](backup-azure-backup-import-export.md) para obtener información adicional.</span><span class="sxs-lookup"><span data-stu-id="7098e-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="7098e-246">En la página de confirmación de hello, revise la información de hello y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="7098e-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="7098e-247">Cuando finalice el Asistente de hello, crear la programación de copia de seguridad de hello, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="7098e-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="7098e-248">tooback seguridad de archivos y carpetas para hello primera vez</span><span class="sxs-lookup"><span data-stu-id="7098e-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="7098e-249">En el agente de servicios de recuperación de hello, haga clic en **Back Up Now** toocomplete Hola inicial de la propagación a través de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Copia de seguridad de Windows Server ahora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="7098e-251">En la página de confirmación de hello, revise la configuración Hola que Hola a ahora Asistente de Back Up usará tooback máquina Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="7098e-252">Luego, haga clic en **Crear copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="7098e-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="7098e-253">Haga clic en **cerrar** Asistente de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="7098e-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="7098e-254">Si cierra al Asistente de hello antes de que finalice el proceso de copia de seguridad de hello, Asistente Hola continúa toorun en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="7098e-255">Una vez completada la copia de seguridad inicial de hello, Hola **ha completado el trabajo** estado aparece en la consola de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7098e-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR completado](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="7098e-257">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="7098e-257">Questions?</span></span>
<span data-ttu-id="7098e-258">Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="7098e-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7098e-259">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7098e-259">Next steps</span></span>
* <span data-ttu-id="7098e-260">Obtenga más información acerca de cómo [realizar copias de seguridad de máquinas Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="7098e-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="7098e-261">Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="7098e-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="7098e-262">Si necesita toorestore una copia de seguridad, use este artículo demasiado[restaurar archivos tooa Windows máquina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="7098e-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>

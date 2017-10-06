---
title: tooback de agente de copia de seguridad de Azure de aaaUse seguridad de archivos y carpetas | Documentos de Microsoft
description: "Utilice tooback de agente de copia de seguridad de Microsoft Azure Hola seguridad tooAzure de archivos y carpetas de Windows. Crear un almacén de servicios de recuperación, instalar el agente de copia de seguridad de hello, definir la directiva de copia de seguridad de Hola y ejecutar copia de seguridad inicial de hello en las carpetas y archivos de Hola."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "almacén de copia de seguridad; copia de seguridad de un equipo de Windows Server; ventanas de copia de seguridad;"
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="4fd4c-105">Copia un tooAzure de Windows Server o cliente utilizando el modelo de implementación del Administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="4fd4c-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fd4c-106">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4fd4c-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="4fd4c-107">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="4fd4c-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="4fd4c-108">Este artículo explica cómo tooback el servidor de Windows (o cliente de Windows) tooAzure de archivos y carpetas con el uso de copia de seguridad de Azure Hola modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Pasos del proceso de copia de seguridad](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="4fd4c-110">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="4fd4c-110">Before you start</span></span>
<span data-ttu-id="4fd4c-111">tooback un servidor o cliente tooAzure, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="4fd4c-112">En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="4fd4c-113">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="4fd4c-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="4fd4c-114">Un almacén de servicios de recuperación es una entidad que almacena todas las copias de seguridad de Hola y puntos de recuperación que se crea con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="4fd4c-115">almacén de servicios de recuperación de Hello también contiene Hola directiva de copia de seguridad aplicada toohello protegida archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="4fd4c-116">Cuando se crea un almacén de servicios de recuperación, también debe seleccionar opción de redundancia de almacenamiento adecuada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="4fd4c-117">toocreate un almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="4fd4c-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="4fd4c-118">Si aún no lo ha hecho, inicie sesión en toohello [Portal de Azure](https://portal.azure.com/) con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="4fd4c-119">En el menú del concentrador hello, haga clic en **más servicios** y en la lista de Hola de recursos, escriba **servicios de recuperación** y haga clic en **servicios de recuperación de los almacenes de credenciales**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="4fd4c-121">Si no hay almacenes de servicios de recuperación de la suscripción de hello, se enumeran los almacenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="4fd4c-122">En hello **servicios de recuperación de los almacenes de credenciales** menú, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="4fd4c-124">Servicios de recuperación de Hello del almacén se abre de hoja, que le pide que tooprovide una **nombre**, **suscripción**, **grupo de recursos**, y **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creación del almacén de Recovery Services, paso 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="4fd4c-126">Para **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="4fd4c-127">nombre de Hello debe toobe único para hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="4fd4c-128">Escriba un nombre que tenga entre 2 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="4fd4c-129">Debe comenzar por una letra y solo puede contener letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="4fd4c-130">Hola **suscripción** sección, usar Hola menú desplegable toochoose hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="4fd4c-131">Si usa una sola suscripción, que aparece de la suscripción y puede omitir el paso siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="4fd4c-132">Si no está seguro de qué toouse de suscripción, utilice Hola predeterminado (o sugiere) suscripción.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="4fd4c-133">Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="4fd4c-134">Hola **grupo de recursos** sección:</span><span class="sxs-lookup"><span data-stu-id="4fd4c-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="4fd4c-135">Seleccione **crear nuevo** si desea que toocreate un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="4fd4c-136">O</span><span class="sxs-lookup"><span data-stu-id="4fd4c-136">Or</span></span>
    * <span data-ttu-id="4fd4c-137">Seleccione **utilizar existente** y haga clic en hello menú desplegable toosee Hola disponible lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="4fd4c-138">Para obtener información completa sobre los grupos de recursos, vea hello [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="4fd4c-139">Haga clic en **ubicación** región geográfica de tooselect hello para el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="4fd4c-140">Esta opción determina dónde se envían los datos de copia de seguridad de región geográfica Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="4fd4c-141">En la parte inferior de Hola de hoja de almacén de servicios de recuperación de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="4fd4c-142">Puede tardar varios minutos para hello que toobe creado del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="4fd4c-143">Supervisar las notificaciones de estado de hello en el área superior derecha de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="4fd4c-144">Una vez creado el almacén, aparece en la lista de Hola de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="4fd4c-145">Si no ve el almacén pasados unos minutos, haga clic en **Refresh** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Clic en el botón Refresh (Actualizar)](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="4fd4c-147">Una vez que vea el almacén en la lista de Hola de almacenes de servicios de recuperación, son redundancia de almacenamiento de hello tooset listo.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="4fd4c-148">Establecimiento de la redundancia de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4fd4c-148">Set storage redundancy</span></span>
<span data-ttu-id="4fd4c-149">Al crear un almacén de Servicios de recuperación se determina cómo se replica el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="4fd4c-150">De hello **servicios de recuperación de los almacenes de credenciales** hoja, haga clic en nuevo almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Seleccione el nuevo almacén de Hola de lista de Hola de almacén de servicios de recuperación](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="4fd4c-152">Cuando se selecciona el almacén de hello, Hola **del almacén de servicios de recuperación** permite delimitar hoja y hoja de configuración de hello (*que tiene el nombre de Hola de almacén de hello en la parte superior de hello*) y hoja de detalles de almacén de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Configuración de almacenamiento de vista Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="4fd4c-154">En la hoja de configuración del nuevo almacén de hello, hello tooscroll de desplazamiento vertical hacia abajo toohello sección administrar y haga clic en **infraestructura de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="4fd4c-155">se abre la hoja de la infraestructura de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="4fd4c-156">En la hoja de la infraestructura de copia de seguridad de hello, haga clic en **configuración de copia de seguridad** tooopen hello **configuración de copia de seguridad** hoja.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![Establecer configuración de almacenamiento de Hola de nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="4fd4c-158">Elija la opción de replicación de almacenamiento apropiada de hello para el almacén.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![opciones de configuración de almacenamiento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="4fd4c-160">De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="4fd4c-161">Si utiliza Azure como un punto de conexión de almacenamiento principal de copia de seguridad, continúe toouse **con redundancia geográfica**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="4fd4c-162">Si no utiliza Azure como un punto de conexión de almacenamiento de copia de seguridad principal, a continuación, elija **localmente redundante**, lo que reduce los costos de almacenamiento de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="4fd4c-163">En esta página de [información general sobre la redundancia del almacenamiento](../storage/common/storage-redundancy.md) encontrará más información sobre las opciones de almacenamiento con [redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="4fd4c-164">Ahora que ha creado un almacén, preparar su tooback de infraestructura de seguridad de archivos y carpetas, se descargan e instalar a agente de servicios de recuperación de Microsoft Azure hello, descargar las credenciales de almacén y, a continuación, usar esas credenciales tooregister Hola agente almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="4fd4c-165">Configurar el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="4fd4c-165">Configure hello vault</span></span>

1. <span data-ttu-id="4fd4c-166">Hola hoja de almacén de servicios de recuperación (hello para el almacén de que acaba de crear), en la sección de introducción de hello en, haga clic en **copia de seguridad**, a continuación, en hello **Introducción a la copia de seguridad** hoja, seleccione  **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="4fd4c-168">Hola **objetivo de copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="4fd4c-169">Si se ha configurado previamente Hola del almacén de servicios de recuperación, Hola **objetivo de copia de seguridad** hojas se abre al hacer clic en **copia de seguridad** en servicios de recuperación de hello del almacén de hoja.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="4fd4c-171">De hello **donde se está ejecutando la carga de trabajo?** menú desplegable, seleccione **local**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="4fd4c-172">Elija **Local** ya que su equipo Windows o Windows Server es una máquina física que no está en Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="4fd4c-173">De hello **especifique qué desea toobackup?** menú, seleccione **archivos y carpetas**y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Configuración de archivos y carpetas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="4fd4c-175">Después de hacer clic en Aceptar, aparece una marca siguiente demasiado**objetivo de copia de seguridad**, hello y **preparar infraestructura** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![Objetivo de copia de seguridad configurado, a continuación, prepare la infraestructura](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="4fd4c-177">En hello **preparar infraestructura** hoja, haga clic en **descargar agente para Windows Server o cliente de Windows**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="4fd4c-179">Si usa Windows Server esencial, a continuación, elija a agente de hello toodownload para Windows Server esenciales.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="4fd4c-180">Un menú emergente le pide que toorun o guardar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![Cuadro de diálogo de MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="4fd4c-182">En el menú emergente de descarga de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="4fd4c-183">De forma predeterminada, Hola **MARSagentinstaller.exe** archivo se guarda la carpeta de descargas de tooyour.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="4fd4c-184">Cuando se completa el instalador de hello, verá una ventana emergente que pregunta si desea que el instalador de toorun hello, o Abrir carpeta Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="4fd4c-186">No es necesario a tooinstall agente de hello todavía.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="4fd4c-187">Puede instalar a agente de hello después de haber descargado las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="4fd4c-188">En hello **preparar infraestructura** hoja, haga clic en **descargar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![descargar las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="4fd4c-190">carpeta de descargas de tooyour de descarga de las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="4fd4c-191">Después de que las credenciales de almacén de hello termine la descarga, verá una ventana emergente que pregunta si desea tooopen o guardar las credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="4fd4c-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-192">Click **Save**.</span></span> <span data-ttu-id="4fd4c-193">Si hace clic en accidentalmente **abiertos**, permitir que el cuadro de diálogo de Hola que trata las credenciales de almacén de hello tooopen, producirá un error.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="4fd4c-194">No se puede abrir las credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="4fd4c-195">Continúe toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-195">Proceed toohello next step.</span></span> <span data-ttu-id="4fd4c-196">las credenciales de almacén de Hola están en la carpeta de descargas de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![finalizó la descarga de las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="4fd4c-198">Instalar y registrar el agente de Hola</span><span class="sxs-lookup"><span data-stu-id="4fd4c-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="4fd4c-199">Habilitar copia de seguridad a través del portal de Azure Hola todavía no está disponible.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="4fd4c-200">Utilice tooback de agente de servicios de recuperación de Microsoft Azure Hola seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="4fd4c-201">Busque y haga doble clic en hello **MARSagentinstaller.exe** desde la carpeta de descargas de hello (u otra ubicación de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="4fd4c-202">instalador de Hello proporciona una serie de mensajes cuando extrae, instala y registra el agente de servicios de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![ejecutar las credenciales del instalador del agente de Recovery Services](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="4fd4c-204">Asistente para la instalación de Microsoft Azure Recovery Services agente de hello completa.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="4fd4c-205">Asistente de hello toocomplete, debe:</span><span class="sxs-lookup"><span data-stu-id="4fd4c-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="4fd4c-206">Elegir una ubicación para la carpeta de instalación y de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="4fd4c-207">Proporcionar la proxy información al servidor si usa un toohello de tooconnect de servidor proxy internet.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="4fd4c-208">Si usa un servidor proxy autenticado, escriba los detalles de nombre y contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="4fd4c-209">Proporcione las credenciales de almacén de hello descargado</span><span class="sxs-lookup"><span data-stu-id="4fd4c-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="4fd4c-210">Guarde la frase de contraseña de cifrado de hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4fd4c-211">Si pierde u olvida la frase de contraseña de hello, Microsoft no puede ayudar a recuperar datos de copia de seguridad de saludo.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="4fd4c-212">Guarde el archivo hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-212">Save hello file in a secure location.</span></span> <span data-ttu-id="4fd4c-213">Es necesario toorestore una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="4fd4c-214">Ahora está instalado el agente de Hola y su equipo es el almacén de toohello registrados.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="4fd4c-215">Está listo tooconfigure y programar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="4fd4c-216">Requisitos de conectividad y de red</span><span class="sxs-lookup"><span data-stu-id="4fd4c-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="4fd4c-217">Si el máquina/proxy tiene limitado el acceso a internet, asegúrese de que configuración de firewall en el proxy de la máquina hello es hello tooallow configurado las siguientes direcciones URL:</span><span class="sxs-lookup"><span data-stu-id="4fd4c-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="4fd4c-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="4fd4c-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="4fd4c-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="4fd4c-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="4fd4c-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="4fd4c-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="4fd4c-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="4fd4c-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="4fd4c-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="4fd4c-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="4fd4c-223">Crear directiva de copia de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="4fd4c-223">Create hello backup policy</span></span>
<span data-ttu-id="4fd4c-224">Directiva de copia de seguridad de Hello es la programación de hello cuando se realizan puntos de recuperación y Hola período de tiempo se conservan los puntos de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="4fd4c-225">Usar la directiva copia de seguridad de hello copia de seguridad de Microsoft Azure agente toocreate Hola para archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="4fd4c-226">toocreate una programación de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="4fd4c-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="4fd4c-227">Abra el agente de copia de seguridad de Microsoft Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="4fd4c-228">Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Iniciar el agente de copia de seguridad de Azure Hola](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="4fd4c-230">En el agente de copia de seguridad hello **acciones** panel, haga clic en **programar copias de seguridad** toolaunch Hola Asistente para la programación de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="4fd4c-232">En hello **Introducción** página de hello Asistente para la programación de copia de seguridad, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="4fd4c-233">En hello **seleccionar elementos tooBackup** página, haga clic en **agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="4fd4c-234">se abre el cuadro de diálogo de Hello seleccionar elementos.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="4fd4c-235">Seleccione Hola archivos y carpetas que desee tooprotect y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="4fd4c-236">Hola **seleccionar elementos tooBackup** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="4fd4c-237">En hello **especificar una programación de copia de seguridad** página, especifique la programación de copia de seguridad de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="4fd4c-238">Puede programar copias de seguridad diarias (con una frecuencia máxima de tres veces al día) o semanales.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="4fd4c-240">Para obtener más información acerca de cómo toospecify Hola programar copia de seguridad, vea el artículo de hello [tooreplace utilice Azure Backup su infraestructura de cinta](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="4fd4c-241">En hello **Seleccionar directiva de retención** página, elija Hola Hola de las directivas de retención específico para la copia de seguridad de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="4fd4c-242">Directiva de retención de Hello especifica duración Hola se almacena la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="4fd4c-243">En vez de simplemente especificar una "directiva" para todos los puntos de copia de seguridad, puede especificar las directivas de retención diferente en función de cuando se produce la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="4fd4c-244">Puede modificar toomeet de directivas de retención diaria, semanal, mensual y anual de hello sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="4fd4c-245">En la página Elegir tipo de copia de seguridad inicial de hello, elija el tipo de copia de seguridad inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="4fd4c-246">Deje la opción de hello **automáticamente a través de la red de hello** seleccionada y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="4fd4c-247">Hacer copias de seguridad automáticamente a través de red de hello, o puede realizar una copia sin conexión.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="4fd4c-248">resto de Hola de este artículo describe proceso Hola para realizar copias de seguridad automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="4fd4c-249">Si lo prefiere toodo una copia de seguridad sin conexión, revise el artículo de hello [flujo de trabajo de copia de seguridad sin conexión en copia de seguridad de Azure](backup-azure-backup-import-export.md) para obtener información adicional.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="4fd4c-250">En la página de confirmación de hello, revise la información de hello y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="4fd4c-251">Cuando finalice el Asistente de hello, crear la programación de copia de seguridad de hello, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="4fd4c-252">Habilitación de la limitación de la red</span><span class="sxs-lookup"><span data-stu-id="4fd4c-252">Enable network throttling</span></span>
<span data-ttu-id="4fd4c-253">agente de copia de seguridad de Microsoft Azure Hola proporciona el límite de red.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="4fd4c-254">Esta limitación controla cómo se utiliza el ancho de banda de red durante la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="4fd4c-255">Este control puede ser útil si necesita tooback los datos durante las horas laborables, pero no desea hello toointerfere de proceso de copia de seguridad con otro tráfico de Internet.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="4fd4c-256">La limitación se aplica tooback seguridad y restaurar las actividades.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="4fd4c-257">La limitación de la red no está disponible en Windows Server 2008 R2 SP1, Windows Server 2008 SP2 ni en Windows 7 (con Service Packs).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="4fd4c-258">característica de limitación de red de copia de seguridad de Azure de Hello involucre a calidad de servicio (QoS) en el sistema operativo local de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="4fd4c-259">Aunque la copia de seguridad de Azure puede proteger estos sistemas operativos, versión de Hola de QoS disponibles en estas plataformas no funciona con la limitación de red de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="4fd4c-260">La limitación de la red puede usarse en todos los demás [sistemas operativos admitidos](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="4fd4c-261">**límite de red tooenable**</span><span class="sxs-lookup"><span data-stu-id="4fd4c-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="4fd4c-262">En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **cambiar las propiedades de**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Cambiar propiedades](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="4fd4c-264">En hello **limitación** ficha, seleccione hello **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Limitación de la red](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="4fd4c-266">Después de haber habilitado la limitación, especifique Hola permitido ancho de banda para transfirieron datos de copia de seguridad durante la **horas laborables** y **horas de descanso**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="4fd4c-267">los valores de ancho de banda de Hello comienzan en 512 kilobits por segundo (Kbps) y pueden crecer hasta too1, 023 megabytes por segundo (MBps).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="4fd4c-268">También puede designar el inicio de Hola y de fin para **horas laborables**, y qué días de la semana de hello son días laborables considerada.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="4fd4c-269">Las horas que se encuentran fuera de las horas laborables designadas se consideran como no laborables.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="4fd4c-270">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="4fd4c-271">tooback seguridad de archivos y carpetas para hello primera vez</span><span class="sxs-lookup"><span data-stu-id="4fd4c-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="4fd4c-272">En el agente de copia de seguridad de hello, haga clic en **Back Up Now** toocomplete Hola inicial de la propagación a través de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Realizar copia de seguridad de Windows Server ahora](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="4fd4c-274">En la página de confirmación de hello, revise la configuración Hola que Hola a ahora Asistente de Back Up usará tooback máquina Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="4fd4c-275">Luego, haga clic en **Crear copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="4fd4c-276">Haga clic en **cerrar** Asistente de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="4fd4c-277">Si lo hace antes de que finalice el proceso de copia de seguridad de hello, Asistente Hola continúa toorun en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="4fd4c-278">Una vez completada la copia de seguridad inicial de hello, Hola **ha completado el trabajo** estado aparece en la consola de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd4c-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR completado](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="4fd4c-280">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="4fd4c-280">Questions?</span></span>
<span data-ttu-id="4fd4c-281">Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fd4c-282">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4fd4c-282">Next steps</span></span>
<span data-ttu-id="4fd4c-283">Para más información sobre la copia de seguridad de máquinas virtuales u otras cargas de trabajo, consulte:</span><span class="sxs-lookup"><span data-stu-id="4fd4c-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="4fd4c-284">Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="4fd4c-285">Si necesita toorestore una copia de seguridad, use este artículo demasiado[restaurar archivos tooa Windows máquina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="4fd4c-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>

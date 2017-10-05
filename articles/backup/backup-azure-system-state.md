---
title: Copias de seguridad del estado del sistema de Windows en Azure | Microsoft Docs
description: Aprenda a hacer copias de seguridad del estado del sistema de Windows Server y/o equipos Windows en Azure.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "cómo realizar copias de seguridad; cómo realizar una copia de seguridad; copia de seguridad de archivos y carpetas"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: 6fbd96935f444d8b0c6d068ebd0d28e612f19816
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="ab2ec-104">Copias de seguridad del estado del sistema de Windows en la implementación de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ab2ec-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="ab2ec-105">En este artículo se explica cómo realizar copias de seguridad del estado del sistema de Windows Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-105">This article explains how to back up your Windows Server system state to Azure.</span></span> <span data-ttu-id="ab2ec-106">Es un tutorial diseñado para guiarle por los aspectos básicos.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-106">It's a tutorial intended to walk you through the basics.</span></span>

<span data-ttu-id="ab2ec-107">Si desea más información acerca de Copia de seguridad de Azure, lea esta [introducción](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-107">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="ab2ec-108">Si no tiene una suscripción de Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) que le permita acceder a todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ab2ec-109">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="ab2ec-109">Create a recovery services vault</span></span>
<span data-ttu-id="ab2ec-110">Para hacer una copia de seguridad de los archivos y las carpetas, tiene que crear un almacén de Servicios de recuperación en la región donde desea almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-110">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="ab2ec-111">También debe determinar cómo desea que se replique el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-111">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="ab2ec-112">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="ab2ec-112">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="ab2ec-113">Si aún no lo ha hecho, inicie sesión en el [Portal de Azure](https://portal.azure.com/) mediante su suscripción.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-113">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="ab2ec-114">En el menú central, haga clic en **Más servicios** y, en la lista de recursos, escriba **Recovery Services** y haga clic en **Almacenes de Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-114">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="ab2ec-116">Si hay almacenes de Recovery Services en la suscripción, estos aparecerán en una lista.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-116">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="ab2ec-117">En el menú **Almacenes de servicios de recuperación**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-117">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="ab2ec-119">Se abre la hoja del almacén de Recovery Services, donde se le pide que especifique los valores de **Nombre**, **Suscripción**, **Grupo de recursos** y **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-119">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creación del almacén de Recovery Services, paso 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="ab2ec-121">En **Nombre**, escriba un nombre descriptivo que identifique el almacén.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-121">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="ab2ec-122">El nombre debe ser único para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-122">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="ab2ec-123">Escriba un nombre que tenga entre 2 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="ab2ec-124">Debe comenzar por una letra y solo puede contener letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="ab2ec-125">En la sección **Suscripción**, utilice el menú desplegable para elegir la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-125">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="ab2ec-126">Si utiliza una sola suscripción, esta aparece y puede pasar al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-126">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="ab2ec-127">Si no está seguro de la suscripción que desea utilizar, use la suscripción predeterminada (o sugerida).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-127">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="ab2ec-128">Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="ab2ec-129">En la sección **Grupo de recursos**:</span><span class="sxs-lookup"><span data-stu-id="ab2ec-129">In the **Resource group** section:</span></span>

    * <span data-ttu-id="ab2ec-130">Si desea crear un nuevo grupo de recursos, seleccione **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-130">select **Create new** if you want to create a Resource group.</span></span>
    <span data-ttu-id="ab2ec-131">O</span><span class="sxs-lookup"><span data-stu-id="ab2ec-131">Or</span></span>
    * <span data-ttu-id="ab2ec-132">Seleccione **Use existing** (Usar existente) y haga clic en el menú desplegable para ver la lista de grupos de recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-132">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="ab2ec-133">Para más información sobre los grupos de recursos, consulte [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-133">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="ab2ec-134">Haga clic en **Ubicación** para seleccionar la región geográfica del almacén.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-134">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="ab2ec-135">Esta elección determina la región geográfica a la que se envían los datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-135">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="ab2ec-136">En la parte inferior de la hoja de almacén de recovery Services, haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-136">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="ab2ec-137">La creación del almacén de Recovery Services puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-137">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="ab2ec-138">Supervise las notificaciones de estado de la parte superior derecha del portal.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-138">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="ab2ec-139">Una vez creado el almacén, aparece en la lista de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-139">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="ab2ec-140">Si no ve el almacén pasados unos minutos, haga clic en **Refresh** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Clic en el botón Refresh (Actualizar)](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="ab2ec-142">Cuando vea el almacén en la lista de almacenes de Recovery Services, estará listo para configurar la redundancia de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-142">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="ab2ec-143">Establecimiento de la redundancia de almacenamiento para el almacén</span><span class="sxs-lookup"><span data-stu-id="ab2ec-143">Set storage redundancy for the vault</span></span>
<span data-ttu-id="ab2ec-144">Cuando cree un almacén de Recovery Services, asegúrese de que la configuración de la redundancia de almacenamiento sea la que quiere.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-144">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="ab2ec-145">En la hoja **Almacenes de Recovery Services**, haga clic en el almacén nuevo.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-145">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Selección del almacén nuevo en la lista de almacenes de Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="ab2ec-147">Al seleccionar el almacén, la hoja **Almacén de Recovery Services** se delimita, y la hoja de configuración (*con el nombre del almacén en la parte superior*) y la hoja de detalles del almacén se abren.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-147">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Vista de la configuración de almacenamiento del nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="ab2ec-149">En la hoja de configuración del nuevo almacén, desplácese con el control deslizante vertical hasta la sección Manage (Administrar) y haga clic en **Backup Infrastructure** (Infraestructura de copia de seguridad).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-149">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="ab2ec-150">Con ello, se abrirá esta hoja.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-150">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="ab2ec-151">En la hoja Infraestructura de copia de seguridad, haga clic en **Configuración de copia de seguridad** para abrir la hoja **Configuración de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-151">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Establecimiento de la configuración de almacenamiento del nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="ab2ec-153">Elija la opción de replicación del almacenamiento apropiada para su almacén.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-153">Choose the appropriate storage replication option for your vault.</span></span>

    ![opciones de configuración de almacenamiento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="ab2ec-155">De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="ab2ec-156">Si usa Azure como punto de conexión de almacenamiento de copia de seguridad principal, siga utilizando **Redundancia geográfica**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-156">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="ab2ec-157">Si no utiliza Azure como punto de conexión de almacenamiento de copia de seguridad principal, elija **Redundancia local** para reducir los costes de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="ab2ec-158">En esta página de [información general sobre la redundancia del almacenamiento](../storage/common/storage-redundancy.md) encontrará más información sobre las opciones de almacenamiento con [redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="ab2ec-159">Ahora que ha creado un almacén, configúrelo para realizar copias de seguridad del estado del sistema de Windows.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="ab2ec-160">Configuración del almacén</span><span class="sxs-lookup"><span data-stu-id="ab2ec-160">Configure the vault</span></span>
1. <span data-ttu-id="ab2ec-161">En la hoja del almacén de Recovery Services (el almacén que acaba de crear), en la sección de introducción, haga clic en **Copia de seguridad** y, a continuación, en la hoja **Introducción a la copia de seguridad**, seleccione **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-161">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="ab2ec-163">Se abrirá la hoja **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-163">The **Backup Goal** blade opens.</span></span>

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="ab2ec-165">En el menú desplegable **¿Dónde se ejecuta su carga de trabajo?**, seleccione **Local**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-165">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="ab2ec-166">Elija **Local** ya que su equipo Windows o Windows Server es una máquina física que no está en Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="ab2ec-167">En el menú **What do you want to backup?** (¿De qué quiere realizar una copia de seguridad?), seleccione **Estado del sistema** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-167">From the **What do you want to backup?** menu, select **System State**, and click **OK**.</span></span>

    ![Configuración de archivos y carpetas](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="ab2ec-169">Después de hacer clic en Aceptar, aparecerá una marca de verificación junto a **Objetivo de copia de seguridad**y se abrirá la hoja **Preparar infraestructura**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-169">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Objetivo de copia de seguridad configurado, a continuación, prepare la infraestructura](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="ab2ec-171">En la hoja **Preparar infraestructura**, haga clic en **Descargar agente para Windows Server o cliente de Windows**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-171">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="ab2ec-173">Si usa Windows Server Essential, elija descargar el agente de Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-173">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="ab2ec-174">Un menú emergente le preguntará si desea ejecutar o guardar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-174">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Cuadro de diálogo de MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="ab2ec-176">Haga clic en **Guardar** en el menú emergente de descarga.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-176">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="ab2ec-177">De forma predeterminada, se guarda el archivo **MARSagentinstaller.exe** en la carpeta de descargas.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-177">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="ab2ec-178">Cuando haya finalizado el instalador, verá un menú emergente que le preguntará si desea ejecutar el instalador o abrir la carpeta.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-178">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="ab2ec-180">No es necesario instalar el agente todavía.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-180">You don't need to install the agent yet.</span></span> <span data-ttu-id="ab2ec-181">Puede instalar el agente una vez descargadas las credenciales del almacén.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-181">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="ab2ec-182">En la hoja **Preparar infraestructura**, haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-182">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![descargar las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="ab2ec-184">Descargue las credenciales de almacén en la carpeta Descargas.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-184">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="ab2ec-185">Una vez que haya terminado de descargar las credenciales del almacén, aparecerá una ventana emergente en la que se le preguntará si desea abrirlas o guardarlas.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-185">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="ab2ec-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-186">Click **Save**.</span></span> <span data-ttu-id="ab2ec-187">Si, accidentalmente, hace clic en **Abrir**, deje que el cuadro de diálogo intente abrir las credenciales de almacén. Se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-187">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="ab2ec-188">No se pueden abrir las credenciales de almacén.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-188">You cannot open the vault credentials.</span></span> <span data-ttu-id="ab2ec-189">Siga con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-189">Proceed to the next step.</span></span> <span data-ttu-id="ab2ec-190">Las credenciales del almacén están en la carpeta de descargas.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-190">The vault credentials are in the Downloads folder.</span></span>   

    ![finalizó la descarga de las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="ab2ec-192">Instalación y registro del agente</span><span class="sxs-lookup"><span data-stu-id="ab2ec-192">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="ab2ec-193">La habilitación de la copia de seguridad a través de Azure Portal todavía no está disponible.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-193">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="ab2ec-194">Use el agente de Microsoft Azure Recovery Services para hacer la copia de seguridad del estado del sistema de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-194">Use the Microsoft Azure Recovery Services Agent to back up Windows Server System State.</span></span>
>

1. <span data-ttu-id="ab2ec-195">Busque y haga doble clic en **MARSagentinstaller.exe** en la carpeta de descargas (u otra ubicación guardada).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-195">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="ab2ec-196">El instalador proporciona una serie de mensajes ya que este extrae, instala y registra el agente de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-196">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![ejecutar las credenciales del instalador del agente de Recovery Services](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="ab2ec-198">Complete el asistente para la instalación del agente de Servicios de recuperación de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-198">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="ab2ec-199">Para completar al asistente, tendrá que hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab2ec-199">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="ab2ec-200">Elija una ubicación para la instalación y la carpeta de caché.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-200">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="ab2ec-201">Proporcione la información del servidor proxy si usa un servidor proxy para conectarse a Internet.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-201">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="ab2ec-202">Si usa un servidor proxy autenticado, escriba los detalles de nombre y contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="ab2ec-203">Proporcione las credenciales del almacén descargado</span><span class="sxs-lookup"><span data-stu-id="ab2ec-203">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="ab2ec-204">Guarde la frase de contraseña en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-204">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ab2ec-205">Si pierde u olvida la frase de contraseña, Microsoft no puede ayudarle a recuperar los datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-205">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="ab2ec-206">Guarde el archivo en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-206">Save the file in a secure location.</span></span> <span data-ttu-id="ab2ec-207">Es necesario restaurar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-207">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="ab2ec-208">Ahora está instalado el agente y el equipo está registrado en el almacén.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-208">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="ab2ec-209">Está listo para configurar y programar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-209">You're ready to configure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="ab2ec-210">Copia de seguridad del estado del sistema de Windows Server (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="ab2ec-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="ab2ec-211">La copia de seguridad inicial incluye tres tareas:</span><span class="sxs-lookup"><span data-stu-id="ab2ec-211">The initial backup includes three tasks:</span></span>

* <span data-ttu-id="ab2ec-212">Habilitación de la copia de seguridad del estado del sistema mediante el agente de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="ab2ec-212">Enable System State Backup using the Azure Backup agent</span></span>
* <span data-ttu-id="ab2ec-213">Programación de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="ab2ec-213">Schedule the backup</span></span>
* <span data-ttu-id="ab2ec-214">Creación de copias de seguridad de archivos y carpetas por primera vez</span><span class="sxs-lookup"><span data-stu-id="ab2ec-214">Back up files and folders for the first time</span></span>

<span data-ttu-id="ab2ec-215">Para realizar la copia de seguridad inicial use el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-enable-system-state-backup-using-the-azure-backup-agent"></a><span data-ttu-id="ab2ec-216">Para habilitar la copia de seguridad del estado del sistema mediante el agente de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="ab2ec-216">To enable System State backup using the Azure Backup agent</span></span>

1. <span data-ttu-id="ab2ec-217">En una sesión de PowerShell, ejecute el siguiente comando para detener el motor de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-217">In a PowerShell session, run the following command to stop the Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="ab2ec-218">Abra el Registro de Windows.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-218">Open the Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="ab2ec-219">Agregue la siguiente clave del Registro con el valor DWord especificado.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-219">Add the following registry key with the specified DWord Value.</span></span>

  | <span data-ttu-id="ab2ec-220">Ruta de acceso del Registro</span><span class="sxs-lookup"><span data-stu-id="ab2ec-220">Registry path</span></span> | <span data-ttu-id="ab2ec-221">Clave del Registro</span><span class="sxs-lookup"><span data-stu-id="ab2ec-221">Registry key</span></span> | <span data-ttu-id="ab2ec-222">Valor DWord</span><span class="sxs-lookup"><span data-stu-id="ab2ec-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="ab2ec-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="ab2ec-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="ab2ec-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="ab2ec-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="ab2ec-225">2</span><span class="sxs-lookup"><span data-stu-id="ab2ec-225">2</span></span> |

4. <span data-ttu-id="ab2ec-226">Reinicie el motor de Backup ejecutando el siguiente comando en un símbolo del sistema con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-226">Restart the Backup engine by executing the following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="ab2ec-227">Programación de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="ab2ec-227">To schedule the backup job</span></span>

1. <span data-ttu-id="ab2ec-228">Abra el agente de Servicios de recuperación de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-228">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="ab2ec-229">Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Iniciar el agente de los Servicios de recuperación de Azure](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="ab2ec-231">En el agente de Servicios de recuperación, haga clic en **Programar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-231">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Programación de una copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="ab2ec-233">En la página de introducción del Asistente para programar copias de seguridad, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-233">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="ab2ec-234">En la página Seleccionar elementos de los que realizar copia de seguridad, haga clic en **Agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-234">On the Select Items to Backup page, click **Add Items**.</span></span>

5. <span data-ttu-id="ab2ec-235">Seleccione **Estado del sistema** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="ab2ec-236">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-236">Click **Next**.</span></span>

7. <span data-ttu-id="ab2ec-237">La programación de retención y copia de seguridad del estado del sistema se establece automáticamente para hacer la copia de seguridad todos los domingos a las 9:00 p. m. (hora local) y el período de retención se establece en 60 días.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-237">The System State Backup and Retention schedule is automatically set to back up every Sunday at 9:00 PM local time, and the retention period is set to 60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ab2ec-238">La directiva de retención y copia de seguridad del estado del sistema se configura automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="ab2ec-239">Si la copia de seguridad también incluye archivos y carpetas, además del estado del sistema de Windows Server, especifique solamente la directiva de copia de seguridad y retención para copias de seguridad de archivos desde el asistente.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-239">If you back up Files and Folders in addition to the Windows Server System State, specify only the Backup and Retention policy for file backups from the wizard.</span></span> 
   >

8. <span data-ttu-id="ab2ec-240">En la página Confirmación, revise la información y, luego, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-240">On the Confirmation page, review the information, and then click **Finish**.</span></span>

9. <span data-ttu-id="ab2ec-241">Cuando el asistente termine de crear la programación de copia de seguridad, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-241">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-windows-server-system-state-for-the-first-time"></a><span data-ttu-id="ab2ec-242">Para hacer una copia de seguridad del estado del sistema de Windows Server por primera vez</span><span class="sxs-lookup"><span data-stu-id="ab2ec-242">To back up Windows Server System State for the first time</span></span>

1. <span data-ttu-id="ab2ec-243">Asegúrese de que no hay actualizaciones pendientes para Windows Server que requieran un reinicio.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="ab2ec-244">En el agente de Servicios de recuperación, haga clic en **Back Up Now** (Iniciar copia de seguridad) para completar la propagación inicial a través de la red.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-244">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Copia de seguridad de Windows Server ahora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="ab2ec-246">En la página Confirmación, revise la configuración que el asistente para iniciar copia de seguridad usará para crear la copia de seguridad de la máquina.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-246">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="ab2ec-247">Luego, haga clic en **Crear copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="ab2ec-248">Haga clic en **Cerrar** para cerrar el asistente.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-248">Click **Close** to close the wizard.</span></span> <span data-ttu-id="ab2ec-249">Si lo hace antes de que finalice la copia de seguridad, el asistente se sigue ejecutando en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-249">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

5. <span data-ttu-id="ab2ec-250">Si realiza la copia de seguridad de archivos y carpetas en el servidor, además del estado del sistema de Windows Server, el asistente para copias de seguridad solo se centrará en los archivos.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-250">If you back up Files and Folders on your server, in addition to the Windows Server System State, the Backup Now wizard will only back up files.</span></span> <span data-ttu-id="ab2ec-251">Para llevar a cabo una copia de seguridad del estado del sistema ad hoc, use el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ab2ec-251">To perform an ad hoc System State back up, use the following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="ab2ec-252">Una vez que finalice la copia de seguridad inicial, el estado **Trabajo completado** se refleja en la consola de Copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-252">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

  ![IR completado](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="ab2ec-254">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="ab2ec-254">Frequently asked questions</span></span>

<span data-ttu-id="ab2ec-255">Las siguientes preguntas y respuestas proporcionan información complementaria.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-255">The following questions and answers provide supplementary information.</span></span>

### <a name="what-is-the-staging-volume"></a><span data-ttu-id="ab2ec-256">¿Qué es el volumen de almacenamiento provisional?</span><span class="sxs-lookup"><span data-stu-id="ab2ec-256">What is the Staging Volume?</span></span>

<span data-ttu-id="ab2ec-257">El volumen de almacenamiento provisional representa la ubicación intermedia donde Copias de seguridad de Windows Server, disponible de forma nativa, almacena temporalmente la copia de seguridad del estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-257">The Staging Volume represents the intermediate location where the natively available, Windows Server Backup stages the System State Backup.</span></span> <span data-ttu-id="ab2ec-258">Después, el agente de Azure Backup comprime y cifra esta copia de seguridad intermedia y la envía a través del protocolo HTTPS seguro al almacén de Recovery Services configurado.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol to the configured Recovery Services Vault.</span></span> <span data-ttu-id="ab2ec-259">**Se recomienda encarecidamente establecer el volumen de almacenamiento provisional en un volumen con un SO que no sea Windows. Si observa problemas con las copias de seguridad del estado del sistema, la comprobación de la ubicación del volumen de almacenamiento provisional es el primer paso para solucionar problemas.**</span><span class="sxs-lookup"><span data-stu-id="ab2ec-259">**We strongly recommended you establish the Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking the location of your Staging Volume is the first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-the-staging-volume-path-specified-in-the-azure-backup-agent"></a><span data-ttu-id="ab2ec-260">¿Cómo se puede cambiar la ruta de acceso del volumen de almacenamiento provisional especificada en el agente de Azure Backup?</span><span class="sxs-lookup"><span data-stu-id="ab2ec-260">How can I change the Staging Volume Path specified in the Azure Backup agent?</span></span>

<span data-ttu-id="ab2ec-261">El volumen de almacenamiento provisional se encuentra en la carpeta de caché de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-261">The Staging Volume is located in the cache folder by default.</span></span> 

1. <span data-ttu-id="ab2ec-262">Para cambiar esta ubicación, utilice el siguiente comando (en un símbolo del sistema con privilegios elevados):</span><span class="sxs-lookup"><span data-stu-id="ab2ec-262">To change this location, use the following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="ab2ec-263">Después, actualice las siguientes entradas del Registro con la ruta de acceso a la nueva carpeta del volumen de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-263">Then update the following registry entries with the path to the new Staging Volume folder.</span></span>

  |<span data-ttu-id="ab2ec-264">Ruta de acceso del Registro</span><span class="sxs-lookup"><span data-stu-id="ab2ec-264">Registry path</span></span>|<span data-ttu-id="ab2ec-265">Clave del Registro</span><span class="sxs-lookup"><span data-stu-id="ab2ec-265">Registry key</span></span>|<span data-ttu-id="ab2ec-266">Valor</span><span class="sxs-lookup"><span data-stu-id="ab2ec-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="ab2ec-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="ab2ec-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="ab2ec-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="ab2ec-268">SSBStagingPath</span></span> | <span data-ttu-id="ab2ec-269">nueva ubicación del volumen de almacenamiento provisional</span><span class="sxs-lookup"><span data-stu-id="ab2ec-269">new staging volume location</span></span> |

<span data-ttu-id="ab2ec-270">La ruta de acceso del almacenamiento provisional distingue mayúsculas de minúsculas y debe escribirse exactamente igual que la existente en el servidor.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-270">The Staging Path is case sensitive and must be the exact same casing as what exists on the server.</span></span> 

3. <span data-ttu-id="ab2ec-271">Cuando cambie la ruta de acceso del volumen de almacenamiento provisional, reinicie el motor de Backup:</span><span class="sxs-lookup"><span data-stu-id="ab2ec-271">Once you change the Staging volume path, restart the Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="ab2ec-272">Para adquirir la ruta de acceso cambiada, abra el agente de Microsoft Azure Recovery Services y desencadene una copia de seguridad ad hoc del estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-272">To pick up the changed path, open the Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-the-system-state-default-retention-set-to-60-days"></a><span data-ttu-id="ab2ec-273">¿Por qué se establece la retención predeterminada del estado del sistema en 60 días?</span><span class="sxs-lookup"><span data-stu-id="ab2ec-273">Why is the System State default retention set to 60 days?</span></span>

<span data-ttu-id="ab2ec-274">La vida útil de una copia de seguridad del estado del sistema es la misma que el valor de "duración del marcador de exclusión" para el rol de Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-274">The useful life of a system state backup is the same as the "tombstone lifetime" setting for the Windows Server Active Directory role.</span></span> <span data-ttu-id="ab2ec-275">El valor predeterminado para la entrada de duración del marcador de exclusión es de 60 días.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-275">The default value for the tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="ab2ec-276">Este valor se puede establecer en el objeto de configuración del servicio de directorio (NTDS).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-276">This value can be set on the Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-the-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="ab2ec-277">¿Cómo se cambia la directiva predeterminada de copia de seguridad y retención para el estado del sistema?</span><span class="sxs-lookup"><span data-stu-id="ab2ec-277">How do I change the default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="ab2ec-278">Para cambiar la directiva predeterminada de copia de seguridad y retención para el estado del sistema:</span><span class="sxs-lookup"><span data-stu-id="ab2ec-278">To change the default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="ab2ec-279">Detenga el motor de Backup.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-279">Stop the Backup engine.</span></span> <span data-ttu-id="ab2ec-280">Ejecute el siguiente comando en un símbolo del sistema con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-280">Run the following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="ab2ec-281">Agregue o actualice las siguientes entradas de clave del Registro en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-281">Add or update the following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="ab2ec-282">Nombre en el Registro</span><span class="sxs-lookup"><span data-stu-id="ab2ec-282">Registry Name</span></span>|<span data-ttu-id="ab2ec-283">Descripción</span><span class="sxs-lookup"><span data-stu-id="ab2ec-283">Description</span></span>|<span data-ttu-id="ab2ec-284">Valor</span><span class="sxs-lookup"><span data-stu-id="ab2ec-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="ab2ec-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="ab2ec-285">SSBScheduleTime</span></span>|<span data-ttu-id="ab2ec-286">Se utiliza para configurar la hora de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-286">Used to configure the time of the backup.</span></span> <span data-ttu-id="ab2ec-287">El valor predeterminado es 9 p. m. (hora local).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-287">Default is 9PM local time.</span></span>|<span data-ttu-id="ab2ec-288">DWord: Formato HHMM (decimal), por ejemplo 2130 para 9:30 p. m. (hora local)</span><span class="sxs-lookup"><span data-stu-id="ab2ec-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="ab2ec-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="ab2ec-289">SSBScheduleDays</span></span>|<span data-ttu-id="ab2ec-290">Se utiliza para configurar los días en los que se debe realizar la copia de seguridad del estado del sistema a la hora especificada.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-290">Used to configure the days when System State Backup must be performed at the specified time.</span></span> <span data-ttu-id="ab2ec-291">Los dígitos individuales especifican los días de la semana.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-291">Individual digits specify days of the week.</span></span> <span data-ttu-id="ab2ec-292">0 representa el domingo, 1 es el lunes y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="ab2ec-293">El día predeterminado para hacer la copia de seguridad es el domingo.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="ab2ec-294">DWord: Días de la semana para ejecutar la copia de seguridad (decimal); por ejemplo, 1230 programa copias de seguridad para el lunes, martes, miércoles y domingo.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-294">DWord: days of the week to run backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="ab2ec-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="ab2ec-295">SSBRetentionDays</span></span>|<span data-ttu-id="ab2ec-296">Se utiliza para configurar los días para conservar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-296">Used to configure the days to retain backup.</span></span> <span data-ttu-id="ab2ec-297">El valor predeterminado es 60.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-297">Default value is 60.</span></span> <span data-ttu-id="ab2ec-298">El valor máximo permitido es 180.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="ab2ec-299">DWord: Días que se conserva la copia de seguridad (decimal).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-299">DWord: Days to retain backup (decimal).</span></span>|

3. <span data-ttu-id="ab2ec-300">Utilice el siguiente comando para reiniciar el motor de Backup.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-300">Use the following command to restart the backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="ab2ec-301">Abra el agente de Microsoft Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-301">Open the Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="ab2ec-302">Haga clic en **Programar copia de seguridad** y luego en **Siguiente** hasta que vea los cambios reflejados.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-302">Click **Schedule Backup** and then click **Next** until you see the changes reflected.</span></span>

6. <span data-ttu-id="ab2ec-303">Haga clic en **Finalizar** para aplicar los cambios.</span><span class="sxs-lookup"><span data-stu-id="ab2ec-303">Click **Finish** to apply the changes.</span></span>


## <a name="questions"></a><span data-ttu-id="ab2ec-304">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="ab2ec-304">Questions?</span></span>
<span data-ttu-id="ab2ec-305">Si tiene alguna pregunta o hay alguna característica que le gustaría que se incluyera, [envíenos sus comentarios](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-305">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab2ec-306">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab2ec-306">Next steps</span></span>
* <span data-ttu-id="ab2ec-307">Obtenga más información acerca de cómo [realizar copias de seguridad de máquinas Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="ab2ec-308">Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="ab2ec-309">Si necesita restaurar una copia de seguridad, use este artículo: [Restaurar archivos en una máquina de Windows Server o del Cliente de Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ab2ec-309">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>

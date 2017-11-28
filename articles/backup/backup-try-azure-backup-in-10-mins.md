---
title: Copia de seguridad de archivos y carpetas de Windows en Azure (Resource Manager) | Microsoft Docs
description: "Aprenda a realizar una copia de seguridad de los archivos y las carpetas de Windows en Azure en una implementación de Resource Manager."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "cómo realizar copias de seguridad; cómo realizar una copia de seguridad; copia de seguridad de archivos y carpetas"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: b21edb70eca3ec9552dc157ee3bb658d243b8fcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="39e34-104">Primer análisis: Copia de seguridad de archivos y carpetas en la implementación de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="39e34-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="39e34-105">En este artículo se explica cómo realizar una copia de seguridad de los archivos y las carpetas de Windows Server (o equipo Windows) en Azure mediante una implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39e34-105">This article explains how to back up your Windows Server (or Windows computer) files and folders to Azure using a Resource Manager deployment.</span></span> <span data-ttu-id="39e34-106">Es un tutorial diseñado para guiarle por los aspectos básicos.</span><span class="sxs-lookup"><span data-stu-id="39e34-106">It's a tutorial intended to walk you through the basics.</span></span> <span data-ttu-id="39e34-107">Si desea empezar a usar Copia de seguridad de Azure, está en el lugar correcto.</span><span class="sxs-lookup"><span data-stu-id="39e34-107">If you want to get started using Azure Backup, you're in the right place.</span></span>

<span data-ttu-id="39e34-108">Si desea más información acerca de Copia de seguridad de Azure, lea esta [introducción](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="39e34-108">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="39e34-109">Si no tiene una suscripción de Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) que le permita acceder a todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="39e34-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="39e34-110">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="39e34-110">Create a recovery services vault</span></span>
<span data-ttu-id="39e34-111">Para hacer una copia de seguridad de los archivos y las carpetas, tiene que crear un almacén de Servicios de recuperación en la región donde desea almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="39e34-111">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="39e34-112">También debe determinar cómo desea que se replique el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="39e34-112">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="39e34-113">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="39e34-113">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="39e34-114">Si aún no lo ha hecho, inicie sesión en el [Portal de Azure](https://portal.azure.com/) mediante su suscripción.</span><span class="sxs-lookup"><span data-stu-id="39e34-114">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="39e34-115">En el menú central, haga clic en **Más servicios** y, en la lista de recursos, escriba **Recovery Services** y haga clic en **Almacenes de Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="39e34-115">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="39e34-117">Si hay almacenes de Recovery Services en la suscripción, estos aparecerán en una lista.</span><span class="sxs-lookup"><span data-stu-id="39e34-117">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="39e34-118">En el menú **Almacenes de servicios de recuperación**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="39e34-118">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="39e34-120">Se abre la hoja del almacén de Recovery Services, donde se le pide que especifique los valores de **Nombre**, **Suscripción**, **Grupo de recursos** y **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="39e34-120">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creación del almacén de Recovery Services, paso 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="39e34-122">En **Nombre**, escriba un nombre descriptivo que identifique el almacén.</span><span class="sxs-lookup"><span data-stu-id="39e34-122">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="39e34-123">El nombre debe ser único para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="39e34-123">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="39e34-124">Escriba un nombre que tenga entre 2 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="39e34-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="39e34-125">Debe comenzar por una letra y solo puede contener letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="39e34-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="39e34-126">En la sección **Suscripción**, utilice el menú desplegable para elegir la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="39e34-126">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="39e34-127">Si utiliza una sola suscripción, esta aparece y puede pasar al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="39e34-127">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="39e34-128">Si no está seguro de la suscripción que desea utilizar, use la suscripción predeterminada (o sugerida).</span><span class="sxs-lookup"><span data-stu-id="39e34-128">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="39e34-129">Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="39e34-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="39e34-130">En la sección **Grupo de recursos**:</span><span class="sxs-lookup"><span data-stu-id="39e34-130">In the **Resource group** section:</span></span>

    * <span data-ttu-id="39e34-131">Si desea crear un nuevo grupo de recursos, seleccione **Create new** (Crear nuevo).</span><span class="sxs-lookup"><span data-stu-id="39e34-131">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="39e34-132">O</span><span class="sxs-lookup"><span data-stu-id="39e34-132">Or</span></span>
    * <span data-ttu-id="39e34-133">Seleccione **Use existing** (Usar existente) y haga clic en el menú desplegable para ver la lista de grupos de recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="39e34-133">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="39e34-134">Para más información sobre los grupos de recursos, consulte [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39e34-134">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="39e34-135">Haga clic en **Ubicación** para seleccionar la región geográfica del almacén.</span><span class="sxs-lookup"><span data-stu-id="39e34-135">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="39e34-136">Esta elección determina la región geográfica a la que se envían los datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-136">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="39e34-137">En la parte inferior de la hoja de almacén de recovery Services, haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="39e34-137">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="39e34-138">La creación del almacén de Recovery Services puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="39e34-138">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="39e34-139">Supervise las notificaciones de estado de la parte superior derecha del portal.</span><span class="sxs-lookup"><span data-stu-id="39e34-139">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="39e34-140">Una vez creado el almacén, aparece en la lista de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="39e34-140">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="39e34-141">Si no ve el almacén pasados unos minutos, haga clic en **Refresh** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="39e34-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Clic en el botón Refresh (Actualizar)](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="39e34-143">Cuando vea el almacén en la lista de almacenes de Recovery Services, estará listo para configurar la redundancia de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="39e34-143">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="39e34-144">Establecimiento de la redundancia de almacenamiento para el almacén</span><span class="sxs-lookup"><span data-stu-id="39e34-144">Set storage redundancy for the vault</span></span>
<span data-ttu-id="39e34-145">Cuando cree un almacén de Recovery Services, asegúrese de que la configuración de la redundancia de almacenamiento sea la que quiere.</span><span class="sxs-lookup"><span data-stu-id="39e34-145">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="39e34-146">En la hoja **Almacenes de Recovery Services**, haga clic en el almacén nuevo.</span><span class="sxs-lookup"><span data-stu-id="39e34-146">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Selección del almacén nuevo en la lista de almacenes de Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="39e34-148">Al seleccionar el almacén, la hoja **Almacén de Recovery Services** se delimita, y la hoja de configuración (*con el nombre del almacén en la parte superior*) y la hoja de detalles del almacén se abren.</span><span class="sxs-lookup"><span data-stu-id="39e34-148">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Vista de la configuración de almacenamiento del nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="39e34-150">En la hoja de configuración del nuevo almacén, desplácese con el control deslizante vertical hasta la sección Manage (Administrar) y haga clic en **Backup Infrastructure** (Infraestructura de copia de seguridad).</span><span class="sxs-lookup"><span data-stu-id="39e34-150">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="39e34-151">Con ello, se abrirá esta hoja.</span><span class="sxs-lookup"><span data-stu-id="39e34-151">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="39e34-152">En la hoja Infraestructura de copia de seguridad, haga clic en **Configuración de copia de seguridad** para abrir la hoja **Configuración de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="39e34-152">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Establecimiento de la configuración de almacenamiento del nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="39e34-154">Elija la opción de replicación del almacenamiento apropiada para su almacén.</span><span class="sxs-lookup"><span data-stu-id="39e34-154">Choose the appropriate storage replication option for your vault.</span></span>

    ![opciones de configuración de almacenamiento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="39e34-156">De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="39e34-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="39e34-157">Si usa Azure como punto de conexión de almacenamiento de copia de seguridad principal, siga utilizando **Redundancia geográfica**.</span><span class="sxs-lookup"><span data-stu-id="39e34-157">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="39e34-158">Si no utiliza Azure como punto de conexión de almacenamiento de copia de seguridad principal, elija **Redundancia local** para reducir los costes de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="39e34-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="39e34-159">En esta página de [información general sobre la redundancia del almacenamiento](../storage/common/storage-redundancy.md) encontrará más información sobre las opciones de almacenamiento con [redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="39e34-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="39e34-160">Ahora que ha creado un almacén, configúrelo para realizar copias de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="39e34-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="39e34-161">Configuración del almacén</span><span class="sxs-lookup"><span data-stu-id="39e34-161">Configure the vault</span></span>
1. <span data-ttu-id="39e34-162">En la hoja del almacén de Recovery Services (el almacén que acaba de crear), en la sección de introducción, haga clic en **Copia de seguridad** y, a continuación, en la hoja **Introducción a la copia de seguridad**, seleccione **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="39e34-162">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="39e34-164">Se abrirá la hoja **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="39e34-164">The **Backup Goal** blade opens.</span></span>

    ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="39e34-166">En el menú desplegable **¿Dónde se ejecuta su carga de trabajo?**, seleccione **Local**.</span><span class="sxs-lookup"><span data-stu-id="39e34-166">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="39e34-167">Elija **Local** ya que su equipo Windows o Windows Server es una máquina física que no está en Azure.</span><span class="sxs-lookup"><span data-stu-id="39e34-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="39e34-168">En el menú **What do you want to backup?** (¿De qué quiere realizar una copia de seguridad?), seleccione **Archivos y carpetas** (Archivos y carpetas) y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="39e34-168">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Configuración de archivos y carpetas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="39e34-170">Después de hacer clic en Aceptar, aparecerá una marca de verificación junto a **Objetivo de copia de seguridad**y se abrirá la hoja **Preparar infraestructura**.</span><span class="sxs-lookup"><span data-stu-id="39e34-170">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Objetivo de copia de seguridad configurado, a continuación, prepare la infraestructura](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="39e34-172">En la hoja **Preparar infraestructura**, haga clic en **Descargar agente para Windows Server o cliente de Windows**.</span><span class="sxs-lookup"><span data-stu-id="39e34-172">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="39e34-174">Si usa Windows Server Essential, elija descargar el agente de Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="39e34-174">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="39e34-175">Un menú emergente le preguntará si desea ejecutar o guardar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="39e34-175">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Cuadro de diálogo de MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="39e34-177">Haga clic en **Guardar** en el menú emergente de descarga.</span><span class="sxs-lookup"><span data-stu-id="39e34-177">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="39e34-178">De forma predeterminada, se guarda el archivo **MARSagentinstaller.exe** en la carpeta de descargas.</span><span class="sxs-lookup"><span data-stu-id="39e34-178">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="39e34-179">Cuando haya finalizado el instalador, verá un menú emergente que le preguntará si desea ejecutar el instalador o abrir la carpeta.</span><span class="sxs-lookup"><span data-stu-id="39e34-179">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="39e34-181">No es necesario instalar el agente todavía.</span><span class="sxs-lookup"><span data-stu-id="39e34-181">You don't need to install the agent yet.</span></span> <span data-ttu-id="39e34-182">Puede instalar el agente una vez descargadas las credenciales del almacén.</span><span class="sxs-lookup"><span data-stu-id="39e34-182">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="39e34-183">En la hoja **Preparar infraestructura**, haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="39e34-183">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![descargar las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="39e34-185">Descargue las credenciales de almacén en la carpeta Descargas.</span><span class="sxs-lookup"><span data-stu-id="39e34-185">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="39e34-186">Una vez que haya terminado de descargar las credenciales del almacén, aparecerá una ventana emergente en la que se le preguntará si desea abrirlas o guardarlas.</span><span class="sxs-lookup"><span data-stu-id="39e34-186">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="39e34-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="39e34-187">Click **Save**.</span></span> <span data-ttu-id="39e34-188">Si, accidentalmente, hace clic en **Abrir**, deje que el cuadro de diálogo intente abrir las credenciales de almacén. Se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="39e34-188">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="39e34-189">No se pueden abrir las credenciales de almacén.</span><span class="sxs-lookup"><span data-stu-id="39e34-189">You cannot open the vault credentials.</span></span> <span data-ttu-id="39e34-190">Siga con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="39e34-190">Proceed to the next step.</span></span> <span data-ttu-id="39e34-191">Las credenciales del almacén están en la carpeta de descargas.</span><span class="sxs-lookup"><span data-stu-id="39e34-191">The vault credentials are in the Downloads folder.</span></span>   

    ![finalizó la descarga de las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="39e34-193">Instalación y registro del agente</span><span class="sxs-lookup"><span data-stu-id="39e34-193">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="39e34-194">La habilitación de la copia de seguridad a través de Azure Portal todavía no está disponible.</span><span class="sxs-lookup"><span data-stu-id="39e34-194">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="39e34-195">Use el agente de Microsoft Azure Recovery Services para hacer la copia de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="39e34-195">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="39e34-196">Busque y haga doble clic en **MARSagentinstaller.exe** en la carpeta de descargas (u otra ubicación guardada).</span><span class="sxs-lookup"><span data-stu-id="39e34-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="39e34-197">El instalador proporciona una serie de mensajes ya que este extrae, instala y registra el agente de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="39e34-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![ejecutar las credenciales del instalador del agente de Recovery Services](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="39e34-199">Complete el asistente para la instalación del agente de Servicios de recuperación de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="39e34-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="39e34-200">Para completar al asistente, tendrá que hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="39e34-200">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="39e34-201">Elija una ubicación para la instalación y la carpeta de caché.</span><span class="sxs-lookup"><span data-stu-id="39e34-201">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="39e34-202">Proporcione la información del servidor proxy si usa un servidor proxy para conectarse a Internet.</span><span class="sxs-lookup"><span data-stu-id="39e34-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="39e34-203">Si usa un servidor proxy autenticado, escriba los detalles de nombre y contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="39e34-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="39e34-204">Proporcione las credenciales del almacén descargado</span><span class="sxs-lookup"><span data-stu-id="39e34-204">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="39e34-205">Guarde la frase de contraseña en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="39e34-205">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="39e34-206">Si pierde u olvida la frase de contraseña, Microsoft no puede ayudarle a recuperar los datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="39e34-207">Guarde el archivo en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="39e34-207">Save the file in a secure location.</span></span> <span data-ttu-id="39e34-208">Es necesario restaurar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-208">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="39e34-209">Ahora está instalado el agente y el equipo está registrado en el almacén.</span><span class="sxs-lookup"><span data-stu-id="39e34-209">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="39e34-210">Está listo para configurar y programar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-210">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="39e34-211">Requisitos de conectividad y de red</span><span class="sxs-lookup"><span data-stu-id="39e34-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="39e34-212">Si la máquina o el proxy tienen limitado el acceso a Internet, asegúrese de que su configuración de firewall esté establecida para permitir las direcciones URL siguientes:</span><span class="sxs-lookup"><span data-stu-id="39e34-212">If your machine/proxy has limited internet access, ensure that firewall settings on the mcahine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="39e34-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="39e34-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="39e34-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="39e34-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="39e34-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="39e34-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="39e34-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="39e34-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="39e34-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="39e34-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="39e34-218">Realización de copias de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="39e34-218">Back up your files and folders</span></span>
<span data-ttu-id="39e34-219">La copia de seguridad inicial incluye dos tareas clave:</span><span class="sxs-lookup"><span data-stu-id="39e34-219">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="39e34-220">Programación de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="39e34-220">Schedule the backup</span></span>
* <span data-ttu-id="39e34-221">Creación de copias de seguridad de archivos y carpetas por primera vez</span><span class="sxs-lookup"><span data-stu-id="39e34-221">Back up files and folders for the first time</span></span>

<span data-ttu-id="39e34-222">Para realizar la copia de seguridad inicial use el agente de Microsoft Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="39e34-222">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="39e34-223">Programación de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="39e34-223">To schedule the backup job</span></span>
1. <span data-ttu-id="39e34-224">Abra el agente de Servicios de recuperación de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="39e34-224">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="39e34-225">Para encontrarlo, busque **Copia de seguridad de Microsoft Azure**en la máquina.</span><span class="sxs-lookup"><span data-stu-id="39e34-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Iniciar el agente de los Servicios de recuperación de Azure](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="39e34-227">En el agente de Servicios de recuperación, haga clic en **Programar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="39e34-227">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Programación de una copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="39e34-229">En la página de introducción del Asistente para programar copias de seguridad, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="39e34-229">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="39e34-230">En la página Seleccionar elementos de los que realizar copia de seguridad, haga clic en **Agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="39e34-230">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="39e34-231">Seleccione los archivos y las carpetas de los que desea crear la copia de seguridad y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="39e34-231">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="39e34-232">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="39e34-232">Click **Next**.</span></span>
7. <span data-ttu-id="39e34-233">En la página **Especifique la programación de copia de seguridad**, indique la **programación de copia de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="39e34-233">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="39e34-234">Puede programar copias de seguridad diarias (con una frecuencia máxima de tres veces al día) o semanales.</span><span class="sxs-lookup"><span data-stu-id="39e34-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="39e34-236">Si desea más información sobre cómo especificar la programación de las copias de seguridad, consulte el artículo [Usar la copia de seguridad de Azure para cambiar su infraestructura de cintas](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="39e34-236">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="39e34-237">En la página **Seleccione la directiva de retención**, elija la **directiva de retención** para la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-237">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="39e34-238">La directiva de retención especifica cuánto tiempo se almacenan los datos de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-238">The retention policy specifies how long the backup data is stored.</span></span> <span data-ttu-id="39e34-239">En vez de especificar una directiva para todos los puntos de copia de seguridad, puede especificar directivas de retención distintas en función de cuándo se realice la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="39e34-240">Puede modificar las directivas de retención diarias, semanales, mensuales y anuales según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="39e34-240">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="39e34-241">En la página Elija el tipo de copia de seguridad inicial, elija el tipo de copia de seguridad inicial.</span><span class="sxs-lookup"><span data-stu-id="39e34-241">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="39e34-242">Deje activada la opción **Automáticamente a través de la red** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="39e34-242">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="39e34-243">Puede hacer una copia de seguridad automáticamente en la red, o puede realizar una copia sin conexión.</span><span class="sxs-lookup"><span data-stu-id="39e34-243">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="39e34-244">En el resto de este artículo, se describe el proceso para crear automáticamente una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-244">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="39e34-245">Si prefiere crear una copia de seguridad sin conexión, consulte el artículo [Flujo de trabajo de copia de seguridad sin conexión en Copia de seguridad de Azure](backup-azure-backup-import-export.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="39e34-245">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="39e34-246">En la página Confirmación, revise la información y, luego, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="39e34-246">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="39e34-247">Cuando el asistente termine de crear la programación de copia de seguridad, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="39e34-247">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="39e34-248">Creación de copias de seguridad de archivos y carpetas por primera vez</span><span class="sxs-lookup"><span data-stu-id="39e34-248">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="39e34-249">En el agente de Servicios de recuperación, haga clic en **Back Up Now** (Iniciar copia de seguridad) para completar la propagación inicial a través de la red.</span><span class="sxs-lookup"><span data-stu-id="39e34-249">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Copia de seguridad de Windows Server ahora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="39e34-251">En la página Confirmación, revise la configuración que el asistente para iniciar copia de seguridad usará para crear la copia de seguridad de la máquina.</span><span class="sxs-lookup"><span data-stu-id="39e34-251">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="39e34-252">Luego, haga clic en **Crear copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="39e34-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="39e34-253">Haga clic en **Cerrar** para cerrar el asistente.</span><span class="sxs-lookup"><span data-stu-id="39e34-253">Click **Close** to close the wizard.</span></span> <span data-ttu-id="39e34-254">Si lo hace antes de que finalice la copia de seguridad, el asistente se sigue ejecutando en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="39e34-254">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="39e34-255">Una vez que finalice la copia de seguridad inicial, el estado **Trabajo completado** se refleja en la consola de Copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="39e34-255">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR completado](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="39e34-257">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="39e34-257">Questions?</span></span>
<span data-ttu-id="39e34-258">Si tiene alguna pregunta o hay alguna característica que le gustaría que se incluyera, [envíenos sus comentarios](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="39e34-258">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39e34-259">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39e34-259">Next steps</span></span>
* <span data-ttu-id="39e34-260">Obtenga más información acerca de cómo [realizar copias de seguridad de máquinas Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="39e34-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="39e34-261">Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="39e34-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="39e34-262">Si necesita restaurar una copia de seguridad, use este artículo: [Restaurar archivos en una máquina de Windows Server o del Cliente de Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="39e34-262">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>

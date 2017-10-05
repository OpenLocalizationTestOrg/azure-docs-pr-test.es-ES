---
title: Uso del agente de Azure Backup para realizar copias de seguridad de archivos y carpetas | Microsoft Docs
description: "Use el agente de Microsoft Azure Backup para realizar copias de seguridad de archivos y carpetas de Windows en Azure. Cree un almacén de Recovery Services, instale el agente de Backup, defina la directiva de copia de seguridad y ejecute la copia de seguridad inicial de los archivos y las carpetas."
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="63416-105">Copia de seguridad desde Windows Server o un cliente de Windows en Azure mediante el modelo de implementación de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63416-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="63416-106">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="63416-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="63416-107">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="63416-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="63416-108">En este artículo se explica cómo realizar una copia de seguridad de los archivos y carpetas de Windows Server (o del cliente de Windows) en Azure con Azure Backup usando el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63416-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Pasos del proceso de copia de seguridad](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="63416-110">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="63416-110">Before you start</span></span>
<span data-ttu-id="63416-111">Si desea crear una copia de seguridad de un servidor o cliente en Azure, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="63416-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="63416-112">En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="63416-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="63416-113">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="63416-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="63416-114">Un almacén de Servicios de recuperación es una entidad que almacena todas las copias de seguridad y todos los puntos de recuperación creados con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="63416-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="63416-115">El almacén de Servicios de recuperación contiene también la directiva de copia de seguridad que se aplica a los archivos y las carpetas protegidos.</span><span class="sxs-lookup"><span data-stu-id="63416-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="63416-116">Cuando se crea un almacén de Servicios de recuperación, también se debe seleccionar la opción de redundancia de almacenamiento adecuada.</span><span class="sxs-lookup"><span data-stu-id="63416-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="63416-117">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="63416-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="63416-118">Si aún no lo ha hecho, inicie sesión en el [Portal de Azure](https://portal.azure.com/) mediante su suscripción.</span><span class="sxs-lookup"><span data-stu-id="63416-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="63416-119">En el menú central, haga clic en **Más servicios** y, en la lista de recursos, escriba **Recovery Services** y haga clic en **Almacenes de Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="63416-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="63416-121">Si hay almacenes de Recovery Services en la suscripción, estos aparecerán en una lista.</span><span class="sxs-lookup"><span data-stu-id="63416-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="63416-122">En el menú **Almacenes de servicios de recuperación**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="63416-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="63416-124">Se abre la hoja del almacén de Recovery Services, donde se le pide que especifique los valores de **Nombre**, **Suscripción**, **Grupo de recursos** y **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="63416-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Creación del almacén de Recovery Services, paso 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="63416-126">En **Nombre**, escriba un nombre descriptivo que identifique el almacén.</span><span class="sxs-lookup"><span data-stu-id="63416-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="63416-127">El nombre debe ser único para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="63416-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="63416-128">Escriba un nombre que tenga entre 2 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="63416-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="63416-129">Debe comenzar por una letra y solo puede contener letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="63416-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="63416-130">En la sección **Suscripción**, utilice el menú desplegable para elegir la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="63416-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="63416-131">Si utiliza una sola suscripción, esta aparece y puede pasar al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="63416-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="63416-132">Si no está seguro de la suscripción que desea utilizar, use la suscripción predeterminada (o sugerida).</span><span class="sxs-lookup"><span data-stu-id="63416-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="63416-133">Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="63416-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="63416-134">En la sección **Grupo de recursos**:</span><span class="sxs-lookup"><span data-stu-id="63416-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="63416-135">Si desea crear un nuevo grupo de recursos, seleccione **Create new** (Crear nuevo).</span><span class="sxs-lookup"><span data-stu-id="63416-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="63416-136">O</span><span class="sxs-lookup"><span data-stu-id="63416-136">Or</span></span>
    * <span data-ttu-id="63416-137">Seleccione **Use existing** (Usar existente) y haga clic en el menú desplegable para ver la lista de grupos de recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="63416-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="63416-138">Para más información sobre los grupos de recursos, consulte [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="63416-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="63416-139">Haga clic en **Ubicación** para seleccionar la región geográfica del almacén.</span><span class="sxs-lookup"><span data-stu-id="63416-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="63416-140">Esta elección determina la región geográfica a la que se envían los datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="63416-141">En la parte inferior de la hoja de almacén de recovery Services, haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="63416-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="63416-142">La creación del almacén de Recovery Services puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="63416-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="63416-143">Supervise las notificaciones de estado de la parte superior derecha del portal.</span><span class="sxs-lookup"><span data-stu-id="63416-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="63416-144">Una vez creado el almacén, aparece en la lista de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="63416-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="63416-145">Si no ve el almacén pasados unos minutos, haga clic en **Refresh** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="63416-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Clic en el botón Refresh (Actualizar)](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="63416-147">Cuando vea el almacén en la lista de almacenes de Recovery Services, estará listo para configurar la redundancia de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="63416-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="63416-148">Establecimiento de la redundancia de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="63416-148">Set storage redundancy</span></span>
<span data-ttu-id="63416-149">Al crear un almacén de Servicios de recuperación se determina cómo se replica el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="63416-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="63416-150">En la hoja **Almacenes de Recovery Services**, haga clic en el almacén nuevo.</span><span class="sxs-lookup"><span data-stu-id="63416-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Selección del almacén nuevo en la lista de almacenes de Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="63416-152">Al seleccionar el almacén, la hoja **Almacén de Recovery Services** se delimita, y la hoja de configuración (*con el nombre del almacén en la parte superior*) y la hoja de detalles del almacén se abren.</span><span class="sxs-lookup"><span data-stu-id="63416-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Vista de la configuración de almacenamiento del nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="63416-154">En la hoja de configuración del nuevo almacén, desplácese con el control deslizante vertical hasta la sección Manage (Administrar) y haga clic en **Backup Infrastructure** (Infraestructura de copia de seguridad).</span><span class="sxs-lookup"><span data-stu-id="63416-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="63416-155">Con ello, se abrirá esta hoja.</span><span class="sxs-lookup"><span data-stu-id="63416-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="63416-156">En la hoja Infraestructura de copia de seguridad, haga clic en **Configuración de copia de seguridad** para abrir la hoja **Configuración de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="63416-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![Establecimiento de la configuración de almacenamiento del nuevo almacén](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="63416-158">Elija la opción de replicación del almacenamiento apropiada para su almacén.</span><span class="sxs-lookup"><span data-stu-id="63416-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![opciones de configuración de almacenamiento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="63416-160">De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="63416-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="63416-161">Si usa Azure como punto de conexión de almacenamiento de copia de seguridad principal, siga utilizando **Redundancia geográfica**.</span><span class="sxs-lookup"><span data-stu-id="63416-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="63416-162">Si no utiliza Azure como punto de conexión de almacenamiento de copia de seguridad principal, elija **Redundancia local** para reducir los costes de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="63416-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="63416-163">En esta página de [información general sobre la redundancia del almacenamiento](../storage/common/storage-redundancy.md) encontrará más información sobre las opciones de almacenamiento con [redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="63416-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="63416-164">Ahora que ha creado un almacén, prepare la infraestructura para realizar una copia de seguridad de los archivos y las carpetas; para ello, descargue e instale el agente de Microsoft Azure Recovery Services, descargue las credenciales del almacén y luego use esas credenciales para registrar el agente en el almacén.</span><span class="sxs-lookup"><span data-stu-id="63416-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="63416-165">Configuración del almacén</span><span class="sxs-lookup"><span data-stu-id="63416-165">Configure the vault</span></span>

1. <span data-ttu-id="63416-166">En la hoja del almacén de Recovery Services (el almacén que acaba de crear), en la sección de introducción, haga clic en **Copia de seguridad** y, a continuación, en la hoja **Introducción a la copia de seguridad**, seleccione **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="63416-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="63416-168">Se abrirá la hoja **Objetivo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="63416-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="63416-169">Si el almacén de Recovery Services se ha configurado previamente, la hoja **Objetivo de Backup** se abre al hacer clic en **Backup** en la hoja del almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="63416-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![Abrir hoja de objetivo de copia de seguridad](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="63416-171">En el menú desplegable **¿Dónde se ejecuta su carga de trabajo?**, seleccione **Local**.</span><span class="sxs-lookup"><span data-stu-id="63416-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="63416-172">Elija **Local** ya que su equipo Windows o Windows Server es una máquina física que no está en Azure.</span><span class="sxs-lookup"><span data-stu-id="63416-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="63416-173">En el menú **What do you want to backup?** (¿De qué quiere realizar una copia de seguridad?), seleccione **Archivos y carpetas** (Archivos y carpetas) y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="63416-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Configuración de archivos y carpetas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="63416-175">Después de hacer clic en Aceptar, aparecerá una marca de verificación junto a **Objetivo de copia de seguridad**y se abrirá la hoja **Preparar infraestructura**.</span><span class="sxs-lookup"><span data-stu-id="63416-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![Objetivo de copia de seguridad configurado, a continuación, prepare la infraestructura](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="63416-177">En la hoja **Preparar infraestructura**, haga clic en **Descargar agente para Windows Server o cliente de Windows**.</span><span class="sxs-lookup"><span data-stu-id="63416-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="63416-179">Si usa Windows Server Essential, elija descargar el agente de Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="63416-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="63416-180">Un menú emergente le preguntará si desea ejecutar o guardar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="63416-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![Cuadro de diálogo de MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="63416-182">Haga clic en **Guardar** en el menú emergente de descarga.</span><span class="sxs-lookup"><span data-stu-id="63416-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="63416-183">De forma predeterminada, se guarda el archivo **MARSagentinstaller.exe** en la carpeta de descargas.</span><span class="sxs-lookup"><span data-stu-id="63416-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="63416-184">Cuando haya finalizado el instalador, verá un menú emergente que le preguntará si desea ejecutar el instalador o abrir la carpeta.</span><span class="sxs-lookup"><span data-stu-id="63416-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![Prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="63416-186">No es necesario instalar el agente todavía.</span><span class="sxs-lookup"><span data-stu-id="63416-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="63416-187">Puede instalar el agente una vez descargadas las credenciales del almacén.</span><span class="sxs-lookup"><span data-stu-id="63416-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="63416-188">En la hoja **Preparar infraestructura**, haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="63416-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![descargar las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="63416-190">Descargue las credenciales de almacén en la carpeta Descargas.</span><span class="sxs-lookup"><span data-stu-id="63416-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="63416-191">Una vez que haya terminado de descargar las credenciales del almacén, aparecerá una ventana emergente en la que se le preguntará si desea abrirlas o guardarlas.</span><span class="sxs-lookup"><span data-stu-id="63416-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="63416-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="63416-192">Click **Save**.</span></span> <span data-ttu-id="63416-193">Si, accidentalmente, hace clic en **Abrir**, deje que el cuadro de diálogo intente abrir las credenciales de almacén. Se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="63416-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="63416-194">No se pueden abrir las credenciales de almacén.</span><span class="sxs-lookup"><span data-stu-id="63416-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="63416-195">Siga con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="63416-195">Proceed to the next step.</span></span> <span data-ttu-id="63416-196">Las credenciales del almacén están en la carpeta de descargas.</span><span class="sxs-lookup"><span data-stu-id="63416-196">The vault credentials are in the Downloads folder.</span></span>   

  ![finalizó la descarga de las credenciales de almacén](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="63416-198">Instalación y registro del agente</span><span class="sxs-lookup"><span data-stu-id="63416-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="63416-199">La habilitación de la copia de seguridad a través de Azure Portal todavía no está disponible.</span><span class="sxs-lookup"><span data-stu-id="63416-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="63416-200">Use el agente de Microsoft Azure Recovery Services para hacer la copia de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="63416-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="63416-201">Busque y haga doble clic en **MARSagentinstaller.exe** en la carpeta de descargas (u otra ubicación guardada).</span><span class="sxs-lookup"><span data-stu-id="63416-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="63416-202">El instalador proporciona una serie de mensajes ya que este extrae, instala y registra el agente de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="63416-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![ejecutar las credenciales del instalador del agente de Recovery Services](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="63416-204">Complete el asistente para la instalación del agente de Servicios de recuperación de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="63416-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="63416-205">Para completar al asistente, tendrá que hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="63416-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="63416-206">Elija una ubicación para la instalación y la carpeta de caché.</span><span class="sxs-lookup"><span data-stu-id="63416-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="63416-207">Proporcione la información del servidor proxy si usa un servidor proxy para conectarse a Internet.</span><span class="sxs-lookup"><span data-stu-id="63416-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="63416-208">Si usa un servidor proxy autenticado, escriba los detalles de nombre y contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="63416-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="63416-209">Proporcione las credenciales del almacén descargado</span><span class="sxs-lookup"><span data-stu-id="63416-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="63416-210">Guarde la frase de contraseña en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="63416-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="63416-211">Si pierde u olvida la frase de contraseña, Microsoft no puede ayudarle a recuperar los datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="63416-212">Guarde el archivo en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="63416-212">Save the file in a secure location.</span></span> <span data-ttu-id="63416-213">Es necesario restaurar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="63416-214">Ahora está instalado el agente y el equipo está registrado en el almacén.</span><span class="sxs-lookup"><span data-stu-id="63416-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="63416-215">Está listo para configurar y programar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="63416-216">Requisitos de conectividad y de red</span><span class="sxs-lookup"><span data-stu-id="63416-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="63416-217">Si la máquina o proxy tienen limitado el acceso a Internet, asegúrese de que su configuración de firewall esté establecida para permitir las direcciones URL siguientes:</span><span class="sxs-lookup"><span data-stu-id="63416-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="63416-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="63416-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="63416-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="63416-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="63416-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="63416-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="63416-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="63416-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="63416-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="63416-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="63416-223">Creación de la directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="63416-223">Create the backup policy</span></span>
<span data-ttu-id="63416-224">La directiva de copia de seguridad constituye la programación del momento en que se establecen los puntos de recuperación y del período de retención de dichos puntos.</span><span class="sxs-lookup"><span data-stu-id="63416-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="63416-225">Use el agente de Microsoft Azure Backup para crear la directiva de copia de seguridad de archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="63416-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="63416-226">Para crear una programación de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="63416-226">To create a backup schedule</span></span>
1. <span data-ttu-id="63416-227">Abra el agente de Microsoft Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="63416-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="63416-228">Para encontrarlo, busque **Microsoft Azure Backup** en la máquina.</span><span class="sxs-lookup"><span data-stu-id="63416-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Lanzamiento del agente de Azure Backup](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="63416-230">En el panel **Acciones** del agente de Backup, haga clic en **Programar copia de seguridad** para iniciar el Asistente para programar copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="63416-232">En la página de **introducción** del Asistente para programar copias de seguridad, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="63416-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="63416-233">En la página **Seleccionar elementos de los que realizar copia de seguridad**, haga clic en **Agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="63416-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="63416-234">Se abre el cuadro de diálogo Seleccionar elementos.</span><span class="sxs-lookup"><span data-stu-id="63416-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="63416-235">Seleccione los archivos y carpetas que desea proteger y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="63416-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="63416-236">En la página **Seleccionar elementos de los que realizar copia de seguridad**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="63416-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="63416-237">En la página **Especifique la programación de copia de seguridad**, indique la programación de copia de seguridad y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="63416-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="63416-238">Puede programar copias de seguridad diarias (con una frecuencia máxima de tres veces al día) o semanales.</span><span class="sxs-lookup"><span data-stu-id="63416-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="63416-240">Si desea más información sobre cómo especificar la programación de las copias de seguridad, consulte el artículo [Usar Azure Backup para cambiar su infraestructura de cintas](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="63416-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="63416-241">En la página **Seleccione la directiva de retención**, elija las directivas de retención específicas para la copia de seguridad y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="63416-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="63416-242">La directiva de retención especifica el período durante el cual se almacena la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="63416-243">En vez de especificar solo una directiva para todos los puntos de copia de seguridad, puede especificar directivas de retención distintas en función de cuándo se realice la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="63416-244">Puede modificar las directivas de retención diarias, semanales, mensuales y anuales según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="63416-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="63416-245">En la página Elija el tipo de copia de seguridad inicial, elija el tipo de copia de seguridad inicial.</span><span class="sxs-lookup"><span data-stu-id="63416-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="63416-246">Deje activada la opción **Automáticamente a través de la red** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="63416-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="63416-247">Puede hacer una copia de seguridad automáticamente en la red, o puede realizar una copia sin conexión.</span><span class="sxs-lookup"><span data-stu-id="63416-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="63416-248">En el resto de este artículo, se describe el proceso para crear automáticamente una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="63416-249">Si prefiere crear una copia de seguridad sin conexión, consulte el artículo [Flujo de trabajo de copia de seguridad sin conexión en Copia de seguridad de Azure](backup-azure-backup-import-export.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="63416-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="63416-250">En la página Confirmación, revise la información y, luego, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="63416-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="63416-251">Cuando el asistente termine de crear la programación de copia de seguridad, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="63416-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="63416-252">Habilitación de la limitación de la red</span><span class="sxs-lookup"><span data-stu-id="63416-252">Enable network throttling</span></span>
<span data-ttu-id="63416-253">El agente de Microsoft Azure Backup proporciona limitación de red.</span><span class="sxs-lookup"><span data-stu-id="63416-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="63416-254">Esta limitación controla cómo se utiliza el ancho de banda de red durante la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="63416-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="63416-255">Este control puede resultar útil si necesita realizar una copia de seguridad durante las horas de trabajo, pero no quiere que el proceso interfiera con otro tráfico de Internet.</span><span class="sxs-lookup"><span data-stu-id="63416-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="63416-256">La limitación se aplica a las actividades de copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="63416-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="63416-257">La limitación de la red no está disponible en Windows Server 2008 R2 SP1, Windows Server 2008 SP2 ni en Windows 7 (con Service Packs).</span><span class="sxs-lookup"><span data-stu-id="63416-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="63416-258">La característica de limitación de la red de Azure Backup participa en la Calidad del servicio (QoS) del sistema operativo local.</span><span class="sxs-lookup"><span data-stu-id="63416-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="63416-259">Aunque Azure Backup puede proteger estos sistemas operativos, la versión de QoS disponible en estas plataformas no funciona con la limitación de la red de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="63416-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="63416-260">La limitación de la red puede usarse en todos los demás [sistemas operativos admitidos](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="63416-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="63416-261">**Para habilitar la limitación de red**</span><span class="sxs-lookup"><span data-stu-id="63416-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="63416-262">En el agente de Microsoft Azure Backup, haga clic en **Cambiar propiedades**.</span><span class="sxs-lookup"><span data-stu-id="63416-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Cambiar propiedades](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="63416-264">En la pestaña **Limitación**, active la casilla **Habilitar el límite de uso del ancho de banda de Internet para operaciones de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="63416-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Limitación de la red](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="63416-266">Una vez que se ha habilitado la limitación, especifique el ancho de banda permitido para la transferencia de datos de copia de seguridad durante la **jornada laboral** y las **horas de descanso**.</span><span class="sxs-lookup"><span data-stu-id="63416-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="63416-267">Los valores de ancho de banda comienzan en 512 kilobytes por segundo (Kbps) y pueden subir hasta 1023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="63416-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="63416-268">También puede designar el inicio y el final de la **jornada laboral**, así como qué días de la semana se consideran laborables.</span><span class="sxs-lookup"><span data-stu-id="63416-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="63416-269">Las horas que se encuentran fuera de las horas laborables designadas se consideran como no laborables.</span><span class="sxs-lookup"><span data-stu-id="63416-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="63416-270">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="63416-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="63416-271">Creación de copias de seguridad de archivos y carpetas por primera vez</span><span class="sxs-lookup"><span data-stu-id="63416-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="63416-272">En el agente de Copia de seguridad, haga clic en **Iniciar copia de seguridad** para completar la propagación inicial a través de la red.</span><span class="sxs-lookup"><span data-stu-id="63416-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Realizar copia de seguridad de Windows Server ahora](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="63416-274">En la página Confirmación, revise la configuración que el asistente para iniciar copia de seguridad usará para crear la copia de seguridad de la máquina.</span><span class="sxs-lookup"><span data-stu-id="63416-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="63416-275">Luego, haga clic en **Crear copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="63416-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="63416-276">Haga clic en **Cerrar** para cerrar el asistente.</span><span class="sxs-lookup"><span data-stu-id="63416-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="63416-277">Si lo hace antes de que finalice el proceso de copia de seguridad, el asistente se sigue ejecutando en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="63416-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="63416-278">Una vez que finalice la copia de seguridad inicial, el estado **Trabajo completado** se refleja en la consola de Copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63416-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR completado](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="63416-280">¿Tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="63416-280">Questions?</span></span>
<span data-ttu-id="63416-281">Si tiene alguna pregunta o hay alguna característica que le gustaría que se incluyera, [envíenos sus comentarios](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="63416-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63416-282">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63416-282">Next steps</span></span>
<span data-ttu-id="63416-283">Para más información sobre la copia de seguridad de máquinas virtuales u otras cargas de trabajo, consulte:</span><span class="sxs-lookup"><span data-stu-id="63416-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="63416-284">Ahora que ha realizado una copia de seguridad de los archivos y las carpetas, puede [administrar los almacenes y servidores](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="63416-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="63416-285">Si necesita restaurar una copia de seguridad, use este artículo: [Restaurar archivos en una máquina de Windows Server o del Cliente de Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="63416-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>

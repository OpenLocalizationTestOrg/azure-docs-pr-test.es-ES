---
title: "Hola a aaaRestore datos tooa Windows Server o cliente de Windows de Azure mediante el modelo de implementación clásica | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorestore desde un cliente de Windows o Windows Server."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="d3cc5-103">Restaurar archivos tooa Windows server o el equipo de cliente de Windows mediante el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="d3cc5-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3cc5-104">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="d3cc5-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="d3cc5-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d3cc5-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="d3cc5-106">Este artículo explica cómo toorecover datos desde una copia de seguridad del almacén y restauración tooa servidor o equipo.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="d3cc5-107">A partir de marzo de 2017, ya no se pueden crear almacenes de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3cc5-108">Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="d3cc5-109">Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="d3cc5-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="d3cc5-110">Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="d3cc5-111">**15 de octubre de 2017**, ya no estará almacenes de copia de seguridad de toocreate de toouse capaz de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="d3cc5-112">**A partir del 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="d3cc5-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="d3cc5-113">Los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="d3cc5-114">No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="d3cc5-115">En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="d3cc5-116">datos de toorestore, usar a Asistente para recuperar datos de hello en el agente de servicios de recuperación de Microsoft Azure (MARS) Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="d3cc5-117">Al restaurar datos, es posible realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="d3cc5-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="d3cc5-118">Restaurar datos toohello mismo equipo desde las copias de seguridad de Hola se tomaron.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="d3cc5-119">Restaurar datos tooan alternativo máquina.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="d3cc5-120">En enero de 2017 Microsoft lanzó a un agente de MARS de toohello de actualización de vista previa.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="d3cc5-121">Junto con correcciones de errores, esta actualización permite restaurar instantánea, lo que permite toomount una instantánea de punto de recuperación puede escribir como un volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="d3cc5-122">A continuación, puede explorar Hola recuperación volumen y copia archivos tooa equipo local, por tanto, de forma selectiva restaurar archivos.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="d3cc5-123">Hola [de enero de 2017 actualización de copia de seguridad de Azure](https://support.microsoft.com/en-us/help/3216528?preview) es necesario si desea toouse Restore instantáneo toorestore los datos.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="d3cc5-124">También se deben proteger los datos de copia de seguridad de hello en los almacenes en configuraciones regionales que aparecen en el artículo de soporte técnico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="d3cc5-125">Consulte hello [de enero de 2017 actualización de copia de seguridad de Azure](https://support.microsoft.com/en-us/help/3216528?preview) para la lista más reciente de Hola de configuraciones regionales que admitan la restauración de instantánea.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="d3cc5-126">La restauración instantánea **no** está actualmente disponible en todas las configuraciones regionales.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="d3cc5-127">Restauración de instantánea está disponible para su uso en los almacenes de servicios de recuperación en hello portal de Azure y almacenes de copia de seguridad en portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="d3cc5-128">Si desea toouse Restore instantáneo, descargar la actualización de hello MARS y siga los procedimientos de Hola que mencionan restaurar instantánea.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="d3cc5-129">Use Restore instantáneo toorecover datos toohello mismo equipo</span><span class="sxs-lookup"><span data-stu-id="d3cc5-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="d3cc5-130">Si ha eliminado accidentalmente un archivo y deseos toorestore se toohello al mismo equipo (de qué Hola se realiza copia de seguridad), Hola siguiendo los pasos le ayudarán a recuperar datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="d3cc5-131">Abra hello **copia de seguridad de Microsoft Azure** ajuste en.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="d3cc5-132">Si no sabe que se instaló el complemento de hello en, buscar Hola equipo o servidor para **copia de seguridad de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="d3cc5-133">aplicación de escritorio de Hello debe aparecer en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="d3cc5-134">Haga clic en **recuperar datos** Asistente de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="d3cc5-136">En hello **Introducción** panel, toorestore Hola datos toohello mismo servidor o equipo, seleccione **este servidor (`<server name>`)** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Elija este toohello de datos de servidor opción toorestore Hola mismo equipo](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="d3cc5-138">En hello **seleccionar modo de recuperación** panel, elija **archivos y carpetas individuales** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Examinar archivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="d3cc5-140">En hello **Seleccionar volumen y fecha** panel, volumen de hello select que contiene los archivos de Hola o carpetas que desee toorestore.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="d3cc5-141">En el calendario de hello, seleccione un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="d3cc5-142">Puede realizar la restauración desde cualquier momento dado de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="d3cc5-143">Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="d3cc5-144">Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Fecha y volumen](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="d3cc5-146">Una vez que haya elegido toorestore de punto de recuperación de hello, haga clic en **montar**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="d3cc5-147">Copia de seguridad de Azure monta el punto de recuperación local de Hola y lo utiliza como un volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="d3cc5-148">En hello **examinar y recuperar archivos** panel, haga clic en **examinar** tooopen el Explorador de Windows y buscar Hola archivos y carpetas que desee.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opciones de recuperación](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="d3cc5-150">En el Explorador de Windows, copia Hola archivos o carpetas desea toorestore y péguelos tooany ubicación local toohello servidor o equipo.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="d3cc5-151">Puede abrir o transmitir Hola archivos directamente desde el volumen de recuperación de Hola y comprobar Hola correcto de las versiones recuperadas.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Copie y pegue los archivos y carpetas desde la ubicación de toolocal volumen montado](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="d3cc5-153">Cuando termine de restaurar los archivos de Hola o las carpetas, en hello **examinar y recuperación** panel, haga clic en **desmontar**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="d3cc5-154">A continuación, haga clic en **Sí** tooconfirm que desea que el volumen de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Desmonte el volumen de Hola y confirmar](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="d3cc5-156">Si no hace clic en desmontar, Hola recuperación volumen permanecerá montada durante seis horas desde el momento de hello cuando donde se montó.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="d3cc5-157">No hay ninguna operación de copia de seguridad se ejecutará mientras está montado el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="d3cc5-158">Cualquier toorun de operación de copia de seguridad programada durante el tiempo de hello cuando está montado el volumen de hello, se ejecutará después de volumen de recuperación de Hola se desmonta.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="d3cc5-159">Recuperar datos toohello mismo equipo</span><span class="sxs-lookup"><span data-stu-id="d3cc5-159">Recover data toohello same machine</span></span>
<span data-ttu-id="d3cc5-160">Si ha eliminado accidentalmente un archivo y deseos toorestore se toohello al mismo equipo (de qué Hola se realiza copia de seguridad), Hola siguiendo los pasos le ayudarán a recuperar datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="d3cc5-161">Abra hello **copia de seguridad de Microsoft Azure** ajuste en.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="d3cc5-162">Haga clic en **recuperar datos** el flujo de trabajo de tooinitiate Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="d3cc5-164">Seleccione hello  **este servidor (*nombreDelEquipo*) ** Hola de toorestore opción copia de archivo en hello misma máquina.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![Misma máquina](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="d3cc5-166">Elija demasiado**examinar archivos** o **buscar archivos**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="d3cc5-167">Deje Hola predeterminado opción si tiene previsto toorestore uno o más archivos cuya ruta de acceso se conoce.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="d3cc5-168">Si no está seguro acerca de la estructura de carpetas de hello pero desea toosearch para un archivo, elegir hello **buscar archivos** opción.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="d3cc5-169">A fin de Hola de esta sección, se continuará con la opción predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![Examinar archivos](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="d3cc5-171">Seleccione el volumen de Hola desde el que desea que el archivo de hello toorestore.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="d3cc5-172">Puede realizar la restauración a un momento dado.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-172">You can restore from any point in time.</span></span> <span data-ttu-id="d3cc5-173">Las fechas que aparecen en **negrita** en control de calendario Hola indicar disponibilidad Hola de un punto de restauración.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="d3cc5-174">Una vez que se selecciona una fecha, en función de la programación de copia de seguridad (y el éxito de Hola de una operación de copia de seguridad), puede seleccionar un punto en el tiempo de hello **tiempo** de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![Fecha y volumen](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="d3cc5-176">Seleccione Hola elementos toorecover.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-176">Select hello items toorecover.</span></span> <span data-ttu-id="d3cc5-177">Puede seleccionar varias carpetas y archivos que se va toorestore.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![Seleccionar archivos](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="d3cc5-179">Especificar parámetros de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-179">Specify hello recovery parameters.</span></span>

    ![Opciones de recuperación](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="d3cc5-181">Tiene la opción de restauración toohello ubicación original (en qué Hola archivo o carpeta se sobrescribiría) o una ubicación de tooanother en hello mismo equipo.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="d3cc5-182">Si Hola de archivo o carpeta que se va a toorestore existe en la ubicación de destino de hello, puede crear copias (dos versiones de hello mismo archivo), sobrescribir los archivos de hello en la ubicación de destino de Hola u omitir recuperación de Hola de archivos de Hola que existe en el destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="d3cc5-183">Se recomienda que deje opción predeterminada Hola restaurar las ACL de hello en los archivos de Hola que se van a recuperar.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="d3cc5-184">Una vez proporcionadas estas entradas, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="d3cc5-185">Hola recuperación flujo de trabajo, que restaura una máquina de hello archivos toothis, se iniciará.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="d3cc5-186">Recuperar máquina alternativo tooan</span><span class="sxs-lookup"><span data-stu-id="d3cc5-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="d3cc5-187">Si se pierde todo el servidor, todavía puede recuperar datos desde otro equipo de copia de seguridad de Azure tooa.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="d3cc5-188">Hola pasos muestra el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="d3cc5-189">terminología de Hola que se usa en estos pasos se incluye:</span><span class="sxs-lookup"><span data-stu-id="d3cc5-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="d3cc5-190">*Máquina de origen* : tomada máquina original de Hola desde la copia de seguridad de Hola y que no está disponible actualmente.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="d3cc5-191">*El equipo de destino* : se va a recuperar datos de saludo máquina toowhich Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="d3cc5-192">*Almacén de ejemplo* : Hola Hola de toowhich de almacén de copia de seguridad *máquina de origen* y *equipo de destino* están registrados.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="d3cc5-193">No se puede restaurar copias de seguridad realizadas desde un equipo en un equipo que está ejecutando una versión anterior del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="d3cc5-194">Por ejemplo, si se realizan copias de seguridad de una máquina con Windows 7, esta puede restaurarse en un Windows 8 o una máquina con una versión superior.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="d3cc5-195">Sin embargo, al contrario de hello no cumplirse.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="d3cc5-196">Abra hello **copia de seguridad de Microsoft Azure** ajuste en hello *equipo de destino*.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="d3cc5-197">Asegúrese de que hello *equipo de destino* hello y *máquina de origen* están registrado toohello mismo almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="d3cc5-198">Haga clic en **recuperar datos** el flujo de trabajo de tooinitiate Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="d3cc5-200">Seleccione **Otro servidor**</span><span class="sxs-lookup"><span data-stu-id="d3cc5-200">Select **Another server**</span></span>

    ![Otro servidor](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="d3cc5-202">Proporcione el archivo de credenciales de almacén de hello correspondiente toohello *el almacén de ejemplo*.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="d3cc5-203">Si el archivo de credenciales de almacén de hello es válida (o expiró) descargar un nuevo archivo de credenciales de almacén de hello *almacén ejemplo* Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="d3cc5-204">Una vez que se proporciona el archivo de credenciales de almacén de hello, se muestra el almacén de copia de seguridad de hello en el archivo de credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="d3cc5-205">Seleccione hello *máquina de origen* en lista de Hola de máquinas mostradas.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lista de máquinas](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="d3cc5-207">Seleccione cualquier hello **buscar archivos** o **examinar archivos** opción.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="d3cc5-208">Para el propósito de Hola de esta sección, se utilizará hello **buscar archivos** opción.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="d3cc5-210">Seleccionar volumen hello y la fecha en la pantalla de bienvenida siguiente.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="d3cc5-211">Búsqueda de nombre de archivo/carpeta Hola desea toorestore.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-211">Search for hello folder/file name you want toorestore.</span></span>

    ![Buscar artículos](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="d3cc5-213">Seleccionar ubicación de Hola donde es necesario toobe restaurar archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-213">Select hello location where hello files need toobe restored.</span></span>

    ![Restaurar ubicación](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="d3cc5-215">Proporcione la frase de contraseña de cifrado de Hola que se proporcionó durante la *la máquina de origen* registro demasiado*el almacén de ejemplo*.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="d3cc5-217">Una vez que se proporciona la entrada de hello, haga clic en **recuperar**, qué desencadenadores Hola restauración de hello copia archivos toohello destino proporcionado.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="d3cc5-218">Use Restore instantáneo toorestore datos tooan alternativo máquina</span><span class="sxs-lookup"><span data-stu-id="d3cc5-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="d3cc5-219">Si se pierde todo el servidor, todavía puede recuperar datos desde otro equipo de copia de seguridad de Azure tooa.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="d3cc5-220">Hola pasos muestra el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="d3cc5-221">terminología de Hola que se usa en estos pasos se incluye:</span><span class="sxs-lookup"><span data-stu-id="d3cc5-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="d3cc5-222">*Máquina de origen* : tomada máquina original de Hola desde la copia de seguridad de Hola y que no está disponible actualmente.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="d3cc5-223">*El equipo de destino* : se va a recuperar datos de saludo máquina toowhich Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="d3cc5-224">*Almacén de ejemplo* : Hola Hola de toowhich de almacén de servicios de recuperación *máquina de origen* y *equipo de destino* están registrados.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="d3cc5-225">Las copias de seguridad no pueden ser restaurada tooa equipo de destino ejecuta una versión anterior del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="d3cc5-226">Por ejemplo, una copia de seguridad perteneciente a un equipo con Windows 7 se puede restaurar en un equipo con Windows 8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="d3cc5-227">Una copia de seguridad desde un equipo Windows 8 no puede ser el equipo restaurado tooa Windows 7.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="d3cc5-228">Abra hello **copia de seguridad de Microsoft Azure** ajuste en hello *equipo de destino*.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="d3cc5-229">Asegúrese de hello *equipo de destino* hello y *máquina de origen* están registrado toohello mismos servicios de recuperación del almacén.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="d3cc5-230">Haga clic en **recuperar datos** tooopen hello **Asistente para recuperar datos**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="d3cc5-232">En hello **Introducción** panel, seleccione **otro servidor**</span><span class="sxs-lookup"><span data-stu-id="d3cc5-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Otro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="d3cc5-234">Proporcione el archivo de credenciales de almacén de hello correspondiente toohello *almacén ejemplo*y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="d3cc5-235">Si el archivo de credenciales de almacén de hello es válida (o expiró), descargue un nuevo archivo de credenciales de almacén de hello *almacén ejemplo* Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="d3cc5-236">Una vez que proporcione una credencial de almacén válido, el nombre de Hola de hello que aparece de almacén de copia de seguridad correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="d3cc5-237">En hello **Seleccionar servidor de copia de seguridad** panel, seleccione hello *máquina de origen* en lista de Hola de máquinas mostradas y proporcionar la frase de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="d3cc5-238">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-238">Then click **Next**.</span></span>

    ![Lista de máquinas](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="d3cc5-240">En hello **seleccionar modo de recuperación** panel, seleccione **archivos y carpetas individuales** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="d3cc5-242">En hello **Seleccionar volumen y fecha** panel, volumen de hello select que contiene los archivos de Hola o carpetas que desee toorestore.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="d3cc5-243">En el calendario de hello, seleccione un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="d3cc5-244">Puede realizar la restauración desde cualquier momento dado de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="d3cc5-245">Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="d3cc5-246">Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Buscar artículos](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="d3cc5-248">Haga clic en **montar** toolocally montaje el punto de recuperación de Hola como un volumen de recuperación en el *equipo de destino*.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="d3cc5-249">En hello **examinar y recuperar archivos** panel, haga clic en **examinar** tooopen el Explorador de Windows y buscar Hola archivos y carpetas que desee.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="d3cc5-251">En el Explorador de Windows, copie Hola archivos o carpetas del volumen de recuperación de Hola y péguelos tooyour *equipo de destino* ubicación.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="d3cc5-252">Puede abrir o transmitir Hola archivos directamente desde el volumen de recuperación de Hola y comprobar Hola correcto de las versiones recuperadas.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="d3cc5-254">Cuando termine de restaurar los archivos de Hola o las carpetas, en hello **examinar y recuperación** panel, haga clic en **desmontar**.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="d3cc5-255">A continuación, haga clic en **Sí** tooconfirm que desea que el volumen de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="d3cc5-257">Si no hace clic en desmontar, Hola recuperación volumen permanecerá montada durante seis horas desde el momento de hello cuando donde se montó.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="d3cc5-258">No hay ninguna operación de copia de seguridad se ejecutará mientras está montado el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="d3cc5-259">Cualquier toorun de operación de copia de seguridad programada durante el tiempo de hello cuando está montado el volumen de hello, se ejecutará después de volumen de recuperación de Hola se desmonta.</span><span class="sxs-lookup"><span data-stu-id="d3cc5-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="d3cc5-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3cc5-260">Next steps</span></span>
* [<span data-ttu-id="d3cc5-261">Preguntas más frecuentes de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="d3cc5-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="d3cc5-262">Visite hello [foro de copia de seguridad de Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="d3cc5-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="d3cc5-263">Más información</span><span class="sxs-lookup"><span data-stu-id="d3cc5-263">Learn more</span></span>
* [<span data-ttu-id="d3cc5-264">Información general de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="d3cc5-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="d3cc5-265">Copia de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="d3cc5-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="d3cc5-266">Copia de seguridad de las cargas de trabajo de Microsoft</span><span class="sxs-lookup"><span data-stu-id="d3cc5-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)

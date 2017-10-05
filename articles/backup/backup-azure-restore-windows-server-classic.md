---
title: "Restauración de datos en Windows Server o un cliente de Windows desde Azure mediante el modelo de implementación clásica| Microsoft Docs"
description: Aprenda a restaurar desde Windows Server o desde el Cliente de Windows.
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
ms.openlocfilehash: 300b2b17b44e21ed446fd63d572a2461e2fc1343
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-the-classic-deployment-model"></a><span data-ttu-id="0b1aa-103">Restauración de archivos en un equipo de Windows Server o cliente de Windows mediante el modelo de implementación de clásica</span><span class="sxs-lookup"><span data-stu-id="0b1aa-103">Restore files to a Windows server or Windows client machine using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b1aa-104">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="0b1aa-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="0b1aa-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0b1aa-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="0b1aa-106">En este artículo se explica cómo recuperar datos de un almacén de Backup y restaurarlos en un servidor o equipo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-106">This article explains how to recover data from a backup vault and restore it to a server or computer.</span></span> <span data-ttu-id="0b1aa-107">A partir de marzo de 2017, no se podrán crear almacenes de Backup en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-107">Starting in March 2017, you can no longer create backup vaults in the classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b1aa-108">Ahora puede actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-108">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="0b1aa-109">Para más información, consulte el artículo [Actualización de un almacén de Backup a un almacén de Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-109">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="0b1aa-110">Microsoft anima a actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-110">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="0b1aa-111">**15 de octubre de 2017**, ya no podrá usar PowerShell para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-111">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="0b1aa-112">**A partir del 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="0b1aa-113">Los almacenes de Backup restantes se actualizarán automáticamente a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-113">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="0b1aa-114">No podrá acceder a los datos de copia de seguridad en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-114">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="0b1aa-115">En su lugar, utilice Azure Portal para tener acceso a los datos de copia de seguridad en los almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-115">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="0b1aa-116">Para restaurar datos, utilice al Asistente para recuperar datos del agente de Microsoft Azure Recovery Services (MARS).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-116">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="0b1aa-117">Al restaurar datos, es posible realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="0b1aa-118">La restauración de datos en la misma máquina desde la cual se realizaron las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-118">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="0b1aa-119">Restaurar datos en una máquina alternativa.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-119">Restore data to an alternate machine.</span></span>

<span data-ttu-id="0b1aa-120">En enero de 2017, Microsoft publicó una actualización de versión preliminar para el agente de MARS.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-120">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="0b1aa-121">Además de las correcciones de errores, esta actualización permite restaurar de forma instantánea, lo que permite montar una instantánea de punto de recuperación grabable como un volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-121">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="0b1aa-122">Después, puede explorar el volumen y copiar archivos de recuperación en un equipo local, por tanto, restaurando los archivos de forma selectiva.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-122">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="0b1aa-123">Se necesita la [actualización de enero de 2017 de Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) si desea utilizar la restauración instantánea para restaurar datos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-123">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="0b1aa-124">También se deben proteger los datos de copia de seguridad en los almacenes en configuraciones regionales que aparecen en el artículo de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-124">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="0b1aa-125">Consulte la [actualización de Azure Backup de enero de 2017](https://support.microsoft.com/en-us/help/3216528?preview) para obtener la lista más reciente de configuraciones regionales que admitan la restauración instantánea.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-125">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="0b1aa-126">La restauración instantánea **no** está actualmente disponible en todas las configuraciones regionales.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="0b1aa-127">La restauración instantánea está disponible en los almacenes de Recovery Services de Azure Portal y en los almacenes de Backup del portal clásico.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-127">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="0b1aa-128">Si desea usar la restauración instantánea, descargue la actualización de MARS y siga los procedimientos que mencionan la restauración instantánea.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-128">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="0b1aa-129">Uso de la restauración instantánea para recuperar datos en la misma máquina</span><span class="sxs-lookup"><span data-stu-id="0b1aa-129">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="0b1aa-130">Si ha eliminado accidentalmente un archivo y desea restaurarlo en la misma máquina (desde la que se realizó la copia de seguridad), los pasos siguientes le ayudarán a recuperar esos datos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-130">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="0b1aa-131">Abra el complemento **Microsoft Azure Backup** .</span><span class="sxs-lookup"><span data-stu-id="0b1aa-131">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="0b1aa-132">Si no conoce la ubicación donde se instaló el complemento, busque el equipo o servidor para **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-132">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="0b1aa-133">La aplicación de escritorio debe aparecer en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-133">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="0b1aa-134">Haga clic en **Recuperar datos** para iniciar el asistente.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-134">Click **Recover Data** to start the wizard.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="0b1aa-136">En el panel **Introducción**, para restaurar los datos en el mismo servidor o equipo, seleccione **Este servidor (`<server name>`)** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-136">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Elegir la opción Este servidor para restaurar los datos en la misma máquina](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="0b1aa-138">En el panel **Seleccionar modo de recuperación**, seleccione **Archivos y carpetas individuales** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-138">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Examinar archivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="0b1aa-140">En el panel **Seleccionar volumen y fecha**, seleccione el volumen que contiene los archivos y/o carpetas que desea restaurar.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-140">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="0b1aa-141">En el calendario, seleccione un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-141">On the calendar, select a recovery point.</span></span> <span data-ttu-id="0b1aa-142">Puede realizar la restauración desde cualquier momento dado de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="0b1aa-143">Las fechas en **negrita** indican la disponibilidad de al menos un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-143">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="0b1aa-144">Cuando selecciona una fecha, si están disponibles varios puntos de recuperación, elija el punto de recuperación específico desde el menú desplegable **Hora**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-144">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Fecha y volumen](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="0b1aa-146">Una vez que haya elegido el punto de recuperación para restaurar, haga clic en **Montar**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-146">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="0b1aa-147">Azure Backup monta el punto de recuperación local y lo usa como volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-147">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="0b1aa-148">En el panel **Examinar y recuperar archivos**, haga clic en **Examinar** para abrir el Explorador de Windows y buscar los archivos y carpetas que desea.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-148">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Opciones de recuperación](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="0b1aa-150">En el Explorador de Windows, copie los archivos y/o carpetas que desea restaurar y péguelos en cualquier ubicación local en el servidor o equipo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-150">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="0b1aa-151">Puede abrir o transmitir los archivos directamente desde el volumen de recuperación y comprobar que se recuperan las versiones correctas.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-151">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Copia y pegado de archivos y carpetas desde el volumen montado en la ubicación local](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="0b1aa-153">Cuando termine de restaurar los archivos y/o carpetas, en el panel **Examinar y recuperar archivos**, haga clic en **Desmontar**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-153">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="0b1aa-154">Haga clic en **Sí** para confirmar que desea desmontar el volumen.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-154">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Desmontaje del volumen y confirmación](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="0b1aa-156">Si no hace clic en Desmontar, el volumen de recuperación permanecerá montado durante seis horas desde el momento en el que se montó.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-156">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="0b1aa-157">No se ejecutará ninguna operación de copia de seguridad mientras el volumen esté montado.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-157">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="0b1aa-158">Cualquier operación de copia de seguridad programada para ejecutarse durante el tiempo en el que el volumen está montado, se ejecutará después de desmontar el volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-158">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-to-the-same-machine"></a><span data-ttu-id="0b1aa-159">Recuperar los datos en la misma máquina</span><span class="sxs-lookup"><span data-stu-id="0b1aa-159">Recover data to the same machine</span></span>
<span data-ttu-id="0b1aa-160">Si ha eliminado accidentalmente un archivo y desea restaurarlo en la misma máquina (desde la que se realizó la copia de seguridad), los pasos siguientes le ayudarán a recuperar esos datos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-160">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="0b1aa-161">Abra el complemento **Microsoft Azure Backup** .</span><span class="sxs-lookup"><span data-stu-id="0b1aa-161">Open the **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="0b1aa-162">Haga clic en **Recuperar datos** para iniciar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-162">Click **Recover Data** to initiate the workflow.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="0b1aa-164">Seleccione la opción **Este servidor (*nombreDeLaMáquina*)**, para restaurar en la misma máquina el archivo del que ha creado una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-164">Select the **This server (*yourmachinename*)** option to restore the backed up file on the same machine.</span></span>

    ![Misma máquina](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="0b1aa-166">Elija entre **Examinar archivos** o **Buscar archivos**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-166">Choose to **Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="0b1aa-167">Deje la opción predeterminada si va a restaurar uno o varios archivos cuya ruta de acceso se conoce.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-167">Leave the default option if you plan to restore one or more files whose path is known.</span></span> <span data-ttu-id="0b1aa-168">Si no está seguro de la estructura de carpetas pero desea buscar un archivo, escoja la opción **Buscar archivos** .</span><span class="sxs-lookup"><span data-stu-id="0b1aa-168">If you are not sure about the folder structure but would like to search for a file, pick the **Search for files** option.</span></span> <span data-ttu-id="0b1aa-169">En esta sección, se continuará con la opción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-169">For the purpose of this section, we will proceed with the default option.</span></span>

    ![Examinar archivos](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="0b1aa-171">Seleccione el volumen desde el que desea restaurar el archivo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-171">Select the volume from which you wish to restore the file.</span></span>

    <span data-ttu-id="0b1aa-172">Puede realizar la restauración a un momento dado.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-172">You can restore from any point in time.</span></span> <span data-ttu-id="0b1aa-173">Las fechas que aparecen en **negrita** en el control del calendario indican la disponibilidad de un punto de restauración.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-173">Dates which appear in **bold** in the calendar control indicate the availability of a restore point.</span></span> <span data-ttu-id="0b1aa-174">Una vez seleccionada una fecha, según su programación de copia de seguridad (y el éxito que haya tenido al realizar una operación de copia de seguridad), puede seleccionar un momento dato en el menú desplegable **Tiempo** .</span><span class="sxs-lookup"><span data-stu-id="0b1aa-174">Once a date is selected, based on your backup schedule (and the success of a backup operation), you can select a point in time from the **Time** drop down.</span></span>

    ![Fecha y volumen](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="0b1aa-176">Seleccione los elementos que desea recuperar.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-176">Select the items to recover.</span></span> <span data-ttu-id="0b1aa-177">Puede seleccionar varias carpetas y archivos para restaurar.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-177">You can multi-select folders/files you wish to restore.</span></span>

    ![Seleccionar archivos](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="0b1aa-179">Especifique los parámetros de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-179">Specify the recovery parameters.</span></span>

    ![Opciones de recuperación](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="0b1aa-181">Tiene la opción de restaurar en la ubicación original (en la que la carpeta o el archivos se sobrescribirán) o en otra ubicación en la misma máquina.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-181">You have an option of restoring to the original location (in which the file/folder would be overwritten) or to another location in the same machine.</span></span>
   * <span data-ttu-id="0b1aa-182">Si el archivo o carpeta que desea restaurar existe en la ubicación de destino, tiene la opción de crear copias (dos versiones del mismo archivo), sobrescribir los archivos en la ubicación de destino u omitir la recuperación de los archivos que existen en el destino.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-182">If the file/folder you wish to restore exists in the target location, you can create copies (two versions of the same file), overwrite the files in the target location, or skip the recovery of the files which exist in the target.</span></span>
   * <span data-ttu-id="0b1aa-183">Se recomienda que deje la opción predeterminada de la restauración de las ACL en los archivos que se está recuperando.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-183">It is highly recommended that you leave the default option of restoring the ACLs on the files which are being recovered.</span></span>
8. <span data-ttu-id="0b1aa-184">Una vez proporcionadas estas entradas, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="0b1aa-185">El flujo de trabajo de recuperación que se encarga de restaurar los archivos de la máquina, se iniciará.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-185">The recovery workflow, which restores the files to this machine, will begin.</span></span>

## <a name="recover-to-an-alternate-machine"></a><span data-ttu-id="0b1aa-186">Recuperar en una máquina alternativa</span><span class="sxs-lookup"><span data-stu-id="0b1aa-186">Recover to an alternate machine</span></span>
<span data-ttu-id="0b1aa-187">Si ha perdido todo el servidor, todavía puede recuperar los datos de Azure Backup en una máquina diferente.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-187">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="0b1aa-188">Los pasos siguientes muestran el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-188">The following steps illustrate the workflow.</span></span>  

<span data-ttu-id="0b1aa-189">La terminología usada en estos pasos incluye:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-189">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="0b1aa-190">*Máquina de origen* : es la máquina original desde la que se realizó la copia de seguridad y que no está disponible actualmente.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-190">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="0b1aa-191">*Máquina de destino* : es la máquina en la que se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-191">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="0b1aa-192">*Almacén de ejemplo*: almacén de copia de seguridad en el que se registran la *máquina de origen* y la *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-192">*Sample vault* – The Backup vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="0b1aa-193">No se pueden restaurar copias de seguridad realizadas desde una máquina en una máquina que está ejecutando una versión anterior del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of the operating system.</span></span> <span data-ttu-id="0b1aa-194">Por ejemplo, si se realizan copias de seguridad de una máquina con Windows 7, esta puede restaurarse en un Windows 8 o una máquina con una versión superior.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="0b1aa-195">Sin embargo, la acción a la inversa no está asegurada.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-195">However, the vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="0b1aa-196">Abra el complemento **Microsoft Azure Backup** en la *Máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-196">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>
2. <span data-ttu-id="0b1aa-197">Asegúrese de que tanto la *Máquina de destino* como la *Máquina de origen* están registradas en el mismo almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-197">Ensure that the *Target machine* and the *Source machine* are registered to the same backup vault.</span></span>
3. <span data-ttu-id="0b1aa-198">Haga clic en **Recuperar datos** para iniciar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-198">Click **Recover Data** to initiate the workflow.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="0b1aa-200">Seleccione **Otro servidor**</span><span class="sxs-lookup"><span data-stu-id="0b1aa-200">Select **Another server**</span></span>

    ![Otro servidor](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="0b1aa-202">Proporcione el archivo de credenciales de almacén que se corresponde con el *Almacén de ejemplo*.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-202">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="0b1aa-203">Si el archivo de credenciales de almacén no es válido (o ha expirado), descargue un nuevo archivo de credenciales de almacén desde el *almacén de ejemplo* en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-203">If the vault credential file is invalid (or expired) download a new vault credential file from the *Sample vault* in the Azure classic portal.</span></span> <span data-ttu-id="0b1aa-204">Una vez que se proporciona el archivo de almacén de credenciales, se muestra el almacén de copia de seguridad en el archivo de almacén de credenciales.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-204">Once the vault credential file is provided, the backup vault against the vault credential file is displayed.</span></span>
6. <span data-ttu-id="0b1aa-205">Seleccione la *Máquina de origen* en la lista de máquinas mostradas.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-205">Select the *Source machine* from the list of displayed machines.</span></span>

    ![Lista de máquinas](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="0b1aa-207">Seleccione la opción **Buscar archivos** o **Examinar archivos**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-207">Select either the **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="0b1aa-208">En esta sección, usaremos la opción **Buscar archivos** .</span><span class="sxs-lookup"><span data-stu-id="0b1aa-208">For the purpose of this section, we will use the **Search for files** option.</span></span>

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="0b1aa-210">Seleccione el volumen y la fecha en la pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-210">Select the volume and date in the next screen.</span></span> <span data-ttu-id="0b1aa-211">Busque el nombre de la carpeta o el archivo que desea restaurar.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-211">Search for the folder/file name you want to restore.</span></span>

    ![Buscar artículos](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="0b1aa-213">Seleccione la ubicación en la que se deben restaurar los archivos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-213">Select the location where the files need to be restored.</span></span>

    ![Restaurar ubicación](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="0b1aa-215">Proporcione la frase de contraseña de cifrado que se proporcionó durante el registro de la *Máquina de origen* en el *Almacén de ejemplo*.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-215">Provide the encryption passphrase that was provided during *Source machine’s* registration to *Sample vault*.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="0b1aa-217">Una vez especificada la entrada, haga clic en **Recuperar**, para desencadenar la restauración de los archivos con copia de seguridad en el destino proporcionado.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-217">Once the input is provided, click **Recover**, which triggers the restore of the backed up files to the destination provided.</span></span>

## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="0b1aa-218">Uso de restauración instantánea para restaurar datos en una máquina alternativa</span><span class="sxs-lookup"><span data-stu-id="0b1aa-218">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="0b1aa-219">Si ha perdido todo el servidor, todavía puede recuperar los datos de Azure Backup en una máquina diferente.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-219">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="0b1aa-220">Los pasos siguientes muestran el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-220">The following steps illustrate the workflow.</span></span>

<span data-ttu-id="0b1aa-221">La terminología usada en estos pasos incluye:</span><span class="sxs-lookup"><span data-stu-id="0b1aa-221">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="0b1aa-222">*Máquina de origen* : es la máquina original desde la que se realizó la copia de seguridad y que no está disponible actualmente.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-222">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="0b1aa-223">*Máquina de destino* : es la máquina en la que se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-223">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="0b1aa-224">*Almacén de ejemplo*: el almacén de Recovery Services en el que se registran la*máquina de origen* y la *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-224">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="0b1aa-225">Las copias de seguridad no se pueden restaurar en una máquina de destino en la que se ejecuta una versión anterior del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-225">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="0b1aa-226">Por ejemplo, una copia de seguridad perteneciente a un equipo con Windows 7 se puede restaurar en un equipo con Windows 8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="0b1aa-227">Una copia de seguridad perteneciente a un equipo con Windows 8 no se puede restaurar en un equipo con Windows 7.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-227">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="0b1aa-228">Abra el complemento **Microsoft Azure Backup** en la *Máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-228">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="0b1aa-229">Asegúrese de que tanto la *máquina de destino* como la *máquina de origen* están registradas en el mismo almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-229">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="0b1aa-230">Haga clic en **Recuperar datos** para abrir el **Asistente de recuperación de datos**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-230">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="0b1aa-232">En el panel **Introducción**, seleccione **Otro servidor**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-232">On the **Getting Started** pane, select **Another server**</span></span>

    ![Otro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="0b1aa-234">Proporcione el archivo de credenciales de almacén que se corresponde con el *Almacén de ejemplo* y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-234">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="0b1aa-235">Si el archivo de credenciales de almacén no es válido (o ha expirado), descargue un nuevo archivo de credenciales de almacén desde el *Almacén de ejemplo* en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-235">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="0b1aa-236">Cuando proporcione una credencial de almacén válida, aparecerá el nombre del almacén de copia de seguridad correspondiente.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-236">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="0b1aa-237">En el panel **Seleccionar servidor de copia de seguridad**, seleccione la *máquina de origen* en la lista de máquinas mostradas y proporcione la frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-237">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="0b1aa-238">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-238">Then click **Next**.</span></span>

    ![Lista de máquinas](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="0b1aa-240">En el panel **Seleccionar modo de recuperación**, seleccione **Archivos y carpetas individuales** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-240">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="0b1aa-242">En el panel **Seleccionar volumen y fecha**, seleccione el volumen que contiene los archivos y/o carpetas que desea restaurar.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-242">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="0b1aa-243">En el calendario, seleccione un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-243">On the calendar, select a recovery point.</span></span> <span data-ttu-id="0b1aa-244">Puede realizar la restauración desde cualquier momento dado de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="0b1aa-245">Las fechas en **negrita** indican la disponibilidad de al menos un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-245">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="0b1aa-246">Cuando selecciona una fecha, si están disponibles varios puntos de recuperación, elija el punto de recuperación específico desde el menú desplegable **Hora**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-246">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Buscar artículos](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="0b1aa-248">Haga clic en **Montar** para montar localmente el punto de recuperación como un volumen de recuperación en la *máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-248">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="0b1aa-249">En el panel **Examinar y recuperar archivos**, haga clic en **Examinar** para abrir el Explorador de Windows y buscar los archivos y carpetas que desea.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-249">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="0b1aa-251">En el Explorador de Windows, copie los archivos y/o carpetas desde el volumen de recuperación y péguelos en la ubicación *Máquina de destino*.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-251">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="0b1aa-252">Puede abrir o transmitir los archivos directamente desde el volumen de recuperación y comprobar que se recuperan las versiones correctas.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-252">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="0b1aa-254">Cuando termine de restaurar los archivos y/o carpetas, en el panel **Examinar y recuperar archivos**, haga clic en **Desmontar**.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-254">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="0b1aa-255">Haga clic en **Sí** para confirmar que desea desmontar el volumen.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-255">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="0b1aa-257">Si no hace clic en Desmontar, el volumen de recuperación permanecerá montado durante seis horas desde el momento en el que se montó.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-257">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="0b1aa-258">No se ejecutará ninguna operación de copia de seguridad mientras el volumen esté montado.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-258">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="0b1aa-259">Cualquier operación de copia de seguridad programada para ejecutarse durante el tiempo en el que el volumen está montado, se ejecutará después de desmontar el volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b1aa-259">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="0b1aa-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b1aa-260">Next steps</span></span>
* [<span data-ttu-id="0b1aa-261">Preguntas más frecuentes de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="0b1aa-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="0b1aa-262">Visite el [Foro de Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="0b1aa-262">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="0b1aa-263">Más información</span><span class="sxs-lookup"><span data-stu-id="0b1aa-263">Learn more</span></span>
* [<span data-ttu-id="0b1aa-264">Información general de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="0b1aa-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="0b1aa-265">Copia de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="0b1aa-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="0b1aa-266">Copia de seguridad de las cargas de trabajo de Microsoft</span><span class="sxs-lookup"><span data-stu-id="0b1aa-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)

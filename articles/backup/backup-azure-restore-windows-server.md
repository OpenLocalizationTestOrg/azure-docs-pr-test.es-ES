---
title: aaaRestore datos en Azure tooa Windows Server o un equipo de Windows | Documentos de Microsoft
description: "Obtenga información acerca de cómo se almacenan los datos de toorestore en tooa Azure Windows Server o un equipo de Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="21d54-103">Restaurar archivos tooa Windows server o el equipo de cliente de Windows mediante el modelo de implementación del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="21d54-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21d54-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="21d54-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="21d54-105">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="21d54-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="21d54-106">Este artículo se explica cómo toorestore datos desde un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="21d54-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="21d54-107">datos de toorestore, usar a Asistente para recuperar datos de hello en el agente de servicios de recuperación de Microsoft Azure (MARS) Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="21d54-108">Al restaurar datos, es posible realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="21d54-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="21d54-109">Restaurar datos toohello mismo equipo desde las copias de seguridad de Hola se tomaron.</span><span class="sxs-lookup"><span data-stu-id="21d54-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="21d54-110">Restaurar datos tooan alternativo máquina.</span><span class="sxs-lookup"><span data-stu-id="21d54-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="21d54-111">En enero de 2017 Microsoft lanzó a un agente de MARS de toohello de actualización de vista previa.</span><span class="sxs-lookup"><span data-stu-id="21d54-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="21d54-112">Junto con correcciones de errores, esta actualización permite restaurar instantánea, lo que permite toomount una instantánea de punto de recuperación puede escribir como un volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21d54-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="21d54-113">A continuación, puede explorar Hola recuperación volumen y copia archivos tooa equipo local, por tanto, de forma selectiva restaurar archivos.</span><span class="sxs-lookup"><span data-stu-id="21d54-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="21d54-114">Hola [de enero de 2017 actualización de copia de seguridad de Azure](https://support.microsoft.com/en-us/help/3216528?preview) es necesario si desea toouse Restore instantáneo toorestore los datos.</span><span class="sxs-lookup"><span data-stu-id="21d54-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="21d54-115">También se deben proteger los datos de copia de seguridad de hello en los almacenes en configuraciones regionales que aparecen en el artículo de soporte técnico de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="21d54-116">Consulte hello [de enero de 2017 actualización de copia de seguridad de Azure](https://support.microsoft.com/en-us/help/3216528?preview) para la lista más reciente de Hola de configuraciones regionales que admitan la restauración de instantánea.</span><span class="sxs-lookup"><span data-stu-id="21d54-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="21d54-117">La restauración instantánea **no** está actualmente disponible en todas las configuraciones regionales.</span><span class="sxs-lookup"><span data-stu-id="21d54-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="21d54-118">Restauración de instantánea está disponible para su uso en los almacenes de servicios de recuperación en hello portal de Azure y almacenes de copia de seguridad en portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="21d54-119">Si desea toouse Restore instantáneo, descargar la actualización de hello MARS y siga los procedimientos de Hola que mencionan restaurar instantánea.</span><span class="sxs-lookup"><span data-stu-id="21d54-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="21d54-120">Use Restore instantáneo toorecover datos toohello mismo equipo</span><span class="sxs-lookup"><span data-stu-id="21d54-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="21d54-121">Si ha eliminado accidentalmente un archivo y deseos toorestore se toohello al mismo equipo (de qué Hola se realiza copia de seguridad), Hola siguiendo los pasos le ayudarán a recuperar datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="21d54-122">Abra hello **copia de seguridad de Microsoft Azure** ajuste en.</span><span class="sxs-lookup"><span data-stu-id="21d54-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="21d54-123">Si no sabe que se instaló el complemento de hello en, buscar Hola equipo o servidor para **copia de seguridad de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="21d54-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="21d54-124">aplicación de escritorio de Hello debe aparecer en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="21d54-125">Haga clic en **recuperar datos** Asistente de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="21d54-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="21d54-127">En hello **Introducción** panel, toorestore Hola datos toohello mismo servidor o equipo, seleccione **este servidor (`<server name>`)** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="21d54-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Elija este toohello de datos de servidor opción toorestore Hola mismo equipo](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="21d54-129">En hello **seleccionar modo de recuperación** panel, elija **archivos y carpetas individuales** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="21d54-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Examinar archivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="21d54-131">En hello **Seleccionar volumen y fecha** panel, volumen de hello select que contiene los archivos de Hola o carpetas que desee toorestore.</span><span class="sxs-lookup"><span data-stu-id="21d54-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="21d54-132">En el calendario de hello, seleccione un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21d54-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="21d54-133">Puede realizar la restauración desde cualquier momento dado de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21d54-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="21d54-134">Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21d54-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="21d54-135">Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="21d54-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Fecha y volumen](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="21d54-137">Una vez que haya elegido toorestore de punto de recuperación de hello, haga clic en **montar**.</span><span class="sxs-lookup"><span data-stu-id="21d54-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="21d54-138">Copia de seguridad de Azure monta el punto de recuperación local de Hola y lo utiliza como un volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21d54-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="21d54-139">En hello **examinar y recuperar archivos** panel, haga clic en **examinar** tooopen el Explorador de Windows y buscar Hola archivos y carpetas que desee.</span><span class="sxs-lookup"><span data-stu-id="21d54-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opciones de recuperación](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="21d54-141">En el Explorador de Windows, copia Hola archivos o carpetas desea toorestore y péguelos tooany ubicación local toohello servidor o equipo.</span><span class="sxs-lookup"><span data-stu-id="21d54-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="21d54-142">Puede abrir o transmitir Hola archivos directamente desde el volumen de recuperación de Hola y comprobar Hola correcto de las versiones recuperadas.</span><span class="sxs-lookup"><span data-stu-id="21d54-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Copie y pegue los archivos y carpetas desde la ubicación de toolocal volumen montado](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="21d54-144">Cuando termine de restaurar los archivos de Hola o las carpetas, en hello **examinar y recuperación** panel, haga clic en **desmontar**.</span><span class="sxs-lookup"><span data-stu-id="21d54-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="21d54-145">A continuación, haga clic en **Sí** tooconfirm que desea que el volumen de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="21d54-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Desmonte el volumen de Hola y confirmar](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="21d54-147">Si no hace clic en desmontar, Hola recuperación volumen permanecerá montada durante 6 horas desde el momento de hello cuando donde se montó.</span><span class="sxs-lookup"><span data-stu-id="21d54-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="21d54-148">Sin embargo, el tiempo de montaje de hello es extendido hasta un máximo de 24 horas en el caso de una copia de archivos en curso.</span><span class="sxs-lookup"><span data-stu-id="21d54-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="21d54-149">No hay ninguna operación de copia de seguridad se ejecutará mientras está montado el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="21d54-150">Cualquier toorun de operación de copia de seguridad programada durante el tiempo de hello cuando está montado el volumen de hello, se ejecutará después de volumen de recuperación de Hola se desmonta.</span><span class="sxs-lookup"><span data-stu-id="21d54-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="21d54-151">Use Restore instantáneo toorestore datos tooan alternativo máquina</span><span class="sxs-lookup"><span data-stu-id="21d54-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="21d54-152">Si se pierde todo el servidor, todavía puede recuperar datos desde otro equipo de copia de seguridad de Azure tooa.</span><span class="sxs-lookup"><span data-stu-id="21d54-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="21d54-153">Hola pasos muestra el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="21d54-154">terminología de Hola que se usa en estos pasos se incluye:</span><span class="sxs-lookup"><span data-stu-id="21d54-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="21d54-155">*Máquina de origen* : tomada máquina original de Hola desde la copia de seguridad de Hola y que no está disponible actualmente.</span><span class="sxs-lookup"><span data-stu-id="21d54-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="21d54-156">*El equipo de destino* : se va a recuperar datos de saludo máquina toowhich Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="21d54-157">*Almacén de ejemplo* : Hola Hola de toowhich de almacén de servicios de recuperación *máquina de origen* y *equipo de destino* están registrados.</span><span class="sxs-lookup"><span data-stu-id="21d54-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="21d54-158">Las copias de seguridad no pueden ser restaurada tooa equipo de destino ejecuta una versión anterior del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="21d54-159">Por ejemplo, una copia de seguridad perteneciente a un equipo con Windows 7 se puede restaurar en un equipo con Windows 8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="21d54-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="21d54-160">Una copia de seguridad desde un equipo Windows 8 no puede ser el equipo restaurado tooa Windows 7.</span><span class="sxs-lookup"><span data-stu-id="21d54-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="21d54-161">Abra hello **copia de seguridad de Microsoft Azure** ajuste en hello *equipo de destino*.</span><span class="sxs-lookup"><span data-stu-id="21d54-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="21d54-162">Asegúrese de hello *equipo de destino* hello y *máquina de origen* están registrado toohello mismos servicios de recuperación del almacén.</span><span class="sxs-lookup"><span data-stu-id="21d54-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="21d54-163">Haga clic en **recuperar datos** tooopen hello **Asistente para recuperar datos**.</span><span class="sxs-lookup"><span data-stu-id="21d54-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="21d54-165">En hello **Introducción** panel, seleccione **otro servidor**</span><span class="sxs-lookup"><span data-stu-id="21d54-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Otro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="21d54-167">Proporcione el archivo de credenciales de almacén de hello correspondiente toohello *almacén ejemplo*y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="21d54-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="21d54-168">Si el archivo de credenciales de almacén de hello es válida (o expiró), descargue un nuevo archivo de credenciales de almacén de hello *almacén ejemplo* Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="21d54-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="21d54-169">Una vez que proporcione una credencial de almacén válido, el nombre de Hola de hello que aparece de almacén de copia de seguridad correspondiente.</span><span class="sxs-lookup"><span data-stu-id="21d54-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="21d54-170">En hello **Seleccionar servidor de copia de seguridad** panel, seleccione hello *máquina de origen* en lista de Hola de máquinas mostradas y proporcionar la frase de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="21d54-171">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="21d54-171">Then click **Next**.</span></span>

    ![Lista de máquinas](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="21d54-173">En hello **seleccionar modo de recuperación** panel, seleccione **archivos y carpetas individuales** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="21d54-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="21d54-175">En hello **Seleccionar volumen y fecha** panel, volumen de hello select que contiene los archivos de Hola o carpetas que desee toorestore.</span><span class="sxs-lookup"><span data-stu-id="21d54-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="21d54-176">En el calendario de hello, seleccione un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21d54-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="21d54-177">Puede realizar la restauración desde cualquier momento dado de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21d54-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="21d54-178">Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="21d54-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="21d54-179">Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="21d54-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Buscar artículos](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="21d54-181">Haga clic en **montar** toolocally montaje el punto de recuperación de Hola como un volumen de recuperación en el *equipo de destino*.</span><span class="sxs-lookup"><span data-stu-id="21d54-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="21d54-182">En hello **examinar y recuperar archivos** panel, haga clic en **examinar** tooopen el Explorador de Windows y buscar Hola archivos y carpetas que desee.</span><span class="sxs-lookup"><span data-stu-id="21d54-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="21d54-184">En el Explorador de Windows, copie Hola archivos o carpetas del volumen de recuperación de Hola y péguelos tooyour *equipo de destino* ubicación.</span><span class="sxs-lookup"><span data-stu-id="21d54-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="21d54-185">Puede abrir o transmitir Hola archivos directamente desde el volumen de recuperación de Hola y comprobar Hola correcto de las versiones recuperadas.</span><span class="sxs-lookup"><span data-stu-id="21d54-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="21d54-187">Cuando termine de restaurar los archivos de Hola o las carpetas, en hello **examinar y recuperación** panel, haga clic en **desmontar**.</span><span class="sxs-lookup"><span data-stu-id="21d54-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="21d54-188">A continuación, haga clic en **Sí** tooconfirm que desea que el volumen de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="21d54-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Cifrado](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="21d54-190">Si no hace clic en desmontar, Hola recuperación volumen permanecerá montada durante 6 horas desde el momento de hello cuando donde se montó.</span><span class="sxs-lookup"><span data-stu-id="21d54-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="21d54-191">Sin embargo, el tiempo de montaje de hello es extendido hasta un máximo de 24 horas en el caso de una copia de archivos en curso.</span><span class="sxs-lookup"><span data-stu-id="21d54-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="21d54-192">No hay ninguna operación de copia de seguridad se ejecutará mientras está montado el volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="21d54-193">Cualquier toorun de operación de copia de seguridad programada durante el tiempo de hello cuando está montado el volumen de hello, se ejecutará después de volumen de recuperación de Hola se desmonta.</span><span class="sxs-lookup"><span data-stu-id="21d54-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="21d54-194">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="21d54-194">Troubleshooting</span></span>
<span data-ttu-id="21d54-195">Si copia de seguridad de Azure no correctamente montar volúmenes de recuperación de hello incluso después de hacer clic en varios minutos **montar** o se produce un error toomount Hola recuperación volumen con uno o varios errores, siga los pasos de hello debajo toobegin recuperación normalmente.</span><span class="sxs-lookup"><span data-stu-id="21d54-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="21d54-196">Cancelar el proceso de montaje en curso de hello en caso de que se ha estado ejecutando durante varios minutos.</span><span class="sxs-lookup"><span data-stu-id="21d54-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="21d54-197">Asegúrese de que se encuentra en la versión más reciente de Hola de agente de copia de seguridad de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="21d54-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="21d54-198">toofind información de versión de Hola de agente de copia de seguridad de Azure, haga clic en **sobre Microsoft Azure Backup Agent** en hello **acciones** panel de copia de seguridad de Microsoft Azure de la consola y asegúrese de que hello  **Versión** número es igual tooor superior de la versión de Hola mencionada en [este artículo](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="21d54-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="21d54-199">Puede descargar la versión más reciente de Hola desde [aquí](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="21d54-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="21d54-200">Vaya demasiado**el Administrador de dispositivos** -> **controladores de almacenamiento** y asegurarse de que puede encontrar **iniciador iSCSI de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="21d54-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="21d54-201">Si puede encontrarlo, vaya directamente toostep 7 siguiente.</span><span class="sxs-lookup"><span data-stu-id="21d54-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="21d54-202">Si no encuentra el servicio de iniciador iSCSI de Microsoft como se mencionó en el paso 3, compruebe toosee si puede encontrar una entrada en **el Administrador de dispositivos** -> **controladores de almacenamiento** llama  **Los dispositivos desconocidos** con el Id. de Hardware **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="21d54-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="21d54-203">Haga clic con el botón derecho en **Dispositivo desconocido** y seleccione **Actualizar software de controlador**.</span><span class="sxs-lookup"><span data-stu-id="21d54-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="21d54-204">Actualizar el controlador de hello seleccionando la opción de hello demasiado **buscar software de controlador actualizado automáticamente**.</span><span class="sxs-lookup"><span data-stu-id="21d54-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="21d54-205">Debe cambiar la finalización de la actualización de hello **dispositivo desconocido** demasiado**iniciador iSCSI de Microsoft** tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="21d54-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Cifrado](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="21d54-207">Vaya demasiado**el Administrador de tareas** -> **servicios (Local)** -> **servicio del iniciador iSCSI de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="21d54-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Cifrado](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="21d54-209">Reinicie el servicio de iniciador iSCSI de Microsoft de hello con el botón secundario en servicio de hello, haga clic en **detener** y haga clic en nuevo y haga clic en obtener más **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="21d54-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="21d54-210">Vuelva a intentar la recuperación mediante la restauración instantánea.</span><span class="sxs-lookup"><span data-stu-id="21d54-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="21d54-211">Si sigue sin funcionar recuperación hello, reinicie al cliente y el servidor.</span><span class="sxs-lookup"><span data-stu-id="21d54-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="21d54-212">Si no es deseable un reinicio o recuperación Hola sigue sin funcionar incluso después de reiniciar el servidor de hello, intente recuperar desde un equipo alternativo y póngase en contacto con soporte técnico de Azure, vaya demasiado[Portal de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) y enviar una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="21d54-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21d54-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="21d54-213">Next steps</span></span>
* <span data-ttu-id="21d54-214">Ahora que ha recuperado los archivos y las carpetas, puede [administrar las copias de seguridad](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="21d54-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>

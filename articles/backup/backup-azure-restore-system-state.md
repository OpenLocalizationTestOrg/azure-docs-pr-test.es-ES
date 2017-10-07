---
title: "Copia de seguridad de Azure: Tooa de estado del sistema de restauración Windows Server | Documentos de Microsoft"
description: "Explicación detallada para restaurar el estado de sistema de Windows Server a partir de una copia de seguridad en Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="bfdd9-103">Estado del sistema de restauración tooWindows Server</span><span class="sxs-lookup"><span data-stu-id="bfdd9-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="bfdd9-104">Este artículo explica cómo del almacén de copias de seguridad de estado del sistema de Windows Server de toorestore desde los servicios de recuperación de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="bfdd9-105">toorestore estado del sistema, debe tener una copia de seguridad de estado del sistema (creadas utilizando las instrucciones de hello en [estado del sistema de copia de seguridad](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) y asegúrese de que ha instalado hello [versión más reciente del programa Hola a Microsoft Azure Recovery El agente de servicios (MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="bfdd9-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="bfdd9-106">La recuperación de datos del estado de sistema de Windows Server a partir de un almacén de Azure Recovery Services es un proceso que consta de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="bfdd9-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="bfdd9-107">Restaurar el estado del sistema como archivos a partir de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="bfdd9-108">Al restaurar el estado del sistema como archivos a partir de Azure Backup, puede:</span><span class="sxs-lookup"><span data-stu-id="bfdd9-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="bfdd9-109">Estado del sistema de restauración toohello mismo servidor donde se han realizado copias de seguridad de hello, o</span><span class="sxs-lookup"><span data-stu-id="bfdd9-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="bfdd9-110">Servidor alternativo de estado del sistema de restauración archivo tooan.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="bfdd9-111">Aplicar tooa de archivos de hello Restaurar estado del sistema Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="bfdd9-112">Recuperar el estado del sistema de archivos toohello mismo servidor</span><span class="sxs-lookup"><span data-stu-id="bfdd9-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="bfdd9-113">Hola pasos explica cómo hacer copia de su estado anterior de Windows Server configuration tooa tooroll.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="bfdd9-114">Poner al servidor de configuración tooa espera, estable estado conocido, puede ser muy importante.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="bfdd9-115">Hola después de estado del sistema del servidor de pasos restauración Hola desde un almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="bfdd9-116">Abra hello **copia de seguridad de Microsoft Azure** complemento.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="bfdd9-117">Si no sabe donde se instaló el complemento hello, buscar Hola equipo o servidor para **copia de seguridad de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="bfdd9-118">aplicación de escritorio de Hello debe aparecer en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="bfdd9-119">Haga clic en **recuperar datos** Asistente de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="bfdd9-121">En hello **Introducción** panel, toorestore Hola datos toohello mismo servidor o equipo, seleccione **este servidor (`<server name>`)** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Elija este toohello de datos de servidor opción toorestore Hola mismo equipo](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="bfdd9-123">En hello **seleccionar modo de recuperación** panel, elija **estado del sistema** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Examinar archivos](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="bfdd9-125">En el calendario de hello en **Seleccionar volumen y fecha** punto del panel, seleccione una recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="bfdd9-126">Puede realizar la restauración desde cualquier momento dado de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="bfdd9-127">Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="bfdd9-128">Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Fecha y volumen](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="bfdd9-130">Una vez que haya elegido toorestore de punto de recuperación de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="bfdd9-131">Copia de seguridad de Azure monta el punto de recuperación local de Hola y lo utiliza como un volumen de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="bfdd9-132">En el panel siguiente de hello, especifique el destino de Hola para hello recupera archivos de estado del sistema y haga clic en **examinar** tooopen el Explorador de Windows y buscar Hola archivos y carpetas que desee.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="bfdd9-133">Hola opción, **crear copias para tener ambas versiones**, crea copias de los archivos individuales en un archivo de archivo de estado del sistema existente en lugar de crear la copia de hello del archivo de estado del sistema completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Opciones de recuperación](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="bfdd9-135">Compruebe los detalles de Hola de recuperación en hello **confirmación** panel y haga clic en **recuperar**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Haga clic en recuperar tooacknowledge Hola recuperar acción](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="bfdd9-137">Hola copia *WindowsImageBackup* directorio hello las no críticas volumen de tooa del destino de recuperación del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="bfdd9-138">Hola volumen del sistema operativo de Windows suele ser de los volúmenes imprescindibles Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="bfdd9-139">Una vez que la recuperación de hello es correcta, siga los pasos de hello en la sección de hello, [aplicar restaura toohello de archivos de estado del sistema Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), hello toocomplete proceso de recuperación de estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="bfdd9-140">Recuperar el estado del sistema de archivos de servidor alternativo tooan</span><span class="sxs-lookup"><span data-stu-id="bfdd9-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="bfdd9-141">Si el servidor de Windows está dañado o es inaccesible y desea toorestore lo Hola de estado estable de tooa mediante la recuperación de estado de sistema de Windows Server, puede restaurar el estado del sistema del servidor dañado Hola desde otro servidor.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="bfdd9-142">Usar hello siguiendo los pasos para restaurar toohello estado del sistema en un servidor independiente.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="bfdd9-143">terminología de Hola que se usa en estos pasos se incluye:</span><span class="sxs-lookup"><span data-stu-id="bfdd9-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="bfdd9-144">*Máquina de origen* : tomada máquina original de Hola desde la copia de seguridad de Hola y que no está disponible actualmente.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="bfdd9-145">*El equipo de destino* : se va a recuperar datos de saludo máquina toowhich Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="bfdd9-146">*Almacén de ejemplo* : Hola Hola de toowhich de almacén de servicios de recuperación *máquina de origen* y *equipo de destino* están registrados.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="bfdd9-147">Copias de seguridad de un equipo no pueden ser máquina restaurada tooa ejecuta una versión anterior del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="bfdd9-148">Por ejemplo, copias de seguridad realizadas desde un equipo no puede ser de Windows Server 2016 restauran tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="bfdd9-149">Sin embargo, la inversa de hello es posible.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-149">However, hello inverse is possible.</span></span> <span data-ttu-id="bfdd9-150">Puede usar copias de seguridad de Windows Server 2012 R2 toorestore Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="bfdd9-151">Abra hello **copia de seguridad de Microsoft Azure** complemento en hello *equipo de destino*.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="bfdd9-152">Asegúrese de que hello *equipo de destino* hello y *máquina de origen* están registrado toohello mismos servicios de recuperación del almacén.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="bfdd9-153">Haga clic en **recuperar datos** el flujo de trabajo de tooinitiate Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Recuperar datos](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="bfdd9-155">Seleccione **Otro servidor**</span><span class="sxs-lookup"><span data-stu-id="bfdd9-155">Select **Another server**</span></span>

    ![Otro servidor](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="bfdd9-157">Proporcione el archivo de credenciales de almacén de hello correspondiente toohello *el almacén de ejemplo*.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="bfdd9-158">Si el archivo de credenciales de almacén de hello es válida (o expiró), descargue un nuevo archivo de credenciales de almacén de hello *almacén ejemplo* Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="bfdd9-159">Una vez que se proporciona el archivo de credenciales de almacén de hello, aparece el almacén de servicios de recuperación de hello asociado con el archivo de credenciales de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="bfdd9-160">En el panel de seleccionar el servidor de copia de seguridad de hello, seleccione hello *máquina de origen* en lista de Hola de máquinas mostradas.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lista de máquinas](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="bfdd9-162">En el panel de seleccionar el modo de recuperación de hello, elija **estado del sistema** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="bfdd9-164">En el calendario de Hola Hola **Seleccionar volumen y fecha** punto del panel, seleccione una recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="bfdd9-165">Puede realizar la restauración desde cualquier momento dado de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="bfdd9-166">Las fechas en **negrita** indicar la disponibilidad de Hola de al menos un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="bfdd9-167">Cuando selecciona una fecha, si existen varios puntos de recuperación, elija punto de recuperación específico de Hola de hello **tiempo** menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Buscar artículos](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="bfdd9-169">Una vez que haya elegido toorestore de punto de recuperación de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="bfdd9-170">En hello **seleccionar un modo de recuperación de estado de sistema** panel, especificar destino de hello en el que desea toobe recuperar archivos de estado del sistema, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Cifrado](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="bfdd9-172">Hola opción, **crear copias para tener ambas versiones**, crea copias de los archivos individuales en un archivo de archivo de estado del sistema existente en lugar de crear la copia de hello del archivo de estado del sistema completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="bfdd9-173">Compruebe los detalles de Hola de recuperación en el panel de la confirmación de Hola y haga clic en **recuperar**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![Haga clic en el proceso de recuperación de hello recuperar botón tooconfirm Hola](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="bfdd9-175">Hola copia *WindowsImageBackup* tooa no críticos volumen de directorio del servidor de hello (por ejemplo, D:\).</span><span class="sxs-lookup"><span data-stu-id="bfdd9-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="bfdd9-176">Hola volumen del sistema operativo de Windows suele ser de los volúmenes imprescindibles Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="bfdd9-177">proceso de recuperación de toocomplete hello, use siguiente de hello sección demasiado[Hola restaurar archivos de estado del sistema en un servidor de Windows se aplican](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="bfdd9-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="bfdd9-178">Aplicación del estado del sistema restaurado a Windows Server</span><span class="sxs-lookup"><span data-stu-id="bfdd9-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="bfdd9-179">Una vez se ha recuperado el estado del sistema como archivos con el agente de servicios de recuperación de Azure, use Hola copias de seguridad de Windows Server utilidad tooapply Hola recuperarse tooWindows de estado del sistema servidor.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="bfdd9-180">Hola utilidad de copia de seguridad de Windows Server ya está disponible en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="bfdd9-181">Hola pasos explica cómo hello tooapply recupera el estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="bfdd9-182">Siguiente de hello use comandos tooreboot el servidor en *modo de reparación de servicios de directorio*.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="bfdd9-183">En un símbolo del sistema con privilegios elevados:</span><span class="sxs-lookup"><span data-stu-id="bfdd9-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="bfdd9-184">Después del reinicio de hello, abra complemento Hola copias de seguridad de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="bfdd9-185">Si no sabe donde se instaló el complemento hello, buscar Hola equipo o servidor para **copias de seguridad de Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="bfdd9-186">aplicación de escritorio de Hello aparece en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="bfdd9-187">En el complemento de hello, seleccione **copia de seguridad Local**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Seleccione toorestore de copia de seguridad Local desde allí](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="bfdd9-189">En la consola de copia de seguridad Local de hello, Hola **panel acciones**, haga clic en **recuperar** tooopen Hola Asistente para recuperación.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="bfdd9-190">Seleccione la opción de hello, **una copia de seguridad almacenada en otra ubicación**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Elija otro servidor de toorecover tooa](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="bfdd9-192">Cuando se especifica el tipo de ubicación de hello, seleccione **carpeta compartida remota** si la copia de seguridad de estado del sistema se ha recuperado tooanother server.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="bfdd9-193">Si el estado del sistema se recuperó localmente, seleccione **Unidades locales**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Seleccione si toorecovery desde el servidor local o en otro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="bfdd9-195">Escriba Hola ruta de acceso toohello *WindowsImageBackup* directorio, o elija Hola unidad local que contiene este directorio (por ejemplo, D:\WindowsImageBackup), que se recupera como parte de la recuperación de archivos de estado del sistema de hello mediante la recuperación de Azure Servicios de agente y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![ruta de acceso compartido archivo de toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="bfdd9-197">Versión de estado del sistema seleccione Hola que desee toorestore y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="bfdd9-198">En panel de hello Seleccionar tipo de recuperación, seleccione **estado del sistema** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="bfdd9-199">Para la ubicación de Hola de hello recuperación del estado del sistema, seleccione **ubicación Original**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="bfdd9-200">Revise los detalles de confirmación de hello, compruebe la configuración de reinicio de Hola y haga clic en **recuperar** tooapplly Hola restaura archivos de estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![Hola iniciar Restaurar archivos de estado del sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="bfdd9-202">Consideraciones especiales para la recuperación del estado del sistema en el servidor de Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfdd9-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="bfdd9-203">La copia de seguridad del estado del sistema incluye datos de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="bfdd9-204">Usar hello siguiendo los pasos toorestore los servicios de dominio de Active Directory (AD DS) de su estado anterior de tooa de estado actual.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="bfdd9-205">Reinicie el controlador de dominio de hello en el modo de restauración de servicios de directorio (DSRM).</span><span class="sxs-lookup"><span data-stu-id="bfdd9-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="bfdd9-206">Siga los pasos de hello [aquí](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover de cmdlets de copias de seguridad de Windows Server toouse AD DS.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="bfdd9-207">Solución de problemas en la restauración del estado del sistema</span><span class="sxs-lookup"><span data-stu-id="bfdd9-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="bfdd9-208">Si el proceso anterior de Hola de aplicar el estado del sistema no se completa correctamente, use hello toorecover de entorno de recuperación de Windows (Windows RE) el servidor de Windows.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="bfdd9-209">Hello pasos siguientes se explica cómo toorecover con Windows RE.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="bfdd9-210">Utilice esta opción solo si Windows Server no se inicia normalmente después de una restauración del estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="bfdd9-211">Hola siguiendo proceso borra datos no son del sistema, tenga cuidado.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="bfdd9-212">Arranque el servidor de Windows en hello entorno de recuperación de Windows (Windows RE).</span><span class="sxs-lookup"><span data-stu-id="bfdd9-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="bfdd9-213">Seleccione la solución de problemas de tres opciones disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-213">Select Troubleshoot from hello three available options.</span></span>

    ![Apertura del menú](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="bfdd9-215">De hello **opciones avanzadas** pantalla, seleccione **símbolo** y proporcione el nombre de usuario de administrador de servidor de hello y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![Apertura del menú](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="bfdd9-217">Proporcionar el nombre de usuario de administrador de servidor de hello y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-217">Provide hello server administrator username and password.</span></span>

    ![Apertura del menú](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="bfdd9-219">Al abrir símbolo del sistema de hello en modo de administrador, ejecutar las siguientes versiones de copia de seguridad de estado del sistema de comando tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="bfdd9-221">Ejecute hello después comando tooget todos los volúmenes disponibles en la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="bfdd9-223">Hello comando siguiente recupera todos los volúmenes que forman parte del programa Hola a copia de seguridad de estado del sistema.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="bfdd9-224">Tenga en cuenta que este paso recupera solo Hola volúmenes críticos que forman parte del estado del sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="bfdd9-225">Se borran todos los datos que no son del sistema.</span><span class="sxs-lookup"><span data-stu-id="bfdd9-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Obtención de las versiones de copia de seguridad del estado del sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="bfdd9-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfdd9-227">Next steps</span></span>
* <span data-ttu-id="bfdd9-228">Ahora que ha recuperado los archivos y las carpetas, puede [administrar las copias de seguridad](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="bfdd9-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>

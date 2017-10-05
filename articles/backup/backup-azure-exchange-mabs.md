---
title: Copia de seguridad de un servidor Exchange en Azure Backup con el servidor de copia de seguridad de Azure | Microsoft Docs
description: "Obtenga información sobre cómo realizar una copia de seguridad de un servidor Exchange en Azure Backup con el Azure Backup Server"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="17f54-103">Realice una copia de seguridad de un servidor Exchange en Azure Backup con el servidor de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="17f54-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="17f54-104">En este artículo se describe cómo configurar un servidor de copia de seguridad de Microsoft Azure (MABS) para realizar una copia de seguridad de un servidor Microsoft Exchange en Azure.</span><span class="sxs-lookup"><span data-stu-id="17f54-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="17f54-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="17f54-105">Prerequisites</span></span>
<span data-ttu-id="17f54-106">Antes de continuar, asegúrese de que el servidor de copia de seguridad de Azure esté [instalado y preparado](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="17f54-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="17f54-107">Agente de protección MABS</span><span class="sxs-lookup"><span data-stu-id="17f54-107">MABS protection agent</span></span>
<span data-ttu-id="17f54-108">Para instalar al agente de protección MABS en el servidor Exchange, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="17f54-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="17f54-109">Asegúrese de que los firewalls estén configurados correctamente.</span><span class="sxs-lookup"><span data-stu-id="17f54-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="17f54-110">Consulte [Configuración de excepciones de firewall para el agente](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="17f54-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="17f54-111">Instale el agente en el servidor Exchange; para ello, haga clic en **Administración > Agentes > Instalar** en la consola de administrador de MABS.</span><span class="sxs-lookup"><span data-stu-id="17f54-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="17f54-112">Consulte [Instalación del agente de protección MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para ver pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="17f54-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="17f54-113">Creación de un grupo de protección para el servidor Exchange</span><span class="sxs-lookup"><span data-stu-id="17f54-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="17f54-114">En la consola de administrador de MABS, haga clic en **Protección** y luego en **Nuevo** en la cinta de herramientas para abrir el asistente **Crear nuevo grupo de protección**.</span><span class="sxs-lookup"><span data-stu-id="17f54-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="17f54-115">En la pantalla **Bienvenido** del asistente, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="17f54-116">En la pantalla **Seleccionar tipo de grupo de protección**, seleccione **Servidores** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="17f54-117">Seleccione la base de datos del servidor Exchange que desea proteger y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17f54-118">Si va a proteger Exchange 2013, compruebe en [Requisitos previos de Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="17f54-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="17f54-119">En el ejemplo siguiente, está seleccionada la base de datos de Exchange 2010.</span><span class="sxs-lookup"><span data-stu-id="17f54-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="17f54-121">Seleccione el método de protección de datos.</span><span class="sxs-lookup"><span data-stu-id="17f54-121">Select the data protection method.</span></span>

    <span data-ttu-id="17f54-122">Asigne un nombre al grupo de protección y, a continuación, seleccione las dos opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="17f54-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="17f54-123">Deseo protección a corto plazo mediante disco.</span><span class="sxs-lookup"><span data-stu-id="17f54-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="17f54-124">Deseo protección en línea.</span><span class="sxs-lookup"><span data-stu-id="17f54-124">I want online protection.</span></span>
6. <span data-ttu-id="17f54-125">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="17f54-125">Click **Next**.</span></span>
7. <span data-ttu-id="17f54-126">Seleccione la opción **Ejecutar Eseutil para comprobar la integridad de los datos** si desea comprobar la integridad de las bases de datos de Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="17f54-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="17f54-127">Después de seleccionar esta opción, se ejecutará una comprobación de coherencia de copia de seguridad en MABS para evitar el tráfico de E/S que se genera al ejecutar el comando **eseutil** en el servidor Exchange.</span><span class="sxs-lookup"><span data-stu-id="17f54-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17f54-128">Para usar esta opción, debe copiar los archivos Ese.dll y Eseutil.exe en el directorio C:\Archivos de programa\Microsoft Azure Backup\DPM\DPM\bin del servidor MAB.</span><span class="sxs-lookup"><span data-stu-id="17f54-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="17f54-129">De lo contrario, se desencadena el siguiente error: </span><span class="sxs-lookup"><span data-stu-id="17f54-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="17f54-130">![Error de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="17f54-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="17f54-131">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-131">Click **Next**.</span></span>
9. <span data-ttu-id="17f54-132">Seleccione la base de datos para **Copia de seguridad de copia**, y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17f54-133">Si no selecciona "Copia de seguridad completa" al menos para una copia de DAG de una base de datos, no se truncarán los registros.</span><span class="sxs-lookup"><span data-stu-id="17f54-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="17f54-134">Configure los objetivos de **Copia de seguridad a corto plazo** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="17f54-135">Revise el espacio en disco disponible y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="17f54-136">Seleccione la hora a la que el servidor MAB creará la replicación inicial y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="17f54-137">Seleccione las opciones de comprobación de coherencia y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="17f54-138">Elija la base de datos de la que desea realizar una copia de seguridad en Azure y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="17f54-139">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="17f54-139">For example:</span></span>

    ![Especificar datos de protección en línea](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="17f54-141">Defina la programación de **Copia de seguridad de Azure** y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="17f54-142">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="17f54-142">For example:</span></span>

    ![Especificar programación de copia de seguridad en línea](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="17f54-144">Los puntos de recuperación de notas en línea están basados en los puntos de recuperación completos rápidos.</span><span class="sxs-lookup"><span data-stu-id="17f54-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="17f54-145">Por lo tanto, debe programar el punto de recuperación en línea después de la hora especificada para el punto de recuperación completo rápido.</span><span class="sxs-lookup"><span data-stu-id="17f54-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="17f54-146">Configure la directiva de retención para **Copia de seguridad de Azure** y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="17f54-147">Elija una opción de replicación en línea y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17f54-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="17f54-148">Si tiene una base de datos grande, se puede tardar mucho tiempo en crear la copia de seguridad inicial a través de la red.</span><span class="sxs-lookup"><span data-stu-id="17f54-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="17f54-149">Para evitar este problema, puede crear una copia de seguridad sin conexión.</span><span class="sxs-lookup"><span data-stu-id="17f54-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Especificar directiva de retención en línea](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="17f54-151">Confirme la configuración y haga clic en **Crear grupo**.</span><span class="sxs-lookup"><span data-stu-id="17f54-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="17f54-152">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="17f54-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="17f54-153">Recuperación de la base de datos de Exchange</span><span class="sxs-lookup"><span data-stu-id="17f54-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="17f54-154">Para recuperar una base de datos de Exchange, haga clic en **Recuperación** en la consola de administrador de MABS.</span><span class="sxs-lookup"><span data-stu-id="17f54-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="17f54-155">Busque la base de datos de Exchange que desea recuperar.</span><span class="sxs-lookup"><span data-stu-id="17f54-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="17f54-156">Seleccione un punto de recuperación en línea en la lista desplegable *Hora de recuperación* .</span><span class="sxs-lookup"><span data-stu-id="17f54-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="17f54-157">Haga clic en **Recuperar** para iniciar el **Asistente para recuperación**.</span><span class="sxs-lookup"><span data-stu-id="17f54-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="17f54-158">Para los puntos de recuperación en línea, existen cinco tipos de recuperación:</span><span class="sxs-lookup"><span data-stu-id="17f54-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="17f54-159">**Recuperar en ubicación original de servidor de Exchange :** los datos se recuperarán en el servidor Exchange original.</span><span class="sxs-lookup"><span data-stu-id="17f54-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="17f54-160">**Recuperar en otra base de datos en un servidor de Exchange:** los datos se recuperarán en otra base de datos de otro servidor Exchange.</span><span class="sxs-lookup"><span data-stu-id="17f54-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="17f54-161">**Recuperar en una base de datos de recuperación:** los datos se recuperarán en una base de datos de recuperación de Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="17f54-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="17f54-162">**Copiar en una carpeta de red:** los datos se recuperarán en una carpeta de red.</span><span class="sxs-lookup"><span data-stu-id="17f54-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="17f54-163">**Copiar en cinta:** si tiene una biblioteca de cintas o una unidad de cinta independiente conectada y configurada en MABS, el punto de recuperación se copiará en una cinta libre.</span><span class="sxs-lookup"><span data-stu-id="17f54-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Elegir replicación en línea](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="17f54-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17f54-165">Next steps</span></span>
* [<span data-ttu-id="17f54-166">Preguntas más frecuentes de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="17f54-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)

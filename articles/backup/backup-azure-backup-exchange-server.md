---
title: Copia de seguridad de un servidor Exchange en Copia de seguridad de Azure con System Center 2012 R2 DPM | Microsoft Docs
description: "Obtenga información acerca de cómo realizar una copia de seguridad de un servidor Exchange en Copia de seguridad de Azure con System Center 2012 R2 DPM"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="44f2e-103">Copia de seguridad de un servidor Exchange en Copia de seguridad de Azure con System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="44f2e-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="44f2e-104">En este artículo se describe cómo configurar un servidor de System Center 2012 R2 Data Protection Manager (DPM) para realizar una copia de seguridad de un servidor Microsoft Exchange en Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="44f2e-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="44f2e-105">Actualizaciones</span><span class="sxs-lookup"><span data-stu-id="44f2e-105">Updates</span></span>
<span data-ttu-id="44f2e-106">Para registrar correctamente el servidor DPM con Copia de seguridad de Azure, debe instalar el paquete acumulativo de actualizaciones más reciente de System Center 2012 R2 DPM y la versión más reciente de Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="44f2e-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="44f2e-107">Obtenga el último paquete acumulativo de actualizaciones en el [Catálogo de Microsoft Update](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="44f2e-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="44f2e-108">En los ejemplos de este artículo, se instala la versión 2.0.8719.0 de Azure Backup Agent y el paquete acumulativo de actualizaciones 6 en System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="44f2e-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="44f2e-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="44f2e-109">Prerequisites</span></span>
<span data-ttu-id="44f2e-110">Antes de continuar, asegúrese de que se cumplen todos los [requisitos previos](backup-azure-dpm-introduction.md#prerequisites) para usar Copia de seguridad de Microsoft Azure a fin de proteger las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="44f2e-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="44f2e-111">Entre estos requisitos previos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="44f2e-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="44f2e-112">Se ha creado un almacén de Copia de seguridad en el sitio de Azure.</span><span class="sxs-lookup"><span data-stu-id="44f2e-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="44f2e-113">En el servidor DPM se han descargado las credenciales del almacén y del agente.</span><span class="sxs-lookup"><span data-stu-id="44f2e-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="44f2e-114">El agente está instalado en el servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="44f2e-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="44f2e-115">Las credenciales de almacén se utilizaban para registrar el servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="44f2e-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="44f2e-116">Si va a proteger Exchange 2016, actualice al paquete acumulativo de actualizaciones 9 de DPM 2012 R2 o posterior.</span><span class="sxs-lookup"><span data-stu-id="44f2e-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="44f2e-117">Agente de protección DPM</span><span class="sxs-lookup"><span data-stu-id="44f2e-117">DPM protection agent</span></span>
<span data-ttu-id="44f2e-118">Para instalar al agente de protección DPM en el servidor Exchange, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="44f2e-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="44f2e-119">Asegúrese de que los firewalls estén configurados correctamente.</span><span class="sxs-lookup"><span data-stu-id="44f2e-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="44f2e-120">Consulte [Configuración de excepciones de firewall para el agente](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="44f2e-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="44f2e-121">Instale el agente en el servidor Exchange; para ello, haga clic en **Administración > Agentes > Instalar** en la Consola de administrador DPM.</span><span class="sxs-lookup"><span data-stu-id="44f2e-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="44f2e-122">Consulte [Instalación del agente de protección DPM](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para ver pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="44f2e-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="44f2e-123">Creación de un grupo de protección para el servidor Exchange</span><span class="sxs-lookup"><span data-stu-id="44f2e-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="44f2e-124">En la Consola de administrador DPM, haga clic en **Protección** y luego en **Nuevo** en la cinta de herramientas para abrir el asistente **Crear nuevo grupo de protección**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="44f2e-125">En la pantalla **Bienvenido** del asistente, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="44f2e-126">En la pantalla **Seleccionar tipo de grupo de protección**, seleccione **Servidores** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="44f2e-127">Seleccione la base de datos del servidor Exchange que desea proteger y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="44f2e-128">Si va a proteger Exchange 2013, compruebe en [Requisitos previos de Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="44f2e-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="44f2e-129">En el ejemplo siguiente, está seleccionada la base de datos de Exchange 2010.</span><span class="sxs-lookup"><span data-stu-id="44f2e-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="44f2e-131">Seleccione el método de protección de datos.</span><span class="sxs-lookup"><span data-stu-id="44f2e-131">Select the data protection method.</span></span>

    <span data-ttu-id="44f2e-132">Asigne un nombre al grupo de protección y, a continuación, seleccione las dos opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="44f2e-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="44f2e-133">Deseo protección a corto plazo mediante disco.</span><span class="sxs-lookup"><span data-stu-id="44f2e-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="44f2e-134">Deseo protección en línea.</span><span class="sxs-lookup"><span data-stu-id="44f2e-134">I want online protection.</span></span>
6. <span data-ttu-id="44f2e-135">Haga clic en **Next**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-135">Click **Next**.</span></span>
7. <span data-ttu-id="44f2e-136">Seleccione la opción **Ejecutar Eseutil para comprobar la integridad de los datos** si desea comprobar la integridad de las bases de datos de Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="44f2e-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="44f2e-137">Después de seleccionar esta opción, se ejecutará una comprobación de coherencia de copia de seguridad en el servidor DPM para evitar el tráfico de E/S que se genera al ejecutar el comando **eseutil** en el servidor Exchange.</span><span class="sxs-lookup"><span data-stu-id="44f2e-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="44f2e-138">Para usar esta opción, debe copiar los archivos Ese.dll y Eseutil.exe en el directorio C:\Archivos de programa\Microsoft System Center 2012 R2\DPM\DPM\bin del servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="44f2e-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="44f2e-139">De lo contrario, se desencadena el siguiente error: </span><span class="sxs-lookup"><span data-stu-id="44f2e-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="44f2e-140">![Error de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="44f2e-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="44f2e-141">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-141">Click **Next**.</span></span>
9. <span data-ttu-id="44f2e-142">Seleccione la base de datos para **Copia de seguridad de copia**, y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="44f2e-143">Si no selecciona "Copia de seguridad completa" al menos para una copia de DAG de una base de datos, no se truncarán los registros.</span><span class="sxs-lookup"><span data-stu-id="44f2e-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="44f2e-144">Configure los objetivos de **Copia de seguridad a corto plazo** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="44f2e-145">Revise el espacio en disco disponible y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="44f2e-146">Seleccione la hora a la que el servidor DPM creará la replicación inicial y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="44f2e-147">Seleccione las opciones de comprobación de coherencia y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="44f2e-148">Elija la base de datos de la que desea realizar una copia de seguridad en Azure y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="44f2e-149">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44f2e-149">For example:</span></span>

    ![Especificar datos de protección en línea](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="44f2e-151">Defina la programación de **Copia de seguridad de Azure** y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="44f2e-152">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44f2e-152">For example:</span></span>

    ![Especificar programación de copia de seguridad en línea](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="44f2e-154">Los puntos de recuperación de notas en línea están basados en los puntos de recuperación completos rápidos.</span><span class="sxs-lookup"><span data-stu-id="44f2e-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="44f2e-155">Por lo tanto, debe programar el punto de recuperación en línea después de la hora especificada para el punto de recuperación completo rápido.</span><span class="sxs-lookup"><span data-stu-id="44f2e-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="44f2e-156">Configure la directiva de retención para **Copia de seguridad de Azure** y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="44f2e-157">Elija una opción de replicación en línea y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="44f2e-158">Si tiene una base de datos grande, se puede tardar mucho tiempo en crear la copia de seguridad inicial a través de la red.</span><span class="sxs-lookup"><span data-stu-id="44f2e-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="44f2e-159">Para evitar este problema, puede crear una copia de seguridad sin conexión.</span><span class="sxs-lookup"><span data-stu-id="44f2e-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![Especificar directiva de retención en línea](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="44f2e-161">Confirme la configuración y haga clic en **Crear grupo**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="44f2e-162">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="44f2e-163">Recuperación de la base de datos de Exchange</span><span class="sxs-lookup"><span data-stu-id="44f2e-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="44f2e-164">Para recuperar una base de datos de Exchange, haga clic en **Recuperación** en la Consola de administrador DPM.</span><span class="sxs-lookup"><span data-stu-id="44f2e-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="44f2e-165">Busque la base de datos de Exchange que desea recuperar.</span><span class="sxs-lookup"><span data-stu-id="44f2e-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="44f2e-166">Seleccione un punto de recuperación en línea en la lista desplegable *Hora de recuperación* .</span><span class="sxs-lookup"><span data-stu-id="44f2e-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="44f2e-167">Haga clic en **Recuperar** para iniciar el **Asistente para recuperación**.</span><span class="sxs-lookup"><span data-stu-id="44f2e-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="44f2e-168">Para los puntos de recuperación en línea, existen cinco tipos de recuperación:</span><span class="sxs-lookup"><span data-stu-id="44f2e-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="44f2e-169">**Recuperar en ubicación original de servidor de Exchange :** los datos se recuperarán en el servidor Exchange original.</span><span class="sxs-lookup"><span data-stu-id="44f2e-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="44f2e-170">**Recuperar en otra base de datos en un servidor de Exchange:** los datos se recuperarán en otra base de datos de otro servidor Exchange.</span><span class="sxs-lookup"><span data-stu-id="44f2e-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="44f2e-171">**Recuperar en una base de datos de recuperación:** los datos se recuperarán en una base de datos de recuperación de Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="44f2e-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="44f2e-172">**Copiar en una carpeta de red:** los datos se recuperarán en una carpeta de red.</span><span class="sxs-lookup"><span data-stu-id="44f2e-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="44f2e-173">**Copiar en cinta:** si tiene una biblioteca de cintas o una unidad de cinta independiente conectada y configurada en el servidor DPM, el punto de recuperación se copiará en una cinta libre.</span><span class="sxs-lookup"><span data-stu-id="44f2e-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![Elegir replicación en línea](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="44f2e-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44f2e-175">Next steps</span></span>
* [<span data-ttu-id="44f2e-176">Preguntas más frecuentes de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="44f2e-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)

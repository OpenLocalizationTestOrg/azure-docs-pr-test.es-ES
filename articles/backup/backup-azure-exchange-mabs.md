---
title: aaaBack seguridad un tooAzure de Exchange server copia de seguridad con el servidor de copia de seguridad de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooback seguridad un tooAzure del servidor de Exchange de copia de seguridad utilizando el servidor de copia de seguridad de Azure"
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
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="c0af9-103">Hacer copia de seguridad de un tooAzure de Exchange server copia de seguridad con el servidor de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="c0af9-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="c0af9-104">Este artículo se describe cómo tooconfigure tooback de servidor de copia de seguridad de Microsoft Azure (MABS) de un tooAzure de servidor de Microsoft Exchange.</span><span class="sxs-lookup"><span data-stu-id="c0af9-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c0af9-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c0af9-105">Prerequisites</span></span>
<span data-ttu-id="c0af9-106">Antes de continuar, asegúrese de que el servidor de copia de seguridad de Azure esté [instalado y preparado](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="c0af9-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="c0af9-107">Agente de protección MABS</span><span class="sxs-lookup"><span data-stu-id="c0af9-107">MABS protection agent</span></span>
<span data-ttu-id="c0af9-108">agente de protección de MABS tooinstall hello en el servidor de Exchange de hello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c0af9-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="c0af9-109">Asegúrese de que los firewalls de hello estén configurados correctamente.</span><span class="sxs-lookup"><span data-stu-id="c0af9-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="c0af9-110">Vea [configurar excepciones de firewall para el agente de hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0af9-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="c0af9-111">Instalar agente de hello en el servidor de Exchange de hello haciendo clic en **Administración > agentes > instalar** en la consola de administrador de MABS.</span><span class="sxs-lookup"><span data-stu-id="c0af9-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="c0af9-112">Vea [agente de protección de instalación hello MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para obtener pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="c0af9-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="c0af9-113">Cree un grupo de protección para Exchange server de Hola</span><span class="sxs-lookup"><span data-stu-id="c0af9-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="c0af9-114">En la consola de administrador de MABS hello, haga clic en **protección**y, a continuación, haga clic en **New** en Hola Hola de tooopen de cinta de opciones de herramienta **crear nuevo grupo de protección** asistente.</span><span class="sxs-lookup"><span data-stu-id="c0af9-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="c0af9-115">En hello **bienvenida** pantalla del asistente, haga clic hello **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="c0af9-116">En hello **Seleccionar tipo de grupo de protección** pantalla, seleccione **servidores** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="c0af9-117">Base de datos de servidor de Exchange de hello SELECT que desee tooprotect y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c0af9-118">Si va a proteger Exchange 2013, compruebe hello [requisitos previos de Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0af9-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="c0af9-119">En el siguiente ejemplo de Hola, base de datos de Exchange 2010 Hola está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="c0af9-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="c0af9-121">Seleccionar método de protección de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0af9-121">Select hello data protection method.</span></span>

    <span data-ttu-id="c0af9-122">Nombre de grupo de protección de hello y, a continuación, seleccione ambos Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="c0af9-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="c0af9-123">Deseo protección a corto plazo mediante disco.</span><span class="sxs-lookup"><span data-stu-id="c0af9-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="c0af9-124">Deseo protección en línea.</span><span class="sxs-lookup"><span data-stu-id="c0af9-124">I want online protection.</span></span>
6. <span data-ttu-id="c0af9-125">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-125">Click **Next**.</span></span>
7. <span data-ttu-id="c0af9-126">Seleccione hello **integridad de los datos toocheck ejecutar Eseutil** opción si desea que la integridad de hello toocheck de bases de datos de Exchange Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0af9-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="c0af9-127">Después de seleccionar esta opción, la comprobación de coherencia de copia de seguridad se ejecutará en MABS tooavoid Hola E/S el tráfico que se genera mediante la ejecución de hello **eseutil** comando en el servidor de Exchange de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0af9-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c0af9-128">toouse esta opción, debe copiar Hola Ese.dll y Eseutil.exe archivos toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directorio Hola AM servidor.</span><span class="sxs-lookup"><span data-stu-id="c0af9-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="c0af9-129">En caso contrario, se desencadena Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="c0af9-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="c0af9-130">![Error de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="c0af9-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="c0af9-131">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-131">Click **Next**.</span></span>
9. <span data-ttu-id="c0af9-132">Base de datos seleccione hello **copia de seguridad**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c0af9-133">Si no selecciona "Copia de seguridad completa" al menos para una copia de DAG de una base de datos, no se truncarán los registros.</span><span class="sxs-lookup"><span data-stu-id="c0af9-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="c0af9-134">Configure los objetivos de Hola para **copia de seguridad a corto plazo**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="c0af9-135">Revise el espacio en disco disponible hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="c0af9-136">Seleccione hora de hello en qué Hola AM Server creará la replicación inicial de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="c0af9-137">Seleccione las opciones de comprobación de coherencia de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="c0af9-138">Elija la base de datos de Hola que desee tooback seguridad tooAzure y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="c0af9-139">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c0af9-139">For example:</span></span>

    ![Especificar datos de protección en línea](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="c0af9-141">Definir programación Hola para **copia de seguridad de Azure**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="c0af9-142">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c0af9-142">For example:</span></span>

    ![Especificar programación de copia de seguridad en línea](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="c0af9-144">Los puntos de recuperación de notas en línea están basados en los puntos de recuperación completos rápidos.</span><span class="sxs-lookup"><span data-stu-id="c0af9-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="c0af9-145">Por lo tanto, debe programar el punto de recuperación en línea hello después del horario de Hola que se especifica para hello express punto de recuperación completa.</span><span class="sxs-lookup"><span data-stu-id="c0af9-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="c0af9-146">Configurar la directiva de retención de Hola para **copia de seguridad de Azure**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="c0af9-147">Elija una opción de replicación en línea y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="c0af9-148">Si tiene una base de datos grande, puede tardar mucho tiempo para toobe de copia de seguridad inicial de hello creado a través de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0af9-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="c0af9-149">tooavoid este problema, puede crear una copia de seguridad sin conexión.</span><span class="sxs-lookup"><span data-stu-id="c0af9-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Especificar directiva de retención en línea](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="c0af9-151">Confirmar configuración de hello y, a continuación, haga clic en **crear grupo**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="c0af9-152">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="c0af9-153">Recuperar base de datos de Exchange de Hola</span><span class="sxs-lookup"><span data-stu-id="c0af9-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="c0af9-154">toorecover una base de datos de Exchange, haga clic en **recuperación** en la consola de administrador de MABS Hola.</span><span class="sxs-lookup"><span data-stu-id="c0af9-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="c0af9-155">Busque la base de datos de Exchange de Hola que desea toorecover.</span><span class="sxs-lookup"><span data-stu-id="c0af9-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="c0af9-156">Seleccione un punto de recuperación en línea de hello *tiempo de recuperación* lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="c0af9-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="c0af9-157">Haga clic en **recuperar** toostart hello **Asistente para recuperación**.</span><span class="sxs-lookup"><span data-stu-id="c0af9-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="c0af9-158">Para los puntos de recuperación en línea, existen cinco tipos de recuperación:</span><span class="sxs-lookup"><span data-stu-id="c0af9-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="c0af9-159">**Recuperar la ubicación del servidor de Exchange de toooriginal:** datos Hola sea servidor de Exchange original toohello recuperada.</span><span class="sxs-lookup"><span data-stu-id="c0af9-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="c0af9-160">**Recuperar base de datos de tooanother en un servidor Exchange:** datos Hola será la base de datos de tooanother recuperada en otro servidor de Exchange.</span><span class="sxs-lookup"><span data-stu-id="c0af9-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="c0af9-161">**Recuperar la base de datos de recuperación de tooa:** datos Hola será tooan recuperada base de datos de recuperación de Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="c0af9-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="c0af9-162">**Carpeta de red de copia tooa:** datos Hola será la carpeta de red de tooa recuperada.</span><span class="sxs-lookup"><span data-stu-id="c0af9-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="c0af9-163">**Copie tootape:** si dispone de una biblioteca de cintas o una unidad de cinta independiente que se adjunta y se ha configurado en MABS, punto de recuperación de hello será copiados tooa de cintas libres.</span><span class="sxs-lookup"><span data-stu-id="c0af9-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![Elegir replicación en línea](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="c0af9-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0af9-165">Next steps</span></span>
* [<span data-ttu-id="c0af9-166">Preguntas más frecuentes de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="c0af9-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)

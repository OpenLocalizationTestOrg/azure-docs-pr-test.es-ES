---
title: aaaBack seguridad un tooAzure de Exchange server copia de seguridad con System Center 2012 R2 DPM | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooback seguridad un tooAzure del servidor de Exchange de copia de seguridad con System Center 2012 R2 DPM"
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
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="dc44d-103">Hacer copia de seguridad de un tooAzure de Exchange server copia de seguridad con System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="dc44d-103">Back up an Exchange server tooAzure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="dc44d-104">Este artículo se describe cómo tooconfigure una tooback de servidor de System Center 2012 R2 Data Protection Manager (DPM) de un servidor de Microsoft Exchange demasiado Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="dc44d-104">This article describes how tooconfigure a System Center 2012 R2 Data Protection Manager (DPM) server tooback up a Microsoft Exchange server too Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="dc44d-105">Actualizaciones</span><span class="sxs-lookup"><span data-stu-id="dc44d-105">Updates</span></span>
<span data-ttu-id="dc44d-106">toosuccessfully el servidor DPM de registro Hola con copia de seguridad de Azure, debe instalar Hola último paquete acumulativo de actualizaciones para System Center 2012 R2 DPM y Hola la versión más reciente de hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="dc44d-106">toosuccessfully register hello DPM server with Azure Backup, you must install hello latest update rollup for System Center 2012 R2 DPM and hello latest version of hello Azure Backup Agent.</span></span> <span data-ttu-id="dc44d-107">Obtener el paquete acumulativo de actualizaciones más reciente de Hola de hello [catálogo de Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="dc44d-107">Get hello latest update rollup from hello [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="dc44d-108">Para obtener ejemplos de hello en este artículo, se instala la versión 2.0.8719.0 de hello Azure Backup Agent y actualización paquete acumulativo de actualizaciones 6 está instalado en System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="dc44d-108">For hello examples in this article, version 2.0.8719.0 of hello Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="dc44d-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dc44d-109">Prerequisites</span></span>
<span data-ttu-id="dc44d-110">Antes de continuar, asegúrese de que todos los Hola [requisitos previos](backup-azure-dpm-introduction.md#prerequisites) para el uso de copia de seguridad de Microsoft Azure se cumplieron las cargas de trabajo tooprotect.</span><span class="sxs-lookup"><span data-stu-id="dc44d-110">Before you continue, make sure that all hello [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup tooprotect workloads have been met.</span></span> <span data-ttu-id="dc44d-111">Estos requisitos previos Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="dc44d-111">These prerequisites include hello following:</span></span>

* <span data-ttu-id="dc44d-112">Se ha creado un almacén de copia de seguridad en hello sitio de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc44d-112">A backup vault on hello Azure site has been created.</span></span>
* <span data-ttu-id="dc44d-113">Credenciales del almacén y agente han sido toohello descargado el servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="dc44d-113">Agent and vault credentials have been downloaded toohello DPM server.</span></span>
* <span data-ttu-id="dc44d-114">Hola agente está instalado en el servidor DPM Hola.</span><span class="sxs-lookup"><span data-stu-id="dc44d-114">hello agent is installed on hello DPM server.</span></span>
* <span data-ttu-id="dc44d-115">las credenciales de almacén de Hello eran servidor DPM usa tooregister Hola.</span><span class="sxs-lookup"><span data-stu-id="dc44d-115">hello vault credentials were used tooregister hello DPM server.</span></span>
* <span data-ttu-id="dc44d-116">Si va a proteger Exchange 2016, actualice tooDPM 2012 R2 UR9 o posterior</span><span class="sxs-lookup"><span data-stu-id="dc44d-116">If you are protecting Exchange 2016, please upgrade tooDPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="dc44d-117">Agente de protección DPM</span><span class="sxs-lookup"><span data-stu-id="dc44d-117">DPM protection agent</span></span>
<span data-ttu-id="dc44d-118">agente de protección de DPM tooinstall hello en el servidor de Exchange de hello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dc44d-118">tooinstall hello DPM protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="dc44d-119">Asegúrese de que los firewalls de hello estén configurados correctamente.</span><span class="sxs-lookup"><span data-stu-id="dc44d-119">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="dc44d-120">Vea [configurar excepciones de firewall para el agente de hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc44d-120">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="dc44d-121">Instalar agente de hello en el servidor de Exchange de hello haciendo clic en **Administración > agentes > instalar** en la consola de administrador DPM.</span><span class="sxs-lookup"><span data-stu-id="dc44d-121">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="dc44d-122">Vea [agente de protección DPM Install hello](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para obtener pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="dc44d-122">See [Install hello DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="dc44d-123">Cree un grupo de protección para Exchange server de Hola</span><span class="sxs-lookup"><span data-stu-id="dc44d-123">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="dc44d-124">Hola consola de administrador DPM, haga clic en **protección**y, a continuación, haga clic en **New** en Hola Hola de tooopen de cinta de opciones de herramienta **crear nuevo grupo de protección** asistente.</span><span class="sxs-lookup"><span data-stu-id="dc44d-124">In hello DPM Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="dc44d-125">En hello **bienvenida** pantalla del asistente, haga clic hello **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-125">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="dc44d-126">En hello **Seleccionar tipo de grupo de protección** pantalla, seleccione **servidores** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-126">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="dc44d-127">Base de datos de servidor de Exchange de hello SELECT que desee tooprotect y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-127">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dc44d-128">Si va a proteger Exchange 2013, compruebe hello [requisitos previos de Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc44d-128">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="dc44d-129">En el siguiente ejemplo de Hola, base de datos de Exchange 2010 Hola está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="dc44d-129">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="dc44d-131">Seleccionar método de protección de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc44d-131">Select hello data protection method.</span></span>

    <span data-ttu-id="dc44d-132">Nombre de grupo de protección de hello y, a continuación, seleccione ambos Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="dc44d-132">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="dc44d-133">Deseo protección a corto plazo mediante disco.</span><span class="sxs-lookup"><span data-stu-id="dc44d-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="dc44d-134">Deseo protección en línea.</span><span class="sxs-lookup"><span data-stu-id="dc44d-134">I want online protection.</span></span>
6. <span data-ttu-id="dc44d-135">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-135">Click **Next**.</span></span>
7. <span data-ttu-id="dc44d-136">Seleccione hello **integridad de los datos toocheck ejecutar Eseutil** opción si desea que la integridad de hello toocheck de bases de datos de Exchange Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc44d-136">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="dc44d-137">Después de seleccionar esta opción, la comprobación de coherencia de copia de seguridad se ejecutará en hello DPM tooavoid Hola E/S tráfico del servidor que se genera mediante la ejecución de hello **eseutil** comando en el servidor de Exchange de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc44d-137">After you select this option, backup consistency checking will be run on hello DPM server tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dc44d-138">toouse esta opción, debe copiar Hola Ese.dll y Eseutil.exe directorio archivos de toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin servidor DPM de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc44d-138">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on hello DPM server.</span></span> <span data-ttu-id="dc44d-139">En caso contrario, se desencadena Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="dc44d-139">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="dc44d-140">![Error de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="dc44d-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="dc44d-141">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-141">Click **Next**.</span></span>
9. <span data-ttu-id="dc44d-142">Base de datos seleccione hello **copia de seguridad**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-142">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dc44d-143">Si no selecciona "Copia de seguridad completa" al menos para una copia de DAG de una base de datos, no se truncarán los registros.</span><span class="sxs-lookup"><span data-stu-id="dc44d-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="dc44d-144">Configure los objetivos de Hola para **copia de seguridad a corto plazo**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-144">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="dc44d-145">Revise el espacio en disco disponible hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-145">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="dc44d-146">Seleccione hora de hello en qué Hola DPM server creará la replicación inicial de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-146">Select hello time at which hello DPM server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="dc44d-147">Seleccione las opciones de comprobación de coherencia de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-147">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="dc44d-148">Elija la base de datos de Hola que desee tooback seguridad tooAzure y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-148">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="dc44d-149">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dc44d-149">For example:</span></span>

    ![Especificar datos de protección en línea](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="dc44d-151">Definir programación Hola para **copia de seguridad de Azure**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-151">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="dc44d-152">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dc44d-152">For example:</span></span>

    ![Especificar programación de copia de seguridad en línea](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="dc44d-154">Los puntos de recuperación de notas en línea están basados en los puntos de recuperación completos rápidos.</span><span class="sxs-lookup"><span data-stu-id="dc44d-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="dc44d-155">Por lo tanto, debe programar el punto de recuperación en línea hello después del horario de Hola que se especifica para hello express punto de recuperación completa.</span><span class="sxs-lookup"><span data-stu-id="dc44d-155">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="dc44d-156">Configurar la directiva de retención de Hola para **copia de seguridad de Azure**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-156">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="dc44d-157">Elija una opción de replicación en línea y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="dc44d-158">Si tiene una base de datos grande, puede tardar mucho tiempo para toobe de copia de seguridad inicial de hello creado a través de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc44d-158">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="dc44d-159">tooavoid este problema, puede crear una copia de seguridad sin conexión.</span><span class="sxs-lookup"><span data-stu-id="dc44d-159">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Especificar directiva de retención en línea](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="dc44d-161">Confirmar configuración de hello y, a continuación, haga clic en **crear grupo**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-161">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="dc44d-162">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-162">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="dc44d-163">Recuperar base de datos de Exchange de Hola</span><span class="sxs-lookup"><span data-stu-id="dc44d-163">Recover hello Exchange database</span></span>
1. <span data-ttu-id="dc44d-164">Haga clic en una base de datos de Exchange, toorecover **recuperación** Hola consola de administrador DPM.</span><span class="sxs-lookup"><span data-stu-id="dc44d-164">toorecover an Exchange database, click **Recovery** in hello DPM Administrator Console.</span></span>
2. <span data-ttu-id="dc44d-165">Busque la base de datos de Exchange de Hola que desea toorecover.</span><span class="sxs-lookup"><span data-stu-id="dc44d-165">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="dc44d-166">Seleccione un punto de recuperación en línea de hello *tiempo de recuperación* lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="dc44d-166">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="dc44d-167">Haga clic en **recuperar** toostart hello **Asistente para recuperación**.</span><span class="sxs-lookup"><span data-stu-id="dc44d-167">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="dc44d-168">Para los puntos de recuperación en línea, existen cinco tipos de recuperación:</span><span class="sxs-lookup"><span data-stu-id="dc44d-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="dc44d-169">**Recuperar la ubicación del servidor de Exchange de toooriginal:** datos Hola sea servidor de Exchange original toohello recuperada.</span><span class="sxs-lookup"><span data-stu-id="dc44d-169">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="dc44d-170">**Recuperar base de datos de tooanother en un servidor Exchange:** datos Hola será la base de datos de tooanother recuperada en otro servidor de Exchange.</span><span class="sxs-lookup"><span data-stu-id="dc44d-170">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="dc44d-171">**Recuperar la base de datos de recuperación de tooa:** datos Hola será tooan recuperada base de datos de recuperación de Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="dc44d-171">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="dc44d-172">**Carpeta de red de copia tooa:** datos Hola será la carpeta de red de tooa recuperada.</span><span class="sxs-lookup"><span data-stu-id="dc44d-172">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="dc44d-173">**Copie tootape:** si dispone de una biblioteca de cintas o una unidad de cinta independiente será Hola adjunta y se ha configurado en servidor DPM, el punto de recuperación de hello copiados tooa de cintas libres.</span><span class="sxs-lookup"><span data-stu-id="dc44d-173">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on hello DPM server, hello recovery point will be copied tooa free tape.</span></span>

    ![Elegir replicación en línea](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="dc44d-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc44d-175">Next steps</span></span>
* [<span data-ttu-id="dc44d-176">Preguntas más frecuentes de Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="dc44d-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)

---
title: "aaaGet iniciado a la auditoría de base de datos de SQL de Azure | Documentos de Microsoft"
description: "Introducción a la auditoría de base de datos SQL de Azure"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="0523f-103">Introducción a la auditoría de bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="0523f-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="0523f-104">Auditoría de base de datos SQL Azure realiza un seguimiento de eventos de base de datos y escribe el registro de auditoría tooan en su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0523f-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="0523f-105">La auditoría también:</span><span class="sxs-lookup"><span data-stu-id="0523f-105">Auditing also:</span></span>

* <span data-ttu-id="0523f-106">Puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas.</span><span class="sxs-lookup"><span data-stu-id="0523f-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="0523f-107">Habilita y facilita estándares de cumplimiento toocompliance, aunque no garantiza el cumplimiento de normas.</span><span class="sxs-lookup"><span data-stu-id="0523f-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="0523f-108">Para obtener más información sobre Azure programas ese cumplimiento de estándares de soporte técnico, consulte hello [centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="0523f-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="0523f-109"><a id="subheading-1"></a>Información general de auditoría de base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0523f-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="0523f-110">Puede usar la auditoría de base de datos SQL para:</span><span class="sxs-lookup"><span data-stu-id="0523f-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="0523f-111">**Conservar** una traza de auditoría de eventos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="0523f-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="0523f-112">Puede definir categorías de base de datos acciones toobe auditado.</span><span class="sxs-lookup"><span data-stu-id="0523f-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="0523f-113">**Informar** sobre la actividad de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0523f-113">**Report** on database activity.</span></span> <span data-ttu-id="0523f-114">Puede usar los informes preconfigurados y un tooget de panel a trabajar rápidamente con actividad y los informes de eventos.</span><span class="sxs-lookup"><span data-stu-id="0523f-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="0523f-115">**Analizar** informes.</span><span class="sxs-lookup"><span data-stu-id="0523f-115">**Analyze** reports.</span></span> <span data-ttu-id="0523f-116">Puede buscar eventos sospechosos, actividades inusuales y tendencias.</span><span class="sxs-lookup"><span data-stu-id="0523f-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="0523f-117">Puede configurar la auditoría para distintos tipos de categorías de eventos, como se explica en hello [configurar la auditoría para la base de datos](#subheading-2) sección.</span><span class="sxs-lookup"><span data-stu-id="0523f-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="0523f-118">Los registros de auditoría se escriben tooAzure el almacenamiento de blobs de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0523f-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="0523f-119"><a id="subheading-8"></a>Definir la directiva de auditoría de nivel de servidor frente la de nivel de base de datos</span><span class="sxs-lookup"><span data-stu-id="0523f-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="0523f-120">Puede definirse una directiva de auditoría para una base de datos específica o como directiva de servidor predeterminada:</span><span class="sxs-lookup"><span data-stu-id="0523f-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="0523f-121">Una directiva de servidor aplica tooall existente y las bases de datos recién creadas en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="0523f-122">Si *está habilitada la auditoría de servidor blob*, lo *siempre se aplica a la base de datos de toohello* (es decir, base de datos de Hola se auditarán), independientemente de la base de datos de hello configuración de auditoría.</span><span class="sxs-lookup"><span data-stu-id="0523f-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="0523f-123">Habilitación de blob de auditoría de base de datos de hello en suma tooenabling en servidor hello, le *no* invalidar o cambiar cualquiera de las opciones de Hola de auditoría de hello server blob.</span><span class="sxs-lookup"><span data-stu-id="0523f-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="0523f-124">Ambas auditorías existirán en paralelo.</span><span class="sxs-lookup"><span data-stu-id="0523f-124">Both audits will exist side by side.</span></span> <span data-ttu-id="0523f-125">En otras palabras, base de datos de Hola se auditará dos veces en paralelo (una vez mediante la directiva de servidor de hello y una vez por la directiva de la base de datos de hello).</span><span class="sxs-lookup"><span data-stu-id="0523f-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="0523f-126">Debe habilitar tanto la auditoría de blobs de servidor como la auditoría de blobs de base de datos, a menos que:</span><span class="sxs-lookup"><span data-stu-id="0523f-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="0523f-127">Desea que otro toouse *cuenta de almacenamiento* o *período de retención* para una base de datos.</span><span class="sxs-lookup"><span data-stu-id="0523f-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="0523f-128">Desea tooaudit evento tipos o categorías de una base de datos que difieren de los tipos de eventos o las categorías que se está auditando para rest Hola de bases de datos de hello en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="0523f-129">Por ejemplo, podría tener inserciones de la tabla que necesitan toobe auditar sólo para una base de datos.</span><span class="sxs-lookup"><span data-stu-id="0523f-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="0523f-130">En caso contrario, se recomienda que habilite la auditoría de nivel de servidor solo blobs y deje proceso de auditoría de nivel de base de datos de hello deshabilitada para todas las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="0523f-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="0523f-131"><a id="subheading-2"></a>Configuración de la auditoría para su base de datos</span><span class="sxs-lookup"><span data-stu-id="0523f-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="0523f-132">Hello siguiente sección describe configuración Hola de auditoría usando Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0523f-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="0523f-133">Vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0523f-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0523f-134">Vaya toohello **configuración** hoja de hello servidor de base de datos/SQL de SQL que desee tooaudit.</span><span class="sxs-lookup"><span data-stu-id="0523f-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="0523f-135">Hola **configuración** hoja, seleccione **detección de auditoría y amenaza**.</span><span class="sxs-lookup"><span data-stu-id="0523f-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="0523f-136"><a id="auditing-screenshot"></a>![Panel de navegación][1]</span><span class="sxs-lookup"><span data-stu-id="0523f-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="0523f-137">Si lo prefiere tooset una directiva de auditoría de servidor (que se aplicará tooall existente y las bases de datos recién creadas en este servidor), puede seleccionar hello **ver configuración del servidor** vínculo en la hoja de auditoría de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="0523f-138">A continuación, puede ver o modificar la configuración de auditoría de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="0523f-138">You can then view or modify hello server auditing settings.</span></span>

    ![Panel de navegación][2]
4. <span data-ttu-id="0523f-140">Si lo prefiere tooenable blob auditoría de nivel de base de datos de hello (en suma tooor en lugar de auditoría de nivel de servidor), para **auditoría**, seleccione **ON**y para **auditoría de tipo** , seleccione **Blob**.</span><span class="sxs-lookup"><span data-stu-id="0523f-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="0523f-141">Si está habilitada la auditoría de servidor blobs, auditoría de base de datos configurada de hello existirá paralelo con la auditoría de blob de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="0523f-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![Panel de navegación][3]
5. <span data-ttu-id="0523f-143">Hola tooopen **almacenamiento de registros de auditoría** hoja, seleccione **detalles del almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="0523f-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="0523f-144">Seleccione la cuenta de almacenamiento de Azure de Hola donde se guardarán los registros y, a continuación, seleccione el período de retención de hello, después de que Hola se eliminarán los registros antiguos.</span><span class="sxs-lookup"><span data-stu-id="0523f-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="0523f-145">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0523f-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="0523f-146">Hola tooget máximo partido de plantillas de informes de auditoría de hello, utilice Hola misma cuenta de almacenamiento para todas las bases de datos auditados.</span><span class="sxs-lookup"><span data-stu-id="0523f-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="0523f-147"><a id="storage-screenshot"></a>![Panel de navegación][4]</span><span class="sxs-lookup"><span data-stu-id="0523f-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="0523f-148">Si desea toocustomize Hola auditar eventos, puede hacerlo a través de PowerShell o API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="0523f-149">Para obtener más información, vea hello [automatización (API de REST o PowerShell)](#subheading-7) sección.</span><span class="sxs-lookup"><span data-stu-id="0523f-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="0523f-150">Después de configurar la configuración de auditoría, puede activar la nueva característica de detección de amenazas hello y configurar alertas de seguridad de mensajes de correo electrónico tooreceive.</span><span class="sxs-lookup"><span data-stu-id="0523f-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="0523f-151">Cuando se usa la detección de amenazas, se reciben alertas proactivas sobre actividades anómalas de la base de datos que pueden indicar posibles amenazas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0523f-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="0523f-152">Para obtener más detalles, vea [Introducción a la detección de amenazas](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0523f-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="0523f-153">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0523f-153">Click **Save**.</span></span>





## <span data-ttu-id="0523f-154"><a id="subheading-3"></a>Análisis de registros e informes de auditoría</span><span class="sxs-lookup"><span data-stu-id="0523f-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="0523f-155">Los registros de auditoría se agregan en hello cuenta de almacenamiento de Azure que ha elegido durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="0523f-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="0523f-156">Puede explorar los registros de auditoría con una herramienta como el [Explorador de Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0523f-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="0523f-157">Los registros de auditoría de blobs se guardan como una colección de archivos de blob dentro de un contenedor llamado **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="0523f-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="0523f-158">Para obtener más información acerca de la jerarquía de Hola de carpeta de almacenamiento de registros de auditoría de blob de hello, convenciones de nomenclatura de blob y formato de registro, vea hello [referencia del formato de registro de auditoría de Blob (descarga de archivo .docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="0523f-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="0523f-159">Hay varios métodos que puede usar registros de auditoría de blob de tooview:</span><span class="sxs-lookup"><span data-stu-id="0523f-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="0523f-160">Hola de uso [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0523f-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="0523f-161">Base de datos pertinentes de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="0523f-161">Open hello relevant database.</span></span> <span data-ttu-id="0523f-162">AT Hola superior de la base de datos de hello **detección de auditoría y amenaza** hoja, haga clic en **ver registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="0523f-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Panel de navegación][7]

    <span data-ttu-id="0523f-164">Un **registros de auditoría** se abre la hoja, desde el que podrá tooview capaz de hello registros.</span><span class="sxs-lookup"><span data-stu-id="0523f-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="0523f-165">Puede ver fechas específicas haciendo clic en **filtro** en parte superior de Hola de hello **registros de auditoría** hoja.</span><span class="sxs-lookup"><span data-stu-id="0523f-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="0523f-166">Puede cambiar entre los registros de auditoría que se crearon mediante la directiva de servidor o una directiva de base de datos de auditoría.</span><span class="sxs-lookup"><span data-stu-id="0523f-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Panel de navegación][8]

* <span data-ttu-id="0523f-168">Utilice la función de sistema de hello **sys.fn_get_audit_file** datos del registro de auditoría (T-SQL) tooreturn hello en formato tabular.</span><span class="sxs-lookup"><span data-stu-id="0523f-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="0523f-169">Para obtener más información sobre el uso de esta función, vea hello [sys.fn_get_audit_file documentación](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="0523f-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="0523f-170">Use **Combinar archivos de auditoría** en SQL Server Management Studio (a partir de SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="0523f-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="0523f-171">En el menú de SSMS hello, seleccione **archivo** > **abiertos** > **combinar archivos de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="0523f-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Panel de navegación][9]
    2. <span data-ttu-id="0523f-173">Hola **agregar archivos de auditoría** abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0523f-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="0523f-174">Seleccione uno de hello **agregar** opciones para elegir si auditoría toomerge los archivos de una variable local de disco o importarlos desde el almacenamiento de Azure (será necesario tooprovide los detalles del almacenamiento de Azure y la clave de cuenta).</span><span class="sxs-lookup"><span data-stu-id="0523f-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="0523f-175">Después de haber agregado toomerge de todos los archivos, haga clic en **Aceptar** operación de combinación de toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="0523f-176">Abre el archivo combinado de Hello en SSMS, donde puede ver y analizarlos, así como la exportación se tooan XEL o CSV archivo o tooa una tabla.</span><span class="sxs-lookup"><span data-stu-id="0523f-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="0523f-177">Hola de uso [sincronizar aplicación](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que hemos creado.</span><span class="sxs-lookup"><span data-stu-id="0523f-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="0523f-178">Se ejecuta en Azure y utiliza el análisis de registros de Operations Management Suite (OMS) pública API toopush SQL los registros de auditoría en OMS.</span><span class="sxs-lookup"><span data-stu-id="0523f-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="0523f-179">aplicación de sincronización de Hello inserta los registros de auditoría SQL en análisis de registros de OMS para su uso a través del panel de análisis de registros de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="0523f-180">Use Power BI.</span><span class="sxs-lookup"><span data-stu-id="0523f-180">Use Power BI.</span></span> <span data-ttu-id="0523f-181">Puede ver y analizar los datos de registro de auditoría en Power BI.</span><span class="sxs-lookup"><span data-stu-id="0523f-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="0523f-182">Obtenga más información sobre [Power BI y tenga acceso a una plantilla que se puede descargar](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="0523f-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="0523f-183">Descargar archivos de registro de su contenedor de blob de almacenamiento de Azure mediante el portal de Hola o mediante una herramienta como [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0523f-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="0523f-184">Después de haber descargado localmente un archivo de registro, puede hacer doble clic hello tooopen de archivo, ver y analizar los registros de hello en SSMS.</span><span class="sxs-lookup"><span data-stu-id="0523f-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="0523f-185">También puede descargar varios archivos al mismo tiempo a través del Explorador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0523f-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="0523f-186">Haga clic en una subcarpeta específica (por ejemplo, una subcarpeta que incluye todos los archivos de registro para una fecha concreta) y seleccione **Guardar como** toosave en una carpeta local.</span><span class="sxs-lookup"><span data-stu-id="0523f-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="0523f-187">Otros métodos:</span><span class="sxs-lookup"><span data-stu-id="0523f-187">Additional methods:</span></span>
   * <span data-ttu-id="0523f-188">Después de descargar varios archivos (o en una subcarpeta que incluya los archivos de registro durante un día completo, como se describe en el elemento anterior de hello en esta lista), puede combinarlos localmente como se describe en las instrucciones de los archivos de auditoría de mezcla de SSMS Hola que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0523f-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="0523f-189">Ver los registros de auditoría de blobs mediante programación:</span><span class="sxs-lookup"><span data-stu-id="0523f-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="0523f-190">Hola de uso [lector de eventos extendidos](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) biblioteca de C#.</span><span class="sxs-lookup"><span data-stu-id="0523f-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="0523f-191">[Consulta de archivos de eventos extendidos](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0523f-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="0523f-192"><a id="subheading-5"></a>Prácticas de producción</span><span class="sxs-lookup"><span data-stu-id="0523f-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="0523f-193"><a id="subheading-6">Auditoría de bases de datos con replicación geográfica</a></span><span class="sxs-lookup"><span data-stu-id="0523f-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="0523f-194">Cuando se utiliza bases de datos de replicación geográfica, es posible tooset la auditoría en la base de datos principal de hello, base de datos secundaria de hello o ambos, según el tipo de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="0523f-195">Siga estas instrucciones (Recuerde que auditoría de blobs puede estar activada o desactivada solo desde base de datos principal de hello configuración de auditoría):</span><span class="sxs-lookup"><span data-stu-id="0523f-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="0523f-196">**Base de datos principal**.</span><span class="sxs-lookup"><span data-stu-id="0523f-196">**Primary database**.</span></span> <span data-ttu-id="0523f-197">Activar la auditoría de blob, en el servidor de Hola o en hello propia base de datos, como se describe en hello [configurar la auditoría para la base de datos](#subheading-2) sección.</span><span class="sxs-lookup"><span data-stu-id="0523f-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="0523f-198">**Base de datos secundaria**.</span><span class="sxs-lookup"><span data-stu-id="0523f-198">**Secondary database**.</span></span> <span data-ttu-id="0523f-199">Activar la auditoría de blob en la base de datos principal de hello, como se describe en hello [configurar la auditoría para la base de datos](#subheading-2) sección.</span><span class="sxs-lookup"><span data-stu-id="0523f-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="0523f-200">Auditoría de blobs debe estar habilitada en hello *principal propia base de datos*, no el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="0523f-201">Después de habilita la auditoría de blobs en la base de datos principal de hello, también se habilitará en la base de datos secundaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="0523f-202">De forma predeterminada, configuración de almacenamiento de Hola de base de datos secundaria de hello será idéntico toothose de base de datos principal de hello, haciendo que el tráfico entre regional.</span><span class="sxs-lookup"><span data-stu-id="0523f-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="0523f-203">Para evitarlo, puede habilitar la auditoría de blobs en el servidor secundario de Hola y configurar el almacenamiento local en la configuración de almacenamiento del servidor secundario de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="0523f-204">Esto anulará la ubicación de almacenamiento de Hola de base de datos secundaria de Hola y el resultado en cada base de datos guardar su almacenamiento de toolocal de registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="0523f-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="0523f-205"><a id="subheading-6">Regeneración de clave de almacenamiento</a></span><span class="sxs-lookup"><span data-stu-id="0523f-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="0523f-206">En producción, es probable toorefresh el almacenamiento de claves de forma periódica.</span><span class="sxs-lookup"><span data-stu-id="0523f-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="0523f-207">Al actualizar las claves, necesita la directiva de auditoría de hello tooresave.</span><span class="sxs-lookup"><span data-stu-id="0523f-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="0523f-208">proceso de Hello es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0523f-208">hello process is as follows:</span></span>

1. <span data-ttu-id="0523f-209">Abra hello **detalles del almacenamiento** hoja.</span><span class="sxs-lookup"><span data-stu-id="0523f-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="0523f-210">Hola **clave de acceso de almacenamiento** cuadro, seleccione **secundaria**y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0523f-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="0523f-211">A continuación, haga clic en **guardar** princip Hola de hello hoja de configuración de auditoría.</span><span class="sxs-lookup"><span data-stu-id="0523f-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![Panel de navegación][5]
2. <span data-ttu-id="0523f-213">Vaya toohello hoja de configuración de almacenamiento y volver a generar clave de acceso principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="0523f-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![Panel de navegación][6]
3. <span data-ttu-id="0523f-215">Volver atrás toohello hoja de configuración de auditoría, cambiar la clave de acceso de almacenamiento de Hola de tooprimary secundario y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0523f-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="0523f-216">A continuación, haga clic en **guardar** princip Hola de hello hoja de configuración de auditoría.</span><span class="sxs-lookup"><span data-stu-id="0523f-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="0523f-217">Volver atrás toohello hoja de configuración de almacenamiento y la clave de acceso secundaria de hello Regenerar (como preparación para el ciclo de actualización de la clave siguiente hello).</span><span class="sxs-lookup"><span data-stu-id="0523f-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="0523f-218"><a id="subheading-7"></a>Automatización (PowerShell o API de REST)</span><span class="sxs-lookup"><span data-stu-id="0523f-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="0523f-219">También puede configurar la auditoría de base de datos de SQL Azure mediante el uso de hello después de herramientas de automatización:</span><span class="sxs-lookup"><span data-stu-id="0523f-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="0523f-220">**Cmdlets de PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="0523f-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="0523f-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="0523f-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="0523f-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="0523f-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="0523f-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="0523f-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="0523f-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="0523f-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="0523f-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="0523f-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="0523f-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="0523f-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="0523f-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="0523f-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="0523f-228">Para ver un script de ejemplo, consulte [Configuración de la auditoría y detección de amenazas mediante PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0523f-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="0523f-229">**API de REST: auditoría de blobs**:</span><span class="sxs-lookup"><span data-stu-id="0523f-229">**REST API - Blob auditing**:</span></span>

   * <span data-ttu-id="0523f-230">[Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx) (Creación o actualización de la directiva de auditoría de blobs de la base de datos)</span><span class="sxs-lookup"><span data-stu-id="0523f-230">[Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx)</span></span>
   * <span data-ttu-id="0523f-231">[Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx) (Creación o actualización de la directiva de audioría de blobs del servidor)</span><span class="sxs-lookup"><span data-stu-id="0523f-231">[Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx)</span></span>
   * <span data-ttu-id="0523f-232">[Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx) (Obtención de la directiva de auditoría de bobs de la base de datos)</span><span class="sxs-lookup"><span data-stu-id="0523f-232">[Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx)</span></span>
   * <span data-ttu-id="0523f-233">[Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx) (Obtención de la directiva de auditoría de blobs del servidor)</span><span class="sxs-lookup"><span data-stu-id="0523f-233">[Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx)</span></span>
   * <span data-ttu-id="0523f-234">[Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx) (Obtención de resultados de funcionamiento de la auditoría de blobs del servidor)</span><span class="sxs-lookup"><span data-stu-id="0523f-234">[Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx)</span></span>


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy

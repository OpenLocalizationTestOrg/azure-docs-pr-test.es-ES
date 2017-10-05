---
title: "Introducción a la auditoría de Azure SQL Database | Microsoft Docs"
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
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="687d8-103">Introducción a la auditoría de bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="687d8-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="687d8-104">La auditoría de base de datos SQL de Azure realiza el seguimiento de eventos de base de datos y los registra en un registro de auditoría de la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="687d8-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="687d8-105">La auditoría también:</span><span class="sxs-lookup"><span data-stu-id="687d8-105">Auditing also:</span></span>

* <span data-ttu-id="687d8-106">Puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas.</span><span class="sxs-lookup"><span data-stu-id="687d8-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="687d8-107">Posibilita y facilita la observancia de estándares reguladores aunque no garantiza el cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="687d8-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="687d8-108">Para obtener más información acerca de los programas de Azure compatibles con la observancia de estándares, consulte el [Centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="687d8-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="687d8-109"><a id="subheading-1"></a>Información general de auditoría de base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="687d8-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="687d8-110">Puede usar la auditoría de base de datos SQL para:</span><span class="sxs-lookup"><span data-stu-id="687d8-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="687d8-111">**Conservar** una traza de auditoría de eventos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="687d8-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="687d8-112">Puede definir categorías de acciones de base de datos para auditar.</span><span class="sxs-lookup"><span data-stu-id="687d8-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="687d8-113">**Informar** sobre la actividad de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="687d8-113">**Report** on database activity.</span></span> <span data-ttu-id="687d8-114">Puede usar informes preconfigurados y un panel para empezar rápidamente con el informe de actividades y eventos.</span><span class="sxs-lookup"><span data-stu-id="687d8-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="687d8-115">**Analizar** informes.</span><span class="sxs-lookup"><span data-stu-id="687d8-115">**Analyze** reports.</span></span> <span data-ttu-id="687d8-116">Puede buscar eventos sospechosos, actividades inusuales y tendencias.</span><span class="sxs-lookup"><span data-stu-id="687d8-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="687d8-117">Puede configurar la auditoría para diferentes tipos de categorías de eventos, como se explica en la sección [Configuración de la auditoría para su base de datos](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="687d8-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="687d8-118">Los registros de auditoría se escriben en Azure Blob Storage en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="687d8-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="687d8-119"><a id="subheading-8"></a>Definir la directiva de auditoría de nivel de servidor frente la de nivel de base de datos</span><span class="sxs-lookup"><span data-stu-id="687d8-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="687d8-120">Puede definirse una directiva de auditoría para una base de datos específica o como directiva de servidor predeterminada:</span><span class="sxs-lookup"><span data-stu-id="687d8-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="687d8-121">Una directiva de servidor se aplica a todas las bases de datos recién creadas en el servidor.</span><span class="sxs-lookup"><span data-stu-id="687d8-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="687d8-122">Si *está habilitada la auditoría de blobs de servidor*, *siempre se aplica a la base de datos* (es decir, la base de datos se va a auditar), sin tener en cuenta la configuración de auditoría de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="687d8-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="687d8-123">Habilitar la auditoría de blobs en la base de datos, además de en el servidor, *no* invalidará ni cambiará ninguna de las opciones de la auditoría del servidor de blobs.</span><span class="sxs-lookup"><span data-stu-id="687d8-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="687d8-124">Ambas auditorías existirán en paralelo.</span><span class="sxs-lookup"><span data-stu-id="687d8-124">Both audits will exist side by side.</span></span> <span data-ttu-id="687d8-125">En otras palabras, la base de datos se auditará dos veces en paralelo (una vez por la directiva de servidor y otra vez por la directiva de base de datos).</span><span class="sxs-lookup"><span data-stu-id="687d8-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="687d8-126">Debe habilitar tanto la auditoría de blobs de servidor como la auditoría de blobs de base de datos, a menos que:</span><span class="sxs-lookup"><span data-stu-id="687d8-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="687d8-127">Quiera usar una *cuenta de almacenamiento* o un *período de retención* diferentes para una base de datos específica.</span><span class="sxs-lookup"><span data-stu-id="687d8-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="687d8-128">Quiera auditar tipos de eventos o categorías para una base de datos específica que difieren de los tipos de eventos o categorías que se están auditando para el resto de las bases de datos del servidor.</span><span class="sxs-lookup"><span data-stu-id="687d8-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="687d8-129">Por ejemplo, es posible que tenga inserciones de tabla que solo tengan que deban auditarse para una base de datos concreta.</span><span class="sxs-lookup"><span data-stu-id="687d8-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="687d8-130">En caso contrario, se recomienda habilitar solo la auditoría de blobs de nivel de servidor y dejar que la auditoría de nivel de base de datos esté deshabilitada para todas las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="687d8-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="687d8-131"><a id="subheading-2"></a>Configuración de la auditoría para su base de datos</span><span class="sxs-lookup"><span data-stu-id="687d8-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="687d8-132">En la sección siguiente se describe la configuración de auditoría mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="687d8-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="687d8-133">Vaya al [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="687d8-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="687d8-134">Vaya a la hoja **Configuración** de la base de datos SQL o el servidor SQL que quiere auditar.</span><span class="sxs-lookup"><span data-stu-id="687d8-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="687d8-135">En la hoja **Configuración**, seleccione **Auditoría y detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="687d8-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="687d8-136"><a id="auditing-screenshot"></a>![Panel de navegación][1]</span><span class="sxs-lookup"><span data-stu-id="687d8-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="687d8-137">Si quiere configurar una directiva de auditoría del servidor (que se aplicará a todas las bases de datos recién creadas y existentes en este servidor), puede seleccionar el vínculo **Ver configuración del servidor** en la hoja de la auditoría de base de datos.</span><span class="sxs-lookup"><span data-stu-id="687d8-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="687d8-138">Después, puede ver o modificar la configuración de auditoría del servidor.</span><span class="sxs-lookup"><span data-stu-id="687d8-138">You can then view or modify the server auditing settings.</span></span>

    ![Panel de navegación][2]
4. <span data-ttu-id="687d8-140">Si prefiere habilitar la auditoría de blobs en el nivel de la base de datos (además o en lugar de la auditoría a nivel de servidor), para **Auditoría**, seleccione **Activado** y para **Tipo de auditoría**, seleccione **Blob**.</span><span class="sxs-lookup"><span data-stu-id="687d8-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="687d8-141">Si está habilitada la auditoría de blobs del servidor, la auditoría configurada de base de datos se producirá de forma paralela a la auditoría de blobs del servidor.</span><span class="sxs-lookup"><span data-stu-id="687d8-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![Panel de navegación][3]
5. <span data-ttu-id="687d8-143">Para abrir la hoja **Almacenamiento de registros de auditoría**, seleccione **Detalles de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="687d8-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="687d8-144">Seleccione la cuenta de Azure Storage donde se guardarán los registros, y el período de retención, después del cual los registros antiguos se eliminarán.</span><span class="sxs-lookup"><span data-stu-id="687d8-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="687d8-145">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="687d8-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="687d8-146">Con el fin de obtener el máximo rendimiento de las plantillas de informes de auditorías, use la misma cuenta de almacenamiento para todas las bases de datos auditadas.</span><span class="sxs-lookup"><span data-stu-id="687d8-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="687d8-147"><a id="storage-screenshot"></a>![Panel de navegación][4]</span><span class="sxs-lookup"><span data-stu-id="687d8-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="687d8-148">Si quiere personalizar los eventos auditados, puede hacerlo a través de PowerShell o de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="687d8-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="687d8-149">Para obtener más información, vea la sección [Automatización (API de REST o PowerShell)](#subheading-7).</span><span class="sxs-lookup"><span data-stu-id="687d8-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="687d8-150">Después de configurar los valores de auditoría, puede activar la nueva característica de detección de amenazas y configurar los mensajes de correo para recibir alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="687d8-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="687d8-151">Cuando se usa la detección de amenazas, se reciben alertas proactivas sobre actividades anómalas de la base de datos que pueden indicar posibles amenazas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="687d8-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="687d8-152">Para obtener más detalles, vea [Introducción a la detección de amenazas](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="687d8-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="687d8-153">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="687d8-153">Click **Save**.</span></span>





## <span data-ttu-id="687d8-154"><a id="subheading-3"></a>Análisis de registros e informes de auditoría</span><span class="sxs-lookup"><span data-stu-id="687d8-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="687d8-155">Los registros de auditoría se agregan a la cuenta de almacenamiento de Azure que eligió durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="687d8-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="687d8-156">Puede explorar los registros de auditoría con una herramienta como el [Explorador de Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="687d8-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="687d8-157">Los registros de auditoría de blobs se guardan como una colección de archivos de blob dentro de un contenedor llamado **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="687d8-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="687d8-158">Para obtener más información sobre la jerarquía de las carpetas de almacenamiento de registros de auditoría de blobs, las convenciones de nomenclatura y el formato del registro, vea la [referencia del formato de registro de auditoría de blobs (descarga del archivo de documento)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="687d8-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="687d8-159">Existen varios métodos que puede usar para ver los registros de auditoría de blobs:</span><span class="sxs-lookup"><span data-stu-id="687d8-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="687d8-160">Usar [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="687d8-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="687d8-161">Abra la base de datos pertinente.</span><span class="sxs-lookup"><span data-stu-id="687d8-161">Open the relevant database.</span></span> <span data-ttu-id="687d8-162">En la parte superior de la hoja **Auditoría y detección de amenazas** de la base de datos, haga clic en **Ver registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="687d8-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Panel de navegación][7]

    <span data-ttu-id="687d8-164">Se abre una hoja **Registros de auditoría**, desde la que podrá ver los registros.</span><span class="sxs-lookup"><span data-stu-id="687d8-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="687d8-165">Puede elegir ver fechas específicas si hace clic en **Filtrar** en la parte superior de la hoja **Registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="687d8-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="687d8-166">Puede cambiar entre los registros de auditoría que se crearon mediante la directiva de servidor o una directiva de base de datos de auditoría.</span><span class="sxs-lookup"><span data-stu-id="687d8-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Panel de navegación][8]

* <span data-ttu-id="687d8-168">Use la función del sistema **sys.fn_get_audit_file** (T-SQL) para devolver los datos de registro de auditoría en formato tabular.</span><span class="sxs-lookup"><span data-stu-id="687d8-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="687d8-169">Para más información sobre el uso de esta función, vea la [documentación de sys.fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="687d8-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="687d8-170">Use **Combinar archivos de auditoría** en SQL Server Management Studio (a partir de SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="687d8-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="687d8-171">En el menú SSMS, seleccione **Archivo** > **Abrir** > **Combinar archivos de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="687d8-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Panel de navegación][9]
    2. <span data-ttu-id="687d8-173">Se abre el cuadro de diálogo **Agregar archivos de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="687d8-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="687d8-174">Seleccione una de las opciones **Agregar** para elegir si quiere combinar los archivos de auditoría desde un disco local o importarlos desde Azure Storage (se le pedirá que proporcione los detalles y la clave de cuenta de Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="687d8-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="687d8-175">Una vez agregados todos los archivos que se van a combinar, haga clic en **Aceptar** para completar la operación de combinación.</span><span class="sxs-lookup"><span data-stu-id="687d8-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="687d8-176">El archivo combinado se abre en SSMS, donde puede verlo y analizarlo, y también exportarlo a un archivo XEL o CSV, o a una tabla.</span><span class="sxs-lookup"><span data-stu-id="687d8-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="687d8-177">Use la [aplicación de sincronización](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que hemos creado.</span><span class="sxs-lookup"><span data-stu-id="687d8-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="687d8-178">Se ejecuta en Azure y usa las API públicas de Log Analytics de Operations Management Suite (OMS) para insertar los registros de auditoría SQL en OMS.</span><span class="sxs-lookup"><span data-stu-id="687d8-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="687d8-179">La aplicación de sincronización inserta los registros de auditoría SQL en Log Analytics de OMS para su consumo mediante el panel de Log Analytics de OMS.</span><span class="sxs-lookup"><span data-stu-id="687d8-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="687d8-180">Use Power BI.</span><span class="sxs-lookup"><span data-stu-id="687d8-180">Use Power BI.</span></span> <span data-ttu-id="687d8-181">Puede ver y analizar los datos de registro de auditoría en Power BI.</span><span class="sxs-lookup"><span data-stu-id="687d8-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="687d8-182">Obtenga más información sobre [Power BI y tenga acceso a una plantilla que se puede descargar](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="687d8-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="687d8-183">Descargue los archivos de registro del contenedor de blobs de Azure Storage mediante el portal o con una herramienta como el [Explorador de Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="687d8-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="687d8-184">Después de descargar localmente un archivo de registro, puede hacer doble clic en él para abrir, ver y analizar los registros en SSMS.</span><span class="sxs-lookup"><span data-stu-id="687d8-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="687d8-185">También puede descargar varios archivos al mismo tiempo a través del Explorador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="687d8-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="687d8-186">Haga clic con el botón derecho en una subcarpeta específica (por ejemplo, una que incluya todos los archivos de registro para una fecha concreta) y seleccione **Guardar como** para guardar en una carpeta local.</span><span class="sxs-lookup"><span data-stu-id="687d8-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="687d8-187">Otros métodos:</span><span class="sxs-lookup"><span data-stu-id="687d8-187">Additional methods:</span></span>
   * <span data-ttu-id="687d8-188">Después de descargar varios archivos (o una subcarpeta que incluya los archivos de registro de un día completo, tal como se describe en el elemento anterior de esta lista), puede combinarlos localmente como se describe en las instrucciones anteriores para combinar archivos de auditoría de SSMS.</span><span class="sxs-lookup"><span data-stu-id="687d8-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="687d8-189">Ver los registros de auditoría de blobs mediante programación:</span><span class="sxs-lookup"><span data-stu-id="687d8-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="687d8-190">Use la biblioteca de C# de [lector de eventos extendidos](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/).</span><span class="sxs-lookup"><span data-stu-id="687d8-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="687d8-191">[Consulta de archivos de eventos extendidos](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="687d8-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="687d8-192"><a id="subheading-5"></a>Prácticas de producción</span><span class="sxs-lookup"><span data-stu-id="687d8-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="687d8-193"><a id="subheading-6">Auditoría de bases de datos con replicación geográfica</a></span><span class="sxs-lookup"><span data-stu-id="687d8-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="687d8-194">Cuando se usan bases de datos con replicación geográfica, es posible configurar la auditoría en la base de datos principal, la base de datos secundaria, o ambas, según el tipo de auditoría.</span><span class="sxs-lookup"><span data-stu-id="687d8-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="687d8-195">Siga estas instrucciones (recuerde que la auditoría de blobs solo se puede activar o desactivar desde la configuración de auditoría de la base de datos principal):</span><span class="sxs-lookup"><span data-stu-id="687d8-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="687d8-196">**Base de datos principal**.</span><span class="sxs-lookup"><span data-stu-id="687d8-196">**Primary database**.</span></span> <span data-ttu-id="687d8-197">Active la auditoría de blobs en el servidor o en la propia base de datos, como se describe en la sección [Configuración de la auditoría para su base de datos](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="687d8-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="687d8-198">**Base de datos secundaria**.</span><span class="sxs-lookup"><span data-stu-id="687d8-198">**Secondary database**.</span></span> <span data-ttu-id="687d8-199">Active la auditoría de blobs en la base de datos principal, como se describe en la sección [Configuración de la auditoría para su base de datos](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="687d8-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="687d8-200">La auditoría de blobs debe estar habilitada en la *propia base de datos principal*, no en el servidor.</span><span class="sxs-lookup"><span data-stu-id="687d8-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="687d8-201">Después de habilitar la auditoría de blobs en la base de datos principal, también se habilitará en la base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="687d8-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="687d8-202">De forma predeterminada, la configuración de almacenamiento de la base de datos secundaria será idéntica a la de la base de datos principal, lo que provocará tráfico interregional.</span><span class="sxs-lookup"><span data-stu-id="687d8-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="687d8-203">Para evitarlo, puede habilitar la auditoría de blobs en el servidor secundario y configurar el almacenamiento local en la configuración de almacenamiento del servidor secundario.</span><span class="sxs-lookup"><span data-stu-id="687d8-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="687d8-204">Esto anulará la ubicación de almacenamiento para la base de datos secundaria y, como resultado, cada base de datos guardará sus registros de auditoría en el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="687d8-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="687d8-205"><a id="subheading-6">Regeneración de clave de almacenamiento</a></span><span class="sxs-lookup"><span data-stu-id="687d8-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="687d8-206">En el entorno de producción, es probable que actualice periódicamente las claves de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="687d8-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="687d8-207">Al actualizar las claves se debe volver a guardar la directiva de auditoría.</span><span class="sxs-lookup"><span data-stu-id="687d8-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="687d8-208">El proceso es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="687d8-208">The process is as follows:</span></span>

1. <span data-ttu-id="687d8-209">Abra la hoja **Detalles de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="687d8-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="687d8-210">En el cuadro **Clave de acceso de almacenamiento**, seleccione **Secundaria** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="687d8-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="687d8-211">Después, haga clic en **Guardar** en la parte superior de la hoja de configuración de auditoría.</span><span class="sxs-lookup"><span data-stu-id="687d8-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Panel de navegación][5]
2. <span data-ttu-id="687d8-213">Vaya a la hoja de configuración de almacenamiento y vuelva a generar la clave de acceso primaria.</span><span class="sxs-lookup"><span data-stu-id="687d8-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Panel de navegación][6]
3. <span data-ttu-id="687d8-215">Vuelva a la hoja de configuración de auditoría, cambie el valor de la clave de acceso de almacenamiento de Secundaria a Principal y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="687d8-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="687d8-216">Después, haga clic en **Guardar** en la parte superior de la hoja de configuración de auditoría.</span><span class="sxs-lookup"><span data-stu-id="687d8-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="687d8-217">Vuelva a la hoja de configuración de almacenamiento y vuelva a generar la clave de acceso secundaria (como preparación para el siguiente ciclo de actualización de claves).</span><span class="sxs-lookup"><span data-stu-id="687d8-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="687d8-218"><a id="subheading-7"></a>Automatización (PowerShell o API de REST)</span><span class="sxs-lookup"><span data-stu-id="687d8-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="687d8-219">También puede configurar la auditoría en Azure SQL Database mediante las siguientes herramientas de automatización:</span><span class="sxs-lookup"><span data-stu-id="687d8-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="687d8-220">**Cmdlets de PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="687d8-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="687d8-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="687d8-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="687d8-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="687d8-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="687d8-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="687d8-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="687d8-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="687d8-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="687d8-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="687d8-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="687d8-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="687d8-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="687d8-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="687d8-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="687d8-228">Para ver un script de ejemplo, consulte [Configuración de la auditoría y detección de amenazas mediante PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="687d8-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="687d8-229">**API de REST: auditoría de blobs**:</span><span class="sxs-lookup"><span data-stu-id="687d8-229">**REST API - Blob auditing**:</span></span>

   * <span data-ttu-id="687d8-230">[Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx) (Creación o actualización de la directiva de auditoría de blobs de la base de datos)</span><span class="sxs-lookup"><span data-stu-id="687d8-230">[Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx)</span></span>
   * <span data-ttu-id="687d8-231">[Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx) (Creación o actualización de la directiva de audioría de blobs del servidor)</span><span class="sxs-lookup"><span data-stu-id="687d8-231">[Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx)</span></span>
   * <span data-ttu-id="687d8-232">[Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx) (Obtención de la directiva de auditoría de bobs de la base de datos)</span><span class="sxs-lookup"><span data-stu-id="687d8-232">[Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx)</span></span>
   * <span data-ttu-id="687d8-233">[Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx) (Obtención de la directiva de auditoría de blobs del servidor)</span><span class="sxs-lookup"><span data-stu-id="687d8-233">[Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx)</span></span>
   * <span data-ttu-id="687d8-234">[Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx) (Obtención de resultados de funcionamiento de la auditoría de blobs del servidor)</span><span class="sxs-lookup"><span data-stu-id="687d8-234">[Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx)</span></span>


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

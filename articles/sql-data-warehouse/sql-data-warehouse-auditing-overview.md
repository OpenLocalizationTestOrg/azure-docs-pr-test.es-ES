---
title: "Auditoría en Azure SQL Data Warehouse | Microsoft Docs"
description: "Introducción a la auditoría en Almacenamiento de datos SQL de Azure"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: f851c82ebeaa647f663d499a4d327c3479e36121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="4910c-103">Auditoría en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="4910c-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4910c-104">Auditoría</span><span class="sxs-lookup"><span data-stu-id="4910c-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="4910c-105">Detección de amenazas</span><span class="sxs-lookup"><span data-stu-id="4910c-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="4910c-106">La auditoría de SQL Data Warehouse permite grabar los eventos de la base de datos en un registro de auditoría de una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4910c-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="4910c-107">La auditoría puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas.</span><span class="sxs-lookup"><span data-stu-id="4910c-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="4910c-108">La auditoría de SQL Data Warehouse también se integra con Microsoft Power BI, con el fin de facilitar la generación de análisis e informes detallados.</span><span class="sxs-lookup"><span data-stu-id="4910c-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="4910c-109">Las herramientas de auditoría posibilitan y facilitan la observancia de estándares reguladores pero no garantizan el cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="4910c-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="4910c-110">Para obtener más información acerca de los programas de Azure compatibles con el cumplimiento de estándares, consulte el <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Centro de confianza de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="4910c-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="4910c-111">[Conceptos básicos de auditoría de Base de datos]</span><span class="sxs-lookup"><span data-stu-id="4910c-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="4910c-112">[Configuración de la auditoría para su base de datos]</span><span class="sxs-lookup"><span data-stu-id="4910c-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="4910c-113">[Análisis de registros e informes de auditoría]</span><span class="sxs-lookup"><span data-stu-id="4910c-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="4910c-114"><a id="subheading-1"></a>Conceptos básicos de auditoría de Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="4910c-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="4910c-115">La auditoría de Almacenamiento de datos SQL la permite que:</span><span class="sxs-lookup"><span data-stu-id="4910c-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="4910c-116">**Conservar** una traza de auditoría de eventos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="4910c-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="4910c-117">Puede definir categorías de acciones de base de datos para auditar.</span><span class="sxs-lookup"><span data-stu-id="4910c-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="4910c-118">**Informar** sobre la actividad de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="4910c-118">**Report** on database activity.</span></span> <span data-ttu-id="4910c-119">Puede usar informes preconfigurados y un panel para empezar rápidamente con el informe de actividades y eventos.</span><span class="sxs-lookup"><span data-stu-id="4910c-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="4910c-120">**Analizar** informes.</span><span class="sxs-lookup"><span data-stu-id="4910c-120">**Analyze** reports.</span></span> <span data-ttu-id="4910c-121">Puede buscar eventos sospechosos, actividades inusuales y tendencias.</span><span class="sxs-lookup"><span data-stu-id="4910c-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="4910c-122">Puede configurar la auditoría para las categorías de eventos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4910c-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="4910c-123">**SQL sin formato** y **SQL parametrizado** para los que los registros de auditoría recopilados se clasifican como</span><span class="sxs-lookup"><span data-stu-id="4910c-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="4910c-124">**Acceso a datos**</span><span class="sxs-lookup"><span data-stu-id="4910c-124">**Access to data**</span></span>
* <span data-ttu-id="4910c-125">**Cambios de esquema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="4910c-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="4910c-126">**Cambios de datos (DML)**</span><span class="sxs-lookup"><span data-stu-id="4910c-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="4910c-127">**Cuentas, roles y permisos (DCL)**</span><span class="sxs-lookup"><span data-stu-id="4910c-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="4910c-128">**Procedimiento almacenado**, **Inicio de sesión** y **Administración de transacciones**.</span><span class="sxs-lookup"><span data-stu-id="4910c-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="4910c-129">Para cada categoría de eventos, las operaciones de **aciertos** y **errores** se configuran por separado.</span><span class="sxs-lookup"><span data-stu-id="4910c-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="4910c-130">Para más información acerca de las actividades y eventos auditados, consulte la <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Referencia de formato del registro de auditoría (descarga de archivo .doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="4910c-130">For more information about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="4910c-131">Los registros de auditoría se almacenan en su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4910c-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="4910c-132">Puede definir un período de retención de registro de auditoría.</span><span class="sxs-lookup"><span data-stu-id="4910c-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="4910c-133">Puede definirse una directiva de auditoría para una base de datos específica o como directiva de servidor predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4910c-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="4910c-134">La directiva de auditoría de servidor predeterminada se aplica a todas las bases de datos de un servidor que no tengan una directiva de auditoría de base de datos de reemplazo específica definida.</span><span class="sxs-lookup"><span data-stu-id="4910c-134">A default server auditing policy applies to all databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="4910c-135">Antes de configurar la auditoría, compruebe si usa un ["Cliente de nivel inferior"](sql-data-warehouse-auditing-downlevel-clients.md)</span><span class="sxs-lookup"><span data-stu-id="4910c-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="4910c-136"><a id="subheading-2"></a>Configuración de la auditoría para su base de datos</span><span class="sxs-lookup"><span data-stu-id="4910c-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="4910c-137">Inicie <a href="https://portal.azure.com" target="_blank">Azure Portal</a>.</span><span class="sxs-lookup"><span data-stu-id="4910c-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="4910c-138">Vaya a la hoja **Configuración** de la instancia de SQL Data Warehouse que quiere auditar.</span><span class="sxs-lookup"><span data-stu-id="4910c-138">Go to the **Settings** blade of the SQL Data Warehouse you want to audit.</span></span> <span data-ttu-id="4910c-139">En la hoja **Configuración**, seleccione **Auditoría y detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="4910c-139">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="4910c-140">A continuación, para habilitar la auditoría, haga clic en el botón **ACTIVADO** .</span><span class="sxs-lookup"><span data-stu-id="4910c-140">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="4910c-141">En la hoja de configuración de auditoría, seleccione **DETALLES DE ALMACENAMIENTO** para abrir la hoja Almacenamiento de registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="4910c-141">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage blade.</span></span> <span data-ttu-id="4910c-142">Seleccione la cuenta de almacenamiento de Azure donde se guardarán los registros y el período de retención.</span><span class="sxs-lookup"><span data-stu-id="4910c-142">Select the Azure storage account where logs will be saved and, the retention period.</span></span> 
>[!TIP]
><span data-ttu-id="4910c-143">Use la misma cuenta de almacenamiento para todas las bases de datos auditadas con el fin de obtener el máximo rendimiento de las plantillas de informes preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="4910c-143">Use the same storage account for all audited databases to get the most out of the pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="4910c-144">Haga clic en el botón **Aceptar** para guardar los detalles de configuración de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4910c-144">Click the **OK** button to save the storage details configuration.</span></span>
6. <span data-ttu-id="4910c-145">En **REGISTRO POR EVENTO**, haga clic en **CORRECTO** y **ERROR** para registrar todos los eventos, o elija categorías individuales de eventos.</span><span class="sxs-lookup"><span data-stu-id="4910c-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="4910c-146">Si va a configurar la auditoría para una base de datos, puede que tenga que modificar la cadena de conexión del cliente para asegurarse de que los datos de auditoría se capturan correctamente.</span><span class="sxs-lookup"><span data-stu-id="4910c-146">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="4910c-147">Consulte el tema [Modificación del FDQN de servidor en la cadena de conexión](sql-data-warehouse-auditing-downlevel-clients.md) sobre conexiones de cliente de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="4910c-147">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="4910c-148">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4910c-148">Click **OK**.</span></span>

## <span data-ttu-id="4910c-149"><a id="subheading-3"></a>Análisis de registros e informes de auditoría</span><span class="sxs-lookup"><span data-stu-id="4910c-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="4910c-150">Los registros de auditoría se agregan en una recopilación de tablas de Almacenamiento con el prefijo **SQLDBAuditLogs** en la cuenta de almacenamiento de Azure que eligió durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="4910c-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="4910c-151">Puede ver los archivos de registro usando una herramienta como el <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Explorador de almacenamiento de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="4910c-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="4910c-152">Hay una plantilla de informe de panel preconfigurada disponible como <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">hoja de cálculo de Excel descargable</a> para ayudarle a analizar datos de registro rápidamente.</span><span class="sxs-lookup"><span data-stu-id="4910c-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="4910c-153">Para utilizar la plantilla en los registros de auditoría, necesita Excel 2013 o posterior y Power Query, que puede descargar <a href="http://www.microsoft.com/download/details.aspx?id=39379">aquí</a>.</span><span class="sxs-lookup"><span data-stu-id="4910c-153">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="4910c-154">La plantilla contiene datos de ejemplo ficticios y puede configurar Power Query para importar el registro de auditoría directamente desde la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4910c-154">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="4910c-155"><a id="subheading-4"></a>Regeneración de clave de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4910c-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="4910c-156">En el entorno de producción, es probable que actualice periódicamente las claves de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4910c-156">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="4910c-157">Cuando actualice las claves, debe volver a guardar la directiva.</span><span class="sxs-lookup"><span data-stu-id="4910c-157">When refreshing your keys, you need to save the policy.</span></span> <span data-ttu-id="4910c-158">El proceso es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="4910c-158">The process is as follows:</span></span>

1. <span data-ttu-id="4910c-159">En la hoja de configuración de auditoría (descrita anteriormente en la sección de configuración de auditoría), cambie la **Clave de acceso de almacenamiento** de *Principal* a *Secundaria* y haga clic en **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="4910c-159">In the auditing configuration blade (described above in the setup auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="4910c-160">Vaya a la hoja de configuración de almacenamiento y **regenere** la *Clave de acceso primaria*.</span><span class="sxs-lookup"><span data-stu-id="4910c-160">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="4910c-161">Vuelva a la hoja de configuración de auditoría, cambie el valor de **Clave de acceso de almacenamiento** de *Secundaria* a *Principal* y presione **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="4910c-161">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="4910c-162">Vuelva a la interfaz de usuario de almacenamiento y **regenere** la *Clave de acceso secundaria* (como preparación para el siguiente ciclo de actualización de las claves).</span><span class="sxs-lookup"><span data-stu-id="4910c-162">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <span data-ttu-id="4910c-163"><a id="subheading-5"></a>Automatización (PowerShell o API de REST)</span><span class="sxs-lookup"><span data-stu-id="4910c-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="4910c-164">También puede configurar la auditoría en Azure SQL Data Warehouse mediante las siguientes herramientas de automatización:</span><span class="sxs-lookup"><span data-stu-id="4910c-164">You can also configure auditing in Azure SQL Data Warehouse by using the following automation tools:</span></span>

* <span data-ttu-id="4910c-165">**Cmdlets de PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="4910c-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="4910c-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="4910c-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="4910c-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="4910c-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="4910c-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="4910c-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="4910c-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="4910c-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="4910c-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="4910c-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="4910c-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="4910c-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="4910c-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="4910c-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[Conceptos básicos de auditoría de Base de datos]: #subheading-1
[Configuración de la auditoría para su base de datos]: #subheading-2
[Análisis de registros e informes de auditoría]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
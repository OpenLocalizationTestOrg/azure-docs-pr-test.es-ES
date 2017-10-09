---
title: "aaaAuditing en el almacén de datos de SQL de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="27a0f-103">Auditoría en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="27a0f-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27a0f-104">Auditoría</span><span class="sxs-lookup"><span data-stu-id="27a0f-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="27a0f-105">Detección de amenazas</span><span class="sxs-lookup"><span data-stu-id="27a0f-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="27a0f-106">Auditoría de almacenamiento de datos SQL permite toorecord eventos en el registro de auditoría de base de datos tooan en su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="27a0f-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="27a0f-107">La auditoría puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas.</span><span class="sxs-lookup"><span data-stu-id="27a0f-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="27a0f-108">La auditoría de SQL Data Warehouse también se integra con Microsoft Power BI, con el fin de facilitar la generación de análisis e informes detallados.</span><span class="sxs-lookup"><span data-stu-id="27a0f-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="27a0f-109">Las herramientas de auditoría habilitan y facilitan estándares de cumplimiento toocompliance pero no garantizan el cumplimiento de normas.</span><span class="sxs-lookup"><span data-stu-id="27a0f-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="27a0f-110">Para obtener más información sobre Azure programas ese cumplimiento de estándares de soporte técnico, consulte hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">centro de confianza de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="27a0f-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="27a0f-111">[Conceptos básicos de auditoría de Base de datos]</span><span class="sxs-lookup"><span data-stu-id="27a0f-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="27a0f-112">[Configuración de la auditoría para su base de datos]</span><span class="sxs-lookup"><span data-stu-id="27a0f-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="27a0f-113">[Análisis de registros e informes de auditoría]</span><span class="sxs-lookup"><span data-stu-id="27a0f-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="27a0f-114"><a id="subheading-1"></a>Conceptos básicos de auditoría de Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="27a0f-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="27a0f-115">La auditoría de Almacenamiento de datos SQL la permite que:</span><span class="sxs-lookup"><span data-stu-id="27a0f-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="27a0f-116">**Conservar** una traza de auditoría de eventos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="27a0f-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="27a0f-117">Puede definir categorías de base de datos acciones toobe auditado.</span><span class="sxs-lookup"><span data-stu-id="27a0f-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="27a0f-118">**Informar** sobre la actividad de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="27a0f-118">**Report** on database activity.</span></span> <span data-ttu-id="27a0f-119">Puede usar los informes preconfigurados y un tooget de panel a trabajar rápidamente con actividad y los informes de eventos.</span><span class="sxs-lookup"><span data-stu-id="27a0f-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="27a0f-120">**Analizar** informes.</span><span class="sxs-lookup"><span data-stu-id="27a0f-120">**Analyze** reports.</span></span> <span data-ttu-id="27a0f-121">Puede buscar eventos sospechosos, actividades inusuales y tendencias.</span><span class="sxs-lookup"><span data-stu-id="27a0f-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="27a0f-122">Puede configurar la auditoría para hello siguientes categorías de eventos:</span><span class="sxs-lookup"><span data-stu-id="27a0f-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="27a0f-123">**Sin formato SQL** y **SQL parametrizadas** para qué hello los registros de auditoría recopilados se clasifican como</span><span class="sxs-lookup"><span data-stu-id="27a0f-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="27a0f-124">**Toodata de acceso**</span><span class="sxs-lookup"><span data-stu-id="27a0f-124">**Access toodata**</span></span>
* <span data-ttu-id="27a0f-125">**Cambios de esquema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="27a0f-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="27a0f-126">**Cambios de datos (DML)**</span><span class="sxs-lookup"><span data-stu-id="27a0f-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="27a0f-127">**Cuentas, roles y permisos (DCL)**</span><span class="sxs-lookup"><span data-stu-id="27a0f-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="27a0f-128">**Procedimiento almacenado**, **Inicio de sesión** y **Administración de transacciones**.</span><span class="sxs-lookup"><span data-stu-id="27a0f-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="27a0f-129">Para cada categoría de eventos, las operaciones de **aciertos** y **errores** se configuran por separado.</span><span class="sxs-lookup"><span data-stu-id="27a0f-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="27a0f-130">Para obtener más información acerca de las actividades de Hola y auditados los eventos, vea hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">referencia de formato de registro de auditoría (descarga de los archivos doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="27a0f-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="27a0f-131">Los registros de auditoría se almacenan en su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="27a0f-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="27a0f-132">Puede definir un período de retención de registro de auditoría.</span><span class="sxs-lookup"><span data-stu-id="27a0f-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="27a0f-133">Puede definirse una directiva de auditoría para una base de datos específica o como directiva de servidor predeterminada.</span><span class="sxs-lookup"><span data-stu-id="27a0f-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="27a0f-134">Una directiva de auditoría de servidor predeterminada aplica a las bases de datos de tooall en un servidor, que no tienen una reemplazo base de datos auditoría directiva específica definida.</span><span class="sxs-lookup"><span data-stu-id="27a0f-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="27a0f-135">Antes de configurar la auditoría, compruebe si usa un ["Cliente de nivel inferior"](sql-data-warehouse-auditing-downlevel-clients.md)</span><span class="sxs-lookup"><span data-stu-id="27a0f-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="27a0f-136"><a id="subheading-2"></a>Configuración de la auditoría para su base de datos</span><span class="sxs-lookup"><span data-stu-id="27a0f-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="27a0f-137">Iniciar hello <a href="https://portal.azure.com" target="_blank">portal de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="27a0f-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="27a0f-138">Vaya toohello **configuración** hoja de hello desea tooaudit de almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="27a0f-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="27a0f-139">Hola **configuración** hoja, seleccione **detección de auditoría y amenaza**.</span><span class="sxs-lookup"><span data-stu-id="27a0f-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="27a0f-140">A continuación, habilitar la auditoría, haga clic en hello **ON** botón.</span><span class="sxs-lookup"><span data-stu-id="27a0f-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="27a0f-141">En la hoja de configuración de auditoría de hello, seleccione **detalles del almacenamiento** hoja de almacenamiento de registros de auditoría de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="27a0f-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="27a0f-142">Seleccione Hola donde se guardará los registros de cuenta de almacenamiento de Azure, hello y período de retención.</span><span class="sxs-lookup"><span data-stu-id="27a0f-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="27a0f-143">Hola uso preconfigurada de la misma cuenta de almacenamiento para todas las bases de datos auditados tooget Hola máximo partido de hello informa de plantillas.</span><span class="sxs-lookup"><span data-stu-id="27a0f-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="27a0f-144">Haga clic en hello **Aceptar** botón toosave Hola almacenamiento detalles de configuración.</span><span class="sxs-lookup"><span data-stu-id="27a0f-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="27a0f-145">En **registro por evento**, haga clic en **correcto** y **error** toolog todos los eventos, o elegir categorías de eventos individuales.</span><span class="sxs-lookup"><span data-stu-id="27a0f-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="27a0f-146">Si va a configurar la auditoría para una base de datos, debe cadena de conexión de hello tooalter de su tooensure cliente auditoría de datos se ha capturado correctamente.</span><span class="sxs-lookup"><span data-stu-id="27a0f-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="27a0f-147">Comprobar hello [modificar el FQDN de servidor en la cadena de conexión de hello](sql-data-warehouse-auditing-downlevel-clients.md) tema para las conexiones de cliente de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="27a0f-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="27a0f-148">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="27a0f-148">Click **OK**.</span></span>

## <span data-ttu-id="27a0f-149"><a id="subheading-3"></a>Análisis de registros e informes de auditoría</span><span class="sxs-lookup"><span data-stu-id="27a0f-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="27a0f-150">Los registros de auditoría se agrupan en una colección de tablas de almacén con un **SQLDBAuditLogs** prefijo Hola cuenta de almacenamiento de Azure que ha elegido durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="27a0f-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="27a0f-151">Puede ver los archivos de registro usando una herramienta como el <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Explorador de almacenamiento de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="27a0f-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="27a0f-152">Una plantilla de informe panel preconfigurado está disponible como un <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">hoja de cálculo de Excel que se puede descargar</a> toohelp analizar rápidamente los datos de registro.</span><span class="sxs-lookup"><span data-stu-id="27a0f-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="27a0f-153">plantilla de hello toouse en los registros de auditoría, necesita Excel 2013 o versiones posterior y Power Query, que puede descargar <a href="http://www.microsoft.com/download/details.aspx?id=39379">aquí</a>.</span><span class="sxs-lookup"><span data-stu-id="27a0f-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="27a0f-154">plantilla de Hello tiene datos de ejemplo ficticio en ella y puede configurar Power Query tooimport el registro de auditoría directamente desde su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="27a0f-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="27a0f-155"><a id="subheading-4"></a>Regeneración de clave de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="27a0f-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="27a0f-156">En producción, es probable toorefresh el almacenamiento de claves de forma periódica.</span><span class="sxs-lookup"><span data-stu-id="27a0f-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="27a0f-157">Al actualizar las claves, debe directiva de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="27a0f-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="27a0f-158">proceso de Hello es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="27a0f-158">hello process is as follows:</span></span>

1. <span data-ttu-id="27a0f-159">Hola auditoría hoja de configuración (descrita anteriormente en el programa de instalación de hello auditoría sección) cambiar hello **clave de acceso de almacenamiento** de *principal* demasiado*secundaria* y  **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="27a0f-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="27a0f-160">Hoja de configuración de almacenamiento vaya toohello y **regenerar** hello *clave de acceso principal*.</span><span class="sxs-lookup"><span data-stu-id="27a0f-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="27a0f-161">Volver atrás toohello auditoría hoja de configuración, conmutador hello **clave de acceso de almacenamiento** de *secundaria* demasiado*principal* y presione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="27a0f-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="27a0f-162">Volver atrás toohello almacenamiento interfaz de usuario y **regenerar** hello *clave de acceso secundaria* (como preparación para hello claves siguientes ciclo de actualización.</span><span class="sxs-lookup"><span data-stu-id="27a0f-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="27a0f-163"><a id="subheading-5"></a>Automatización (PowerShell o API de REST)</span><span class="sxs-lookup"><span data-stu-id="27a0f-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="27a0f-164">También puede configurar la auditoría en el almacén de datos de SQL Azure mediante el uso de hello después de herramientas de automatización:</span><span class="sxs-lookup"><span data-stu-id="27a0f-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="27a0f-165">**Cmdlets de PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="27a0f-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="27a0f-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="27a0f-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="27a0f-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="27a0f-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="27a0f-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="27a0f-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="27a0f-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="27a0f-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="27a0f-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="27a0f-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="27a0f-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="27a0f-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="27a0f-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="27a0f-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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
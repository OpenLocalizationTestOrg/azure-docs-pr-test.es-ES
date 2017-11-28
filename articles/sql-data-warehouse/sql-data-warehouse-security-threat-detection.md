---
title: "aaaGet a trabajar con la detección de amenazas de almacenamiento de datos de SQL"
description: "¿Cómo tooget a usar la detección de amenazas"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="fb48e-103">Introducción a la detección de amenazas</span><span class="sxs-lookup"><span data-stu-id="fb48e-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb48e-104">Auditoría</span><span class="sxs-lookup"><span data-stu-id="fb48e-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="fb48e-105">Detección de amenazas</span><span class="sxs-lookup"><span data-stu-id="fb48e-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="fb48e-106">Información general</span><span class="sxs-lookup"><span data-stu-id="fb48e-106">Overview</span></span>
<span data-ttu-id="fb48e-107">La detección de amenazas detecta actividades anómalas de la base de datos que indica la base de datos toohello amenazas de seguridad potenciales.</span><span class="sxs-lookup"><span data-stu-id="fb48e-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="fb48e-108">Detección de amenazas está en vista previa y es compatible con Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="fb48e-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="fb48e-109">La detección de amenazas proporciona una nueva capa de seguridad, lo cual permite toodetect de los clientes y responde a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas.</span><span class="sxs-lookup"><span data-stu-id="fb48e-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="fb48e-110">Los usuarios pueden explorar eventos sospechosos hello mediante [auditoría de almacenamiento de datos de SQL de Azure](sql-data-warehouse-auditing-overview.md) toodetermine si son el resultado de un intento de tooaccess, incumplen o almacén de datos de Hola de vulnerabilidad de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fb48e-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="fb48e-111">La detección de amenazas resulta sencillo tooaddress posibles amenazas toohello datos de almacenamiento sin Hola necesidad toobe un experto en seguridad o administración sistemas de supervisión de seguridad avanzada.</span><span class="sxs-lookup"><span data-stu-id="fb48e-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="fb48e-112">Por ejemplo, Detección de amenazas detecta determinadas actividades anómalas en la base de datos que sugieren posibles intentos de inyección de código SQL.</span><span class="sxs-lookup"><span data-stu-id="fb48e-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="fb48e-113">Inyección de código SQL es uno de hello Web aplicación problemas de seguridad comunes en hello Internet, aplicaciones usadas tooattack controladas por datos.</span><span class="sxs-lookup"><span data-stu-id="fb48e-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="fb48e-114">Los atacantes aprovechar aplicación vulnerabilidades tooinject instrucciones SQL malintencionadas en campos de entrada de la aplicación, para la infracción o modificar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb48e-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="fb48e-115">Configuración de la detección de amenazas para la base de datos</span><span class="sxs-lookup"><span data-stu-id="fb48e-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="fb48e-116">Inicio Hola Portal de Azure en [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb48e-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fb48e-117">Navegue toohello hoja de configuración de almacenamiento de datos de SQL que desee toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="fb48e-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="fb48e-118">En la hoja de configuración de hello, seleccione **auditoría y la detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="fb48e-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Panel de navegación][1]
3. <span data-ttu-id="fb48e-120">Hola **auditoría y la detección de amenazas** hoja de configuración a su vez **ON** auditoría, que mostrarán opciones de detección de amenazas de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb48e-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![Panel de navegación][2]
4. <span data-ttu-id="fb48e-122">**Active** Detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="fb48e-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="fb48e-123">Configurar la lista de Hola de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades de almacén de datos anómalos.</span><span class="sxs-lookup"><span data-stu-id="fb48e-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="fb48e-124">Haga clic en **guardar** en hello **detección de auditoría y amenaza** toosave de hoja de configuración Hola nuevo o actualizado directiva de detección de amenaza y auditoría.</span><span class="sxs-lookup"><span data-stu-id="fb48e-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![Panel de navegación][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="fb48e-126">Exploración de las actividades anómalas en el almacenamiento cuando se detecta un evento sospechoso</span><span class="sxs-lookup"><span data-stu-id="fb48e-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="fb48e-127">Recibirá una notificación por correo electrónico tras la detección de actividades anómalas en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="fb48e-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="fb48e-128">correo electrónico de Hello proporcionará información sobre eventos de seguridad sospechosos de hello incluidos naturaleza Hola de actividades anómalas hello, el nombre de base de datos, hora del evento de hello y nombre de servidor.</span><span class="sxs-lookup"><span data-stu-id="fb48e-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="fb48e-129">Además, se proporcionará información sobre las posibles causas y recomienda acciones tooinvestigate y mitigar la base de datos de toohello de amenaza potencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb48e-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![Panel de navegación][4]
2. <span data-ttu-id="fb48e-131">En correo electrónico de hello, haga clic en hello **el registro de auditoría de SQL de Azure** vínculo, que se inicie Hola Portal clásico de Azure y mostrar los registros de auditoría pertinentes de hello aproximadamente hora de Hola de eventos sospechosos Hola.</span><span class="sxs-lookup"><span data-stu-id="fb48e-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![Panel de navegación][5]
3. <span data-ttu-id="fb48e-133">Haga clic en tooview de registros de auditoría de hello más detalles sobre las actividades de base de datos sospechosa hello como instrucción SQL, IP de cliente y el motivo del error.</span><span class="sxs-lookup"><span data-stu-id="fb48e-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Panel de navegación][6]
4. <span data-ttu-id="fb48e-135">En la hoja de registros de auditoría de hello, haga clic en **abierto en Excel** tooopen configurada previamente excel tooimport de plantilla y ejecución análisis más profundos de registro de auditoría de hello aproximadamente hora de Hola de eventos sospechosos Hola.</span><span class="sxs-lookup"><span data-stu-id="fb48e-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="fb48e-136">
   **Nota:** en Excel 2010 o posterior, Power Query y hello **combinación rápida** configuración es necesaria</span><span class="sxs-lookup"><span data-stu-id="fb48e-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![Panel de navegación][7]
5. <span data-ttu-id="fb48e-138">Hola tooconfigure **combinación rápida** configuración - Hola **POWER QUERY** ficha de cinta de opciones, seleccione **opciones** cuadro de diálogo de opciones de toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="fb48e-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="fb48e-139">Seleccione la sección de privacidad de Hola y elige Hola segunda opción - 'Ignorar los niveles de privacidad de Hola y mejorar el rendimiento potencialmente':</span><span class="sxs-lookup"><span data-stu-id="fb48e-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![Panel de navegación][8]
6. <span data-ttu-id="fb48e-141">registros de auditoría SQL tooload, asegúrese de que parámetros hello en la pestaña de configuración de hello están establecidos correctamente y, a continuación, seleccione la cinta de opciones de "Datos" hello y haga clic en botón 'Actualizar todo' hello.</span><span class="sxs-lookup"><span data-stu-id="fb48e-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![Panel de navegación][9]
7. <span data-ttu-id="fb48e-143">los resultados de Hello aparecen en hello **los registros de auditoría de SQL** hoja que le permite realizar análisis más profundos toorun actividades anómalas de Hola que se detectaron y mitigar el impacto de Hola de eventos de seguridad de hello en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb48e-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png

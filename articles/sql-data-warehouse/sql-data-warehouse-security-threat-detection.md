---
title: "Introducción a Detección de amenazas de Almacenamiento de datos SQL"
description: "Cómo empezar a trabajar con la detección de amenazas"
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
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="67551-103">Introducción a la detección de amenazas</span><span class="sxs-lookup"><span data-stu-id="67551-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67551-104">Auditoría</span><span class="sxs-lookup"><span data-stu-id="67551-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="67551-105">Detección de amenazas</span><span class="sxs-lookup"><span data-stu-id="67551-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="67551-106">Información general</span><span class="sxs-lookup"><span data-stu-id="67551-106">Overview</span></span>
<span data-ttu-id="67551-107">Detección de amenazas detecta actividades anómalas en la base de datos que indican posibles amenazas de seguridad a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="67551-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="67551-108">Detección de amenazas está en vista previa y es compatible con Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="67551-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="67551-109">Detección de amenazas ofrece un nuevo nivel de seguridad, que permite a los clientes detectar amenazas potenciales y responder a ellas a medida que se producen, gracias a las alertas de seguridad sobre actividades anómalas que se proporcionan.</span><span class="sxs-lookup"><span data-stu-id="67551-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="67551-110">Los usuarios pueden explorar los eventos sospechosos mediante la [auditoría de Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) para determinar si proceden de un intento de acceder a los datos del almacenamiento de datos, infringir su seguridad o aprovecharlos.</span><span class="sxs-lookup"><span data-stu-id="67551-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="67551-111">Detección de amenazas facilita la solución de las posibles amenazas al almacenamiento sin necesidad de ser un experto en seguridad ni administrar sistemas de supervisión de seguridad avanzada.</span><span class="sxs-lookup"><span data-stu-id="67551-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="67551-112">Por ejemplo, Detección de amenazas detecta determinadas actividades anómalas en la base de datos que sugieren posibles intentos de inyección de código SQL.</span><span class="sxs-lookup"><span data-stu-id="67551-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="67551-113">La inyección de código SQL es uno de los problemas de seguridad habituales entre las aplicaciones web en Internet y se usa para atacar aplicaciones controladas por datos.</span><span class="sxs-lookup"><span data-stu-id="67551-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="67551-114">Los atacantes aprovechan las vulnerabilidades de la aplicación para inyectar instrucciones SQL malintencionadas en los campos de entrada de la aplicación, con el fin de infringir la seguridad o modificar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="67551-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="67551-115">Configuración de la detección de amenazas para la base de datos</span><span class="sxs-lookup"><span data-stu-id="67551-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="67551-116">Inicie el Portal de Azure en [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67551-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67551-117">Vaya a la hoja de configuración de Almacenamiento de datos SQL que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="67551-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="67551-118">En la hoja Configuración, seleccione **Auditoría y detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="67551-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Panel de navegación][1]
3. <span data-ttu-id="67551-120">En la hoja de configuración de **Auditoría y detección de amenazas**, **active** la auditoría; se mostrará la configuración de Detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="67551-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![Panel de navegación][2]
4. <span data-ttu-id="67551-122">**Active** Detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="67551-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="67551-123">Configure la lista de correos electrónicos que recibirán alertas de seguridad cuando se detecten actividades anómalas en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="67551-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="67551-124">Haga clic en **Guardar** en la hoja de configuración de **Auditoría y detección de amenazas** para guardar la directiva de auditoría y detección de amenazas nueva o actualizada.</span><span class="sxs-lookup"><span data-stu-id="67551-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![Panel de navegación][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="67551-126">Exploración de las actividades anómalas en el almacenamiento cuando se detecta un evento sospechoso</span><span class="sxs-lookup"><span data-stu-id="67551-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="67551-127">Recibirá una notificación por correo electrónico tras la detección de actividades anómalas en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="67551-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="67551-128">El correo electrónico proporciona información sobre el evento de seguridad sospechoso, en la que se incluyen la naturaleza de las actividades anómalas, el nombre de la base de datos, el nombre del servidor y la hora del evento.</span><span class="sxs-lookup"><span data-stu-id="67551-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="67551-129">Además, se proporcionará información sobre las posibles causas y las medidas recomendadas para investigar y mitigar la amenaza potencial para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="67551-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![Panel de navegación][4]
2. <span data-ttu-id="67551-131">En el correo electrónico, haga clic en el vínculo **Registro de auditoría SQL de Azure** , lo que iniciará el Portal de Azure clásico y mostrará los registros de auditoría pertinentes en torno a la hora del evento sospechoso.</span><span class="sxs-lookup"><span data-stu-id="67551-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![Panel de navegación][5]
3. <span data-ttu-id="67551-133">Haga clic en los registros de auditoría para ver más detalles sobre las actividades sospechosas en la base de datos, como instrucción SQL, motivo del error e IP de cliente.</span><span class="sxs-lookup"><span data-stu-id="67551-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Panel de navegación][6]
4. <span data-ttu-id="67551-135">En la hoja Registros de auditoría, haga clic en **Abrir en Excel** para abrir una plantilla de Excel ya configurada para importar y ejecutar un análisis más profundo del registro de auditoría en torno a la hora del evento sospechoso.</span><span class="sxs-lookup"><span data-stu-id="67551-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="67551-136">
   **Nota**: en Excel 2010 o posterior, se necesitan Power Query y la configuración **Combinación rápida**.</span><span class="sxs-lookup"><span data-stu-id="67551-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![Panel de navegación][7]
5. <span data-ttu-id="67551-138">Para definir la configuración **Combinación rápida**: en la pestaña **POWER QUERY** de la cinta, seleccione **Opciones** para mostrar el cuadro de diálogo Opciones.</span><span class="sxs-lookup"><span data-stu-id="67551-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="67551-139">Seleccione la sección Privacidad y elija la segunda opción, "Omitir los niveles de privacidad para mejorar el rendimiento":</span><span class="sxs-lookup"><span data-stu-id="67551-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![Panel de navegación][8]
6. <span data-ttu-id="67551-141">Para cargar registros de auditoría SQL, asegúrese de que los parámetros de la pestaña Configuración sean correctos y después seleccione "Datos" en la cinta y haga clic en el botón "Actualizar todo".</span><span class="sxs-lookup"><span data-stu-id="67551-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![Panel de navegación][9]
7. <span data-ttu-id="67551-143">Los resultados aparecen en la hoja **Registros de auditoría SQL** , que permite ejecutar un análisis más profundo de las actividades anómalas que se detectaron y mitigar el impacto del evento de seguridad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="67551-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

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

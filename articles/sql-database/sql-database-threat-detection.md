---
title: "aaaThreat detección - base de datos de SQL de Azure | Documentos de Microsoft"
description: "La detección de amenazas detecta actividades anómalas de la base de datos que indica la base de datos toohello amenazas de seguridad potenciales."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="a9613-103">Detección de amenazas de SQL Database</span><span class="sxs-lookup"><span data-stu-id="a9613-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="a9613-104">Detección de amenazas SQL detecta actividades anómalas que indica las bases de datos de tooaccess o vulnerabilidad de seguridad de intentos inusuales y potencialmente dañinos.</span><span class="sxs-lookup"><span data-stu-id="a9613-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="a9613-105">Información general</span><span class="sxs-lookup"><span data-stu-id="a9613-105">Overview</span></span>

<span data-ttu-id="a9613-106">Detección de amenazas de SQL proporciona una nueva capa de seguridad, lo cual permite toodetect de los clientes y responde a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas.</span><span class="sxs-lookup"><span data-stu-id="a9613-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="a9613-107">Los usuarios recibirán una alerta en actividades sospechosas de bases de datos, posibles vulnerabilidades y ataques de inyección de SQL, así como patrones de acceso de base de datos anómalos.</span><span class="sxs-lookup"><span data-stu-id="a9613-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="a9613-108">Alertas de detección de amenazas de SQL se proporcionan detalles de actividad sospechosa y recomendarán la acción sobre cómo tooinvestigate y mitigar la amenaza de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9613-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="a9613-109">Los usuarios pueden explorar eventos sospechosos hello mediante [auditoría de base de datos de SQL](sql-database-auditing.md) toodetermine si son el resultado de un intento de tooaccess, de infracción o vulnerabilidad de seguridad de datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9613-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="a9613-110">La detección de amenazas resulta sencillo tooaddress posibles amenazas toohello base de datos sin necesidad de hello toobe un experto en seguridad o administrar sistemas de supervisión de seguridad avanzada.</span><span class="sxs-lookup"><span data-stu-id="a9613-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="a9613-111">Por ejemplo, inyección de código SQL es uno de hello Web aplicación problemas de seguridad comunes en hello Internet, aplicaciones usadas tooattack controladas por datos.</span><span class="sxs-lookup"><span data-stu-id="a9613-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="a9613-112">Los atacantes aprovechar aplicación vulnerabilidades tooinject instrucciones SQL malintencionadas en campos de entrada de la aplicación, infracción o modificar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9613-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="a9613-113">Detección de amenazas SQL integra alertas con [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), y cada servidor de base de datos SQL protegido se facturará en hello mismo precio como nivel estándar de centro de seguridad de Azure, en 15 $/ nodo/mes, donde cada uno de ellos proteger SQL Servidor de base de datos se cuenta como un nodo.</span><span class="sxs-lookup"><span data-stu-id="a9613-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="a9613-114">Le invitamos tootry márquelo durante 60 días para liberar.</span><span class="sxs-lookup"><span data-stu-id="a9613-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="a9613-115">Configurar la detección de amenazas para la base de datos en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a9613-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="a9613-116">Iniciar hello Azure portal en [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9613-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a9613-117">Navegue toohello hoja de configuración de base de datos de SQL que desee toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="a9613-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="a9613-118">En la hoja de configuración de hello, seleccione **auditoría y la detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="a9613-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="a9613-119">![Panel de navegación][1]</span><span class="sxs-lookup"><span data-stu-id="a9613-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="a9613-120">Hola **auditoría y la detección de amenazas** hoja de configuración a su vez **ON** auditoría, que mostrará la configuración de detección de amenazas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9613-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![Panel de navegación][2]
4. <span data-ttu-id="a9613-122">**Active** Detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="a9613-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="a9613-123">Configurar la lista de Hola de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades anómalas de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a9613-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="a9613-124">Haga clic en **guardar** en hello **detección de auditoría y amenaza** hoja toosave Hola nuevos o actualizados configuración de detección de amenazas y auditoría.</span><span class="sxs-lookup"><span data-stu-id="a9613-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![Panel de navegación][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="a9613-126">Configuración de la detección de amenazas mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9613-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="a9613-127">Para ver un script de ejemplo, consulte [Configuración de la auditoría y detección de amenazas mediante PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a9613-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="a9613-128">Exploración de las actividades anómalas en la base de datos cuando se detecta un evento sospechoso</span><span class="sxs-lookup"><span data-stu-id="a9613-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="a9613-129">Recibirá una notificación por correo electrónico tras la detección de actividades anómalas en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a9613-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="a9613-130">correo electrónico de Hello proporcionará información sobre eventos de seguridad sospechosos Hola incluidos naturaleza Hola de actividades anómalas hello, nombre de base de datos, nombre del servidor, nombre de la aplicación y hora del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="a9613-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="a9613-131">Además, correo electrónico de Hola proporcionará información sobre las posibles causas y recomienda acciones tooinvestigate y mitigar la base de datos de toohello de amenaza potencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9613-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![Panel de navegación][4]
2. <span data-ttu-id="a9613-133">alerta de correo electrónico de Hello incluye un registro de auditoría de SQL toohello vínculo directo.</span><span class="sxs-lookup"><span data-stu-id="a9613-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="a9613-134">Al hacer clic en este Hola de lanzamientos de vínculo Azure portal y abre Hola SQL los registros de auditoría aproximadamente hora de Hola de eventos sospechosos Hola.</span><span class="sxs-lookup"><span data-stu-id="a9613-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="a9613-135">Haga clic en un tooview de registro de auditoría más detalles sobre actividades de base de datos sospechosa hello, lo que sea más fácil toofind hello las instrucciones SQL que se ejecutaron (quién ha accedido a, lo que hicieron y cuándo) y determinar si el evento de hello era legítimo o malintencionado (por ejemplo, aplicación inyección de código de vulnerabilidad tooSQL indicase estaba usando, alguien ha realizado la infracción datos confidenciales, etcetera).</span><span class="sxs-lookup"><span data-stu-id="a9613-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="a9613-136">
   ![Panel de navegación][5]</span><span class="sxs-lookup"><span data-stu-id="a9613-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="a9613-137">Explorar las alertas de detección de amenazas en la base de datos en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a9613-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="a9613-138">Detección de amenazas de SQL Database integra la alerta con [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="a9613-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="a9613-139">Un icono de la seguridad SQL dinámico dentro de la hoja de la base de datos de hello en el estado de Hola Hola pistas portal Azure de amenazas activas.</span><span class="sxs-lookup"><span data-stu-id="a9613-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![Panel de navegación][6]
   
1. <span data-ttu-id="a9613-141">Al hacer clic en el icono de seguridad SQL de hello inicia hoja de alertas del centro de seguridad de Azure de Hola y proporciona una visión general de amenazas activas de SQL ha detectado en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9613-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![Panel de navegación][7]

2. <span data-ttu-id="a9613-143">Al hacer clic en una alerta específica se proporcionan detalles y acciones adicionales para investigar esta amenaza y solucionar amenazas futuras.</span><span class="sxs-lookup"><span data-stu-id="a9613-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Panel de navegación][8]


## <a name="next-steps"></a><span data-ttu-id="a9613-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9613-145">Next steps</span></span>

* <span data-ttu-id="a9613-146">Obtener más información sobre la detección de amenazas, visite hello [blog de Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="a9613-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="a9613-147">Más información acerca de la [auditoría de Azure SQL Database](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="a9613-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="a9613-148">Más información acerca de [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="a9613-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="a9613-149">Para obtener más detalles sobre los precios, visite hello [página de precios de base de datos de SQL Server](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="a9613-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="a9613-150">Para ver un script de ejemplo de PowerShell, consulte [Configuración de la auditoría y detección de amenazas mediante PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a9613-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png



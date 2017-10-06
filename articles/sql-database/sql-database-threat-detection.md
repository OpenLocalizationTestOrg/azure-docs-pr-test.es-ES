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
# <a name="sql-database-threat-detection"></a>Detección de amenazas de SQL Database

Detección de amenazas SQL detecta actividades anómalas que indica las bases de datos de tooaccess o vulnerabilidad de seguridad de intentos inusuales y potencialmente dañinos.

## <a name="overview"></a>Información general

Detección de amenazas de SQL proporciona una nueva capa de seguridad, lo cual permite toodetect de los clientes y responde a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas.  Los usuarios recibirán una alerta en actividades sospechosas de bases de datos, posibles vulnerabilidades y ataques de inyección de SQL, así como patrones de acceso de base de datos anómalos. Alertas de detección de amenazas de SQL se proporcionan detalles de actividad sospechosa y recomendarán la acción sobre cómo tooinvestigate y mitigar la amenaza de Hola. Los usuarios pueden explorar eventos sospechosos hello mediante [auditoría de base de datos de SQL](sql-database-auditing.md) toodetermine si son el resultado de un intento de tooaccess, de infracción o vulnerabilidad de seguridad de datos en la base de datos de Hola. La detección de amenazas resulta sencillo tooaddress posibles amenazas toohello base de datos sin necesidad de hello toobe un experto en seguridad o administrar sistemas de supervisión de seguridad avanzada.

Por ejemplo, inyección de código SQL es uno de hello Web aplicación problemas de seguridad comunes en hello Internet, aplicaciones usadas tooattack controladas por datos. Los atacantes aprovechar aplicación vulnerabilidades tooinject instrucciones SQL malintencionadas en campos de entrada de la aplicación, infracción o modificar datos en la base de datos de Hola.

Detección de amenazas SQL integra alertas con [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), y cada servidor de base de datos SQL protegido se facturará en hello mismo precio como nivel estándar de centro de seguridad de Azure, en 15 $/ nodo/mes, donde cada uno de ellos proteger SQL Servidor de base de datos se cuenta como un nodo. Le invitamos tootry márquelo durante 60 días para liberar. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>Configurar la detección de amenazas para la base de datos en hello portal de Azure
1. Iniciar hello Azure portal en [https://portal.azure.com](https://portal.azure.com).
2. Navegue toohello hoja de configuración de base de datos de SQL que desee toomonitor hello. En la hoja de configuración de hello, seleccione **auditoría y la detección de amenazas**. 
    ![Panel de navegación][1]
3. Hola **auditoría y la detección de amenazas** hoja de configuración a su vez **ON** auditoría, que mostrará la configuración de detección de amenazas de Hola.
  
    ![Panel de navegación][2]
4. **Active** Detección de amenazas.
5. Configurar la lista de Hola de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades anómalas de la base de datos.
6. Haga clic en **guardar** en hello **detección de auditoría y amenaza** hoja toosave Hola nuevos o actualizados configuración de detección de amenazas y auditoría.
       
    ![Panel de navegación][3]

## <a name="set-up-threat-detection-using-powershell"></a>Configuración de la detección de amenazas mediante PowerShell

Para ver un script de ejemplo, consulte [Configuración de la auditoría y detección de amenazas mediante PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>Exploración de las actividades anómalas en la base de datos cuando se detecta un evento sospechoso
1. Recibirá una notificación por correo electrónico tras la detección de actividades anómalas en la base de datos. <br/>
   correo electrónico de Hello proporcionará información sobre eventos de seguridad sospechosos Hola incluidos naturaleza Hola de actividades anómalas hello, nombre de base de datos, nombre del servidor, nombre de la aplicación y hora del evento Hola. Además, correo electrónico de Hola proporcionará información sobre las posibles causas y recomienda acciones tooinvestigate y mitigar la base de datos de toohello de amenaza potencial de Hola.<br/>
     
    ![Panel de navegación][4]
2. alerta de correo electrónico de Hello incluye un registro de auditoría de SQL toohello vínculo directo. Al hacer clic en este Hola de lanzamientos de vínculo Azure portal y abre Hola SQL los registros de auditoría aproximadamente hora de Hola de eventos sospechosos Hola. Haga clic en un tooview de registro de auditoría más detalles sobre actividades de base de datos sospechosa hello, lo que sea más fácil toofind hello las instrucciones SQL que se ejecutaron (quién ha accedido a, lo que hicieron y cuándo) y determinar si el evento de hello era legítimo o malintencionado (por ejemplo, aplicación inyección de código de vulnerabilidad tooSQL indicase estaba usando, alguien ha realizado la infracción datos confidenciales, etcetera).<br/>
   ![Panel de navegación][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>Explorar las alertas de detección de amenazas en la base de datos en hello portal de Azure

Detección de amenazas de SQL Database integra la alerta con [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/). Un icono de la seguridad SQL dinámico dentro de la hoja de la base de datos de hello en el estado de Hola Hola pistas portal Azure de amenazas activas. 

   ![Panel de navegación][6]
   
1. Al hacer clic en el icono de seguridad SQL de hello inicia hoja de alertas del centro de seguridad de Azure de Hola y proporciona una visión general de amenazas activas de SQL ha detectado en la base de datos de Hola. 

  ![Panel de navegación][7]

2. Al hacer clic en una alerta específica se proporcionan detalles y acciones adicionales para investigar esta amenaza y solucionar amenazas futuras.

  ![Panel de navegación][8]


## <a name="next-steps"></a>Pasos siguientes

* Obtener más información sobre la detección de amenazas, visite hello [blog de Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* Más información acerca de la [auditoría de Azure SQL Database](sql-database-auditing.md)
* Más información acerca de [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)
* Para obtener más detalles sobre los precios, visite hello [página de precios de base de datos de SQL Server](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* Para ver un script de ejemplo de PowerShell, consulte [Configuración de la auditoría y detección de amenazas mediante PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png



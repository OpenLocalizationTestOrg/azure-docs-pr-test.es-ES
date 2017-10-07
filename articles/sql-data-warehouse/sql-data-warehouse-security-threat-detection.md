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
# <a name="get-started-with-threat-detection"></a>Introducción a la detección de amenazas
> [!div class="op_single_selector"]
> * [Auditoría](sql-data-warehouse-auditing-overview.md)
> * [Detección de amenazas](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>Información general
La detección de amenazas detecta actividades anómalas de la base de datos que indica la base de datos toohello amenazas de seguridad potenciales. Detección de amenazas está en vista previa y es compatible con Almacenamiento de datos SQL.

La detección de amenazas proporciona una nueva capa de seguridad, lo cual permite toodetect de los clientes y responde a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas. Los usuarios pueden explorar eventos sospechosos hello mediante [auditoría de almacenamiento de datos de SQL de Azure](sql-data-warehouse-auditing-overview.md) toodetermine si son el resultado de un intento de tooaccess, incumplen o almacén de datos de Hola de vulnerabilidad de seguridad.
La detección de amenazas resulta sencillo tooaddress posibles amenazas toohello datos de almacenamiento sin Hola necesidad toobe un experto en seguridad o administración sistemas de supervisión de seguridad avanzada.

Por ejemplo, Detección de amenazas detecta determinadas actividades anómalas en la base de datos que sugieren posibles intentos de inyección de código SQL. Inyección de código SQL es uno de hello Web aplicación problemas de seguridad comunes en hello Internet, aplicaciones usadas tooattack controladas por datos. Los atacantes aprovechar aplicación vulnerabilidades tooinject instrucciones SQL malintencionadas en campos de entrada de la aplicación, para la infracción o modificar datos en la base de datos de Hola.

## <a name="set-up-threat-detection-for-your-database"></a>Configuración de la detección de amenazas para la base de datos
1. Inicio Hola Portal de Azure en [https://portal.azure.com](https://portal.azure.com).
2. Navegue toohello hoja de configuración de almacenamiento de datos de SQL que desee toomonitor hello. En la hoja de configuración de hello, seleccione **auditoría y la detección de amenazas**.
   
    ![Panel de navegación][1]
3. Hola **auditoría y la detección de amenazas** hoja de configuración a su vez **ON** auditoría, que mostrarán opciones de detección de amenazas de Hola.
   
    ![Panel de navegación][2]
4. **Active** Detección de amenazas.
5. Configurar la lista de Hola de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades de almacén de datos anómalos.
6. Haga clic en **guardar** en hello **detección de auditoría y amenaza** toosave de hoja de configuración Hola nuevo o actualizado directiva de detección de amenaza y auditoría.
   
    ![Panel de navegación][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>Exploración de las actividades anómalas en el almacenamiento cuando se detecta un evento sospechoso
1. Recibirá una notificación por correo electrónico tras la detección de actividades anómalas en la base de datos. <br/>
   correo electrónico de Hello proporcionará información sobre eventos de seguridad sospechosos de hello incluidos naturaleza Hola de actividades anómalas hello, el nombre de base de datos, hora del evento de hello y nombre de servidor. Además, se proporcionará información sobre las posibles causas y recomienda acciones tooinvestigate y mitigar la base de datos de toohello de amenaza potencial de Hola.<br/>
   
    ![Panel de navegación][4]
2. En correo electrónico de hello, haga clic en hello **el registro de auditoría de SQL de Azure** vínculo, que se inicie Hola Portal clásico de Azure y mostrar los registros de auditoría pertinentes de hello aproximadamente hora de Hola de eventos sospechosos Hola.
   
    ![Panel de navegación][5]
3. Haga clic en tooview de registros de auditoría de hello más detalles sobre las actividades de base de datos sospechosa hello como instrucción SQL, IP de cliente y el motivo del error.
   
    ![Panel de navegación][6]
4. En la hoja de registros de auditoría de hello, haga clic en **abierto en Excel** tooopen configurada previamente excel tooimport de plantilla y ejecución análisis más profundos de registro de auditoría de hello aproximadamente hora de Hola de eventos sospechosos Hola.<br/>
   **Nota:** en Excel 2010 o posterior, Power Query y hello **combinación rápida** configuración es necesaria
   
    ![Panel de navegación][7]
5. Hola tooconfigure **combinación rápida** configuración - Hola **POWER QUERY** ficha de cinta de opciones, seleccione **opciones** cuadro de diálogo de opciones de toodisplay Hola. Seleccione la sección de privacidad de Hola y elige Hola segunda opción - 'Ignorar los niveles de privacidad de Hola y mejorar el rendimiento potencialmente':
   
    ![Panel de navegación][8]
6. registros de auditoría SQL tooload, asegúrese de que parámetros hello en la pestaña de configuración de hello están establecidos correctamente y, a continuación, seleccione la cinta de opciones de "Datos" hello y haga clic en botón 'Actualizar todo' hello.
   
    ![Panel de navegación][9]
7. los resultados de Hello aparecen en hello **los registros de auditoría de SQL** hoja que le permite realizar análisis más profundos toorun actividades anómalas de Hola que se detectaron y mitigar el impacto de Hola de eventos de seguridad de hello en la aplicación.

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

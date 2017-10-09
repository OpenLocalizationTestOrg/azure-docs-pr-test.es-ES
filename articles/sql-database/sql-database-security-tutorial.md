---
title: aaaSecure la base de datos SQL de Azure | Documentos de Microsoft
description: "Obtenga información sobre características y técnicas de toosecure la base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>Protección de Azure SQL Database

Base de datos SQL protege los datos mediante la limitación de base de datos de access tooyour mediante las reglas de firewall que requieren los usuarios tooprove su identidad y autorización toodata a través de pertenencia basada en roles y permisos, así como a través de mecanismos de autenticación seguridad de nivel de fila y enmascaramiento dinámico de datos.

Puede mejorar la protección de hello de la base de datos frente a accesos no autorizados con unos pocos pasos sencillos o usuarios malintencionados. En este tutorial, aprenderá a: 

> [!div class="checklist"]
> * Configurar reglas de firewall de nivel de servidor para el servidor en hello portal de Azure
> * Configurar reglas de firewall de nivel de base de datos para la base de datos con SSMS
> * Conéctese utilizando una cadena de conexión segura de base de datos de tooyour
> * Administrar el acceso de los usuarios
> * Protección de los datos con cifrado
> * Habilitación de la auditoría de SQL Database
> * Habilitación de la detección de amenazas de SQL Database

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

toocomplete Asegúrese de este tutorial, deberá asegurarse de que Hola siguientes:

- Versión más reciente de hello instalada de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). 
- Se ha instalado Microsoft Excel
- Crea un servidor de SQL Azure y la base de datos: vea [crear una base de datos de SQL Azure en el portal de Azure hello](sql-database-get-started-portal.md), [crear una base de datos de SQL Azure único con hello Azure CLI](sql-database-get-started-cli.md), y [crear una instancia única de SQL Azure uso de PowerShell de la base de datos](sql-database-get-started-powershell.md). 

## <a name="log-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Crear una regla de firewall de nivel de servidor en hello portal de Azure

En Azure, las bases de datos SQL están protegidas mediante un firewall. De forma predeterminada, se rechazan todas las conexiones toohello hello y servidor de bases de datos dentro de servidor hello excepto para las conexiones desde otros servicios de Azure. Para más información, consulte [Reglas de firewall de nivel de base de datos y de nivel de servidor de Azure SQL Database](sql-database-firewall-configure.md).

configuración más segura de Hello es tooset 'Permitir acceso a servicios tooAzure' tooOFF. Si necesita tooconnect toohello base de datos de un servicio de máquina virtual de Azure o en la nube, debe crear un [IP reservada](../virtual-network/virtual-networks-reserved-public-ip.md) y permitir solo Hola reservado IP abordar el acceso a través de firewall de Hola. 

Siga estos pasos toocreate una [regla de firewall de nivel de servidor de base de datos SQL](sql-database-firewall-configure.md) para las conexiones del servidor tooallow desde una dirección IP específica. 

> [!NOTE]
> Si ha creado una base de datos de ejemplo en Azure mediante uno de los tutoriales anteriores de Hola o tutoriales rápidos y están realizando este tutorial en un equipo con hello mismo de direcciones IP que TI tenía cuando le guía por los tutoriales, puede omitir este paso ya que tendrá ya creó una regla de firewall de nivel de servidor.
>

1. Haga clic en **bases de datos SQL** de hello izquierdo menú y haga clic en hello base de datos desearía tooconfigure regla de firewall de Hola para en hello **bases de datos SQL** página. página de información general para abrir el base de datos, que muestra que Hola totalmente Hello calificado nombre del servidor (como **mynewserver 20170313.database.windows.net**) y proporciona opciones para otra configuración.

      ![regla de firewall del servidor](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. Haga clic en **Configurar firewall de servidor** de barra de herramientas de hello tal y como se muestra en la imagen anterior de Hola. Hola **configuración del Firewall** se abre la página servidor de base de datos de SQL de Hola. 

3. Haga clic en **agregar dirección IP del cliente** en Hola barra de herramientas tooadd Hola dirección IP pública del portal de hello equipo toohello conectado con o escribir la regla de firewall de hello manualmente y, a continuación, haga clic en **guardar**.

      ![establecer regla de firewall del servidor](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. Haga clic en **Aceptar** y, a continuación, haga clic en hello **X** tooclose hello **configuración del Firewall** página.

Ahora puede conectarse tooany base de datos en el servidor de hello con hello especificado intervalo de direcciones IP o la dirección IP.

> [!NOTE]
> SQL Database se comunica a través del puerto 1433. Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 1433. Si es así, no será capaz de tooconnect tooyour base de datos de SQL Azure servidor a menos que el departamento de TI abre el puerto 1433.
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>Creación de una regla de firewall de nivel de base de datos con SSMS

Las reglas de firewall de nivel de base de datos Habilitar configuración de otro firewall toocreate para bases de datos diferentes dentro de hello mismo firewall de servidor y toocreate lógico reglas que sean portables - lo que significa que se adecuan a base de datos de Hola durante un [conmutación por error ](sql-database-geo-replication-overview.md) en lugar de almacenarse en SQL server de Hola. Reglas de firewall de nivel de base de datos solo se pueden configurar mediante el uso de instrucciones Transact-SQL como solo después de haber configurado la primera regla de firewall de nivel de servidor de Hola. Para más información, consulte [Reglas de firewall de nivel de base de datos y de nivel de servidor de Azure SQL Database](sql-database-firewall-configure.md).

Sigue estos toocreate pasos una regla de firewall de base de datos específica.

1. Conectar la base de datos de tooyour, por ejemplo mediante [SQL Server Management Studio](./sql-database-connect-query-ssms.md).

2. En el Explorador de objetos, haga doble clic en la base de datos de hello desea tooadd un firewall para de la regla y haga clic en **nueva consulta**. Abre una ventana de consulta en blanco que es conectado tooyour base de datos.

3. En la ventana de consulta de hello, modifique hello tooyour pública dirección IP y, a continuación, ejecute hello después de consulta:

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. En la barra de herramientas de hello, haga clic en **Execute** regla de firewall toocreate Hola.

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>Ver cómo tooconnect tooyour de una aplicación de base de datos mediante una cadena de conexión segura

tooensure una conexión cifrada segura entre una aplicación cliente y la base de datos SQL, cadena de conexión de hello tiene toobe configurado para:

- Solicitar una conexión cifrada y
- certificado de servidor de toonot confianza Hola. 

Esto establece una conexión con seguridad de capa de transporte (TLS) y reduce el riesgo de Hola de man-in-the-middle ataques. Puede obtener las cadenas de conexión configurada correctamente para la base de datos SQL de cliente admitida controladores de hello portal de Azure como se muestra para ADO.net en esta captura de pantalla.

1. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.

2. En hello **Introducción** página de la base de datos, haga clic en **mostrar cadenas de conexión de base de datos**.

3. Hola de revisión completa **ADO.NET** cadena de conexión.

    ![Cadena de conexión ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>Creación de usuarios de base de datos

Antes de crear los usuarios, primero debe elegir uno de dos tipos de autenticación admitidos por Azure SQL Database: 

**Autenticación de SQL**, que utiliza el nombre de usuario y contraseña para los inicios de sesión y Hola a los usuarios que son válidos únicamente en el contexto de una base de datos dentro de un servidor lógico. 

**Autenticación de Azure Active Directory**, que usa identidades administradas por Azure Active Directory. 

Si desea que toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate en base de datos de SQL, debe existir un rellenado Azure Active Directory antes de continuar.

Siga estos pasos toocreate un usuario mediante la autenticación de SQL:

1. Conectar la base de datos de tooyour, por ejemplo mediante [SQL Server Management Studio](./sql-database-connect-query-ssms.md) con sus credenciales de administrador de servidor.

2. En el Explorador de objetos, haga doble clic en la base de datos de Hola que desee tooadd un usuario nuevo y haga clic en **nueva consulta**. Abre una ventana de consulta en blanco que es toohello conectado la base de datos seleccionada.

3. En la ventana de consulta de hello, escriba Hola después de consulta:

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. En la barra de herramientas de hello, haga clic en **Execute** toocreate usuario de Hola.

5. De forma predeterminada, usuario de hello puede conectar la base de datos de toohello, pero no tiene ningún dato de tooread o de escritura de permisos. toogrant estas toohello permisos usuario creado recientemente, ejecute hello siguiendo dos comandos en una nueva ventana de consulta

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

Es mejor toocreate práctica estas cuentas sin privilegios de administrador en tooyour de tooconnect de nivel de base de datos de Hola de base de datos a menos que necesite tooexecute tareas de administrador como la creación de nuevos usuarios. Revise hello [tutorial de Azure Active Directory](./sql-database-aad-authentication-configure.md) acerca de cómo tooauthenticate con Azure Active Directory.


## <a name="protect-your-data-with-encryption"></a>Protección de los datos con cifrado

Cifrado de datos transparente de base de datos de SQL Azure (TDE) cifra automáticamente los datos en reposo, sin necesidad de realizar los cambios toohello aplicación acceso a Hola base de datos cifrada. Para las bases de datos recién creadas, el TDE está activado de forma predeterminada. tooenable TDE para su base de datos o tooverify que TDE está activado, siga estos pasos:

1. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página. 

2. Haga clic en **cifrado de datos transparente** página de configuración de hello tooopen de TDE.

    ![Cifrado de datos transparente](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. Si es necesario, establezca **cifrado de datos** tooON y haga clic en **guardar**.

se inicia el proceso de cifrado de Hello en segundo plano de Hola. Puede supervisar el progreso de hello usando conexión de base de datos de tooSQL [SQL Server Management Studio](./sql-database-connect-query-ssms.md) consultando la columna encryption_state de Hola de hello `sys.dm_database_encryption_keys` vista.

## <a name="enable-sql-database-auditing-if-necessary"></a>Habilitación de la auditoría de SQL Database, si es necesario

Auditoría de base de datos de SQL Azure realiza un seguimiento de eventos de base de datos y escribe el registro de auditoría tooan en su cuenta de almacenamiento de Azure. La auditoría puede ayudarle a mantener el cumplimiento de normativas y conocer la actividad de las bases de datos, así como las discrepancias y anomalías que pueden indicar la existencia de potenciales infracciones de la seguridad. Siga estos toocreate pasos una directiva de auditoría predeterminada para la base de datos SQL:

1. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página. 

2. En la hoja de configuración de hello, seleccione **auditoría y la detección de amenazas**. Observe que ha sido la auditoría de nivel de servidor y que hay un **ver configuración del servidor** vínculo que le permite tooview o modificar la configuración de auditoría de servidor hello en este contexto.

    ![Hoja Auditoría](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. Si lo prefiere tooenable un tipo de auditoría (o ubicación?) diferente de hello especificada en el nivel de servidor hello, activar **ON** auditoría y elija hello **Blob** tipo de auditoría. Si está habilitada la auditoría de servidor blobs, auditoría de base de datos configurada de hello existirá paralelo con la auditoría de Blob de servidor hello.

    ![Activar la auditoría](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. Seleccione **detalles de almacenamiento** tooopen Hola hoja de almacenamiento de registros de auditoría. Cuenta de almacenamiento de Azure Hola seleccione donde se guardará los registros y período de retención de hello, se eliminarán los registros antiguos después qué hello, a continuación, haga clic en **Aceptar** final Hola. 

   > [!TIP]
   > Use Hola misma cuenta de almacenamiento para todas las bases de datos auditados tooget hello máximo partido de auditoría de hello informa de plantillas.
   > 

5. Haga clic en **Guardar**.

> [!IMPORTANT]
> Si desea toocustomize Hola auditar eventos, puede hacerlo a través de PowerShell o API de REST - vea hello [automatización (PowerShell / API de REST)](sql-database-auditing.md#subheading-7) sección para obtener más detalles.
>

## <a name="enable-sql-database-threat-detection"></a>Habilitación de la detección de amenazas de SQL Database

La detección de amenazas proporciona una nueva capa de seguridad, lo cual permite toodetect de los clientes y responde a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas. Los usuarios pueden explorar eventos sospechosos hello mediante toodetermine de auditoría de base de datos de SQL Server si producir un tooaccess de intento de infracción o vulnerabilidad de seguridad de datos en la base de datos de Hola. La detección de amenazas resulta sencillo tooaddress posibles amenazas toohello base de datos sin necesidad de hello toobe un experto en seguridad o administrar sistemas de supervisión de seguridad avanzada.
Por ejemplo, Detección de amenazas detecta determinadas actividades anómalas en la base de datos que sugieren posibles intentos de inyección de código SQL. Inyección de código SQL es uno de hello Web aplicación problemas de seguridad comunes en hello Internet, aplicaciones usadas tooattack controladas por datos. Los atacantes aprovechar aplicación vulnerabilidades tooinject instrucciones SQL malintencionadas en campos de entrada de la aplicación, para la infracción o modificar datos en la base de datos de Hola.

1. Navegue toohello hoja de configuración de base de datos SQL que desee toomonitor hello. En la hoja de configuración de hello, seleccione **auditoría y la detección de amenazas**.

    ![Panel de navegación](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. Hola **auditoría y la detección de amenazas** hoja de configuración a su vez **ON** auditoría, que mostrarán opciones de detección de amenazas de Hola.

3. **Active** la detección de amenazas.

4. Configurar la lista de Hola de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades anómalas de la base de datos.

5. Haga clic en **guardar** en hello **detección de auditoría y amenaza** hoja toosave Hola nuevo o actualizado directiva de detección de amenaza y auditoría.

    ![Panel de navegación](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    Si se detectan actividades anómalas en la base de datos, recibirá una notificación por correo electrónico. correo electrónico de Hello proporcionará información sobre eventos de seguridad sospechosos de hello incluidos naturaleza Hola de actividades anómalas hello, el nombre de base de datos, hora del evento de hello y nombre de servidor. Además, se proporcionará información sobre las posibles causas y recomienda acciones tooinvestigate y mitigar la base de datos de toohello de amenaza potencial de Hola. recorrido Hola de pasos siguiente le guían a través de qué toodo debería recibir un mensaje de correo electrónico:

    ![Correo electrónico de detección de amenazas](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. En correo electrónico de hello, haga clic en hello **el registro de auditoría de SQL de Azure** vínculo, que se inicie Hola portal de Azure y mostrar registros de auditoría relevantes de hello aproximadamente hora de Hola de eventos sospechosos Hola.

    ![Registros de auditoría](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. Haga clic en tooview de registros de auditoría de hello más detalles sobre las actividades de base de datos sospechosa hello como instrucción SQL, IP de cliente y el motivo del error.

    ![Detalles del registro](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. En la hoja de registros de auditoría de hello, haga clic en **abierto en Excel** tooopen configurada previamente excel tooimport de plantilla y ejecución análisis más profundos de registro de auditoría de hello aproximadamente hora de Hola de eventos sospechosos Hola.

    > [!NOTE]
    > En Excel 2010 o posterior, Power Query y hello **combinación rápida** configuración es necesaria.

    ![Abrir registros en Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. Hola tooconfigure **combinación rápida** configuración - Hola **POWER QUERY** ficha de cinta de opciones, seleccione **opciones** cuadro de diálogo de opciones de toodisplay Hola. Seleccione la sección de privacidad de Hola y elige Hola segunda opción - 'Ignorar los niveles de privacidad de Hola y mejorar el rendimiento potencialmente':

    ![Combinación rápida de Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. registros de auditoría SQL tooload, asegúrese de que parámetros hello en la pestaña de configuración de hello están establecidos correctamente y, a continuación, seleccione la cinta de opciones de "Datos" hello y haga clic en botón 'Actualizar todo' hello.

    ![Parámetros de Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. los resultados de Hello aparecen en hello **los registros de auditoría de SQL** hoja que le permite realizar análisis más profundos toorun actividades anómalas de Hola que se detectaron y mitigar el impacto de Hola de eventos de seguridad de hello en la aplicación.


## <a name="next-steps"></a>Pasos siguientes
Puede mejorar la protección de hello de la base de datos frente a accesos no autorizados con unos pocos pasos sencillos o usuarios malintencionados. En este tutorial, aprenderá a: 

> [!div class="checklist"]
> * Configurar reglas de firewall para un servidor o una base de datos
> * Conéctese utilizando una cadena de conexión segura de base de datos de tooyour
> * Administrar el acceso de los usuarios
> * Protección de los datos con cifrado
> * Habilitación de la auditoría de SQL Database
> * Habilitación de la detección de amenazas de SQL Database

> [!div class="nextstepaction"]
>[Mejora del rendimiento de SQL Database](sql-database-performance-tutorial.md)


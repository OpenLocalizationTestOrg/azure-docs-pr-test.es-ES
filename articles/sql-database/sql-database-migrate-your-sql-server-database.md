---
title: tooAzure de base de datos de SQL Server aaaMigrate base de datos SQL | Documentos de Microsoft
description: "Obtenga información acerca de toomigrate su tooAzure de base de datos base de datos SQL de SQL Server."
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>Migrar su tooAzure de base de datos base de datos SQL de SQL Server

Mover el servidor SQL tooAzure de base de datos base de datos SQL es un proceso de tres partes: preparar, a continuación, exportar y, a continuación, importar base de datos de Hola. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Preparar una base de datos en un servidor SQL Server para la migración tooAzure base de datos SQL mediante hello [datos Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Exportar archivo BACPAC de tooa de base de datos de Hola
> * Importar archivo BACPAC de hello en una base de datos de SQL Azure

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:

- Versión más reciente de hello instalada de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). Instalar SSMS, también instala la versión más reciente de Hola de SQLPackage, una utilidad de línea de comandos que puede ser utilizado tooautomate una variedad de tareas de desarrollo de base de datos. 
- Hola instalado [datos Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- Ha identificado y tener acceso tooa base de datos toomigrate. Este tutorial usa hello [SQL Server 2008 R2 base de datos AdventureWorks OLTP](https://msftdbprodsamples.codeplex.com/releases/view/59211) en una instancia de SQL Server 2008 R2 o versiones más recientes, pero puede usar cualquier base de datos de su elección. problemas de compatibilidad de toofix, utilice [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Preparación para la migración

Son tooprepare preparado para la migración. Siga estos Hola de toouse pasos  **[datos Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess Hola preparación de la base de datos de migración tooAzure base de datos SQL.

1. Abra hello **datos Migration Assistant**. Puede ejecutar DMA en cualquier equipo con conectividad toohello SQL Server instancia contenedor Hola base de datos que tiene previsto toomigrate, no es necesario tooinstall en el equipo que hospeda Hola Hola instancia de SQL Server.

     ![abrir data migration assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. En el menú izquierdo de hello, haga clic en **+ nuevo** toocreate una **evaluación** proyecto. Rellene el formulario de hello con un **nombre del proyecto** (todos los demás valores deben dejarse en sus valores predeterminados) y haga clic en **crear**. Hola **opciones** se abre la página.

     ![nuevo proyecto de data migration assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. En hello **opciones** página, haga clic en **siguiente**. Hola **seleccione orígenes** se abre la página.

     ![opciones de nueva migración de datos](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. En hello **seleccione orígenes** escriba Hola nombre de instancia de SQL Server que contiene el servidor de hello piensa toomigrate. Cambio Hola otros valores de esta página si es necesario. Haga clic en **Conectar**.

     ![seleccione orígenes de nueva migración de datos](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. Hola **agregar orígenes** parte del programa Hola a **seleccione orígenes** , seleccione las casillas de verificación de Hola para toobe de bases de datos de hello probado la compatibilidad. Haga clic en **Agregar**.

     ![seleccione orígenes de nueva migración de datos](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Haga clic en **Iniciar evaluación**.

     ![inicio de la evaluación de la nueva migración de datos](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Cuando se completa la evaluación de hello, busque primero toosee si base de datos de hello toomigrate suficientemente compatible. Busque la marca de verificación de hello en un círculo verde.

     ![resultado de evaluación de la nueva migración de datos compatible](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Revisar resultados de Hola. Hola **paridad de características de SQL Server** resultados que se muestran son Hola predeterminado resultados tooreview. En concreto, revise Hola sobre las características no compatibles y parcialmente compatibles, Hola proporciona información sobre y las acciones recomendadas. 

     ![evaluación de la nueva migración de datos paridad](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Hola de revisión **problemas de compatibilidad** haciendo clic en esta opción en la parte superior izquierda de Hola. Revisión específicamente Hola información acerca de bloqueos de la migración, cambios de comportamiento y características para cada nivel de compatibilidad en desuso. Para base de datos de hello AdventureWorks2008R2, revise esos cambios de hello tooSERVERPROPERTY('LCID') de cambios de búsqueda de texto tooFull desde hello y SQL Server 2008 desde SQL Server 2000. Para obtener información sobre estos cambios, se proporcionan vínculos para obtener más información. Muchas opciones de búsqueda y la configuración de búsqueda de texto completo han cambiado. 

   > [!IMPORTANT] 
   > Después de migrar la base de datos SQL de tooAzure de base de datos, puede elegir la base de datos de toooperate hello en su nivel de compatibilidad actual (nivel 100 para la base de datos de AdventureWorks2008R2 de hello) o en un nivel superior. Para obtener más información sobre las implicaciones de Hola y opciones para el funcionamiento de una base de datos en un nivel de compatibilidad específico, consulte [nivel de compatibilidad de ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Vea también [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obtener información acerca de la configuración de nivel de base de datos adicional relacionados con los niveles de toocompatibility.
   >

10. Si lo desea, haga clic en **Exportar informe** informe de hello toosave como un archivo JSON.
11. Hola cerrar el Asistente de migración de datos.

## <a name="export-toobacpac-file"></a>Archivo de exportación tooBACPAC 

Un archivo BACPAC es un archivo ZIP con una extensión de BACPAC que contiene los metadatos de Hola y los datos de una base de datos de SQL Server. Un archivo BACPAC puede almacenarse en el almacenamiento de blobs de Azure o en el almacenamiento local para el archivado o para la migración: como de SQL Server tooAzure base de datos SQL. Para una toobe de exportación transaccionalmente coherente, no debe asegurarse de que ninguna escritura se produce actividad durante la exportación de Hola.

Siga estos pasos toouse hello SQLPackage utilidad de línea de comandos tooexport hello AdventureWorks2008R2 base de datos toolocal almacenamiento de información.

1. Abra un símbolo del sistema de Windows y cambie la carpeta de tooa de directorio en el que tenga hello **130** versión de SQLPackage: como **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.

2. Ejecutar el siguiente comando de SQLPackage en Hola símbolo tooexport Hola de Hola **AdventureWorks2008R2** desde la base de datos **localhost** demasiado**AdventureWorks2008R2.bacpac**. Cambiar cualquiera de estos valores como entorno de tooyour adecuado.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![exportación de sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Una vez completada la ejecución de Hola Hola genera BACPAC archivo se almacena en directorio Hola donde se encuentra hello sqlpackage ejecutable. En este ejemplo, C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/). Inicia sesión desde el equipo de Hola desde el que se ejecuta la utilidad de línea de comandos de hello SQLPackage facilita la creación de Hola Hola de regla de firewall en el paso 5.

## <a name="create-a-sql-server-logical-server"></a>Crear un servidor lógico de SQL Server

Un [servidor lógico de SQL Server](sql-database-features.md) actúa como el punto central de administración de varias bases de datos. Siga estos pasos toocreate un Hola de toocontain de servidor lógico de SQL server migra la base de datos OLTP de Adventure Works SQL Server. 

1. Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.

2. Tipo de **sql server** en la ventana de búsqueda de hello en hello **New** página y seleccione **base de datos SQL (servidor lógico)** de hello filtra la lista.

    ![seleccionar servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. En hello **todo** página, haga clic en **SQL server (servidor lógico)** y, a continuación, haga clic en **crear** en hello **SQL Server (servidor lógico)** página .

    ![crear un servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Rellene Hola SQL server (servidor lógico) formulario con hello después de obtener información, como se muestra en hello anterior imagen:     

   | Configuración       | Valor sugerido | Descripción | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Escriba un nombre único global. | Para conocer cuáles son los nombres de servidor válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura). | 
   | **Inicio de sesión del administrador del servidor** | Escriba cualquier nombre válido. | Para conocer los nombres de inicio de sesión válidos, consulte [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificadores de base de datos). |
   | **Password** | Escriba cualquier contraseña válida. | La contraseña debe tener al menos 8 caracteres y debe contener caracteres de tres de las siguientes categorías de hello: caracteres en mayúsculas, caracteres en minúsculas, números y caracteres no alfanuméricos. |
   | **Suscripción** | Selección de una suscripción | Para más información acerca de sus suscripciones, consulte [Suscripciones](https://account.windowsazure.com/Subscriptions). |
   | **Grupos de recursos** | Elija un grupo de recursos existente o cree uno nuevo, como **myResourceGroup** |  Para conocer cuáles son los nombres de grupo de recursos válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura). |
   | **Ubicación** | Escriba ninguna ubicación válida para el nuevo servidor de Hola | Para obtener información acerca de las regiones, consulte [Regiones de Azure](https://azure.microsoft.com/regions/). |

   ![formulario de creación de servidor lógico completado](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Haga clic en **crear** servidor lógico de tooprovision Hola. El aprovisionamiento tarda unos minutos. 

> [!IMPORTANT]
> Recuerde el nombre del servidor, el nombre de inicio de sesión del administrador del servidor y la contraseña. Necesitará estos valores más adelante en el tutorial.
>

## <a name="create-a-server-level-firewall-rule"></a>Crear una regla de firewall de nivel de servidor

Hola servicio de base de datos SQL crea un [firewall en el nivel de servidor hello](sql-database-firewall-configure.md) que evita que las aplicaciones externas y las herramientas conectan toohello server o las bases de datos en el servidor de Hola a menos que se crea una regla de firewall tooopen Hola Firewall para direcciones IP concretas. Siga estos toocreate pasos una regla de firewall de nivel de servidor de base de datos SQL para la dirección IP de Hola del equipo de Hola desde el que se ejecuta la utilidad de línea de comandos de SQLPackage de Hola. Esto permite a SQLPackage tooconnect toohello SQL Server Database servidor lógico a través del firewall de base de datos de SQL Azure Hola. 

1. Haga clic en **todos los recursos** del menú izquierdo hello y haga clic en el nuevo servidor en hello **todos los recursos** página. página de información general de Hello para el servidor se abre y proporciona opciones para otra configuración.

     ![información general del servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Haga clic en **Firewall** en el menú izquierdo de hello en **configuración** en la página de información general de Hola. Hola **configuración del Firewall** se abre la página servidor de base de datos de SQL de Hola. 

3. Haga clic en **agregar dirección IP del cliente** en hello barra de herramientas tooadd Hola dirección IP del equipo de Hola que está usando actualmente y, a continuación, haga clic en **guardar**. Se creará una regla de firewall de nivel de servidor para esta dirección IP.

     ![establecer regla de firewall del servidor](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. Haga clic en **Aceptar**.

Ahora puede conectarse tooall bases de datos en este servidor mediante SQL Server Management Studio u otra herramienta de su elección de esta dirección IP con cuenta de administrador de servidor hello creado anteriormente.

> [!NOTE]
> SQL Database se comunica a través del puerto 1433. Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 1433. Si es así, no se puede conectar el servidor de base de datos de SQL Azure tooyour a menos que el departamento de TI abre el puerto 1433.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>Importar un tooAzure de archivo BACPAC base de datos SQL 

versiones más recientes de Hola de hello utilidad de línea de comandos SQLPackage proporcionan compatibilidad para crear una base de datos de SQL Azure en un determinado [nivel y el rendimiento del servicio](sql-database-service-tiers.md). Para mejorar el rendimiento durante la importación, seleccione un alto rendimiento y la capa de nivel de servicio y, a continuación, reducir verticalmente después de la importación si nivel de rendimiento y de nivel de servicio de hello es mayor que haya inmediatamente.

Siga estos pasos use hello SQLPackage utilidad de línea de comandos tooimport hello AdventureWorks2008R2 base de datos tooAzure base de datos SQL. Aunque puede usar SQL Server Management Studio para esta tarea, SQLPackage es el método de hello preferido para la mayoría de entornos de producción para obtener la máxima flexibilidad y un rendimiento óptimo. Vea [migración desde SQL Server tooAzure base de datos de SQL mediante archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- Ejecutar el siguiente comando de SQLPackage en Hola símbolo tooimport Hola de Hola **AdventureWorks2008R2** base de datos de servidor lógico de almacenamiento local toohello SQL server que se tooa creado anteriormente nueva base de datos, un servicio nivel de **Premium**y un objetivo de servicio **P6**. Sustituir valores de hello de corchetes angulares con los valores adecuados para el servidor lógico de SQL server y especifique un nombre para hello nueva base de datos (también reemplazar Hola los corchetes). También puede elegir valores de hello toochange para ediciones de base de datos y servicio objectgive como entorno de tooyour adecuado. A fin de Hola de este tutorial, se denomina base de datos migrada hello **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![importación de sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Un servidor lógico de SQL Server escucha en el puerto 1433. Si estás intentando tooconnect tooa lógico servidor de SQL server desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo hello para la conexión se toosuccessfully.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>Conexión con SQL Server Management Studio (SSMS)

Usar SQL Server Management Studio tooestablish un servidor de base de datos de SQL Azure tooyour de conexión y base de datos recién migrada, denominada **myMigratedDatabase** en este tutorial. Si está ejecutando SQL Server Management Studio en un equipo diferente desde el que ejecutó SQLPackage, cree una regla de firewall para este equipo mediante los pasos de hello en el procedimiento anterior de Hola.

1. Abra SQL Server Management Studio.

2. Hola **conectar tooServer** diálogo cuadro, escriba Hola siguiente información:
   - **Tipo de servidor**: especifique el motor de base de datos
   - **Nombre del servidor**: escriba el nombre completo del servidor, como **mynewserver20170403.database.windows.net**
   - **Autenticación**: especifique la autenticación de SQL Server
   - **Inicio de sesión**: escriba la cuenta de administrador del servidor
   - **Contraseña**: escriba la contraseña de hello para la cuenta de administrador del servidor
 
    ![conexión con ssms](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. Haga clic en **Conectar**. se abre la ventana del explorador de objetos de Hola. 

4. En el Explorador de objetos, expanda **bases de datos** y, a continuación, expanda **myMigratedDatabase** tooview objetos de hello en la base de datos de ejemplo de Hola.

## <a name="change-database-properties"></a>Modificación de las propiedades de la base de datos

Puede cambiar el nivel de servicio de hello, el nivel de rendimiento y el nivel de compatibilidad con SQL Server Management Studio. Durante la fase de importación de hello, se recomienda que importe tooa mayor rendimiento nivel base de datos para mejorar el rendimiento, pero reducir verticalmente al finalizar la importación de hello toosave dinero hasta que esté listo tooactively usar Hola importados base de datos. Cambiar el nivel de compatibilidad de hello, puede obtener un mejor rendimiento y capacidades más recientes de toohello de acceso del programa Hola a servicio de base de datos de SQL Azure. Al migrar una base de datos anterior, el nivel de compatibilidad de base de datos se mantiene en nivel de hello más bajo compatible que sea compatible con la base de datos de hello va a importar. Para más información, vea [Improved query performance with compatibility Level 130 in Azure SQL Database](sql-database-compatibility-level-query-performance-130.md) (Rendimiento mejorado de consultas con el nivel de compatibilidad 130 en Azure SQL Database).

1. En el Explorador de objetos, haga clic con el botón derecho en **myMigratedDatabase** y, luego, en **Nueva consulta**. Base de datos conectado tooyour abre en una ventana de consulta.

2. Ejecutar Hola siguiendo el nivel de servicio de comando tooset Hola demasiado**estándar** y Hola nivel de rendimiento demasiado**S1**.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![cambio de niveles de servicio](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. Ejecutar Hola siguiendo el nivel de compatibilidad de base de datos de comando toochange Hola demasiado**130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![cambio del nivel de compatibilidad](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Pasos siguientes 
En este tutorial ha preparado, exportado e importado una base de datos. Ha aprendido a:

> [!div class="checklist"]
> * Preparar una base de datos en un servidor SQL Server para la migración tooAzure base de datos SQL
> * Exportar archivo BACPAC de tooa de base de datos de Hola
> * Importar archivo BACPAC de hello en una base de datos de SQL Azure

Avanzar toohello siguiente tutorial toolearn cómo toosecure la base de datos.

> [!div class="nextstepaction"]
> [Protección de Azure SQL Database](sql-database-security-tutorial.md).



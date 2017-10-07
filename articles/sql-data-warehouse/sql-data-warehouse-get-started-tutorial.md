---
title: "Introducción aaaAzure almacenamiento de datos de SQL - tutorial | Documentos de Microsoft"
description: "Este tutorial le enseña cómo tooprovision y cargar datos en almacenamiento de datos de SQL Azure. También aprenderá los conceptos básicos de hello sobre el ajuste de escala, la pausa y la optimización."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>Introducción a SQL Data Warehouse

Este tutorial se muestra cómo tooprovision y cargar datos en almacenamiento de datos de SQL Azure. También aprenderá los conceptos básicos de hello sobre el ajuste de escala, la pausa y la optimización. Cuando haya terminado, podrá ser tooquery listo y explorar el almacenamiento de datos.

**Estimado toocomplete de tiempo:** se trata de un tutorial to-end con código de ejemplo que tarda unos 30 minutos toocomplete una vez que se cumplen los requisitos previos de Hola. 

## <a name="prerequisites"></a>Requisitos previos

tutorial de Hola se da por supuesto que está familiarizado con los conceptos básicos de almacenamiento de datos SQL. Si necesita una introducción, consulte [¿Qué es SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md) 

### <a name="sign-up-for-microsoft-azure"></a>Suscribirse a Microsoft Azure
Si ya no tiene una cuenta de Microsoft Azure, deberá toosign a una toouse este servicio. Si ya tiene una cuenta, puede omitir este paso. 

1. Navegar por las páginas de la cuenta de toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. Cree una cuenta de Azure gratis o compre una cuenta.
3. Siga las instrucciones de Hola

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>Instalación de las herramientas y los controladores del cliente SQL adecuados

Mayoría de las herramientas cliente SQL puede conectarse tooSQL almacenamiento de datos mediante ADO.NET, JDBC o ODBC. Debido a toohello un gran número de características de T-SQL que admite el almacenamiento de datos SQL, algunas aplicaciones cliente no son totalmente compatibles con el almacenamiento de datos de SQL.

Si está ejecutando un sistema operativo Windows, se recomienda usar [Visual Studio] o [SQL Server Management Studio].

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>Creación de Almacenamiento de datos SQL

SQL Data Warehouse es un tipo especial de base de datos diseñado para el procesamiento paralelo masivo. base de datos de Hola se distribuye por varios nodos y procesa las consultas en paralelo. Almacenamiento de datos de SQL tiene un nodo de control que orquesta las actividades de Hola de todos los nodos de Hola. nodos de Hello usan toomanage de base de datos SQL los datos.  

> [!NOTE]
> La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.  Para más información, consulte [Precios de Azure SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).
>

### <a name="create-a-data-warehouse"></a>Creación del almacenamiento de datos

1. Inicio de sesión en hello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo** > **Bases de datos** > **SQL Data Warehouse**.

    ![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png)![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. Rellene los detalles de la implementación

    **Nombre de la base de datos**: elija el que desee. Si tiene varios almacenes de datos, se recomienda que los nombres de incluyen detalles como la región de hello, entorno, por ejemplo *mydw-oesteee. UU.-1-test*.

    **Suscripción**: su suscripción a Azure

    **Grupo de recursos**: cree un grupo de recursos o seleccione uno existente.
    > [!NOTE]
    > Los grupos de recursos son útiles para realizar tareas de administración de recursos como el control de acceso y la implementación de plantillas. Consulte más información sobre los grupos de recursos de Azure [aquí](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).

    **Origen**: base de datos en blanco

    **Servidor**: servidor hello Select que creó en [requisitos previos].

    **Intercalación**: dejar la intercalación predeterminada de hello SQL_Latin1_General_CP1_CI_AS.

    **Seleccione rendimiento**: se recomienda empezar por 400DWU estándar Hola.

4. Elija **Pin toodashboard** ![tooDashboard de Pin](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. Póngase cómodo y espere a que su toodeploy de almacenamiento de datos. Es normal que este proceso tootake varios minutos. portal de Hello le avisa cuando el almacenamiento de datos toouse listo. 

## <a name="connect-toosql-data-warehouse"></a>Conectar tooSQL almacenamiento de datos

Este tutorial usa el almacenamiento de datos de SQL Server Management Studio (SSMS) tooconnect toohello. Se puede conectar tooSQL almacenamiento de datos a través de estos conectores compatibles: ADO.NET, JDBC, ODBC y PHP. Recuerde que la funcionalidad podría ser limitada para herramientas no compatibles con Microsoft.


### <a name="get-connection-information"></a>Obtención de información sobre la conexión

almacenamiento de datos de tooconnect tooyour, necesita tooconnect a través de servidor SQL lógico Hola que creó en [requisitos previos].

1. Seleccione el almacén de datos desde el panel de Hola o búsquelo en los recursos.

    ![Panel de SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. Encontrar el nombre completo de Hola para servidor SQL lógico de Hola.

    ![Seleccionar nombre del servidor](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. Abra SSMS y utilice el objeto explorer tooconnect toothis servidor mediante las credenciales de administrador de servidor hello que creó en [requisitos previos]

    ![Conectarse con SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

Si todo funciona correctamente, ahora debería tooyour conectado lógica SQL server. Puesto que ha iniciado la sesión Hola administrador del servidor, puede conectarse tooany base de datos hospedada por servidor de hello, incluida la base de datos maestra Hola. 

No hay cuenta de administrador de un solo servidor y tiene hello más privilegios de cualquier usuario. Procure no tooallow demasiadas personas de su contraseña de administrador de organización tooknow Hola. 

También puede tener una cuenta de administrador de Azure Active Directory, No ofrecemos detalles Hola aquí. Si desea que toolearn más sobre el uso de autenticación de Azure Active Directory, vea [autenticación de Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

A continuación, veremos la creación de usuarios e inicios de sesión adicionales.


## <a name="create-a-database-user"></a>Creación de un usuario de base de datos

En este paso, creará un tooaccess de cuenta de usuario a su almacén de datos. También le mostraremos cómo toogive ese toorun de capacidad de usuario hello las consultas con una gran cantidad de memoria y recursos de CPU.

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>Notas acerca de las clases de recursos para la asignación de recursos tooqueries

- tookeep los datos seguros, no use las consultas toorun de administración de servidor de hello en las bases de datos de producción. Tiene más privilegios de cualquier usuario hello y mediante tooperform operaciones en los datos de usuario coloca los datos en peligro. Además, puesto que Hola, Administrador de servidor se ha diseñado tooperform las operaciones de administración, se ejecuta operaciones con solo una pequeña asignación de memoria y recursos de CPU. 

- Almacenamiento de datos de SQL utiliza las funciones de base de datos predefinidos, llamado a las clases de recursos, tooallocate distintas cantidades de memoria, los recursos de CPU y toousers de ranuras de simultaneidad. Cada usuario puede pertenecer tooa clase de recursos pequeño, mediano, grande o extragrande. Hello clase de recurso del usuario determina Hola recursos Hola usuario tiene toorun consultas y operaciones de carga.

- Para la compresión de datos óptima, usuario Hola puede necesitar tooload con grandes o asignaciones de recursos extra grande. Obtenga más información sobre las clases de recursos [aquí](./sql-data-warehouse-develop-concurrency.md#resource-classes):

### <a name="create-an-account-that-can-control-a-database"></a>Creación de una cuenta que puede controlar una base de datos

Dado que han iniciado sesión en como administrador del servidor de Hola tiene usuarios e inicios de sesión de toocreate de permisos.

1. Con SSMS u otro cliente de consulta, abra una nueva consulta para **master**.

    ![Nueva consulta en Master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nueva consulta en Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. En la ventana de consulta de hello, ejecute este toocreate de comando de T-SQL un inicio de sesión denominado MedRCLogin y un usuario denominado LoadingUser. Este inicio de sesión puede conectarse toohello lógica SQL server.

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. Consultar ahora Hola *base de datos de almacenamiento de datos de SQL*, cree un usuario de base de datos basado en Hola inicio de sesión creado tooaccess y realizar operaciones en la base de datos de Hola.

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. Asigne Hola usuario control permisos toohello base de datos denominada NYT. 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > Si el nombre de la base de datos tiene guiones en ella, puede toowrap seguro de que entre corchetes. 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>Proporcionar a las asignaciones del medio de recursos de usuario de Hola

1. Ejecute este toomake de comando de T-SQL TI un miembro de clase de recurso intermedio hello, que se denomina mediumrc. 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > Haga clic en [aquí](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn más información acerca de las clases de simultaneidad y recursos. 
    >

2. Conectar el servidor lógico toohello con nuevas credenciales de Hola

    ![Inicie sesión con el nuevo inicio de sesión](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>Carga de datos del almacenamiento de blobs de Azure

Ahora está listo tooload datos en el almacenamiento de datos. Este paso muestra cómo de blob de datos de archivo cab de tooload ciudad de Nueva York taxi desde un almacenamiento de Azure público. 

- Una manera común de datos de tooload en almacenamiento de datos de SQL están toofirst mover el almacenamiento de blobs de hello datos tooAzure y, a continuación, cargarlos en el almacén de datos. toomake sea más fácil toounderstand cómo tooload, tenemos datos de archivo cab de Nueva York taxi ya hospedadas en un blob de almacenamiento de Azure pública. 

- En el futuro, toolearn cómo tooget su tooAzure datos blob almacenamiento o tooload directamente desde el origen en almacenamiento de datos de SQL, vea hello [cargar información general sobre](sql-data-warehouse-overview-load.md).


### <a name="define-external-data"></a>Definición de datos externos

1. Cree una clave maestra. Solo necesita toocreate una clave maestra de una vez por cada base de datos. 

    ```sql
    CREATE MASTER KEY;
    ```

2. Definir la ubicación de Hola de hello Azure blob que contiene los datos de archivo cab de hello taxi.  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. Definir los formatos de archivo externo de Hola

    Hola ```CREATE EXTERNAL FILE FORMAT``` comando es toospecify usa el formato de archivos que contienen datos externos de saludo. Dichos archivos contienen texto separado por uno o más caracteres, denominados delimitadores. Con fines de demostración, los datos de archivo cab de taxi de Hola se almacenan como datos sin comprimir tanto como gzip comprimido datos.

    Ejecutar estos comandos T-SQL toodefine dos formatos diferentes: sin comprimir y comprimido.

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  Cree un esquema para el formato de archivos externos. 

    ```sql
    CREATE SCHEMA ext;
    ```
5. Crear tablas externas de Hola. Estas tablas hacen referencia a los datos almacenados en Azure Blob Storage. Ejecute hello después toocreate de comandos de T-SQL en varias tablas externas que toohello de punto de todos los blobs de Azure hemos definido previamente en el origen de datos externo.

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>Importar datos de Hola desde el almacenamiento de blobs de Azure.

SQL Data Warehouse admite una instrucción clave denominada CREATE TABLE AS SELECT (CTAS). Esta instrucción crea una nueva tabla en función de los resultados de Hola de una instrucción select. Hola la nueva tabla tiene Hola mismos tipos de datos y columnas como resultados de Hola de hello instrucción select.  Se trata de un forma elegante que tooimport los datos desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL.

1. Ejecute este script tooimport los datos.

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. Consulte los datos mientras se carga.

   Está cargando varios gigabytes de datos y comprimiéndolos en índices de almacén de columnas en clúster de alto rendimiento. Ejecute hello después de consulta que usa un estado de administración dinámica (DMV) de vistas tooshow Hola de carga de Hola. Después de iniciar la consulta de hello, tome un café y una pequeña mientras el almacenamiento de datos SQL hace algún trabajo pesado.
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. Consulte todas las consultas del sistema.

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. Disfrute viendo cómo los datos se cargan ordenadamente en Azure SQL Data Warehouse.

    ![Consulte los datos cargados](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>Mejora del rendimiento de las consultas

Hay varias maneras tooimprove consulta el desempeño y tooachieve Hola rendimiento de alta velocidad que es el almacén de datos SQL diseñado tooprovide.  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>Ver Hola efecto de escala en el rendimiento de las consultas 

Rendimiento de las consultas tooimprove unidireccional es tooscale recursos cambiando el nivel de servicio DWU de hello para el almacenamiento de datos. Cada nivel de servicio cuesta más que el anterior, pero se puede reducir la escala o pausar recursos en cualquier momento. 

En este paso se compara el rendimiento de dos configuraciones de DWU distintas.

Primero, vamos a escalar el ajuste de tamaño de hello hacia abajo too100 DWU por lo que podemos obtener una idea de cómo un nodo de proceso puede realizar por sí mismo.

1. Vaya toohello portal y seleccione el almacenamiento de datos de SQL.

2. Seleccionar escala en la hoja de almacenamiento de datos SQL de Hola. 

    ![Escalado de Data Warehouse desde el portal](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. Reducir el rendimiento de hello barra too100 DWU y pulse Guardar.

    ![Escalar y guardar](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. Espere a que su toofinish de operación de escala.

    > [!NOTE]
    > No se pueden ejecutar las consultas al cambiar la escala de Hola. El escalado **elimina** las consultas actualmente en ejecución. Puede reiniciarlas una vez cuando finaliza la operación de Hola.
    >
    
5. Realice una operación de examen en los datos de ida y vuelta hello, seleccionando millones entradas superior de Hola para todas las columnas de Hola. Si le toomove diligente en rápidamente, sentirse tooselect libre menos filas. Tome nota de Hola que tarda toorun esta operación.

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. Escalar el almacenamiento de datos realizar copia de DWU too400. Recuerde que cada 100 DWU consiste en Agregar otro tooyour de nodo de proceso de almacenamiento de datos de SQL Azure.

7. ¡Vuelva a ejecutar la consulta de Hola! Debe observar una diferencia significativa. 

    > [!NOTE]
    > Dado que consulta Hola devuelve una gran cantidad de datos, disponibilidad de ancho de banda de Hola de máquina de hello ejecute SSMS puede ser un cuello de botella de rendimiento. Como consecuencia, es posible que no pueda ver ninguna mejora del rendimiento.

> [!NOTE]
> Como SQL Data Warehouse utiliza el procesamiento paralelo masivo, Las consultas que examinarán o realizan las funciones analíticas en millones de filas experimentar auténtica ventaja de Hola de almacenamiento de datos de SQL Azure.
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>Ver el efecto de Hola de estadísticas de rendimiento de las consultas

1. Ejecutar una consulta que une Hola tabla de fechas con tabla de ida y vuelta de Hola

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    Esta consulta tarda algún tiempo porque almacenamiento de datos de SQL tiene datos tooshuffle antes de realizar la combinación de Hola. Las combinaciones no tienen datos tooshuffle si son datos toojoin diseñado en hello igual que se distribuyó. Esto es un asunto más complicado. 

2. Las estadísticas marcan la diferencia. 
3. Ejecute este estadísticas de toocreate instrucciones en columnas de combinación de Hola.

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > SQL Data Warehouse no administra automáticamente las estadísticas para usted. Las estadísticas son importantes para el rendimiento de las consultas, por lo que se recomienda encarecidamente crearlas y actualizarlas.
    > 
    > **Obtenga Hola máximas ventajas al cuentan con estadísticas en las columnas que intervienen en las combinaciones, las columnas utilizadas en Hola donde se encuentran cláusula y columnas en GROUP BY.**
    >

3. Ejecute de nuevo la consulta de Hola de requisitos previos y observe las diferencias de rendimiento. Mientras que las diferencias de hello en el rendimiento de las consultas no será tan importante como el escalado, debe observar un acelerar. 

## <a name="next-steps"></a>Pasos siguientes

Ahora está listo tooquery y explorar. Consulte nuestras mejores prácticas o sugerencias.

Si ha terminado explorar por día de hello, asegúrese de toopause seguro de la instancia. En producción, puede experimentar una gran ahorro haciendo pausas y ajuste de escala toomeet sus necesidades empresariales.

![Pausar](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>Lecturas útiles

[Simultaneidad y administración de cargas de trabajo][]

[Procedimientos recomendados para Almacenamiento de datos SQL de Azure][]

[Supervisión de consultas][]

[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (Los 10 mejores procedimientos para compilar un almacén de datos relacionales a gran escala)

[Migrar datos tooAzure almacenamiento de datos SQL][]

[Simultaneidad y administración de cargas de trabajo]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Procedimientos recomendados para Almacenamiento de datos SQL de Azure]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Supervisión de consultas]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (Los 10 mejores procedimientos para compilar un almacén de datos relacionales a gran escala)
[Migrar datos tooAzure almacenamiento de datos SQL]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[requisitos previos]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx

---
title: aaaReporting entre bases de datos de escala horizontal en la nube | Documentos de Microsoft
description: "¿Cómo tooset elástico consultas en particiones horizontales"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Informes de bases de datos escaladas horizontalmente en la nube (vista previa)
![Consultas entre particiones][1]

Filas de distribución de bases de datos particionadas en un nivel de datos escalado horizontalmente. esquema de Hello es idéntica en todas las bases de datos participantes, que también se conoce como creación de particiones horizontales. Utilice una consulta elástica para crear informes que abarquen todas las bases de datos en una base de datos particionada.

Para un inicio rápido, consulte [Informes de bases de datos escaladas horizontalmente en la nube](sql-database-elastic-query-getting-started.md).

Para bases de datos no particionadas, consulte [Consulta de bases de datos elásticas para consultas entre bases de datos (particionamiento vertical)](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Requisitos previos
* Crear un mapa de particiones mediante la biblioteca de cliente de base de datos elástica Hola. Consulte [Administración de asignaciones particionadas](sql-database-elastic-scale-shard-map-management.md). O use la aplicación de ejemplo de Hola en [empezar a trabajar con herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).
* Como alternativa, vea [existente migrar bases de datos de las bases de datos fuera de tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).
* usuario de Hello debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE. Este permiso se incluye con el permiso ALTER DATABASE Hola.
* Los permisos ALTER ANY EXTERNAL DATA SOURCE son toohello toorefer necesario el origen de datos subyacentes.

## <a name="overview"></a>Información general
Estas instrucciones crean representación de metadatos de hello de la capa de datos particionada en base de datos de consulta flexible de Hola. 

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 Creación de clave maestra y credenciales con ámbito de base de datos
se utiliza la credencial de Hola Hola consulta elástico tooconnect tooyour remoto las bases de datos.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Asegúrese de que ese hello *"\<nombre de usuario\>"* no incluye ningún *"@servername"* sufijo. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 Creación de orígenes de datos externos
Sintaxis:

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Ejemplo
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Recuperar la lista de hello actual orígenes de datos externos: 

    select * from sys.external_data_sources; 

origen de datos externo de Hello hace referencia a la asignación de particiones. Una consulta flexible, a continuación, usa hello subyacente particiones tooenumerate hello las bases de datos que participan en la capa de datos de Hola y origen de datos externo de Hola. Hello mismas credenciales son mapa de particiones de hello tooread usado y tooaccess Hola datos en particiones de Hola durante el procesamiento de Hola de una consulta flexible. 

## <a name="13-create-external-tables"></a>1.3 Creación de tablas externas
Sintaxis:  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Ejemplo**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

Recuperar la lista de Hola de tablas externas de la base de datos actual de hello: 

    SELECT * from sys.external_tables; 

toodrop tablas externas:

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Comentarios
Hola datos\_cláusula de origen define el origen de datos externo de hello (un mapa de particiones) que se usa para la tabla externa de Hola.  

Hola esquema\_nombre y el objeto\_cláusulas nombre asignan Hola externo tooa tabla de definición de un esquema diferente. Si se omite, se asume el esquema de hello del objeto remoto hello toobe "dbo" y su nombre se supone el nombre de tabla externa de toobe toohello idénticos que se está definiendo. Esto es útil si Hola nombre de la tabla remota ya existe en la base de datos de Hola donde desea que la tabla externa de toocreate Hola. Por ejemplo, desea toodefine una tooget de tabla externa una vista agregada de las vistas de catálogo o capa de DMV en los datos de escalada horizontalmente. Puesto que las vistas de catálogo y DMV ya existen localmente, no puede utilizar sus nombres de definición de tabla externa de Hola. En su lugar, utilice un nombre diferente y usar la vista de catálogo de Hola u Hola nombre DMV Hola esquema\_nombre y/o objeto\_cláusulas de nombre. (Vea el siguiente ejemplo de Hola). 

cláusula de distribución de Hello especifica la distribución de datos de hello utilizada para esta tabla. procesador de consultas de Hello usa información de hello proporcionada Hola distribución cláusula toobuild hello más eficaces en planes de consulta.  

1. **PARTICIONADA** significa datos se particionan horizontalmente a través de las bases de datos de Hola. Hola clave de partición para la distribución de datos de hello es hello **< sharding_column_name >** parámetro.
2. **Replica** significa que copias idénticas de tabla Hola están presentes en cada base de datos. Es el tooensure de responsabilidad que las réplicas de hello son idénticas entre bases de datos de Hola.
3. **REDONDEAR\_ROBIN** significa que esa tabla Hola se particionan horizontalmente mediante un método de distribución depende de la aplicación. 

**Referencia de nivel de datos**: tabla externa de hello DDL hace referencia tooan origen de datos externo. origen de datos externo de Hello especifica un mapa de particiones que proporciona la tabla externa de Hola con hello información necesarios toolocate todas las bases de datos de hello en el nivel de datos. 

### <a name="security-considerations"></a>Consideraciones sobre la seguridad
Los usuarios con la tabla externa de acceso toohello automáticamente acceder toohello de tabla remota subyacente en credencial de hello dada en la definición de origen de datos externo de Hola. Evite no deseada elevación de privilegios a través de la credencial de Hola Hola externa del origen de datos. Use GRANT o REVOKE para una tabla externa como si fuera una tabla normal.  

Una vez que defina el origen de datos externo y las tablas externas, puede usar el T-SQL completo en las tablas externas.

## <a name="example-querying-horizontal-partitioned-databases"></a>Ejemplo: consulta de bases de datos con particiones horizontales
Hello siguiente consulta realiza una combinación de tres vías entre almacenes, pedidos y líneas de pedido y usa varios agregados y un filtro selectivo. Se supone la partición (1) horizontal (particionamiento) y (2) que almacenes, pedidos y líneas de pedido se particionada por columna de Id. de almacenamiento de hello, y esa consulta elástico Hola puede colocar combinaciones de hello en particiones de hello y procesar parte costosa de Hola de consulta de hello en hello particiones en paralelo. 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Procedimiento almacenado para la ejecución remota de T-SQL: sp\_execute_remote
Consulta flexible también introduce un procedimiento almacenado que proporciona acceso directo toohello particiones. Hola se llama al procedimiento almacenado [sp\_ejecutar \_remoto](https://msdn.microsoft.com/library/mt703714) y pueden ser utilizados tooexecute los procedimientos almacenados remotos o código de T-SQL en las bases de datos remoto de Hola. Toma Hola parámetros siguientes: 

* Nombre de origen de datos (nvarchar): nombre de Hola Hola externa del origen de datos de tipo RDBMS. 
* Consulta (nvarchar): Hola T-SQL consulta toobe ejecutado en cada partición. 
* Declaración de parámetro (nvarchar) - opcional: cadena con definiciones de tipo de datos de parámetros de hello utilizados en el parámetro de consulta de hello (por ejemplo, sp_executesql). 
* Lista de valores de los parámetros (opcional): lista separada por comas de valores de los parámetros (por ejemplo, sp_executesql)

Hola sp\_ejecutar\_remoto usa Hola proporcionada parámetros de invocación de Hola tooexecute Hola dada la instrucción de T-SQL en las bases de datos remoto de Hola de origen de datos externo. Utiliza credenciales de Hola Hola externo origen tooconnect toohello shardmap el Administrador de datos y bases de datos remoto de Hola.  

Ejemplo: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>Conectividad para herramientas
Usar regular tooconnect de cadenas de conexión de SQL Server la aplicación, la inteligencia empresarial y los datos integración herramientas toohello base de datos con las definiciones de tabla externa. Asegúrese de que SQL Server se admite como origen de datos para la herramienta. A continuación, hacer referencia a base de datos de consulta flexible de hello como cualquier otra herramienta de toohello conectado de la base de datos de SQL Server y use tablas externas desde la herramienta o la aplicación como si fueran tablas locales. 

## <a name="best-practices"></a>Prácticas recomendadas
* Asegúrese de que se le han otorgado esa base de datos de punto de conexión de consulta flexible de hello base de datos de access toohello shardmap y todas las particiones a través de hello que firewalls de la base de datos SQL.  
* Validar ni se exige la distribución de datos de hello definida por la tabla externa de Hola. Si la distribución de datos real es distinta del especificado en la definición de la tabla de distribución de hello, las consultas pueden producir resultados inesperados. 
* Consulta flexible actualmente no realiza eliminación de particiones cuando predicados de clave de particionamiento de Hola permitiría toosafely excluir ciertas particiones de procesamiento.
* Consulta flexible funciona mejor para las consultas que puede realizarse la mayor parte del cálculo de hello en particiones de Hola. Normalmente se obtendrá Hola mejor rendimiento de las consultas con predicados de filtro selectivo que se pueden evaluar en particiones de Hola o combinaciones sobre Hola claves que se pueden realizar de forma alineada por partición en todas las particiones de partición. Otros patrones de consulta pueden requerir grandes cantidades de datos desde el nodo principal de hello particiones toohello de tooload y pueden tener un rendimiento bajo

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).
* Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales)](sql-database-elastic-query-getting-started-vertical.md).
* Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)
* Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->

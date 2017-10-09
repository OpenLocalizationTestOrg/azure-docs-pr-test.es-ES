---
title: "las bases de datos aaaQuery a través de la nube con esquemas diferentes | Documentos de Microsoft"
description: "¿Cómo tooset consultas entre bases de datos en particiones verticales"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Consulta de bases de datos elásticas para consultas entre bases de datos (particionamiento vertical)
![Consultas entre tablas de bases de datos diferentes][1]

Las bases de datos con particiones verticales usan distintos conjuntos de tablas en bases de datos diferentes. Esto significa que el esquema hello es diferente en distintas bases de datos. Por ejemplo, todas las tablas de inventario se encuentran en una base de datos mientras que todas las relacionadas con la contabilidad se encuentran en otra. 

## <a name="prerequisites"></a>Requisitos previos
* usuario de Hello debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE. Este permiso se incluye con el permiso ALTER DATABASE Hola.
* Los permisos ALTER ANY EXTERNAL DATA SOURCE son toohello toorefer necesario el origen de datos subyacentes.

## <a name="overview"></a>Información general

> [!NOTE]
> A diferencia de con particiones horizontales, estas instrucciones de DDL no dependen de definir una capa de datos con un mapa de particiones a través de la biblioteca de cliente de base de datos elástica Hola.
>

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Creación de clave maestra y credenciales con ámbito de base de datos
se utiliza la credencial de Hola Hola consulta elástico tooconnect tooyour remoto las bases de datos.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Asegúrese de que hello `<username>` no incluye ningún **"@servername"** sufijo. 
>

## <a name="create-external-data-sources"></a>Creación de orígenes de datos externos
Sintaxis:

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> debe establecer el parámetro de tipo Hello demasiado**RDBMS**. 
>

### <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se muestra hello uso de hello instrucción CREATE para orígenes de datos externos. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

lista de hello tooretrieve actual orígenes de datos externos: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Tablas externas
Sintaxis:

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Ejemplo
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

Hola de ejemplo siguiente muestra cómo tooretrieve Hola lista de tablas externas de la base de datos actual de hello: 

    select * from sys.external_tables; 

### <a name="remarks"></a>Comentarios
Consulta flexible extiende Hola existente tabla externa sintaxis toodefine tablas externas que utilizan orígenes de datos externos del tipo RDBMS. Una definición de tabla externa para el particionamiento vertical trata Hola siguientes aspectos: 

* **Esquema**: tabla externa de hello DDL define un esquema que pueden usar las consultas. esquema de Hello proporcionado en la definición de tabla externa debe toomatch esquema de Hola de tablas de hello en hello bases de datos remoto donde se almacenan los datos reales de Hola. 
* **Referencia de base de datos remota**: tabla externa de hello DDL hace referencia tooan origen de datos externo. origen de datos externo de Hello especifica el nombre del servidor lógico de Hola y el nombre de base de datos de hello bases de datos remoto donde se almacenan datos de tabla real de Hola. 

Usa un origen de datos externos como se describe en la sección anterior de hello, tablas externas de hello sintaxis toocreate es la siguiente: 

cláusula de Hello DATA_SOURCE define el origen de datos externo de hello (es decir, Hola base de datos remota en el caso de las particiones verticales) que se usa para la tabla externa de Hola.  

cláusulas de Hello SCHEMA_NAME y OBJECT_NAME proporcionan Hola capacidad toomap Hola externo tooa tabla de definición de un esquema diferente en base de datos remota de Hola o tabla tooa con un nombre distinto, respectivamente. Esto es útil si desea que toodefine una vista de catálogo de tabla externa tooa o DMV en la base de datos remota - o cualquier otra situación donde nombre de la tabla remota de hello ya está en uso localmente.  

Hello siguiente instrucción DDL quita una definición de tabla externa existente de catálogo local Hola. No afecta a la base de datos remoto de Hola. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**Permisos para la tabla externa de CREATE/DROP**: se necesitan permisos ALTER ANY EXTERNAL DATA SOURCE de tabla externa DDL que también es necesario toorefer toohello origen de datos subyacente.  

## <a name="security-considerations"></a>Consideraciones sobre la seguridad
Los usuarios con la tabla externa de acceso toohello automáticamente acceder toohello de tabla remota subyacente en credencial de hello dada en la definición de origen de datos externo de Hola. Debe administrar con cuidado tabla externa de acceso toohello elevación de tooavoid no deseada de orden de privilegios a través de la credencial de Hola Hola externa del origen de datos. Permisos normales de SQL pueden ser usado tooGRANT o tabla externa de REVOCAR acceso tooan solo como si fuera una tabla normal.  

## <a name="example-querying-vertically-partitioned-databases"></a>Ejemplo: consulta de bases de datos con particiones verticales
Hello siguiente consulta realiza una combinación de tres vías entre dos tablas locales Hola para pedidos y líneas de pedido y tabla remota de Hola para los clientes. Este es un ejemplo de Hola caso de uso de datos de referencia de consulta flexible: 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


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
Puede usar el toodatabases de herramientas de integración de BI y los datos de regular tooconnect de cadenas de conexión de SQL Server en servidor de base de datos SQL de hello cuya consulta elástico habilitado y tablas externas definidas. Asegúrese de que SQL Server se admite como origen de datos para la herramienta. A continuación, consulte toohello consultar elástico base de datos y sus tablas externas al igual que cualquier base datos de SQL Server que se conectará toowith la herramienta. 

## <a name="best-practices"></a>Prácticas recomendadas
* Asegúrese de que esa base de datos de punto de conexión de consulta flexible de Hola se le han otorgado base de datos de access toohello remoto al habilitar el acceso para los servicios de Azure en su configuración de firewall de base de datos SQL. Asegúrese también de esa credencial Hola siempre que en datos externos de hello definición de origen puede iniciar sesión correctamente en la base de datos remota de Hola y tiene la tabla remota de hello permisos tooaccess Hola.  
* Consulta flexible funciona mejor para las consultas donde es posible la mayor parte del cálculo de hello en bases de datos remotas de Hola. Se obtiene normalmente Hola mejor rendimiento de las consultas con predicados de filtro selectivo que se pueden evaluar en bases de datos remotas de Hola o combinaciones que se pueden realizar por completo en la base de datos remota Hola. Otros patrones de consulta pueden requerir grandes cantidades de datos de la base de datos remota Hola de tooload y pueden tener un rendimiento bajo. 

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).
* Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales) (versión preliminar)](sql-database-elastic-query-getting-started-vertical.md).
* Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).
* Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->

---
title: "toouse aaaHow el procesamiento por lotes tooimprove rendimiento de la aplicación de base de datos de SQL Azure"
description: "tema Hello proporciona evidencia de que el procesamiento por lotes de base de datos operaciones en gran medida imroves Hola velocidad y la escalabilidad de las aplicaciones de base de datos de SQL Azure. Aunque estas técnicas de procesamiento por lotes de trabajo para cualquier base de datos de SQL Server, Hola Hola artículo está centrado en Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Cómo toouse tooimprove rendimiento de la aplicación de base de datos SQL de procesamiento por lotes
Procesamiento por lotes operaciones tooAzure base de datos SQL significativamente mejora el rendimiento de Hola y escalabilidad de las aplicaciones. En ventajas de orden toounderstand hello, primera parte de este artículo de hello cubre algunos resultados de pruebas de ejemplo que comparan solicitudes por lotes y los no secuenciales tooa base de datos SQL. Hello resto del artículo hello muestra técnicas de hello, escenarios y consideraciones toohelp toouse procesamiento por lotes correctamente en las aplicaciones de Azure.

## <a name="why-is-batching-important-for-sql-database"></a>¿Por qué es el procesamiento por lotes importante para Base de datos SQL?
El servicio remoto tooa llamadas de procesamiento por lotes es una estrategia conocida para aumentar el rendimiento y escalabilidad. Fijos de procesar las interacciones de tooany de costos con un servicio remoto, por ejemplo, la serialización, la transferencia de red y la deserialización. El empaquetado de muchas transacciones diferentes en un único lote minimiza estos costos.

En este documento, deseamos tooexamine diversos escenarios y las estrategias de procesamiento por lotes de base de datos SQL. Aunque estas estrategias también son importantes para las aplicaciones locales que utilizan SQL Server, hay varias razones para resaltar el uso de Hola de procesamiento por lotes para base de datos SQL:

* Hay potencialmente mayor latencia de red al obtener acceso a la base de datos de SQL, especialmente si tiene acceso a base de datos SQL de hello exterior mismo centro de datos de Microsoft Azure.
* características multiempresa de Hola de base de datos SQL decir Hola eficacia de los datos de hello tener acceso a la capa correlaciona toohello escalabilidad global de base de datos de Hola. Base de datos SQL debe impedir que cualquier inquilino o usuario individual monopolice toohello detrimento de recursos de base de datos de otros inquilinos. En respuesta toousage que superan las cuotas predefinidas, base de datos SQL puede reducir el rendimiento o responder con excepciones de limitación. Las eficiencias, como el procesamiento por lotes, permiten toodo más trabajo en la base de datos SQL antes de alcanzar estos límites. 
* Además, el procesamiento por lotes es efectivo para las arquitecturas que usan varias bases de datos (particionamiento). eficacia de saludo de la interacción con cada unidad de base de datos sigue siendo un factor clave para la escalabilidad global. 

Una de las ventajas de hello del uso de la base de datos SQL es que no tiene servidores de hello toomanage esa base de datos de Hola de host. Sin embargo, esta infraestructura administrada significa también que haya toothink diferente acerca de las optimizaciones de la base de datos. Ya no se puede buscar la infraestructura de red o de hardware de la base de datos del hello tooimprove. porque Microsoft Azure controla esos entornos. área principal de Hola que puede controlar es cómo interactúa la aplicación con la base de datos SQL. El procesamiento por lotes es una de estas optimizaciones. 

primera parte de Hola de papel Hola examina diversas técnicas de procesamiento por lotes para aplicaciones de .NET que usan la base de datos de SQL. Hola dos últimas secciones tratan instrucciones y escenarios de procesamiento por lotes.

## <a name="batching-strategies"></a>Estrategias de procesamiento por lotes
### <a name="note-about-timing-results-in-this-topic"></a>Nota sobre los tiempos resultantes en este tema
> [!NOTE]
> Resultados no son pruebas comparativas sino que pretenden tooshow **rendimiento relativo**. Los tiempos se basan en un promedio de un mínimo de 10 series de pruebas. Las operaciones son inserciones en una tabla vacía. Estas pruebas se pre-V12 medido, y no corresponde necesariamente toothroughput que pueden producirse en una base de datos de V12 mediante Hola nueva [niveles de servicio](sql-database-service-tiers.md). beneficio relativo de Hola de hello técnica de procesamiento por lotes debe ser similar.
> 
> 

### <a name="transactions"></a>Transacciones
Parece extraño toobegin una revisión del procesamiento por lotes hablando de transacciones. Pero el uso de Hola de transacciones de cliente tiene un efecto de procesamiento por lotes de servidor sutil que mejora el rendimiento. Y las transacciones se pueden agregar con solo unas pocas líneas de código, lo que proporciona un rendimiento de tooimprove de forma más rápida de las operaciones secuenciales.

Tenga en cuenta el siguiente código de C# que contiene una secuencia de inserción de Hola y operaciones update en una tabla sencilla.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

Hola después el código de ADO.NET secuencialmente realiza estas operaciones.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Hola toooptimize de manera mejor este código es tooimplement alguna forma de procesamiento por lotes del lado cliente de estas llamadas. Pero hay una manera sencilla tooincrease Hola de rendimiento de este código ajustando simplemente secuencia Hola de llamadas en una transacción. Aquí es Hola mismo código que usa una transacción.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

Realmente, se usan transacciones en ambos ejemplos. En el primer ejemplo de Hola, cada llamada individual es una transacción implícita. En el segundo ejemplo de Hola, una transacción explícita ajusta todas las llamadas de Hola. Por documentación Hola Hola [registro de transacciones de escritura anticipada](https://msdn.microsoft.com/library/ms186259.aspx), entradas de registro son toohello vaciado disco cuando se confirma la transacción de Hola. Por lo que al incluir más llamadas en una transacción, hello registro de transacciones de escritura toohello puede retrasar hasta que se confirma la transacción de Hola. En efecto, va a habilitar el procesamiento por lotes para el registro de transacciones del servidor de hello escrituras toohello.

Hello en la tabla siguiente muestra algunos resultados de pruebas ad hoc. pruebas de Hello realizan Hola que mismo secuencial inserta con y sin transacciones. Para tener más perspectiva, primer conjunto de pruebas de hello ejecutó remotamente desde una base de datos de toohello portátil en Microsoft Azure. Hello segundo conjunto de pruebas se ejecutaba desde un servicio en la nube y la base de datos que residían en hello mismo centro de datos de Microsoft Azure (US occidental). Hello siguiente tabla muestra hello duración en milisegundos de inserciones secuenciales con y sin transacciones.

**TooAzure local**:

| Operaciones | Ninguna transacción (ms) | Transacción (ms) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12662 |10395 |
| 1000 |128852 |102917 |

**Azure tooAzure (mismo centro de datos)**:

| Operaciones | Ninguna transacción (ms) | Transacción (ms) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21479 |2756 |

> [!NOTE]
> Los resultados no sirven para pruebas comparativas. Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).
> 
> 

En función de los resultados de pruebas anteriores hello, ajustar una única operación en una transacción reduce realmente el rendimiento. Pero medida que aumenta el número de Hola de operaciones en una única transacción, la mejora del rendimiento Hola se vuelve más marcada. diferencia de rendimiento de Hello también es más destacable cuando todas las operaciones se producen en el centro de datos de hello Microsoft Azure. Hello mayor latencia del uso de base de datos SQL desde el centro de datos de Microsoft Azure Hola exterior oculta mejora del rendimiento Hola de utilizar transacciones.

Aunque el uso de Hola de transacciones puede aumentar el rendimiento, continuar demasiado[observando las prácticas recomendadas para las conexiones y transacciones](https://msdn.microsoft.com/library/ms187484.aspx). Mantener transacciones hello más corta como conexión de base de datos de hello posible y, a continuación, cierre después de que el trabajo de hello completa. Hola utilizando la instrucción en el ejemplo anterior de hello garantiza que se cierra la conexión de hello cuando finaliza el bloque de código siguiente Hola.

ejemplo de Hola anterior muestra que puede agregar un código de ADO.NET de transacción local tooany con dos líneas. Las transacciones ofrecen una forma rápida de rendimiento de hello tooimprove del código que realiza secuencial inserciones, actualizaciones y las operaciones de eliminación. Sin embargo, para lograr rendimiento hello, considere la posibilidad de cambiar Hola código tootake ventaja adicional de procesamiento por lotes de cliente, como los parámetros con valores de tabla.

Para obtener más información acerca de las transacciones en ADO.NET, consulte [Transacciones locales](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>Parámetros con valores de tabla
Los parámetros con valores de tabla admiten tipos de tabla definidos por el usuario como parámetros en instrucciones Transact-SQL, procedimientos almacenados y funciones. Esta técnica de procesamiento por lotes del lado cliente permite toosend varias filas de datos de parámetro con valores de tabla de hello. parámetros con valores de tabla toouse, definir un tipo de tabla. Hola después de la instrucción Transact-SQL crea un tipo de tabla denominado **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


En código, cree un **DataTable** con hello exactamente los mismos nombres y tipos de tipo de tabla de Hola. Pase este **DataTable** en un parámetro de una consulta de texto o una llamada de procedimiento almacenado. Hello en el ejemplo siguiente se muestra esta técnica:

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

En el ejemplo anterior de hello, Hola **SqlCommand** objeto inserta filas de un parámetro con valores de tabla,  **@TestTvp** . Hola creado anteriormente **DataTable** se asigna al objeto parámetro toothis con hello **SqlCommand.Parameters.Add** método. Procesamiento por lotes inserciones de hello en uno llamar a significativamente aumenta Hola de rendimiento a través de las inserciones secuenciales.

tooimprove Hola ejemplo anterior aún más, utilice un procedimiento almacenado en lugar de un comando basado en texto. Hola siguiente comando de Transact-SQL crea un procedimiento almacenado que toma hello **SimpleTestTableType** parámetro con valores de tabla.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

A continuación, cambie hello **SqlCommand** declaración en siguiente para toohello de ejemplo anterior código de hello del objeto.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

En la mayoría de los casos, los parámetros con valores de tabla tienen un rendimiento equivalente o mejor que otras técnicas de procesamiento por lotes. Los parámetros con valores de tabla son a menudo preferibles, ya que son más flexibles que otras opciones. Por ejemplo, otras técnicas como la copia masiva de SQL sólo permiten inserción Hola de filas nuevas. Pero con parámetros con valores de tabla, puede usar lógica en toodetermine de procedimiento almacenado de hello qué filas son actualizaciones y que son inserciones. tipo de tabla de Hello también puede ser modificado toocontain una columna "Operación" que indica si Hola especifica fila debe insertarlos, actualizarlos o eliminarlos.

Hello en la tabla siguiente muestra los resultados de pruebas ad hoc para su uso de Hola de parámetros con valores de tabla en milisegundos.

| Operaciones | TooAzure local (ms) | Azure en el mismo centro de datos (ms) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10000 |23830 |3586 |

> [!NOTE]
> Los resultados no sirven para pruebas comparativas. Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).
> 
> 

Hola mejora del rendimiento de procesamiento por lotes es evidente inmediatamente. En la prueba secuencial anterior hello, 1000 operaciones tardaban 129 segundos fuera Hola datacenter y 21 segundos dentro del centro de datos de Hola. Pero con los parámetros con valores de tabla, 1000 operaciones aprovechar solo 2,6 segundos fuera del centro de datos de Hola y 0,4 segundos dentro del centro de datos de Hola.

Para obtener más información sobre los parámetros con valores de tabla, consulte [Usar parámetros con valores de tabla (motor de base de datos)](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>Copia masiva de SQL
Copia masiva de SQL es otra manera tooinsert grandes cantidades de datos en una base de datos de destino. Las aplicaciones .NET pueden utilizar hello **SqlBulkCopy** operaciones de inserción masiva de tooperform de clase. **SqlBulkCopy** es similar en la herramienta de línea de comandos de función toohello, **Bcp.exe**, o instrucción de Transact-SQL, hello **BULK INSERT**. Hello ejemplo de código siguiente muestra cómo toobulk Hola de copiar filas de origen de hello **DataTable**, tabla, tabla de destino toohello en SQL Server, MyTable.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

Hay algunos casos en que la copia masiva es preferible a los parámetros con valores de tabla. Vea la tabla de comparación de Hola de parámetros con valores de tabla frente a las operaciones BULK INSERT en el tema de hello [parámetros con valores de tabla](https://msdn.microsoft.com/library/bb510489.aspx).

Hello resultados de pruebas ad hoc siguientes muestran rendimiento de Hola de procesamiento por lotes con **SqlBulkCopy** en milisegundos.

| Operaciones | TooAzure local (ms) | Azure en el mismo centro de datos (ms) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10000 |21605 |2737 |

> [!NOTE]
> Los resultados no sirven para pruebas comparativas. Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).
> 
> 

En tamaños de lote menores, parámetros con valores de tabla de uso de hello superó hello **SqlBulkCopy** clase. Sin embargo, **SqlBulkCopy** realiza 12-31% más rápido que los parámetros con valores de tabla para las pruebas de Hola de 1.000 y 10.000 filas. Como los parámetros con valores de tabla, **SqlBulkCopy** es una buena opción para las inserciones por lotes, especialmente cuando se comparan toohello rendimiento de operaciones por lotes no.

Para obtener más información sobre la copia masiva en ADO.NET, consulte [Operaciones de copia masiva en SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Instrucciones INSERT con parámetros de varias filas
Una alternativa para los lotes pequeños es tooconstruct una gran parametrizar la instrucción INSERT que inserta varias filas. Hola, ejemplo de código siguiente muestra esta técnica.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


Este ejemplo está pensado concepto básico de tooshow Hola. Un escenario más realista se recorre en bucle Hola necesario entidades tooconstruct Hola cadena de consulta y parámetros de comando de hello simultáneamente. Está limitado tooa total de 2100 parámetros de consulta, lo que se limita el número total de Hola de filas que se pueden procesar de esta manera.

Hola tras la ejecución ad hoc prueba resultados mostrar hello de este tipo de instrucción de inserción en milisegundos.

| Operaciones | Parámetros con valores de tabla (ms) | Instrucción INSERT única (ms) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> Los resultados no sirven para pruebas comparativas. Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).
> 
> 

Este enfoque puede ser algo más rápido para los lotes de menos de 100 filas. Aunque Hola mejora es pequeña, esta técnica es otra opción que podría funcionar bien en el escenario de aplicación específica.

### <a name="dataadapter"></a>DataAdapter
Hola **DataAdapter** clase le permite toomodify una **conjunto de datos** de objeto y, a continuación, enviar cambios de hello como operaciones INSERT, UPDATE y DELETE. Si usas hello **DataAdapter** de esta manera, es importante toonote que separan las llamadas se realizan para cada operación. tooimprove rendimiento, use hello **UpdateBatchSize** número de toohello de propiedad de las operaciones que deben procesarse por lotes a la vez. Para obtener más información, consulte [Realizar operaciones por lotes mediante DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Entity Framework
Actualmente, Entity Framework no admite el procesamiento por lotes. Varios desarrolladores de la Comunidad de hello han intentado toodemonstrate las soluciones alternativas, como invalidación hello **SaveChanges** método. Pero Hola soluciones suelen ser complejas y personalizadas toohello aplicación y el modelo de datos. proyecto de codeplex de Entity Framework Hola actualmente tiene una página de conversación en esta solicitud de característica. tooview esta explicación, consulte [notas de la reunión de diseño - 2 de agosto de 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Por integridad, creemos que es importante tootalk sobre XML como una estrategia de procesamiento por lotes. Sin embargo, el uso de Hola de XML tiene ningún ventajas sobre otros métodos y varias desventajas. Hola consiste parámetros con valores de tootable similares, pero un archivo XML o una cadena se pasa el procedimiento almacenado de tooa en lugar de una tabla definida por el usuario. procedimiento almacenado de Hello analiza los comandos de hello en el procedimiento almacenado de Hola.

Hay varias desventajas toothis enfoque:

* El trabajo con XML puede resultar tedioso y propenso a errores.
* Hola análisis XML en la base de datos de hello puede usar mucha CPU.
* En la mayoría de los casos, este método es más lento que los parámetros con valores de tabla.

Por estos motivos, no se recomienda el uso de Hola de XML para las consultas del lote.

## <a name="batching-considerations"></a>Consideraciones sobre el procesamiento por lotes
Hola las secciones siguientes proporciona más instrucciones para el uso de Hola de procesamiento por lotes en las aplicaciones de base de datos SQL.

### <a name="tradeoffs"></a>Compromisos
Según la arquitectura, el procesamiento por lotes puede suponer un compromiso entre el rendimiento y la resistencia. Por ejemplo, considere el escenario de Hola donde su rol deja de funcionar inesperadamente. Si pierde una fila de datos, impacto hello es menor que el impacto de Hola de perder un lote grande de filas sin enviar. Hay un riesgo mayor cuando almacena filas en búfer antes de enviarlos toohello base de datos en un período de tiempo especificado.

Debido a esta contrapartida, evalúe el tipo de Hola de operaciones que procesa por lotes. Intensifique el procesamiento por lotes (con lotes y períodos de tiempo mayores) con aquellos datos que sean menos críticos.

### <a name="batch-size"></a>Tamaño de lote
En nuestras pruebas, normalmente no había ningún lote grande de toobreaking ventaja en fragmentos menores. De hecho, esta subdivisión produjo a menudo un rendimiento más lento que el envío de un único lote grande. Por ejemplo, considere un escenario donde desea tooinsert 1000 filas. Hello siguiente tabla muestra el tiempo que tarda parámetros con valores de tabla de toouse tooinsert 1000 filas cuando se divide en lotes más pequeños.

| Tamaño de lote | Iteraciones | Parámetros con valores de tabla (ms) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> Los resultados no sirven para pruebas comparativas. Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).
> 
> 

Puede ver el que obtener el mejor rendimiento para 1000 filas de hello toosubmit ellos a la vez. En otras pruebas (no mostradas aquí) hubo una toobreak de ganancia de rendimiento de pequeñas un lote de 10.000 filas en dos lotes de 5000. Pero el esquema de la tabla de Hola para estas pruebas es relativamente simple, por lo que debe realizar pruebas en los datos específicos y tooverify de tamaños de lote estos hallazgos.

Tooconsider de otro factor es que si el lote total de hello es demasiado grande, base de datos SQL puede limitar y rechazar por lotes de hello toocommit. Para obtener mejores resultados de hello, probar su escenario concreto toodetermine si hay un tamaño de lote ideal. Hacer que el tamaño del lote de hello configurable en tiempo de ejecución tooenable ajustes rápidos en función del rendimiento o de errores.

Por último, sopese tamaño Hola de lote de Hola y riesgos de hello asociados al procesamiento por lotes. Si hay errores transitorios o se produce un error en la función hello, considere la posibilidad de consecuencias de Hola de volver a intentar la operación de Hola o de pérdida de datos de hello en lote Hola.

### <a name="parallel-processing"></a>Procesamiento en paralelo
¿Qué ocurre si tardó enfoque Hola de reducir el tamaño del lote de hello pero utiliza varios subprocesos tooexecute Hola trabajo? Una vez más, nuestras pruebas mostraron que varios lotes multiproceso más pequeños presentaban normalmente un rendimiento peor que un único lote más grande. Hello prueba siguiente intenta tooinsert 1000 filas en uno o varios lotes paralelos. Esta prueba muestra cómo el uso de más lotes simultáneos realmente reduce el rendimiento.

| Tamaño de lote [iteraciones] | Dos subprocesos (ms) | Cuatro subprocesos (ms) | Seis subprocesos (ms) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> Los resultados no sirven para pruebas comparativas. Vea hello [Nota sobre los resultados de los intervalos en este tema](#note-about-timing-results-in-this-topic).
> 
> 

Hay varias razones posibles para la degradación de hello en rendimiento due tooparallelism:

* Se realizan varias llamadas de red simultáneas en lugar de una.
* Varias operaciones en una sola tabla pueden conllevar contención y bloqueo.
* Hay sobrecargas asociadas con el subprocesamiento múltiple.
* gastos de Hello supone abrir varias conexiones supera con creces las ventajas de Hola de procesamiento en paralelo.

Si elige como destino diferentes tablas o bases de datos, es posible toosee el aumento del rendimiento con esta estrategia. Un escenario de particionamiento de base de datos o de federaciones sería adecuado para este enfoque. Particionamiento utiliza varias bases de datos y base de datos de tooeach de datos diferentes de las rutas. Si cada lote pequeño va tooa otra base de datos, puede ser más eficaz, a continuación, realizar operaciones de hello en paralelo. Sin embargo, ganancia de rendimiento de hello no es toouse suficientemente importante como base de Hola para un particionamiento de base de datos de toouse de decisión de la solución.

En algunos diseños, la ejecución en paralelo de lotes más pequeños podría mejorar el rendimiento de las solicitudes en un sistema con mucha carga. En este caso, aunque es más rápido tooprocess un único lote mayor, procesamiento de varios lotes en paralelo puede ser más eficaz.

Si usa la ejecución en paralelo, considere la posibilidad de controlar número máximo de Hola de subprocesos de trabajo. Un número menor podría causar menos contención y un tiempo de ejecución más rápido. Además, considere la posibilidad de una carga adicional Hola que esto impone sobre la base de datos de destino de hello tanto en las conexiones y transacciones.

### <a name="related-performance-factors"></a>Factores de rendimiento relacionados
Las instrucciones típicas sobre el rendimiento de la base de datos también afectan al procesamiento por lotes. Por ejemplo, el rendimiento de inserción se reduce para aquellas tablas que tengan una clave principal grande o varios índices no agrupados.

Si los parámetros con valores de tabla utilizan un procedimiento almacenado, puede usar el comando hello **SET NOCOUNT ON** al principio de hello del procedimiento de Hola. Esta instrucción suprime la devolución de hello del recuento de Hola de filas de hello afectado en el procedimiento de Hola. Sin embargo, en nuestras pruebas, Hola uso de **SET NOCOUNT ON** no tiene ningún efecto o disminución del rendimiento. Hello procedimiento almacenado de prueba era simple con una sola **insertar** comando de parámetro con valores de tabla de hello. Es posible que los procedimientos almacenados más complejos se beneficien de esta instrucción. Pero no suponga que agregar **SET NOCOUNT ON** procedimiento tooyour almacenado mejora automáticamente el rendimiento. toounderstand Hola efecto, pruebe el procedimiento almacenado con y sin hello **SET NOCOUNT ON** instrucción.

## <a name="batching-scenarios"></a>Escenarios de procesamiento por lotes
Hello siguientes secciones se describen cómo parámetros con valores de tabla de toouse en tres escenarios de aplicación. Hola primer escenario muestra cómo almacenar en búfer y el procesamiento por lotes pueden trabajar juntos. segundo escenario de Hello mejora el rendimiento mediante la realización de operaciones de maestro y detalles en una llamada a procedimiento almacenado único. Hola último escenario muestra cómo toouse con valores de tabla de parámetros en una operación "UPSERT".

### <a name="buffering"></a>Almacenamiento en búfer
Aunque hay algunos escenarios que son candidatos obvios para el procesamiento por lotes, muchos otros podrían beneficiarse del procesamiento por lotes difiriendo el procesamiento. Sin embargo, también el procesamiento diferida conlleva un riesgo mayor de que se pueden perder datos de hello en caso de hello de un error inesperado. Es importante toounderstand este riesgo y tenga en cuenta las consecuencias de Hola.

Por ejemplo, considere una aplicación web que realiza un seguimiento del historial de navegación de Hola de cada usuario. En cada solicitud de página, aplicación hello podría realizar la vista de página de base de datos llamada toorecord Hola de un usuario. Pero se consigue un mayor rendimiento y escalabilidad: el almacenamiento en búfer las actividades de navegación de los usuarios de hello y, a continuación, enviar esta base de datos de toohello datos en lotes. Puede desencadenar la actualización de la base de datos de Hola por tiempo transcurrido o el tamaño de búfer. Por ejemplo, una regla podría especificar que ese lote Hola debe procesarse después de 20 segundos o al búfer de hello llegue a tener 1000 elementos.

siguiente Hola código de ejemplo utiliza [extensiones reactivas - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess almacenado en búfer los eventos generados por una clase de supervisión. Cuando Hola rellenos de búfer o se alcanza un tiempo de espera, se envía el lote de Hola de datos de usuario de base de datos de toohello con un parámetro con valores de tabla.

Hola NavHistoryData clase modelos Hola usuario navegación detalles siguientes. Contiene información básica como el identificador de usuario de hello, tiene acceso a la dirección URL de Hola y Hola hora de acceso.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

Hola NavHistoryDataMonitor clase es responsable de hello usuario navegación toohello de datos de almacenamiento en búfer. Contiene un método, RecordUserNavigationEntry, que responde generando un evento **OnAdded** . Hello código siguiente muestra la lógica del constructor Hola que utiliza Rx toocreate una colección observable basada en un evento de Hola. A continuación, se suscribe colección observable toothis con método de búfer de Hola. sobrecarga de Hello especifica que dicho búfer Hola se debe enviar cada 20 segundos o 1000 entradas.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

controlador de Hello convierte todos los elementos almacenados en búfer de hello en un tipo con valores de tabla y, a continuación, pasa este procedimiento tooa almacenado de tipo ese lote Hola de procesos. Hello código siguiente muestra toda la definición para las clases de NavHistoryDataMonitor de Hola y Hola NavHistoryDataEventArgs Hola.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse esta clase de almacenamiento en búfer, aplicación hello crea un objeto de NavHistoryDataMonitor estático. Cada vez que un usuario tiene acceso a una página de la aplicación hello llama método NavHistoryDataMonitor.RecordUserNavigationEntry de hello. Hola lógica de almacenamiento en búfer continúa tootake atención enviando estas bases de datos de toohello de entradas en lotes.

### <a name="master-detail"></a>Maestro/detalle
Los parámetros con valores de tabla son útiles en escenarios INSERT sencillos. Sin embargo, puede ser más difíciles inserciones toobatch que implican más de una tabla. escenario de "maestro y detalles" Hello es un buen ejemplo. tabla maestra Hola identifica la entidad primaria Hola. Una o varias tablas de detalle almacenen más datos sobre la entidad de Hola. En este escenario, las relaciones de clave externas Exigir relación Hola de entidad principal de detalles tooa única. Considere una versión simplificada de una tabla PurchaseOrder y su tabla OrderDetail asociada. Hola después de Transact-SQL crea la tabla de PurchaseOrder de hello con cuatro columnas: OrderID, OrderDate, CustomerID y estado.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Cada pedido contiene una o más compras de productos. Esta información se captura en la tabla PurchaseOrderDetail de Hola. Hola después de Transact-SQL crea la tabla PurchaseOrderDetail de hello con cinco columnas: OrderID, OrderDetailID, ProductID, UnitPrice y OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

columna OrderID de Hello en la tabla PurchaseOrderDetail de hello debe hacer referencia a un pedido de la tabla de PurchaseOrder Hola. Hola después de la definición de una clave externa aplica esta restricción.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

Parámetros con valores de tabla orden toouse, debe tener un tipo de tabla definido por el usuario para cada tabla de destino.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Después, defina un procedimiento almacenado que acepte tablas de estos tipos. Este procedimiento permite a un lote de solicitudes de toolocally un conjunto de pedidos y detalles de pedido en una sola llamada. Hello Transact-SQL siguiente proporciona declaración completa del procedimiento almacenado de hello en este ejemplo de pedido de compra.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

En este ejemplo, Hola definidas localmente @IdentityLink tabla almacena valores de hello reales OrderID de las filas de hello recién insertado. Estos identificadores de pedidos son diferentes de los valores de OrderID temporales Hola Hola @orders y @details parámetros con valores de tabla. Por esta razón, Hola @IdentityLink tabla, a continuación, conecta a valores de hello OrderID de hello @orders toohello real OrderID valores de parámetro para las nuevas filas en la tabla de PurchaseOrder Hola de Hola. Después de este paso, Hola @IdentityLink tabla puede facilitar Insertar detalles de pedido de hello con hello OrderID real que satisface la restricción de clave externa de Hola.

Este procedimiento almacenado puede usarse desde el código o desde otras llamadas Transact-SQL. Vea la sección de parámetros con valores de tabla de Hola de este documento para obtener un ejemplo de código. Hola después de Transact-SQL muestra cómo toocall Hola sp_InsertOrdersBatch.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

Esta solución permite que cada toouse por lotes un conjunto de valores de OrderID que empiezan en 1. Estos valores temporales de OrderID describen relaciones de hello en el lote de hello, pero los valores reales de OrderID de Hola se determinan en tiempo de Hola de operación de inserción de Hola. Puede ejecutar Hola mismas instrucciones en el ejemplo anterior de hello repetidamente y generar pedidos únicos en la base de datos de Hola. Por este motivo, podría agregar más lógica de base de datos o código que evite la duplicación de pedidos cuando se usa esta técnica de procesamiento por lotes.

Este ejemplo demuestra que las operaciones de base de datos más complejas, como las operaciones maestro/detalle, se pueden procesar por lotes con parámetros con valores de tabla.

### <a name="upsert"></a>UPSERT
Otro escenario de procesamiento por lotes supone la actualización de filas existentes y la inserción de nuevas filas de forma simultánea. A veces, esta operación es tooas que se hace referencia una operación "UPSERT" (actualización + inserción). En lugar de realizar llamadas independientes tooINSERT y UPDATE, instrucción MERGE de hello es mejor adecuado toothis tarea. Hola instrucción MERGE puede realizar ambas insert y las operaciones en una única llamada de actualización.

Parámetros con valores de tabla pueden utilizarse con hello mezcla instrucción tooperform actualizaciones e inserciones. Por ejemplo, considere una tabla de empleados simplificada que contiene Hola siguientes columnas: EmployeeID, FirstName, LastName, NúmeroSeguridadSocial:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

En este ejemplo, puede usar la ausencia de Hola que Hola NúmeroSeguridadSocial único tooperform una combinación de varios empleados. En primer lugar, cree el tipo de tabla definido por el usuario de hello:

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

A continuación, crear un procedimiento almacenado o escribir código que usa Hola actualización de Hola de tooperform de instrucción de combinación e insert. Hello en el ejemplo siguiente se utiliza Hola instrucción MERGE en un parámetro con valores de tabla, @employees, del tipo EmployeeTableType. Hola contenido de hello @employees tabla no se muestra aquí.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Para obtener más información, vea Hola documentación y ejemplos para la instrucción de combinación Hola. Aunque Hola se pudo realizar el mismo trabajo en varios pasos almacena la llamada al procedimiento con operaciones INSERT y UPDATE independientes, Hola instrucción MERGE es más eficaz. Código de la base de datos también puede construir llamadas de Transact-SQL que utilizan la instrucción MERGE de hello directamente sin necesidad de dos llamadas de base de datos para INSERT y UPDATE.

## <a name="recommendation-summary"></a>Resumen de recomendaciones
Hello lista siguiente proporciona un resumen de hello procesamiento por lotes las recomendaciones que se describen en este tema:

* Usar almacenamiento en búfer y rendimiento de hello tooincrease y la escalabilidad de las aplicaciones de base de datos SQL de procesamiento por lotes.
* Comprender el equilibrio de hello entre el procesamiento por lotes o el almacenamiento en búfer y resistencia. Error en un rol, riesgo de Hola de perder un lote sin procesar de los datos empresariales críticos puede contrarrestar ventaja de rendimiento de Hola de procesamiento por lotes.
* Intente tookeep todas las bases de datos de toohello llamadas dentro de una latencia de tooreduce único centro de datos.
* Si elige una única técnica de procesamiento por lotes, los parámetros con valores de tabla proporcionan flexibilidad y un rendimiento óptimo Hola.
* Para hello más rápido rendimiento de inserción, siga estas directrices generales y pruebe su escenario:
  * Para < 100 filas, use un único comando INSERT con parámetros.
  * Para < 1000 filas, use parámetros con valores de tabla.
  * Para > = 1000 filas, use SqlBulkCopy.
* Para actualizar y eliminar operaciones, usar parámetros con valores de tabla con lógica de procedimiento almacenado que determina el funcionamiento correcto de hello en cada fila de parámetro de tabla de hello.
* Instrucciones para el tamaño de lote:
  * Utilice Hola tamaños de lote mayores que tengan sentido para su aplicación y los requisitos empresariales.
  * Aumento del rendimiento de Hola de equilibrio de lotes de gran tamaño con los riesgos de Hola de errores temporales o catastróficos. ¿Qué es consecuencia de Hola de reintentos o pérdida de datos de hello en lote Hola? 
  * Probar Hola mayor lote tamaño tooverify que base de datos SQL no lo rechaza.
  * Cree la configuración ese control procesamiento por lotes, como el tamaño de lote de Hola o período de tiempo de almacenamiento en búfer de Hola. Estas configuraciones proporcionan flexibilidad. Puede cambiar Hola procesamiento por lotes de comportamiento en producción sin volver a implementar el servicio en la nube Hola.
* Evite la ejecución en paralelo de lotes que operan en una sola tabla en una base de datos. Si elige toodivide un único lote a través de varios subprocesos de trabajo, ejecute pruebas toodetermine Hola número ideal de subprocesos. Después de traspasar un umbral no especificado, el aumento del número de subprocesos hará que el rendimiento disminuya en lugar de mejorarlo.
* Considere la posibilidad de almacenar en búfer por tamaño y hora como una manera de implementar el procesamiento por lotes para más escenarios.

## <a name="next-steps"></a>Pasos siguientes
En este artículo se centra en cómo el diseño de la base de datos y técnicas de codificación relacionan toobatching puede mejorar el rendimiento de la aplicación y la escalabilidad. Sin embargo, esto es solamente un factor en la estrategia global. Para obtener más formas tooimprove rendimiento y la escalabilidad, vea [Guía de rendimiento de base de datos de SQL Azure para las bases de datos únicos](sql-database-performance-guidance.md) y [consideraciones de precio y el rendimiento para un grupo elástico](sql-database-elastic-pool-guidance.md).


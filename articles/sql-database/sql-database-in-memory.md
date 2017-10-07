---
title: "tecnologías de base de datos de SQL en memoria aaaAzure | Documentos de Microsoft"
description: "Las tecnologías de base de datos de SQL en memoria Azure mejoran considerablemente el rendimiento Hola de transaccional y cargas de trabajo de análisis. Obtenga información acerca de cómo tootake aprovechar estas tecnologías."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>Optimización del rendimiento mediante las tecnologías en memoria de SQL Database

Mediante el uso de tecnologías en memoria en Azure SQL Database, puede lograr mejoras de rendimiento con diversas cargas de trabajo: transaccionales (procesamiento de transacciones en línea [OLTP]), analíticas (procesamiento analítico en línea [OLAP]) y mixtas (procesamiento analítico y transaccional híbrido [HTAP]). Causa de Hola más eficiente de las consultas y procesamiento de transacciones, tecnologías en memoria también le ayudarán a tooreduce costo. Normalmente no es necesario hello tooupgrade tarifa de mejoras de rendimiento de tooachieve de base de datos de Hola. En algunos casos, es posible que incluso pueda reducir Hola tarifa, mientras se sigue viendo mejoras de rendimiento con tecnologías en memoria.

Estos son dos ejemplos de cómo OLTP en memoria ayudó a toosignificantly a mejorar el rendimiento:

- Mediante el uso de OLTP en memoria, [quórum Business Solutions era capaz de toodouble la carga de trabajo mientras mejoran la Dtu en un 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - DTU significa *Unidad de transmisión de datos*, e incluye una medida del consumo de recursos.
- Hello vídeo siguiente muestra mejora significativa del consumo de recursos con una carga de trabajo de ejemplo: [OLTP en memoria en el vídeo para la base de datos de SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Para obtener más información, consulte el blog de hello: [OLTP en memoria en la entrada de Blog de base de datos de SQL de Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

Tecnologías en memoria están disponibles en todas las bases de datos de nivel Premium de hello, incluidas bases de datos en grupos elásticos Premium.

Hello vídeo siguiente explica posibles mejoras de rendimiento con tecnologías en memoria en la base de datos de SQL Azure. Recuerde que la ganancia de rendimiento de Hola que siempre verá depende de muchos factores, como la naturaleza de Hola de carga de trabajo de Hola y de datos, el patrón de acceso de base de datos de hello y así sucesivamente.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

La base de datos de SQL Azure tiene Hola después de tecnologías en memoria:

- *OLTP en memoria* aumenta el rendimiento y reduce la latencia del procesamiento de transacciones. Estas son las situaciones en las que se obtienen ventajas con OLTP en memoria: procesamiento de transacciones de alto rendimiento, como operaciones comerciales y juegos, ingesta de datos de eventos o dispositivos de IoT, almacenamiento en caché, carga de datos y escenarios de tablas temporales y variables de tablas.
- *Índices de almacén de columnas clúster* reducen el consumo de almacenamiento (arriba too10 veces) y mejorar el rendimiento de las consultas de informes y análisis. Puede utilizarlo con las tablas de hechos en su toofit de los puestos de datos más datos en la base de datos y mejorar el rendimiento. Además, puede utilizarlo con datos históricos en la base de datos operativa tooarchive y ser capaz de tooquery too10 horas más datos.
- *Los índices no agrupados* para obtener ayuda HTAP toogain información en tiempo real sobre su empresa mediante la consulta Hola operativa base de datos directamente, sin Hola necesidad toorun costoso extracción, transformación y el proceso de carga (ETL) y espere para toobe de almacenamiento de datos de hello rellena. Índices no agrupados permiten una ejecución muy rápida de las consultas de análisis en la base de datos OLTP hello, al tiempo que reduce el impacto de hello en la carga de trabajo operativa Hola.
- También puede tener la combinación de Hola de una tabla con optimización para memoria con un índice de almacén. Esta combinación le permite tooperform muy rápido procesamiento de transacciones y demasiado*simultáneamente* análisis de ejecución consulta a muy rápidamente en hello mismo datos.

Los índices de almacén de columnas y OLTP en memoria han formado parte del producto de SQL Server de Hola desde 2012 y 2014, respectivamente. Base de datos SQL de Azure y SQL Server comparten Hola misma implementación de tecnologías en memoria. A partir de ahora, las nuevas funciones para estas tecnologías se publican primero en Azure SQL Database y después, en SQL Server.

En este tema se describe los aspectos de los índices de OLTP en memoria y almacén de columnas que están tooAzure específico de base de datos SQL y también incluye ejemplos:
- Podrá ver impacto Hola de estas tecnologías en límites de tamaño de almacenamiento y los datos.
- Podrá ver cómo toomanage Hola movimiento de bases de datos que usan estas tecnologías entre Hola diferente niveles de precios.
- Podrá ver dos ejemplos que ilustran el uso de Hola de OLTP en memoria, así como los índices de almacén de columnas de base de datos de SQL Azure.

Vea Hola siguientes recursos para obtener más información.

Obtener información detallada acerca de las tecnologías de hello:

- [Información general de OLTP en memoria y escenarios de uso](https://msdn.microsoft.com/library/mt774593.aspx) (incluye referencias toocustomer casos prácticos y tooget información iniciado)
- [Documentación de In-Memory OLTP](http://msdn.microsoft.com/library/dn133186.aspx)
- [Descripción de los índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx)
- Procesamiento analítico y transaccional híbrido (HTAP), también conocido como [análisis operativo en tiempo real](https://msdn.microsoft.com/library/dn817827.aspx)

Un texto elemental sobre rápido en OLTP en memoria: [inicio rápido 1: tecnologías de OLTP en memoria para el rendimiento de T-SQL con mayor rapidez](http://msdn.microsoft.com/library/mt694156.aspx) (empezar a otro artículo toohelp)

Vídeos en profundidad acerca de las tecnologías de hello:

- [OLTP en memoria en la base de datos de SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (que contiene una demostración de rendimiento ventajas y los pasos tooreproduce estos resultados usted mismo)
- [Vídeos OLTP en memoria: ¿Qué es/cómo y cuándo toouse,](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Columnstore Index: In-Memory Analytics Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/) (Índice de almacén de columnas: vídeos sobre análisis en memoria de Ignite 2016)

## <a name="storage-and-data-size"></a>Almacenamiento y tamaño de datos

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Límite de almacenamiento y tamaño de datos para OLTP en memoria

OLTP en memoria incluye tablas con optimización de memoria, que se usan para almacenar los datos de los usuarios. Estas tablas forman toofit necesario en la memoria. Dado que administra la memoria directamente en hello servicio de base de datos SQL, tenemos concepto Hola de una cuota para los datos de usuario. Esta idea es que se hace referencia tooas *almacenamiento de OLTP en memoria*.

Cada plan de tarifa de grupo elástico y de base de datos independiente admitido incluye una cantidad determinada de almacenamiento de OLTP en memoria. En tiempo de Hola de escritura, obtendrá un gigabyte de almacenamiento por cada 125 unidades de transacción de base de datos (Dtu) o la base de datos elástica unidades de transacción (Edtu).

Hola [niveles de servicio de base de datos SQL](sql-database-service-tiers.md) artículo tiene lista oficial de Hola de almacenamiento de OLTP en memoria de Hola que está disponible para cada una de las base de datos independiente y nivel de precios de grupo elástico.

Hola siguiendo el recuento de elementos hacia su límite de almacenamiento de OLTP en memoria:

- Las filas de datos de usuarios activos en tablas con optimización de memoria y variables de tabla. Tenga en cuenta que las versiones de fila anteriores no cuentan para el límite de Hola.
- Los índices de tablas con optimización de memoria.
- La sobrecarga operacional de operaciones ALTER TABLE.

Si alcanza el límite de hello, recibirá un error fuera de cuota y ya no es capaz de tooinsert o actualizar los datos. toomitigate este error, elimine datos o aumente Hola nivel de base de datos de Hola o un grupo de precios.

Para obtener más información acerca de cómo supervisar la utilización de almacenamiento de OLTP en memoria y la configuración de alertas cuando se alcance casi cap hello, consulte [almacenamiento en memoria de Monitor](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>Acerca de los grupos elásticos

Con grupos elásticos, Hola almacenamiento de OLTP en memoria se comparte entre todas las bases de datos en bloque de Hola. Por lo tanto, el uso de hello en una base de datos puede afectar a otras bases de datos. Existen dos formas de mitigar este problema:

- Configurar un Max-eDTU para bases de datos que es menor que el número de eDTU de Hola para grupo de Hola como un todo. Este valor máximo limita la utilización del almacenamiento de OLTP en memoria de hello, en cualquier base de datos en el grupo de hello, tamaño de toohello que corresponde el número de eDTU de toohello.
- Configurar un valor de eDTU mín. que sea mayor que 0. Este mínimo garantiza que cada base de datos en bloque de hello tiene cantidad Hola del almacenamiento de OLTP en memoria disponible que corresponde toohello habían configurado Min eDTU.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>Almacenamiento y tamaño de datos para los índices de almacén de columnas

Índices de almacén de columnas no son necesario toofit en la memoria. Por lo tanto, Hola solo límite en el tamaño de Hola de índices de hello es el tamaño de base de datos total máximo de hello, que se documenta en hello [niveles de servicio de base de datos SQL](sql-database-service-tiers.md) artículo.

Cuando se utilicen índices de almacén de columnas agrupado, compresión de columna se utiliza para el almacenamiento de tabla base Hola. Esta compresión puede reducir significativamente el espacio de almacenamiento de información de Hola de los datos de usuario, lo que significa que caben más datos en la base de datos de Hola. Y compresión de hello puede aumentarse aún más con [compresión de archivo columna](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). cantidad de Hola de compresión que se puede lograr depende de naturaleza Hola de datos de hello, pero la compresión 10 veces hello no es raro que.

Por ejemplo, si tiene una base de datos con un tamaño máximo de 1 terabyte (TB) y logran una compresión de hello 10 veces mediante el uso de índices de almacén de columnas, puede incluir un total de 10 TB de datos de usuario de base de datos de Hola.

Cuando utiliza los índices no agrupados, tabla de base de hello todavía se almacena en formato de almacén de filas tradicionales de Hola. Por lo tanto, no es tan grande como con índices de almacén de columnas agrupado Hola ahorro de almacenamiento. Sin embargo, si desea reemplazar un número de índices no clúster tradicionales con un índice de almacén de columnas único, todavía puede ver un ahorro general en el espacio de almacenamiento de información de hello para la tabla de Hola.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Movimiento de bases de datos que usan tecnologías en memoria entre planes de tarifa

Hay nunca las incompatibilidades u otros problemas al actualizar tooa superior tarifa, como de tooPremium estándar. solo aumentan los recursos y la funcionalidad disponible Hola.

Pero instalar versiones anteriores Hola tarifa puede repercutir negativamente en la base de datos. impacto de Hello es especialmente aparente cuando degrade desde tooStandard Premium o Basic cuando la base de datos contiene objetos de OLTP en memoria. Tablas optimizadas en memoria e índices de almacén de columnas, no están disponibles después de la degradación de hello (aunque sigan siendo visibles). Hola mismas consideraciones se aplican al bajar la Hola tarifa de un grupo elástico, o mover una base de datos con tecnologías en memoria, en un estándar o básico grupo elástico.

### <a name="in-memory-oltp"></a>In-Memory OLTP

*Degradar tooBasic/Standard*: OLTP en memoria no se admite en bases de datos de hello nivel estándar o básico. Además, no es posible toomove una base de datos que tiene cualquier toohello de objetos de OLTP en memoria nivel estándar o básico.

Antes de degradar la base de datos de hello tooStandard/Basic, quite todas las tablas optimizadas en memoria y tipos de tabla, así como todos los módulos T-SQL compilados de forma nativa.

No hay un mecanismo de programación toounderstand si una base de datos es compatible con OLTP en memoria. Puede ejecutar Hola después de consulta de Transact-SQL:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Si consulta Hola devuelve **1**, OLTP en memoria se admite en esta base de datos.


*Degradar de nivel inferior de Premium de tooa*: datos en tablas optimizadas en memoria deben caber dentro del almacenamiento de OLTP en memoria de Hola que está asociado con hello tarifa de base de datos de Hola o está disponible en el grupo elástico Hola. Si intente hello toolower tarifa o mover la base de datos de hello en un grupo que no tiene suficiente espacio disponible de OLTP en memoria, se produce un error en la operación de Hola.

### <a name="columnstore-indexes"></a>Índices de almacén de columnas

*Degradar tooBasic o estándar*: los índices se admiten únicamente en el nivel de precios Premium hello y no en el almacén de columnas Hola niveles estándar o básico. Cuando degrade la base de datos tooStandard o Basic, el índice de almacén de columnas no estará disponible. sistema de Hello mantiene el índice de almacén de columnas, pero nunca aprovecha el índice de Hola. Si más tarde actualiza tooPremium atrás, el índice de almacén de columnas es toobe inmediatamente listo aprovechado de nuevo.

Si tiene una **agrupado** índice de almacén de columnas, toda la tabla Hola deja de estar disponible después de la degradación de la capa. Por lo tanto, se recomienda quitar todas *agrupado* antes de degradar la base de datos por debajo del nivel Premium de Hola de índices de almacén de columnas.

*Degradar de nivel inferior de Premium de tooa*: esta degradación se realiza correctamente si la base de datos completa de hello quepa dentro de tamaño de base de datos máximo de hello para el nivel de precios de destino de hello, o dentro del almacenamiento disponible de hello en grupo elástico de Hola. No hay ningún impacto específico de índices de almacén de columnas de Hola.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Instalar el ejemplo de Hola a OLTP en memoria

Puede crear base de datos de ejemplo de Hola AdventureWorksLT con unos pocos clics en hello [portal de Azure](https://portal.azure.com/). A continuación, hello en esta sección se explica cómo puede enriquecer la base de datos AdventureWorksLT con objetos de OLTP en memoria y mostrar las ventajas de rendimiento.

Si desea ver una demostración más simple, pero más atractiva visualmente, del rendimiento de OLTP en memoria, consulte:

- Versión: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Código fuente: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Pasos de instalación

1. Hola [portal de Azure](https://portal.azure.com/), crear una base de datos Premium en un servidor. Conjunto hello **origen** toohello datos de ejemplo AdventureWorksLT. Para obtener instrucciones detalladas, consulte [Creación de la primera Base de datos SQL de Azure](sql-database-get-started-portal.md).

2. Conectar la base de datos de toohello con SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Hola copia [secuencia de comandos de Transact-SQL de OLTP en memoria](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Portapapeles. Hola script T-SQL crea Hola objetos necesarios en memoria Hola datos de ejemplo AdventureWorksLT que creó en el paso 1.

4. Pegue el script de T-SQL de hello en SSMS y, a continuación, ejecute el script de Hola. Hola `MEMORY_OPTIMIZED = ON` instrucciones CREATE TABLE, cláusula son cruciales. Por ejemplo:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Error 40536


Si recibe el error 40536 al ejecutar script de Hola T-SQL, ejecute hello después tooverify de script de T-SQL si admite la base de datos de hello en memoria:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


Un resultado de **0** significa que no se admite en memoria, mientras que un resultado de **1** significa que se admite. problema de hello toodiagnose, asegurarse de esa base de datos de hello está en nivel de servicio Premium de Hola.


#### <a name="about-hello-created-memory-optimized-items"></a>Acerca de hello creó elementos optimizadas en memoria

**Tablas**: ejemplo de Hola contiene hello las tablas optimizadas en memoria siguientes:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


Puede inspeccionar las tablas optimizadas en memoria a través de hello **Explorador de objetos** en SSMS. Haga clic con el botón derecho en **Tablas** > **Filtro** > **Configuración de filtro** > **Con optimización para memoria**. valor de Hello es igual a 1.


O bien, puede consultar vistas de catálogo de hello, como:


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**Procedimiento almacenado compilado de forma nativa**: puede inspeccionar SalesLT.usp_InsertSalesOrder_inmem mediante una consulta de la vista de catálogo:


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Ejecutar la carga de trabajo OLTP de ejemplo de Hola

Hola la única diferencia entre Hola siguiendo dos *procedimientos almacenados* es que el primer procedimiento de hello usa versiones optimizadas en memoria de tablas de hello, mientras Hola segundo procedimiento usa las tablas de hello normales en disco:

- SalesLT**.**usp_InsertSalesOrder**_inmem**
- SalesLT**.**usp_InsertSalesOrder**_ondisk**


En esta sección, verá cómo Hola práctica toouse **ostress.exe** tooexecute utilidad Hola dos procedimientos almacenados en los niveles de estrés. Puede comparar cuánto tiempo tarda Hola dos esfuerzo ejecuciones toofinish.


Cuando se ejecuta ostress.exe, se recomienda pasar valores de parámetro diseñados para los dos procedimientos siguientes de Hola:

- Ejecute un gran número de conexiones simultáneas, mediante el uso de -n100.
- Haga que cada conexión se repita en bucle cientos de veces, mediante el uso de -r500.


Sin embargo, conviene toostart con valores mucho más pequeños como - tooensure n10 y - r50 que todo funciona.


### <a name="script-for-ostressexe"></a>Script para ostress.exe


Esta sección muestra la secuencia de comandos de T-SQL de Hola que se incrusta en la línea de comandos ostress.exe. script de Hola usa elementos creados por hello script T-SQL que instaló con anterioridad.


Hello secuencia de comandos siguiente inserta un pedido de ventas de ejemplo con cinco elementos de línea siguiente Hola optimizadas en memoria *tablas*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


Hola toomake *_ondisk* versión de Hola anterior script T-SQL para ostress.exe, podría reemplazar las apariciones de hello *_inmem* substring con *_ondisk*. Estos reemplazos afectan a los nombres de Hola de tablas y procedimientos almacenados.


### <a name="install-rml-utilities-and-ostress"></a>Instalación de ostress y utilidades de RML


Idealmente, debería planear toorun ostress.exe en una máquina virtual (VM) de Azure. Debe crear un [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) Hola misma región geográfica Azure donde reside la base de datos AdventureWorksLT. Pero puede ejecutar si lo desea ostress.exe en el equipo portátil.


Hola VM o en cualquier host, elija, instalar utilidades de lenguaje de marcado de reproducción (RML) de Hola. Utilidades de Hello incluyen ostress.exe.

Para más información, consulte:
- Hola ostress.exe discusión en [base de datos de ejemplo para OLTP en memoria](http://msdn.microsoft.com/library/mt465764.aspx).
- [Base de datos de ejemplo para OLTP en memoria](http://msdn.microsoft.com/library/mt465764.aspx).
- Hola [blog para la instalación de ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Ejecute hello *_inmem* efectuar una carga de trabajo de esfuerzo en primer lugar


Puede usar un *RML Cmd Prompt* ventana toorun la línea de comandos ostress.exe. parámetros de línea de comandos de Hello directa ostress para:

- Ejecutar 100 conexiones simultáneamente (-n100).
- Dispone de cada conexión ejecutar script de Hola T-SQL 50 veces (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


Hola de toorun delante de la línea de comandos de ostress.exe:


1. Restablecer contenido de datos de base de datos de hello ejecutando Hola siguiente comando en SSMS, toodelete todos los datos de Hola que fuera insertados por todas las ejecuciones anteriores:

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Copiar texto hello de hello anterior ostress.exe línea de comandos tooyour Portapapeles.

3. Reemplace hello `<placeholders>` para hello parámetros -S - U -P -d con hello corregir valores reales.

4. Ejecute la línea de comandos modificada en una ventana del símbolo del sistema de RML.


#### <a name="result-is-a-duration"></a>El resultado es una duración


Cuando finaliza el ostress.exe, escribe Hola duración de la ejecución como su última línea de salida en la ventana de hello RML Cmd. Por ejemplo, una ejecución de prueba más corta duró aproximadamente 1,5 minutos:

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Restablezca y edite *_ondisk* y, después, vuelva a ejecutarlo


Una vez haya resultado Hola Hola *_inmem* ejecutar, lleve a cabo Hola siguiendo los pasos para hello *_ondisk* ejecutar:


1. Restablecer la base de datos de hello ejecutando Hola siguiente comando en SSMS toodelete todos los datos de Hola que fuera insertados por hello anterior ejecutar:
```
EXECUTE Demo.usp_DemoReset;
```

2. Editar la línea de comandos de hello ostress.exe tooreplace todos los *_inmem* con *_ondisk*.

3. Vuelva a ejecutar ostress.exe para hello por segunda vez y capturar los resultados de la duración de Hola.

4. Restablecer de nuevo, base de datos de hello (de forma responsable eliminación cuál puede ser una gran cantidad de datos de prueba).


#### <a name="expected-comparison-results"></a>Resultados de la comparación esperados

Nuestras pruebas en memoria han demostrado que el rendimiento mejorado gracias a **nueve veces** para esta carga de trabajo simplista, con ostress se ejecuta en una máquina virtual de Azure en Hola misma región de Azure como base de datos de Hola.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Instalar el ejemplo de Hola a análisis en memoria


En esta sección, comparar Hola E/S y los resultados de las estadísticas cuando se usa un índice de almacén frente a un índice de árbol b tradicional.


Para realizar análisis en tiempo real en una carga de trabajo OLTP, suele ser mejor toouse un índice no clúster de almacén de columnas. Para obtener más información, consulte [Guía de índices de almacén de columnas](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-hello-columnstore-analytics-test"></a>Preparar la prueba de análisis de almacén de columnas de Hola


1. Usar hello toocreate portal Azure una base de datos AdventureWorksLT actualizada de ejemplo de Hola.
 - Use ese nombre exacto.
 - Elija un nivel de servicio Premium.

2. Hola copia [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Portapapeles.
 - Hola script T-SQL crea Hola objetos necesarios en memoria Hola datos de ejemplo AdventureWorksLT que creó en el paso 1.
 - script de Hola crea la tabla de dimensiones de Hola y dos tablas de hechos. tablas de hechos de Hola se rellenan con 3,5 millones de filas cada uno.
 - script de Hola podría tardar toocomplete de 15 minutos.

3. Pegue el script de T-SQL de hello en SSMS y, a continuación, ejecute el script de Hola. Hola **almacén de columnas** palabra clave en hello **CREATE INDEX** instrucción es fundamental, como en:<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. Establecer el nivel de toocompatibility AdventureWorksLT 130:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    Nivel de 130 no es características memoria tooIn está directamente relacionado. Pero el nivel 130 suele ofrecer un rendimiento de consultas más rápido que el nivel 120.


#### <a name="key-tables-and-columnstore-indexes"></a>Tablas e índices de almacén de columnas clave


- dbo. FactResellerSalesXL_CCI es una tabla que tiene un índice de almacén de columnas agrupado, que se ha avanzado compresión en hello *datos* nivel.

- dbo. FactResellerSalesXL_PageCompressed es una tabla que tiene un equivalente índice normal en clúster se comprime solo en hello *página* nivel.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>Índice de almacén de columnas de clave consultas toocompare Hola


Hay [varios tipos de consulta de T-SQL que se pueden ejecutar](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee mejoras de rendimiento. En el paso 2 en hello script T-SQL, paga par de toothis de atención de consultas. Difieren solo en una línea:


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Es un índice de almacén de columnas agrupado en hello FactResellerSalesXL\_tabla CCI.

Hello extracto de script de T-SQL siguiente imprime las estadísticas de E/S y el tiempo de consulta de Hola de cada tabla.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

En una base de datos con el nivel de precios de hello P2, puede esperar aproximadamente nueve veces el aumento del rendimiento de Hola para esta consulta utilizando el índice de almacén de columnas agrupado hello en comparación con índice tradicional de Hola. Con P15, puede esperar ganancia de rendimiento de aproximadamente 57 veces Hola utilizando el índice de almacén de columnas de Hola.



## <a name="next-steps"></a>Pasos siguientes

- [Inicio rápido 1: Tecnologías OLTP en memoria para acelerar el rendimiento de Transact-SQL](http://msdn.microsoft.com/library/mt694156.aspx)

- [Uso de OLTP en memoria para mejorar el rendimiento de las aplicaciones en Azure SQL](sql-database-in-memory-oltp-migration.md)

- [Supervisión del almacenamiento de OLTP en memoria](sql-database-in-memory-oltp-monitoring.md)


## <a name="additional-resources"></a>Recursos adicionales

#### <a name="deeper-information"></a>Información más detallada

- [Más información sobre cómo Quorum duplica cargas de trabajo clave de las bases de datos a la vez que reduce las DTU en un 70 % con OLTP en memoria en SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (OLTP en memoria en la entrada de Blog de base de datos de SQL de Azure)

- [Más información sobre OLTP en memoria](http://msdn.microsoft.com/library/dn133186.aspx)

- [Más información sobre los índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx)

- [Más información sobre los análisis operativos en tiempo real](http://msdn.microsoft.com/library/dn817827.aspx)

- Consulte [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (Patrones de cargas de trabajo comunes y consideraciones de migración), que describe los patrones de carga de trabajo donde In-Memory OLTP normalmente proporciona importantes mejoras de rendimiento.

#### <a name="application-design"></a>Diseño de aplicación

- [In-Memory OLTP (optimización In-Memory)](http://msdn.microsoft.com/library/dn133186.aspx)

- [Uso de OLTP en memoria para mejorar el rendimiento de las aplicaciones en Azure SQL](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>Herramientas

- [Portal de Azure](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)

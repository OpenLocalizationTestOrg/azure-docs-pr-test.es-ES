---
title: rendimiento de la base de datos SQL de aaaAzure directrices de ajuste | Documentos de Microsoft
description: "En este artículo puede ayudarle a determinar qué toochoose de nivel de servicio para la aplicación. También recomienda formas tootune su Hola de tooget aplicación máximo partido de la base de datos de SQL Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Ajuste del rendimiento en Azure SQL Database

Base de datos de SQL Azure proporciona [recomendaciones](sql-database-advisor.md) que puede usar tooimprove rendimiento de la base de datos, o puede dejar base de datos de SQL Azure [tooyour aplicación se adaptan automáticamente](sql-database-automatic-tuning.md) y aplicar cambios que mejorará el rendimiento de la carga de trabajo.

En el no hay ninguna recomendación aplicable y sigue teniendo problemas de rendimiento, podría utilizar Hola siguientes prestaciones de tooimprove de métodos:
1. Aumentar [niveles de servicio](sql-database-service-tiers.md) y proporcionar la base de datos de más recursos tooyour.
2. Ajuste la aplicación y aplique algunas prácticas recomendadas que puedan mejorar el rendimiento. 
3. Optimizar la base de datos de hello cambiando los índices y las consultas toomore trabajar eficazmente con datos.

Se trata de métodos manuales porque necesita toodecide qué [niveles de servicio](sql-database-service-tiers.md) elegiría o se necesita la aplicación de toorewrite o de código de base de datos e implementar cambios Hola.

## <a name="increasing-performance-tier-of-your-database"></a>Aumento del nivel de rendimiento de su base de datos

Azure SQL Database ofrece cuatro [niveles de servicio](sql-database-service-tiers.md) que puede elegir de entre: Básico, Estándar, Premium y Premium RS (el rendimiento se mide en unidades de procesamiento de base de datos o [DTU](sql-database-what-is-a-dtu.md)). Cada nivel de servicio aísla estrictamente recursos de Hola que puede utilizar la base de datos SQL y garantiza un rendimiento predecible para ese nivel de servicio. En este artículo, se ofrecen directrices que pueden ayudarle a elegir el nivel de servicio de hello para la aplicación. También se explican maneras que se puede ajustar su Hola de tooget aplicación máximo partido de la base de datos de SQL Azure.

> [!NOTE]
> Este artículo se centra en la guía de rendimiento para bases de datos únicas de Azure SQL Database. Para obtener instrucciones de rendimiento los bloques de tooelastic relacionados, consulte [consideraciones de precio y rendimiento para grupos elásticos](sql-database-elastic-pool-guidance.md). Sin embargo, tenga en cuenta que puede aplicar muchas recomendaciones en este toodatabases artículo en un grupo elástico de optimización de Hola y obtener los beneficios de rendimiento similares.
> 

* **Básico**: Hola servicio básico nivel ofrece buena predicción del rendimiento para cada base de datos, la hora en horas. En una base de datos básica, hay suficientes recursos para proporcionar un buen rendimiento en bases de datos pequeñas que no tienen varias solicitudes simultáneas. Los casos de uso típicos de cuándo se usaría un nivel de servicio Básico son los siguientes:
  * **Acaba de empezar con Azure SQL Database**. Las aplicaciones que están en desarrollo no necesitan habitualmente altos niveles de rendimiento. Las bases de datos básicas son un entorno adecuado para el desarrollo de bases de datos o pruebas a un precio bajo.
  * **Tiene una base de datos con un único usuario**. Las aplicaciones que asocian un único usuario a una base de datos normalmente no tienen grandes requisitos de simultaneidad y rendimiento. Estas aplicaciones son candidatos para el nivel de servicio básico de Hola.
* **Estándar**: nivel de servicio estándar de hello ofrece la capacidad de predicción de mejorar el rendimiento y proporciona un buen rendimiento para bases de datos que tienen varias solicitudes simultáneas, como aplicaciones web y de grupo de trabajo. Cuando se usa una base de datos con un nivel de servicio Estándar, puede ajustar el tamaño de la aplicación de base de datos según un rendimiento predecible, minuto a minuto.
  * **La base de datos tiene varias solicitudes simultáneas**. Las aplicaciones que atienden a más de un usuario a la vez suelen necesitar niveles de rendimiento más altos. Por ejemplo, las aplicaciones web o de grupo de trabajo que tengan requisitos de tráfico de E/S de bajo toomedium admite varias consultas simultáneas son buenos candidatos para el nivel de servicio estándar Hola.
* **Premium**: nivel de servicio Premium de hello proporciona un rendimiento predecible, segunda en segundo lugar, para cada base de datos Premium. Cuando se elige el nivel de servicio Premium de hello, puede cambiar el tamaño de la aplicación de base de datos según la carga pico de Hola para esa base de datos. plan de Hello elimina aquellos casos en que la variación de rendimiento puede hacer más tiempo del esperado en operaciones sensibles a la latencia de las consultas pequeñas tootake. Este modelo puede simplificar considerablemente los ciclos de validación de hello desarrollo y producto para las aplicaciones que necesitan toomake declaraciones firmes sobre necesidades máximas de recursos, variación de rendimiento o latencia de las consultas. La mayoría de los casos de uso del nivel de servicio Premium tienen una o varias de estas características:
  * **Carga máxima elevada**. Una aplicación que requiere sustancial CPU, memoria o entrada/salida (E/S) toocomplete sus operaciones requiere un nivel dedicado y de alto rendimiento. Por ejemplo, una operación de base de datos conocido tooconsume varios núcleos de CPU durante un período prolongado es un candidato para el nivel de servicio Premium de Hola.
  * **Muchas solicitudes simultáneas**. Algunas aplicaciones de base de datos atienden muchas solicitudes simultáneas, por ejemplo, cuando dan servicio a un sitio web con un volumen elevado de tráfico. Básico y estándar niveles de servicio limitan número de Hola de solicitudes simultáneas por base de datos. Las aplicaciones que requieren más conexiones necesitaría toochoose un reserva suficiente tamaño toohandle Hola número máximo de solicitudes necesarias.
  * **Baja latencia**. Algunas aplicaciones necesitan tooguarantee una respuesta de la base de datos de hello en un tiempo mínimo. Si se llama a un procedimiento almacenado específico como parte de una operación de cliente más amplia, podría tener un requisito toohave una devolución de llamada en no más de 20 milisegundos, 99 por ciento de tiempo de Hola. Este tipo de los beneficios de la aplicación de nivel de servicio Premium de hello, toomake seguro de que Hola requiere capacidad de ejecución está disponible.
* **Premium RS**: Hola nivel Premium RS está diseñado para cargas de trabajo intensivo que no requieren Hola mayor garantía de disponibilidad. Los ejemplos incluyen las pruebas en cargas de trabajo de alto rendimiento, o una carga de trabajo analítico donde la base de datos de hello no es sistema Hola de registro.

nivel de servicio de Hola que necesite para la base de datos SQL depende de los requisitos de carga máxima de Hola para cada dimensión de recursos. Algunas aplicaciones usan pocas cantidades de un recurso pero tienen necesidades considerables de otros.

### <a name="service-tier-capabilities-and-limits"></a>Límites y capacidades de nivel de servicio

En cada nivel de servicio, establecer el nivel de rendimiento de hello, por lo que tendrá Hola flexibilidad toopay solo para la capacidad de Hola que necesita. También puede [ajustar la capacidad](sql-database-service-tiers.md), hacia arriba o hacia abajo, según los cambios en la carga de trabajo. Por ejemplo, si la carga de trabajo de la base de datos es elevada durante la época de compras de vuelta al colegio hello, puede aumentar el nivel de rendimiento de Hola de base de datos de Hola durante un tiempo establecido, julio a septiembre. Luego, puede reducirla cuando finalice la temporada de actividad máxima. Puede minimizar lo que paga al optimizar la estacionalidad de toohello de entorno de nube de su negocio. Este modelo también funciona bien para los ciclos de lanzamiento de productos de software. Un equipo de pruebas puede asignar capacidad mientras realiza ejecuciones de prueba y luego liberar esa capacidad cuando finalicen las pruebas. En un modelo de solicitud de capacidad, se paga por la capacidad que necesite, así se evita gastos en recursos dedicados que raramente usa.

### <a name="why-service-tiers"></a>¿Por qué niveles de servicio?
Aunque cada carga de trabajo de la base de datos puede ser diferente, el propósito de Hola de niveles de servicio es tooprovide predicción del rendimiento en varios niveles de rendimiento. Los clientes con requisitos de recursos de base de datos a gran escala pueden trabajar en un entorno informático más dedicado.

## <a name="tune-your-application"></a>Optimización de la aplicación
En el servidor SQL local tradicional, a menudo se separa proceso Hola de planeación de la capacidad inicial de proceso Hola de ejecutar una aplicación en producción. Primero se adquieren las licencias de hardware y productos y luego se ajusta el rendimiento. Cuando se utiliza la base de datos de SQL Azure, es un proceso de hello toointerweave buena idea de cómo ejecutar una aplicación y para la optimización se. Con el modelo de Hola de pago por capacidad a petición, puede optimizar los aplicación toouse Hola recursos mínimos necesarios ahora, en lugar de en exceso hardware en función de suposiciones de planes de crecimiento futuro de una aplicación, que a menudo son incorrectos. Algunos clientes pueden elegir no tootune una aplicación y elija en su lugar toooverprovision los recursos de hardware. Este enfoque podría ser una buena idea si no desea toochange una aplicación clave durante un período de ocupación. Sin embargo, optimización de una aplicación puede minimizar los requisitos de recursos y reducir las facturas mensuales cuando se usan los niveles de servicio de hello en base de datos de SQL Azure.

### <a name="application-characteristics"></a>Características de la aplicación
Aunque los niveles de servicio de base de datos de SQL Azure están diseñadas tooimprove estabilidad del rendimiento y capacidad de predicción para una aplicación, algunas prácticas recomendadas pueden ayudarle a optimizar la aplicación toobetter aprovechar las ventajas de los recursos de hello en un nivel de rendimiento. Aunque muchas aplicaciones tienen importantes mejoras de rendimiento simplemente por cambio tooa mayor nivel de rendimiento o servicio de nivel, algunas aplicaciones precisan adicionales para la optimización toobenefit de un mayor nivel de servicio. Para aumentar el rendimiento, puede realizar ajustes adicionales en las aplicaciones para que tengan estas características:

* **Aplicaciones que tienen un rendimiento lento debido a un comportamiento "comunicativo"**. Aplicaciones locuaces realizar operaciones de acceso de exceso de datos que son confidenciales toonetwork latencia. Tendrá que toomodify estos tipos de número de hello tooreduce de las aplicaciones de base de datos SQL toohello de operaciones de acceso de datos. Por ejemplo, podría mejorar el rendimiento de la aplicación mediante el uso de técnicas como el procesamiento por lotes de consultas ad hoc o mover hello toostored procedimientos de consulta. Para más información, consulte [Consultas por lotes](#batch-queries).
* **Bases de datos con una carga de trabajo intensiva que no se admite en una sola máquina**. Las bases de datos que superan los recursos de Hola de mayor nivel de rendimiento de Premium Hola pueden beneficiarse del escalado horizontal de carga de trabajo de Hola. Para más información, consulte [Particionamiento entre bases de datos](#cross-database-sharding) y [Creación de particiones funcional](#functional-partitioning).
* **Aplicaciones que tienen consultas poco óptimas**. Las aplicaciones, especialmente las que en la capa de acceso a datos hello, que tienen consultas poco optimizadas no pueden beneficiarse de un nivel de rendimiento superior. Esto incluye consultas que carecen de una cláusula WHERE, con índices que faltan o tienen estadísticas anticuadas. Estas aplicaciones se benefician de las técnicas de optimización del rendimiento de consultas estándar. Para más información, consulte [Índices que faltan](#identifying-and-adding-missing-indexes) y [Optimización de consultas y sugerencias](#query-tuning-and-hinting).
* **Aplicaciones que tienen un diseño de acceso a datos poco óptimo**. Puede que las aplicaciones que tienen problemas inherentes de simultaneidad de acceso a datos, por ejemplo, interbloqueos, no se beneficien de un nivel de rendimiento más alto. Considere la posibilidad de reducir los viajes de ida y contra Hola base de datos de SQL Azure mediante los datos en caché en el lado del cliente de hello con hello servicio Caching de Azure u otra tecnología de almacenamiento en caché. Consulte [Almacenamiento en caché de la capa de aplicación](#application-tier-caching).

## <a name="tune-your-database"></a>Ajuste de la base de datos
En esta sección, veremos algunas técnicas que puede utilizar un rendimiento óptimo Hola de tootune base de datos de SQL Azure toogain para su aplicación y ejecutarla en el nivel más bajo de rendimiento posible de Hola. Algunas de estas técnicas coinciden con las prácticas recomendadas de optimización tradicionales de SQL Server, pero otras son específica tooAzure base de datos SQL. En algunos casos, puede examinar Hola consumida recursos para una optimización de base de datos toofind áreas toofurther y extender toowork de técnicas tradicionales de SQL Server en la base de datos de SQL Azure.

### <a name="identify-performance-issues-using-azure-portal"></a>Identificación de problemas de rendimiento mediante Azure Portal
Hola después herramientas Hola portal de Azure puede ayudarle a analizar y solucionar problemas de rendimiento con la base de datos SQL:

* [Información de rendimiento de consultas](sql-database-query-performance.md)
* [Asesor de Base de datos SQL](sql-database-advisor.md)

Hello portal de Azure proporciona más información acerca de estas herramientas y cómo toouse ellos. tooefficiently diagnostique y corrija cualquier problema, le recomendamos que primero intente herramientas Hola Hola portal de Azure. Se recomienda que realice manual de hello para la optimización enfoques que se describen a continuación, para los que faltan índices y optimización de consultas, en casos especiales.

Obtenga más información acerca de cómo identificar problemas en Azure SQL Database en el artículo de [supervisión de rendimiento](sql-database-single-database-monitor.md).

### <a name="identifying-and-adding-missing-indexes"></a>Identificación y adición de índices que faltan
Un problema común de rendimiento de base de datos OLTP está relacionado con el diseño de base de datos física toohello. A menudo, los esquemas de base de datos se diseñan y se entregan sin realizar pruebas a escala (ya sea en la carga o en el volumen de datos). Por desgracia, rendimiento de Hola de un plan de consulta podría ser aceptable en una pequeña escala pero degradar sustancialmente en volúmenes de datos de nivel de producción. origen de Hello más común de este problema es la falta de Hola de filtros de índices adecuados toosatisfy u otras restricciones de una consulta. A menudo, la falta de índices se manifiesta como un recorrido de tabla cuando podría ser suficiente una búsqueda de índice.

En este ejemplo, plan de consulta seleccionado Hola utiliza un recorrido cuando bastaría con una búsqueda:

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![Plan de consulta con índices que faltan](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Azure SQL Database puede ayudarle a encontrar y corregir condiciones de falta de índice comunes. DMV que se integran en la base de datos de SQL Azure mire compilaciones de consultas en el que un índice reduciría considerablemente Hola estimado costo toorun una consulta. Durante la ejecución de consultas, base de datos SQL realiza un seguimiento de la frecuencia con la que se ejecuta cada plan de consulta y Hola pistas estimado brecha entre hello en ejecución hello y plan de consulta imaginado uno donde existía ese índice. Puede usar estos estimación de tooquickly DMV qué diseño de base de datos física tooyour cambios podría mejorar el costo de carga de trabajo general para una base de datos y su carga de trabajo real.

Puede utilizar esta posibilidad de tooevaluate consulta índices que faltan:

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

En este ejemplo, consulta Hola devolvió esta sugerencia:

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Después de crearlo, esa misma instrucción SELECT elige un plan diferente, que utiliza una búsqueda en lugar de un análisis y, a continuación, se ejecuta de forma más eficaz en plan hello:

![Plan de consulta con índices corregidos](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

Hola clave es esa capacidad de E/S de un compartido hello, sistema está más limitada que la de un equipo servidor dedicado. Es importante minimizar innecesarios E/S tootake máximo las ventajas de sistema de Hola Hola DTU de cada nivel de rendimiento de los niveles de servicio de base de datos de SQL Azure Hola. Las opciones de diseño de base de datos física adecuada significativamente pueden mejorar la latencia de Hola para consultas individuales, mejorar el rendimiento de Hola de solicitudes simultáneas que se controlan por unidad de escala y minimizar la consulta de hello costos necesarios toosatisfy Hola. Para obtener más información acerca de hello falta DMV de índice, vea [sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Optimización de consultas y sugerencias
optimizador de consultas de Hello en la base de datos de SQL Azure es similar toohello tradicional SQL Server optimizador. En la mayoría de las prácticas recomendadas de Hola para optimizar las consultas y Hola descripción razonamiento limitaciones del modelo de optimizador de consultas de hello también se aplican tooAzure base de datos de SQL. Si optimizar las consultas de base de datos de SQL Azure, podría obtener ventaja adicional de Hola de reducir las demandas de recursos agregados. Su aplicación podría ser capaz de toorun a un costo menor que un equivalente no optimizado ya que se puede ejecutar en un nivel de rendimiento inferior.

Un ejemplo que es común en SQL Server y que también aplica tooAzure base de datos SQL es cómo el optimizador "husmea" parámetros de la consulta de Hola. Durante la compilación, optimizador de consultas de Hola se evalúa como valor actual de Hola de un parámetro toodetermine si puede generar un plan de consulta más óptimo. Aunque a menudo esta estrategia puede provocar tooa plan de consulta que es significativamente más rápido que un plan compilado sin valores de parámetro conocidos, funciona actualmente no entienden bien tanto en SQL Server y en la base de datos de SQL Azure. A veces no se examinan parámetro hello y a veces se examinan parámetro hello pero plan generado hello no es óptimo para el conjunto completo de Hola de valores de parámetro en una carga de trabajo. Microsoft incluye las sugerencias de consulta (directivas) para que pueda especificar intento más deliberado e invalidar el comportamiento predeterminado de Hola de examen de parámetros. A menudo, si usas sugerencias, puede corregir los casos en que el comportamiento de SQL Server o base de datos de SQL de Azure predeterminado hello es imperfecto para una carga de trabajo de cliente específico.

Hello de ejemplo siguiente muestra cómo el procesador de consultas de hello puede generar un plan que no es óptimo para rendimiento y requisitos de recursos. Este ejemplo también muestra que si usa una sugerencia de consulta, puede reducir los requisitos de recursos y el tiempo de ejecución de consultas de su base de datos SQL:

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

código de Hello el programa de instalación crea una tabla que ha sesgado distribución de datos. difiere del plan de consulta óptimo Hola se basa en el parámetro que está seleccionado. Lamentablemente, comportamiento almacenamiento en caché de plan de hello no siempre recompila consulta hello en función del valor de parámetro más común de Hola. Por lo tanto, es posible que un toobe de planes poco óptimos almacena en caché y se utiliza para muchos valores, incluso cuando un plan diferente podría ser una opción mejor de plan en promedio. A continuación, plan de consulta de hello crea dos procedimientos almacenados que son idénticos, salvo que una tiene una sugerencia de consulta especiales.

**Ejemplo (parte 1):**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Ejemplo (parte 2):**

(Se recomienda que espere al menos 10 minutos antes de empezar la parte 2 del ejemplo de Hola, para que los resultados de hello son distintos en hello resultantes de los datos de telemetría).

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

Cada parte de este ejemplo intenta toorun una instrucción insert con parámetros 1.000 veces (toogenerate un toouse de carga suficiente como un conjunto de datos de prueba). Cuando ejecuta los procedimientos almacenados, procesador de consultas de hello examina el valor del parámetro hello que se pasa toohello procedimiento durante su primera compilación ("examen de parámetros"). procesador de Hello almacena en memoria caché el plan resultante de Hola y lo utiliza para invocaciones posteriores, incluso si el valor del parámetro hello es diferente. plan óptimo de Hello no podría utilizarse en todos los casos. En ciertas ocasiones necesitará tooguide Hola optimizador toopick un plan que es mejor para caso promedio de hello en lugar de mayúsculas y minúsculas Hola desde cuando consulta hello en primer lugar se ha compilado. En este ejemplo, plan inicial Hola genera un plan de "recorrido" que lee toofind de todas las filas de cada valor que coincida con el parámetro hello:

![Optimización de consultas mediante un plan de exploración](./media/sql-database-performance-guidance/query_tuning_1.png)

Como ejecutamos el procedimiento de hello mediante Hola valor 1, plan resultante Hola fue óptimo para el valor de hello 1 pero sí poco óptimo para todos los demás valores de tabla de Hola. resultado de Hello es probable que no es lo que desearía si estuviera toopick cada plan al azar, porque el plan de hello tiene un rendimiento más lento y utiliza más recursos.

Si ejecuta pruebas de hello con `SET STATISTICS IO` establecido demasiado`ON`, trabajo de recorrido lógico de hello en este ejemplo se realiza entre bastidores de Hola. Puede ver que hay 1.148 lecturas realizarla plan hello (que es eficaz si caso promedio de hello es tooreturn únicamente una fila):

![Optimización de consultas mediante una exploración lógica](./media/sql-database-performance-guidance/query_tuning_2.png)

Hola segunda parte del ejemplo de Hola utiliza un toouse del optimizador de consultas sugerencia tootell Hola un valor específico durante el proceso de compilación de Hola. En este caso, fuerza Hola procesador tooignore Hola valor de consulta que se pasa como parámetro de hello, y en su lugar tooassume `UNKNOWN`. Esto refiere valor tooa cuya frecuencia promedio de hello en tabla hello (se omite el sesgo). plan resultante de Hello es un plan de búsqueda que es más rápida y utiliza menos recursos, en promedio, que el plan de hello en la parte 1 de este ejemplo:

![Optimización de consultas mediante una sugerencia de consulta](./media/sql-database-performance-guidance/query_tuning_3.png)

Puede ver el efecto de Hola Hola **sys.resource_stats** tabla (no hay un retraso de tiempo de Hola que ejecutar pruebas de Hola y cuando datos Hola rellenan la tabla de hello). Para este ejemplo, parte 1 que se ejecuta durante el período de tiempo de hello 22:25:00 y parte 2 ejecutada a las 22:35:00. Hello período de tiempo anterior usó más recursos en la ventana de tiempo de Hola uno posterior (debido a las mejoras de eficacia del plan).

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Resultados del ejemplo de optimización de consultas](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Aunque el volumen de hello en este ejemplo es pequeño intencionadamente, el efecto de Hola de parámetros poco óptimos puede ser considerable, especialmente en las bases de datos más grandes. diferencia de Hello, en casos extremos, puede estar entre segundos para los casos rápidos y horas para casos lenta.
> 
> 

Puede examinar **sys.resource_stats** toodetermine si el recurso de Hola de una prueba utiliza más o menos recursos que otra prueba. Al comparar los datos, separar tiempo Hola de pruebas para que no se encuentran en hello mismo período de 5 minutos en hello **sys.resource_stats** vista. Hello objetivo del ejercicio hello es cantidad total de hello toominimize de recursos que usa y no toominimize Hola máximo los recursos. Por lo general, al optimizar la latencia de un fragmento de código, también se reduce el consumo de recursos. Asegúrese de que los cambios de Hola que realice tooan aplicación son necesarios y que los cambios de hello no afecten negativamente Hola experiencia de alguien que podría usar sugerencias de consulta en la aplicación hello.

Si una carga de trabajo tiene un conjunto de consultas repetidas, a menudo hace sentido toocapture y validar idoneidad de Hola de las opciones de plan ya que las unidades de base de datos de hello mínima de recursos tamaño unidad requiere toohost Hola. Después de validar, en ocasiones examinar los planes de hello que toohelp Asegúrese de que no se han degradado. Puede aprender más sobre las [sugerencias de consulta (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Particionamiento entre bases de datos
Como base de datos de SQL Azure se ejecuta en hardware estándar, los límites de capacidad de Hola para una sola base de datos son menores que para una instalación de SQL Server local tradicional. Algunos clientes utilizan operaciones de base de datos de toospread de técnicas de particionamiento entre varias bases de datos cuando las operaciones de hello no caben dentro de los límites de Hola de una sola base de datos en la base de datos de SQL Azure. La mayoría de los clientes que usan técnicas de particionamiento en Azure SQL Database divide sus datos en una única dimensión entre varias bases de datos. En este caso, deberá toounderstand que las aplicaciones OLTP suelen realizan las transacciones que se aplican tooonly una fila o tooa grupo pequeño de filas de esquema de Hola.

> [!NOTE]
> Base de datos SQL proporciona ahora una tooassist de biblioteca con el particionamiento. Para obtener más información, consulte [Información general de la biblioteca de cliente de bases de datos elásticas](sql-database-elastic-database-client-library.md).
> 
> 

Por ejemplo, si una base de datos tiene el nombre del cliente, pedido y detalles del pedido (como Hola base de datos Northwind de ejemplo tradicional que se distribuye con SQL Server), podría dividir estos datos en varias bases de datos mediante la agrupación de un cliente con hello relacionados con orden y los detalles de pedido información. Puede garantizar que los datos de ese cliente hello permanecen en una sola base de datos. aplicación Hello dividiría los distintos clientes a través de las bases de datos, repartir eficazmente Hola carga entre varias bases de datos. Con el particionamiento, los clientes no solo pueden evitar límite de tamaño de base de datos máximo de hello, pero la base de datos de SQL Azure también puede procesar las cargas de trabajo que son mucho mayores que los límites de Hola Hola diferentes niveles de rendimiento, siempre y cuando cada base de datos individual se adapta a su DTU.

Aunque el particionamiento de base de datos no reduce la capacidad de recursos agregada de Hola para una solución, es muy eficaz en admitir soluciones muy grandes que se distribuyen en varias bases de datos. Cada base de datos puede ejecutar en un rendimiento de nivel toosupport de muy grande, las bases de datos "eficaces" con requisitos elevados de recursos.

### <a name="functional-partitioning"></a>Creación de particiones funcional
Los usuarios de SQL Server suelen combinar varias funciones en una base de datos única. Por ejemplo, si una aplicación tiene el inventario de toomanage de lógica de una tienda, esa base de datos podría tener lógica asociada con el inventario, pedidos de compra, procedimientos almacenados y vistas indizadas o materializadas que administración los informes de fin de mes. Esta técnica resulta más fácil de base de datos de hello tooadminister para operaciones como copia de seguridad, pero también requiere toosize hello toohandle Hola pico de carga de hardware en todas las funciones de una aplicación.

Si utiliza una arquitectura de escalabilidad horizontal en la base de datos de SQL Azure, es una buena idea toosplit las distintas funciones de una aplicación en diferentes bases de datos. Mediante esta técnica, cada aplicación se escala de forma independiente. Cuando una aplicación realiza una actividad mayor (y Hola carga en los incrementos de la base de datos de hello), Administrador de hello puede elegir niveles de rendimiento independientes para cada función en la aplicación hello. En límite de hello, con esta arquitectura, una aplicación puede ser mayor que un solo equipo estándar puede controlar porque carga Hola se reparte entre varias máquinas.

### <a name="batch-queries"></a>Consultas por lotes
Para las aplicaciones que tienen acceso a datos mediante el uso de gran volumen, frecuentes, consultas ad hoc, una cantidad considerable de tiempo de respuesta se invierte en la comunicación de red entre la capa de aplicación de Hola y de nivel de base de datos de SQL Azure Hola. Aunque ambos Hola aplicación y base de datos de SQL Azure están en hello mismo centro de datos, latencia de red de hello entre Hola dos podría ser agravado por un gran número de operaciones de acceso a datos. red de hello tooreduce round viajes para datos de hello operaciones de acceso, considere el uso de consultas ad hoc de hello opción tooeither lote Hola o toocompile usarlas como procedimientos almacenados. Si procesar por lotes de consultas ad hoc de hello, puede enviar varias consultas como un lote grande en una base de datos SQL de solo viaje tooAzure. Si compila las consultas ad hoc en un procedimiento almacenado, podría conseguir Hola que mismo resultado que si en un lote. Con un procedimiento almacenado también ofrece Hola ventaja de aumentar las posibilidades de Hola de almacenamiento en caché de planes de consulta de hello en la base de datos de SQL Azure para que pueda usar Hola procedimiento almacenado de nuevo.

Algunas aplicaciones requieren operaciones de escritura intensivas. A veces puede reducir la carga de E/S total de hello en una base de datos teniendo en cuenta cómo se escribe toobatch juntos. Con frecuencia es tan sencillo como usar transacciones explícitas en lugar de transacciones de confirmación automática dentro de los procedimientos almacenados y lotes ad hoc. Para ver una evaluación de las distintas técnicas que se pueden usar, consulte [Técnicas de procesamiento por lotes para aplicaciones de SQL Database en Azure](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Experimentar con su propio modelo adecuado de carga de trabajo toofind hello para el procesamiento por lotes. Estar toounderstand seguro de que puede tener un modelo ligeramente garantiza la coherencia transaccional diferentes. Encontrar Hola carga de trabajo adecuada que minimiza el uso de recursos, es necesario encontrar la combinación correcta de Hola de ventajas y desventajas de coherencia y rendimiento.

### <a name="application-tier-caching"></a>Almacenamiento en caché de la capa de aplicación
Algunas aplicaciones de base de datos tienen cargas de trabajo con operaciones de lectura intensivas. Almacenamiento en caché capas puede reducir la carga de hello en la base de datos de Hola y podría reducir potencialmente toosupport requiere nivel de rendimiento de hello una base de datos mediante el uso de la base de datos de SQL Azure. Con [Azure Redis Cache](https://azure.microsoft.com/services/cache/), si tiene una carga de trabajo con muchas lecturas, puede leer datos de hello una vez (o quizás una vez por equipo de capa de aplicación, según cómo esté configurada) y, a continuación, almacene esos datos fuera de la base de datos SQL. Esto supone una carga de base de datos de manera tooreduce (CPU y E/S de lectura), pero no hay un efecto en la coherencia transaccional porque los datos de Hola que se va a leer desde la memoria caché de hello podrían ser sincronizados con datos de hello en la base de datos de Hola. Aunque en muchas aplicaciones algún nivel de incoherencia es aceptable, esto no se aplica a todas las cargas de trabajo. Debería comprender totalmente los requisitos de una aplicación antes de emplear una estrategia de almacenamiento en caché de la capa de aplicación.

## <a name="next-steps"></a>Pasos siguientes
* Para más información sobre los niveles de servicio, consulte [Opciones y rendimiento de SQL Database](sql-database-service-tiers.md)
* Para obtener más información sobre los grupos elásticos, consulte [¿Qué es un grupo elástico de Azure?](sql-database-elastic-pool.md)
* Para obtener información acerca de los grupos de rendimiento y elasticidad, consulte [cuando tooconsider un grupo elástico](sql-database-elastic-pool-guidance.md)


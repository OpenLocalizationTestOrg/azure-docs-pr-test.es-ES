---
title: nivel de compatibilidad de aaaDatabase 130 - base de datos de SQL de Azure | Documentos de Microsoft
description: "En este artículo, nos explore Hola ventajas de ejecutar la base de datos de SQL Azure en el nivel de compatibilidad 130 y aprovechar las ventajas de Hola de nuevo el optimizador de consultas de Hola y características del procesador de consultas. También tratamos Hola posibles efectos secundarios en el rendimiento de las consultas para las aplicaciones existentes de SQL Hola Hola."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Rendimiento mejorado de consultas con el nivel de compatibilidad 130 en Base de datos SQL de Azure
La base de datos de SQL Azure se ejecuta transparente cientos de miles de bases de datos en varios niveles de compatibilidad diferentes, conservar y garantizan toohello de versión correspondiente de Microsoft SQL Server para la compatibilidad con versiones anteriores Hola a todos sus clientes!

En este artículo, nos explore Hola ventajas de la ejecución de su base de datos de SQL Azure en el nivel de compatibilidad 130 y aprovechar las ventajas de Hola de nuevo el optimizador de consultas de Hola y características del procesador de consultas. También tratamos Hola posibles efectos secundarios en el rendimiento de las consultas para las aplicaciones existentes de SQL Hola Hola.

Como recordatorio del historial, la alineación de Hola de niveles de compatibilidad de toodefault de versiones SQL son los siguientes:

* 100: en SQL Server 2008 y Base de datos SQL de Azure V11.
* 110: en SQL Server 2012 y Base de datos SQL de Azure V11.
* 120: en SQL Server 2014 y Base de datos SQL de Azure V12.
* 130: en SQL Server 2016 y Base de datos SQL de Azure V12.

> [!IMPORTANT]
> A partir de **mid junio de 2016**, en la base de datos de SQL Azure, nivel de compatibilidad de hello predeterminado será 130 en lugar de 120 para **recién creado** bases de datos.
> 
> Las bases de datos creadas antes de mediados de junio de 2016 *no* se verán afectadas y mantendrán su nivel de compatibilidad actual (100, 110 o 120). Bases de datos que se migran de la base de datos de SQL Azure versión V11 tooV12 tendrá un nivel de compatibilidad de 100 o 110. 
> 

## <a name="about-compatibility-level-130"></a>Acerca del nivel de compatibilidad 130
En primer lugar, si desea que el nivel tooknow Hola de compatibilidad actual de la base de datos, ejecute hello después de la instrucción Transact-SQL.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


Antes de este cambio se produce para los toolevel 130 **recién** crear bases de datos, vamos a revisar lo que este cambio consiste en ver algunos ejemplos de consulta muy básica y ver cómo cualquiera puede beneficiarse de él.

Procesamiento de consultas en bases de datos relacionales puede ser muy complejo y puede provocar toolots de equipo informática y matemáticas toounderstand Hola inherentes a las opciones de diseño y comportamientos. En este documento, contenido de hello ha sido tooensure intencionadamente simplificada que cualquier persona con algunos conocimientos técnicos mínimos puede comprender el impacto del cambio del nivel de compatibilidad Hola Hola y determinar cómo puede beneficiar a las aplicaciones.

Echemos un vistazo qué nivel de compatibilidad de hello 130 pone en la tabla de Hola.  Puede encontrar más detalles en [Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), pero aquí tiene un breve resumen:

* pueden ser multiproceso Hello operación de inserción de una instrucción Insert select o puede tener un plan paralelo, mientras que antes de que esta operación se un único subproceso.
* Las consultas de tabla con optimización de memoria y variables de tabla pueden tener ahora planes paralelos, mientras que antes esta operación también era de subproceso único.
* Las estadísticas de una tabla con optimización de memoria ahora pueden muestrearse y se actualizan de forma automática. Consulte [Novedades (motor de base de datos): OLTP en memoria](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) para más detalles.
* El modo por lotes frente al modo de fila cambia con los índices de almacenamiento de columnas
  * Las ordenaciones en una tabla con un índice de almacenamiento de columnas están ahora en modo por lotes.
  * Los agregados basados en ventanas operan ahora en modo por lotes, tal como instrucciones de TSQL LAG/LEAD.
  * Las consultas en tablas de almacenamiento de columnas con varias cláusulas Distinct funcionan en modo por lotes.
  * Las consultas que se ejecutan en DOP = 1 o con un plan en serie también se ejecutan en modo por lotes.
* Por último, mejoras de estimación de cardinalidad proceden realmente con el nivel de compatibilidad 120, pero para los que ejecutar en una compatibilidad más bajo nivel (es decir, 100 o 110), hello move toocompatibility nivel 130 también aparecerá estas mejoras y los usuarios pueden también mejorar el rendimiento de la consulta de Hola de las aplicaciones.

## <a name="practicing-compatibility-level-130"></a>Prácticas con el nivel de compatibilidad 130
Primero vamos a algunas tablas, índices y datos aleatorios creados toopractice algunas de estas nuevas capacidades. ejemplos de script de Hola TSQL se pueden ejecutar en SQL Server 2016 o base de datos de SQL Azure. Sin embargo, al crear una base de datos de SQL Azure, asegúrese de que elija en el mínimo de hello P2 de base de datos porque necesita al menos un par de núcleos tooallow subprocesamiento múltiple y por lo tanto beneficiarse de estas características.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


Ahora, echemos un toosome del aspecto de las características de procesamiento de consultas de hello procedentes con nivel de compatibilidad 130.

## <a name="parallel-insert"></a>INSERT en paralelo
Ejecutar instrucciones de TSQL Hola siguiente ejecuta Hola operación de INSERCIÓN en el nivel de compatibilidad 120 y 130, que ejecuta respectivamente Hola operación de INSERCIÓN en un único modelo de subproceso (120) y en un modelo multiproceso (130).

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Solicitando el plan de consulta de Hola Hola real, examinando su representación gráfica o su contenido XML, puede determinar qué función se encuentra en la reproducción de estimación de cardinalidad. Examinando los planes de hello en paralelo en la figura 1, podemos ver claramente que Hola insertar de la tienda en la columna ejecución va de serie en 120 tooparallel en 130. Además, tenga en cuenta ese cambio Hola del icono de iterador de hello en plan 130 Hola que muestra dos flechas paralelas, que ilustra el hecho de Hola que ahora Hola ejecución de iterador es realmente paralela. Si tiene grande toocomplete de operaciones de INSERCIÓN, Hola la ejecución en paralelo, vinculado toohello número de núcleos que tiene a su disposición para base de datos de hello, llevará a cabo mejor; seguridad tooa 100 veces más rápido dependiendo de su situación.

*Figura 1: Inserte los cambios de la operación de tooparallel serie con el nivel de compatibilidad 130.*

![En la Ilustración 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>Modo por lotes EN SERIE
De forma similar, mover el nivel de toocompatibility 130 al procesar las filas de datos permite el procesamiento de modo por lotes. En primer lugar, las operaciones en modo por lotes solo están disponibles cuando tenga un índice de almacenamiento de columnas preparado. En segundo lugar, un lote que normalmente representa aproximadamente 900 filas y utiliza una lógica de código optimizada para varios núcleos de CPU, un mayor rendimiento de memoria y directamente aprovecha Hola datos comprimidos de hello almacén de columnas siempre que sea posible. En estas condiciones, SQL Server 2016 puede procesar aproximadamente 900 filas a la vez, en lugar de 1 fila en el momento de hello, y en consecuencia, hello coste total general de operación de hello ahora compartida por lote completo de hello, reducir Hola general costo por fila. Esta cantidad de operaciones combinadas con compresión de almacén de columnas de hello básicamente compartida reduce la latencia de hello implicada en una operación de modo por lotes SELECT. Puede encontrar más detalles sobre el almacén de columnas de hello y procesar por lotes en el modo en [Guía de índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Como visible a continuación, mediante la observación de hello consulta planes side-by-side en la figura 2, podemos ver que ha cambiado el modo de procesamiento de hello con nivel de compatibilidad de hello y, en consecuencia, al ejecutar consultas de hello en el nivel de compatibilidad de ambos por completo, podemos ver que la mayoría del tiempo de procesamiento de Hola se invierte en fila modo (86%) en comparación con toohello modo por lotes (14%), donde se han procesado 2 lotes. Aumentar el conjunto de datos de hello, hello beneficio aumentará.

*Figura 2: Seleccione los cambios de operación del modo serie toobatch con nivel de compatibilidad 130.*

![Ilustración 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Modo por lotes en ejecución SORT
Toohello similar anterior, pero la operación de ordenación aplicada tooa, transición Hola de fila (nivel de compatibilidad 120) toobatch modo (nivel de compatibilidad 130) mejora el rendimiento de Hola de hello operación de ordenación para hello las mismas razones.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Visible side-by-side en la figura 3, podemos ver que operación de ordenación de hello en el modo de fila representa 81% de hello un costo, mientras que en modo por lotes Hola solo representa 19% del costo de hello (respectivamente 81% y % de 56 en ordenación Hola propio).

*Figura 3: Operación de ordenación cambia de modo de fila toobatch con nivel de compatibilidad 130.*

![Ilustración 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Evidentemente, estos ejemplos sólo contienen decenas de miles de filas, que es nada cuando se examinan datos Hola disponibles en la mayoría de los servidores SQL de hoy en día. Simplemente proyecto estos en millones de filas en su lugar, y esto puede convertir en varios minutos de ejecución ahorran cada día pendiente naturaleza hello de la carga de trabajo.

## <a name="cardinality-estimation-ce-improvements"></a>Mejoras de estimación de cardinalidad (CE)
Se introdujo con SQL Server 2014, cualquier base de datos que se ejecute en un nivel de compatibilidad 120 o superior hará que el uso de la nueva funcionalidad de estimación de cardinalidad Hola. En esencia, estimación de cardinalidad es lógica hello usa toodetermine cómo SQL server ejecutará una consulta basada en su costo estimado. estimación de Hola se calcula con la entrada de las estadísticas asociadas con los objetos implicados en la consulta. En la práctica, en un alto nivel, las funciones de estimación de cardinalidad son estimaciones de recuento de filas junto con información sobre la distribución de Hola de valores de hello, recuentos de valores distintos, y recuentos duplicados contenidos en Hola tablas y objetos que se hace referencia en la consulta de Hola. Obtener estas estimaciones incorrecto, puede provocar la E/S de disco toounnecessary debido concesiones de memoria tooinsufficient (es decir, los volcados de TempDB), o ejecutar, tooname el plan de selección de tooa de la ejecución de un plan en serie a través de un paralelo algunas. Conclusión, estimaciones incorrectas pueden provocar tooan degradación del rendimiento general de la ejecución de la consulta de Hola. En hello otro lado, mejor las estimaciones, estimaciones más precisas, las ejecuciones de consulta de clientes potenciales toobetter!

Como se mencionó antes, optimizaciones de consultas y las estimaciones son un asunto complejo, pero si desea más información acerca de los planes de consulta y Estimador de cardinalidad toolearn, puede hacer referencia a documento toohello en [optimizar los planes de consulta con hello SQL Server 2014 Estimador de cardinalidad](https://msdn.microsoft.com/library/dn673537.aspx) para un análisis más profundo.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>¿Qué estimación de cardinalidad está usando actualmente?
toodetermine bajo qué estimaciones de cardinalidad se ejecutan las consultas, vamos a usar solo la consulta de hello ejemplos a continuación. Tenga en cuenta que este primer ejemplo se ejecutará en el nivel de compatibilidad 110, lo que implica el uso de Hola de funciones de estimación de cardinalidad anteriores de Hola.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Una vez completada la ejecución, haga clic en el vínculo XML de Hola y examine las propiedades de Hola de iterador primera Hola tal y como se muestra a continuación. Nombre de la propiedad de nota Hola llama CardinalityEstimationModelVersion actualmente establecido en 70. Eso no significa que nivel de compatibilidad de base de datos de Hola se establece la versión de SQL Server 7.0 toohello (se establece en 110 como visible en las instrucciones de TSQL Hola anteriores), pero valor Hola 70 simplemente representa la funcionalidad de estimación de cardinalidad heredada de hello disponible desde SQL Server 7.0, que no tenía ningún revisiones principales hasta que SQL Server 2014 (que se incluye con un nivel de compatibilidad de 120).

*Figura 4: Hola CardinalityEstimationModelVersion se establece too70 cuando se usa un nivel de compatibilidad de 110 o inferior.*

![Ilustración 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

Como alternativa, puede cambiar too130 de nivel de compatibilidad de Hola y deshabilitar el uso de Hola de función de hello nueva estimación de cardinalidad mediante el uso de hello LEGACY_CARDINALITY_ESTIMATION establecer tooON con [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx). Esto se puede exactamente Hola igual que utilizando 110 desde un punto de vista de la función de estimación de cardinalidad, mientras que usa el nivel de compatibilidad de procesamiento de consultas más reciente de Hola. De esta forma, puede beneficiarse de nuevas con el nivel de compatibilidad más reciente de hello (es decir, el modo por lotes) características de procesamiento de consultas nuevo de hello, pero aun así, delegar en la funcionalidad de estimación de cardinalidad anterior Hola si es necesario.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Mover simplemente toohello de nivel de compatibilidad 120 o 130 habilita la funcionalidad de estimación de cardinalidad nueva Hola. En tal caso, el predeterminado hello CardinalityEstimationModelVersion se establecerá en consecuencia too120 o 130 como visible.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*Figura 5: Hola CardinalityEstimationModelVersion se establece too130 cuando se usa un nivel de compatibilidad de 130.*

![Ilustración 5.](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Diferencias de estimación de cardinalidad de Hola que hayan presenciado
Ahora, vamos a ejecutar ligeramente más complejo que implica una operación INNER JOIN con una cláusula WHERE con algunos de los predicados de consulta y echemos un vistazo a Hola estimación del recuento de filas en función de estimación de cardinalidad anterior hello en primer lugar.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Para ejecutar esta consulta eficazmente devuelve 200.704 filas, mientras la estimación de la fila de hello con funcionalidad de estimación de cardinalidad anterior Hola notificaciones 194,284 filas. Obviamente, como hemos comentado, estos resultados de recuento de filas también dependerán de la frecuencia con ejecutó Hola ejemplos anteriores, que rellena las tablas de ejemplo de Hola y otra vez en cada ejecución. Obviamente, los predicados de hello en la consulta también tendrá una influencia en la estimación real de hello excepto en forma de tabla de hello, el contenido de datos y cómo estos datos realmente correlación entre sí.

*Figura 6: estimación del recuento de filas Hola procede 194,284 o 6.000 filas desactivar 200.704 filas Hola esperado.*

![Ilustración 6.](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

Hola igual, vamos a ejecutar ahora Hola misma consulta con la nueva funcionalidad de estimación de cardinalidad Hola.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Examinando Hola a continuación, se pueden ver que el cálculo de esa fila de hello es 202,877, o mucho más cercano y superiores a Hola estimación de cardinalidad anterior.

*Figura 7: estimación del recuento de filas Hola ahora es 202,877, en lugar de 194,284.*

![Ilustración 7.](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

En realidad, el conjunto de resultados de hello es 200.704 filas (pero completamente depende de la frecuencia con ejecutó ejemplos anteriores de consultas Hola de hello, pero es más importante, porque Hola TSQL utiliza la instrucción de RAND() hello, devueltos los valores reales Hola pueden variar desde una toohello de ejecución junto). Por consiguiente, en este ejemplo concreto, hello nueva estimación de cardinalidad no más eficaces al calcular el número de Hola de filas porque 202,877 es mucho más cerca de too200, 704, que 194,284! Por último, si cambia hello tooequality de predicados de la cláusula WHERE (en lugar de ">" por ejemplo), esto podría realizar estimaciones de hello entre Hola antigua y nueva función de cardinalidad incluso más diferentes, dependiendo de cuántas coincidencias que puedas.

En este caso, una diferencia de aproximadamente 6000 filas con respecto recuento real, en algunas situaciones no representa una gran cantidad de datos. Ahora, transponer este toomillions de filas a través de varias tablas y consultas más complejas, y en ocasiones Hola estimación puede ser incorrecta millones de filas y por lo tanto, Hola a riesgo de Hola de selección de seguridad incorrecto de plan de ejecución, o la solicitud de memoria insuficiente concede inicial los volcados de tooTempDB y por lo que más i/OS, son mucho mayores.

Si tiene la oportunidad de hello, esta comparación con las consultas más frecuentes y los conjuntos de datos de procedimientos y descubrir por sí mismo cuánto algunas de las estimaciones nuevos y antiguos de Hola se ven afectados, mientras que algunos simplemente dejen de estar más desactivado en realidad de Hola o algunos otros simplemente Cuanto más se acerque toohello real de la fila cuenta realmente devueltos en los conjuntos de resultados de Hola. Completamente dependerán de la forma de Hola de consultas, las características de base de datos de SQL Azure Hola, naturaleza Hola y tamaño de Hola de conjuntos de datos y estadísticas de hello disponibles sobre ellos. Si acaba de crear la instancia de base de datos de SQL Azure, realice una consulta de hello optimizador tendrá toobuild ejecuta su conocimiento desde cero en lugar de reutilizar las estadísticas formadas consulta anterior Hola. Por lo tanto, las estimaciones de hello son situación de servidor y la aplicación de tooevery muy contextuales y casi específico. Es un tookeep aspecto importante en mente.

## <a name="some-considerations-tootake-into-account"></a>Algunos tootake consideraciones en cuenta
Aunque la mayoría de las cargas de trabajo se beneficiarían de nivel de compatibilidad de hello 130, antes de la adopción de nivel de compatibilidad de hello para el entorno de producción, básicamente tiene 3 opciones:

1. Mover el nivel de toocompatibility 130 y vea cómo realizan cosas. En caso de que observe algunas regresiones, simplemente establezca tooits atrás de hello compatibilidad nivel nivel original, o mantener 130 y sólo invertir modo heredado de hello estimación de cardinalidad toohello back-(como se explicó anteriormente, esto solo podría solucionar Hola problema).
2. Probar exhaustivamente las aplicaciones existentes en la carga de producción similares, ajustar y validar el rendimiento de hello antes de ir tooproduction. En el caso de problemas, igual que el anterior, puede siempre volver atrás toohello nivel de compatibilidad original, o simplemente invertir modo heredado de hello estimación de cardinalidad toohello atrás.
3. Como última opción y Hola tooaddress más reciente de manera estas preguntas, es el almacén de consultas de hello tooleverage. Esta es la opción recomendada en este momento. análisis de hello tooassist de las consultas con la compatibilidad con nivel 120 o por debajo frente a 130, no le recomendamos suficiente toouse almacén de consultas. Almacén de consultas está disponible con la versión más reciente de Hola de V12 de base de datos de SQL Azure, y está diseñada toohelp, con la solución de problemas de rendimiento de consulta. Considerar Hola almacén de consultas como una caja negra de datos para la base de datos, recopilar y presentar información histórica detallada sobre todas las consultas. En gran medida Esto simplifica el análisis forense de rendimiento reduciendo Hola tiempo toodiagnose y resolver problemas. Puede encontrar más información en [A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)(Una caja negra para la base de datos).

En alto nivel, si ya tiene un conjunto de bases de datos que se ejecuta en el nivel de compatibilidad 120 o por debajo y planear toomove Hola algunas de ellas too130, o porque la carga de trabajo aprovisionar automáticamente nuevas bases de datos que se va convertirse establecido por too130 de manera predeterminada, considere la posibilidad de siguiente Hello:

* Antes de cambiar toohello nuevo nivel de compatibilidad en producción, habilite el almacén de consultas. Puede hacer referencia demasiado[cambiar el almacén de consultas de Hola de modo de compatibilidad de base de datos y el uso hello](https://msdn.microsoft.com/library/bb895281.aspx) para obtener más información.
* A continuación, pruebe todas estas cargas de trabajo con datos representativos y las consultas de un entorno de producción similar y compare el rendimiento de hello experimentó así como información proporcionada por el almacén de consultas. Si se producen algunas regresiones, puede identificar Hola consultas devueltas con hello almacén de consultas y usar la opción de almacén de consultas de forzado de plan de hello (también conocido como plan de anclaje). En tal caso, definitivamente permanecerá con el nivel de compatibilidad de hello 130 y utilizar el plan de consulta anterior de hello tal como se sugiere por hello almacén de consultas.
* Si desea tooleverage nuevas características y funcionalidad de la base de datos de SQL de Azure (que se está ejecutando SQL Server 2016), pero son confidenciales toochanges pone el nivel de compatibilidad de hello 130, como último recurso, podría considerar la posibilidad de forzar el nivel de compatibilidad Hola nivel de toohello que se ajuste a la carga de trabajo mediante el uso de una instrucción ALTER DATABASE. Pero en primer lugar, tenga en cuenta ese plan de almacén de consultas de hello fijar opción es la mejor opción porque no utiliza 130 básicamente se mantiene en el nivel de funcionalidad de Hola de una versión anterior de SQL Server.
* Si tiene aplicaciones para varios inquilinos que abarcan varias bases de datos, es posible hello tooupdate necesarios aprovisionamiento lógica de su tooensure de bases de datos un nivel de compatibilidad coherente en todas las bases de datos; los antiguos y recién suministrados. El rendimiento de carga de trabajo de la aplicación podría ser hechos toohello confidenciales que algunas bases de datos se ejecutan en los niveles de compatibilidad diferentes, y por lo tanto, podría ser necesaria la coherencia de nivel de compatibilidad a través de cualquier base de datos en orden tooprovide Hola igual experiencia de clientes tooyour todo en el tablero de Hola. Tenga en cuenta que no es obligatorio, realmente depende de cómo su aplicación se ve afectada por el nivel de compatibilidad de Hola.
* Por último, con respecto a la estimación de cardinalidad de hello y, como cambiar el nivel de compatibilidad de hello, antes de continuar en producción, es recomendable tootest la carga de trabajo de producción en hello nuevas condiciones toodetermine si su aplicación se beneficia de mejoras de estimación de cardinalidad de Hola.

## <a name="conclusion"></a>Conclusión
Uso de base de datos de SQL Azure toobenefit de todas las mejoras de SQL Server 2016 puede mejorar claramente las ejecuciones de la consulta. Así de simple. Por supuesto, como ocurre con cualquier característica nueva, una evaluación adecuada debe realizarse en la que la carga de trabajo de la base de datos funciona Hola mejor condiciones toodetermine Hola exactas. Experiencia muestra que la mayoría de la carga de trabajo son tooat esperado menos ejecutan de forma transparente en el nivel de compatibilidad 130, mientras aprovecha las funciones y la nueva estimación de cardinalidad de procesamiento de consultas nuevas. Que dice, de forma realista, siempre hay algunas excepciones y realizar vencimiento apropiado diligencia es un toodetermine de evaluación importante cuánto puede beneficiarse de estas mejoras. Y una vez más, almacén de consultas de Hola de puede ser de gran ayuda para realizar este trabajo.

Medida que evoluciona SQL Azure, puede esperar un nivel de compatibilidad 140 Hola futuras. Cuando el momento sea apropiado, empezaremos a hablar de lo que aportará este futuro nivel de compatibilidad 140, igual que hemos explicado brevemente aquí lo que el nivel de compatibilidad 130 aporta hoy.

Por ahora, no se olvide, a partir de junio de 2016, base de datos de SQL Azure dejará nivel de compatibilidad de saludo predeterminado de 120 too130 para bases de datos recién creadas. ¡Prepárese!

## <a name="references"></a>Referencias
* [Novedades (motor de base de datos)](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Blog: Query Store: A flight data recorder for your database (Almacén de consultas: Una caja negra para la base de datos) por Borko Novakovic, 8 de junio de 2016](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [Nivel de compatibilidad de ALTER TABLE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx)
* [Compatibility Level 130 for Azure SQL Database V12](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Optimizar los planes de consulta con hello Estimador de cardinalidad de SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)
* [Descripción de los índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx)
* [Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database (Rendimiento mejorado de consultas con el nivel de compatibilidad 130 en Base de datos SQL de Azure) por Alain Lissoir, 6 de mayo de 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->

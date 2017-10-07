---
title: aaaResolve problemas de sesgo de datos mediante el uso de Azure Data Lake Tools para Visual Studio | Documentos de Microsoft
description: "Posibles soluciones para problemas de asimetría de datos mediante el uso de Herramientas de Azure Data Lake para Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Resuelva los problemas de asimetría de datos con Herramientas de Azure Data Lake para Visual Studio

## <a name="what-is-data-skew"></a>¿Qué es la asimetría de datos?

En pocas palabras, una asimetría de datos es un valor sobrerrepresentado. Imagine que haya asignado a 50 examinadores de impuestos tooaudit impuestos, uno examinador para cada estado de Estados Unidos. Examinador de Wyoming Hello, porque no existe la población de hello es muy pequeña, tiene poco toodo. En California, sin embargo, Examinador de Hola se mantiene muy ocupado debido a la población grande del estado de Hola.
    ![Ejemplo de problema de asimetría de datos](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

En nuestro escenario, datos de Hola se distribuyen entre todos los examinadores de impuestos, lo que significa que algunos examinadores deben trabajar más que otros. En su propio trabajo experimenta con frecuencia situaciones como este ejemplo de Hola Examinador de impuestos. En términos más técnicos, un vértice obtiene mucho más datos que sus elementos del mismo nivel, una situación que hace que los vértices Hola funcione más Hola otras y que finalmente se ralentiza un trabajo completo. ¿Qué es lo que es peor, trabajo Hola puede producir un error, porque podrían tener vértices, por ejemplo, una limitación de tiempo de ejecución de 5 horas y una limitación de 6 GB de memoria.

## <a name="resolving-data-skew-problems"></a>Resolución de problemas de asimetría de datos

Las Herramientas de Azure Data Lake para Visual Studio pueden ayudar a detectar si el trabajo tiene un problema de asimetría de datos. Si existe algún problema, puede resolverlo realizando soluciones hello en esta sección.

## <a name="solution-1-improve-table-partitioning"></a>Solución 1: Mejorar la partición de tabla

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Opción 1: Hola filtro sesgado clave-valor de antemano

Si no afecta a la lógica de negocios, puede filtrar valores de hello más frecuente de antemano. Por ejemplo, si hay mucha 000-000-000, en la columna GUID, no puede tooaggregate ese valor. Antes de agregado, puede escribir "WHERE GUID! ="000-000 000"" valor de alta frecuencia de toofilter Hola.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Opción 2: Seleccionar una clave de partición o distribución diferente

Hola anterior ejemplo, si desea que la carga de trabajo de solo toocheck Hola auditoría fiscal todos sobre Hola país, puede mejorar la distribución de datos de hello seleccionando el número de Id. de hello como su clave. Seleccionar una partición diferente o una clave de distribución puede a veces distribuir datos hello más uniformemente, pero debe toomake seguro de que esta opción no afecta a la lógica de negocios. Por ejemplo, suma de impuestos de toocalculate Hola para cada estado, es recomendable toodesignate _estado_ como clave de partición de Hola. Si sigues tooexperience este problema, pruebe a usar la opción 3.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Opción 3: Agregar más claves de partición o distribución

En lugar de usar solo _Estado_ como clave de partición, puede usar más de una clave para las particiones. Por ejemplo, considere la posibilidad de agregar _código postal_ como una partición adicional tooreduce clave de partición de datos, tamaños y distribuir más uniformemente los datos de Hola.

### <a name="option-4-use-round-robin-distribution"></a>Opción 4: Usar la distribución round robin

Si no se encuentra una clave adecuada para la partición y distribución, puede intentar toouse distribución por turnos. La distribución round robin trata por igual cada fila y la coloca de forma aleatoria en el depósito correspondiente. datos de Hello obtiene distribuyen uniformemente, pero pierde la información de localidad, un inconveniente de que también se puede reducir el rendimiento de trabajo para algunas operaciones. Además, si está realizando clave sesgados hello las agregaciones de todos modos, se conservará el problema de hello sesgo de datos. toolearn más información acerca de la distribución por turnos, vea hello U-SQL tabla distribuciones sección [CREATE TABLE (U-SQL): crear una tabla con esquema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>Solución 2: Mejorar el plan de consulta de Hola

### <a name="option-1-use-hello-create-statistics-statement"></a>Opción 1: Usar la instrucción CREATE STATISTICS de Hola

U-SQL proporciona la instrucción CREATE STATISTICS de hello en tablas. Esta instrucción da el optimizador de consultas de toohello de más información acerca de características de datos de hello, como la distribución de valor, que se almacenan en una tabla. Para la mayoría de las consultas, el optimizador de consultas de hello ya genera las estadísticas que necesita para un plan de consulta de alta calidad Hola. En ocasiones, puede que tenga tooimprove rendimiento de las consultas creando estadísticas adicionales con CREATE STATISTICS o modificando el diseño de la consulta de Hola. Para obtener más información, vea hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) página.

Ejemplo de código:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>La información de estadísticas no se actualiza automáticamente. Si actualiza datos hello en una tabla sin volver a crear las estadísticas de hello, puede rechazar el rendimiento de las consultas Hola.

### <a name="option-2-use-skewfactor"></a>Opción 2: usar SKEWFACTOR

Si desea que los impuestos hello toosum para cada estado, debe usar Agrupar por estado, un método que no evita el problema de hello sesgo de datos. Sin embargo, puede proporcionar una sugerencia de datos en su tooidentify consulta sesgo de datos en las claves para que el optimizador de hello puede preparar un plan de ejecución automáticamente.

Por lo general, puede establecer el parámetro hello como 0,5 y 1, con lo que significa que no mucho sesgo pesada significado sesgo y 1 de 0,5. Porque la sugerencia de hello afecta a la optimización de plan de ejecución para la instrucción actual de Hola y todas las instrucciones de nivel inferiores, estar seguro de sugerencia de hello tooadd antes de Hola posible había sesgado agregación key-wise.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Ejemplo de código:

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>Opción 3: Usar ROWCOUNT  
Además tooSKEWFACTOR para específico de clave asimétrica unir los casos, si sabe que Hola otro conjunto de filas combinadas es pequeño, puede indicar el optimizador Hola agregando una sugerencia de recuento de filas en la instrucción de SQL U Hola antes de la combinación. De esta manera, el optimizador puede elegir un toohelp de estrategia de combinación difusión mejorar el rendimiento. Tenga en cuenta que recuento de filas no resuelve el problema de hello sesgo de datos, pero puede ofrecer cierta ayuda adicional.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Ejemplo de código:

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Solución 3: Mejorar Combinador y reductor de hello definido por el usuario

En ocasiones, puede escribir un toodeal operador definido por el usuario con la lógica de proceso complicado y un reductor bien escrito y Combinador podrían mitigar un problema de sesgo de datos en algunos casos.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Opción 1: Utilizar un reductor recursivo si es posible

De forma predeterminada, el reductor definido por el usuario se ejecuta como modo no recursivo, lo que significa que el trabajo reducido para una clave se va a distribuir a un solo vértice. Pero si se sesga los datos, conjuntos de datos muy grandes de Hola podría se procesan en un solo vértice y ejecutar durante mucho tiempo.

rendimiento de tooimprove, puede agregar un atributo en su toorun de código toodefine reductor de modo recursivo. A continuación, conjuntos de datos muy grandes de hello pueda toomultiple distribuida vértices y ejecutar en paralelo, lo que acelera el trabajo.

toochange un toorecursive de reductor no recursivo, debe toomake seguro de que el algoritmo es asociativo. Por ejemplo, es asociativo a la suma de Hola y Hola median no es. También necesita toomake seguro de que Hola de entrada y salida para el reductor mantienen Hola mismo esquema.

Atributo del reductor recursivo:

    [SqlUserDefinedReducer(IsRecursive = true)]

Ejemplo de código:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Opción 2: Utilizar el modo de combinador de nivel de fila si es posible

Sugerencia de recuento de filas toohello similar para los casos de combinación concreta de clave asimétrica, modo de Combinador intenta toodistribute valor de clave asimétrica grandes conjuntos de toomultiple vértices para que el trabajo de hello puede ejecutarse simultáneamente. El modo de combinador no puede resolver los problemas de asimetría de datos, pero puede proporcionar ayuda adicional para grandes conjuntos de valores de claves asimétricas.

De forma predeterminada, el modo de Combinador hello es completo, lo que significa que Hola deja el conjunto de filas y no se puede separar el conjunto de filas secundario. Establecer el modo de hello como izquierda o derecha/interna permite la combinación de nivel de fila. sistema de Hello separa los conjuntos de filas correspondientes de Hola y distribuye en varios vértices que se ejecutan en paralelo. Sin embargo, antes de configurar el modo de Combinador hello, tenga cuidado tooensure que Hola conjuntos de filas correspondientes se puede separar.

ejemplo de Hola que sigue muestra un conjunto de filas izquierdo separados. Cada fila de salida depende de una sola fila de entrada de hello izquierda, y potencialmente depende de todas las filas de hello derecha con hello mismo valor de clave. Si establece el modo de Combinador hello como left, sistema de hello separa Hola enorme izquierda-conjunto de filas en las pequeñas y las asigna toomultiple vértices.

![Ilustración del modo de combinador](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Si establece el modo de hello Combinador incorrecto, combinación de hello es menos eficaz y resultados de hello podrían ser incorrectos.

Atributos del modo de combinador:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): Cada fila de salida depende de una sola fila de entrada de hello izquierda (y potencialmente todas las filas de hello derecha con hello mismo valor de clave).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): cada fila de salida depende de una sola fila de entrada de hello derecho (y potencialmente todas las filas de hello izquierda con hello mismo valor de clave).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Cada fila de salida depende de una sola fila de entrada de izquierda Hola y Hola derecha con hello mismo valor.

Ejemplo de código:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }

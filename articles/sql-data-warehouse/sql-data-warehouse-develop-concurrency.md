---
title: "administración de aaaConcurrency y carga de trabajo en el almacén de datos de SQL | Documentos de Microsoft"
description: "Obtenga información sobre la simultaneidad y la administración de cargas de trabajo en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>Simultaneidad y administración de cargas de trabajo en Almacenamiento de datos SQL
toodeliver un rendimiento predecible a escala, almacenamiento de datos de SQL de Microsoft Azure le ayuda a controlar los niveles de simultaneidad y las asignaciones de recursos como memoria y asignación de prioridades de CPU. Este artículo detallan toohello conceptos de administración de simultaneidad y la carga de trabajo, que explica cómo ambas características se han implementado y cómo se puede controlar en el almacenamiento de datos. Administración de cargas de trabajo de almacenamiento de datos SQL es toohelp previsto admitir entornos de varios usuarios. No está diseñada para cargas de trabajo de multiinquilino.

## <a name="concurrency-limits"></a>Límites de simultaneidad
Almacenamiento de datos SQL permite que un too1, 024 conexiones simultáneas. Todas las 1.024 conexiones pueden enviar consultas al mismo tiempo. Sin embargo, toooptimize rendimiento, almacenamiento de datos SQL puede poner en cola algunos tooensure de las consultas que cada consulta recibe una concesión de memoria mínima. Durante el tiempo de ejecución de las consultas, estas se empiezan a poner en cola. Las consultas de puesta en cola cuando puede aumentar la simultaneidad se alcanzan los límites, almacenamiento de datos SQL total rendimiento asegurándose de que las consultas activas obtienen acceso toocritically necesita recursos de memoria.  

Los límites de simultaneidad se rigen por dos conceptos: *consultas simultáneas* y *espacios de simultaneidad*. Para una consulta tooexecute, debe ejecutar dentro de límite de simultaneidad de consultas de Hola y asignación de ranura de simultaneidad de Hola.

* Consultas simultáneas son consultas de hello ejecutar en hello mismo tiempo. Almacenamiento de datos SQL admite hasta too32 consultas simultáneas en hello DWU más grandes.
* Los espacios de simultaneidad se asignan según DWU. Cada 100 DWU proporciona 4 espacios de simultaneidad. Por ejemplo, un DW100 asigna 4 espacios de simultaneidad y DW1000 asigna 40. Cada consulta consume uno o más simultaneidad ranuras, depende de hello [clase de recursos](#resource-classes) de consulta de Hola. Las consultas se ejecutan en la clase de recurso de hello smallrc consuman una ranura de simultaneidad. Las consultas que se ejecutan en una clase de recurso superior consumen más intervalos de simultaneidad.

Hello tabla siguiente describen los límites de Hola para consultas simultáneas y ranuras de simultaneidad en hello diversos tamaños de unidad.

### <a name="concurrency-limits"></a>Límites de simultaneidad
| DWU | N.º máximo de consultas simultáneas | Espacios de simultaneidad asignados |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 | |20 | |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

Cuando se alcanza alguno de estos umbrales, se ponen a la cola nuevas consultas y se ejecutan según la regla "primero en entrar, primero en salir".  Cuando finaliza un consulta y número de Hola de consultas y ranuras cae por debajo de los límites de hello, se liberan las consultas en cola. 

> [!NOTE]  
> *Seleccione* las consultas que se ejecuta exclusivamente en vistas de administración dinámica (DMV) o vistas de catálogo no se rigen por cualquiera de los límites de simultaneidad de Hola. Puede supervisar el sistema de hello independientemente del número de Hola de las consultas que se ejecuta en él.
> 
> 

## <a name="resource-classes"></a>Clases de recursos
Clases de recursos ayudan a controlar la asignación de memoria y ciclos de CPU proporcionados tooa consulta. Puede asignar a dos tipos de usuario de tooa de clases de recursos con formato de Hola de roles de base de datos. Hola dos tipos de clases de recursos son los siguientes:
1. Clases de recursos dinámicos (**smallrc, mediumrc, largerc, xlargerc**) asigne una cantidad de memoria en función hello variable DWU actual. Esto significa que al escalar una tooa DWU más grande, las consultas automáticamente obtengan más memoria. 
2. Las clases estáticas de recursos (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) asignar Hola misma cantidad de memoria con independencia de Hola DWU actual (siempre que Hola DWU propio no tiene suficiente memoria). Esto significa que, con unidades mayores, puede ejecutar más consultas en cada clase de recursos al mismo tiempo.

A los usuarios con **smallrc** y **staticrc10** se les concede una cantidad de memoria menor y pueden aprovechar una mayor simultaneidad. En cambio, los usuarios asignados demasiado**xlargerc** o **staticrc80** reciben grandes cantidades de memoria, y por lo tanto, menos las consultas pueden ejecutarse simultáneamente.

De manera predeterminada, cada usuario es un miembro de clase de recursos pequeño hello, **smallrc**. Hola procedimiento `sp_addrolemember` es usa la clase de recurso tooincrease hello y `sp_droprolemember` es usa la clase de recurso de hello toodecrease. Por ejemplo, este comando podría aumentar la clase de recurso de hello de loaduser demasiado**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>Consultas que no respetan las clases de recursos

Existen algunos tipos de consultas que no se benefician de una mayor asignación de memoria. sistema de Hello omite su asignación de recursos de clase y siempre ejecuta estas consultas en la clase de recursos pequeño hello en su lugar. Si estas consultas se ejecutan siempre en la clase de recursos pequeño de hello, pueden ejecutarse cuando las ranuras de simultaneidad que están bajo presión y no consumen más ranuras de los necesarios. Consulte [Excepciones de clase de recursos](#query-exceptions-to-concurrency-limits) para más información.

## <a name="details-on-resource-class-assignment"></a>Detalles sobre la asignación de la clase de recursos


Más detalles en la clase de recursos:

* *Modificar rol* se requiere permiso de clase de recurso de hello toochange de un usuario.
* Aunque puede agregar un usuario tooone o más de las clases de recursos elevadas Hola, clases de recursos dinámicos tienen prioridad sobre las clases de recurso estático. Es decir, si se asigna a un usuario tooboth **mediumrc**(dinámico) y **staticrc80**(estático), **mediumrc** es la clase de recurso de Hola que se respeta.
 * Cuando se asigna a un usuario toomore que la clase de un recurso en un tipo de clase de recurso específico (más de una clase de recurso dinámico o más de una clase de recurso estático), está asignada la clase de recurso más alto de Hola. Es decir, si un usuario se le asigna largerc y tooboth mediumrc, se respeta la clase de recurso superior hello (largerc). Y si se asigna a un usuario tooboth **staticrc20** y **statirc80**, **staticrc80** se cumplirá.
* no se puede cambiar la clase de recurso de Hola Hola administrativos de usuario del sistema.

Para un ejemplo detallado, consulte [Cambio de ejemplo de clase de recursos de usuario](#changing-user-resource-class-example).

## <a name="memory-allocation"></a>Asignación de memoria
Hay ventajas y desventajas tooincreasing clase de recursos de un usuario. Al aumentar una clase de recursos para un usuario, ofrece a sus consultas memoria toomore de acceso, lo que puede conllevar las consultas se ejecutan con mayor rapidez.  Sin embargo, las clases de recursos elevadas también reducen el número de Hola de consultas simultáneas que se pueden ejecutar. Se trata de equilibrio de hello entre asignar grandes cantidades de consulta única de tooa de memoria o si permite que otras consultas, que también necesitan las asignaciones de memoria, toorun simultáneamente. Si un usuario se le concede alta asignaciones de memoria para una consulta, otros usuarios no tendrán acceso toothat mismo memoria toorun una consulta.

Hello en la tabla siguiente asigna memoria de Hola asignada tooeach distribución por unidad y recursos de clase.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>Asignaciones de memoria por distribución para las clases de recursos dinámicos (MB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1600 |
| DW500 |100 |400 |800 |1600 |
| DW600 |100 |400 |800 |1600 |
| DW1000 |100 |800 |1600 |3.200 |
| DW1200 |100 |800 |1600 |3.200 |
| DW1500 |100 |800 |1600 |3.200 |
| DW2000 |100 |1600 |3.200 |6.400 |
| DW3000 |100 |1600 |3.200 |6.400 |
| DW6000 |100 |3.200 |6.400 |12.800 |

Hello en la tabla siguiente asigna memoria de hello asignada tooeach distribución por unidad y la clase de recurso estático. Tenga en cuenta que las clases de recursos elevadas hello tienen su memoria reduce los límites de DWU globales toohonor Hola.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>Asignaciones de memoria por distribución para las clases de recursos estáticos (MB)
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1600 |1600 |1600 |1600 |
| DW500 |100 |200 |400 |800 |1600 |1600 |1600 |1600 |
| DW600 |100 |200 |400 |800 |1600 |1600 |1600 |1600 |
| DW1000 |100 |200 |400 |800 |1600 |3.200 |3.200 |3.200 |
| DW1200 |100 |200 |400 |800 |1600 |3.200 |3.200 |3.200 |
| DW1500 |100 |200 |400 |800 |1600 |3.200 |3.200 |3.200 |
| DW2000 |100 |200 |400 |800 |1600 |3.200 |6.400 |6.400 |
| DW3000 |100 |200 |400 |800 |1600 |3.200 |6.400 |6.400 |
| DW6000 |100 |200 |400 |800 |1600 |3.200 |6.400 |12.800 |

De hello tabla anterior, puede ver que una consulta que se ejecuta en un DW2000 Hola **xlargerc** clase de recurso tendría acceso too6, 400 MB de memoria en cada una de las bases de datos distribuidas Hola 60.  En Almacenamiento de datos SQL, existe 60 distribuciones. Por lo tanto, asignación de memoria total de hello toocalculate para una consulta en una clase de recurso determinado, Hola por encima de valores debe se multiplica por 60.

### <a name="memory-allocations-system-wide-gb"></a>Asignaciones de memoria en todo el sistema (GB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

En esta tabla de asignaciones de memoria de todo el sistema, puede ver que una consulta que se ejecuta en un DW2000 en la clase de recurso de hello xlargerc se asigna un total de 375 GB de memoria (MB * 60 6.400 distribuciones / 1.024 tooconvert tooGB) en toda Hola el almacenamiento de datos de SQL.

Hello mismo cálculo aplica toostatic clases de recursos.
 
## <a name="concurrency-slot-consumption"></a>Consumo de ranuras de simultaneidad  
Almacenamiento de datos SQL concede más tooqueries memoria ejecuta en las clases de recursos elevadas. La memoria es un recurso fijo.  Por lo tanto, hello más memoria asignada por cada consulta, Hola pueden ejecutar menos consultas simultáneas. Hello siguiente tabla Reitere todos Hola conceptos anterior en una sola vista que muestra el número de Hola de ranuras de simultaneidad disponibles por unidad y ranuras de hello consumidas por cada clase de recursos.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>Asignación y consumo de espacios de simultaneidad para las clases de recursos dinámicos  
| DWU | N.º máximo de consultas simultáneas | Espacios de simultaneidad asignados | Ranuras utilizadas por smallrc | Ranuras utilizadas por mediumrc | Ranuras utilizadas por largerc | Ranuras utilizadas por xlargerc |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 | |20 | |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>Asignación y consumo de espacios de simultaneidad para las clases de recursos estáticos  
| DWU | N.º máximo de consultas simultáneas | Espacios de simultaneidad asignados |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20 || 20 || 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

En esta tabla, puede ver que SQL Data Warehouse, que se ejecuta como DW1000, ofrece 32 consultas simultáneas como máximo y 40 ranuras de simultaneidad en total. Si todos los usuarios se ejecutan en la clase smallrc, se permitirían 32 consultas simultáneas, ya que cada una consumiría 1 espacio de simultaneidad. Si todos los usuarios en un DW1000 se estaban ejecutando en mediumrc, cada consulta se asignaría 800 MB por la distribución para una asignación de memoria total de 47 GB por cada consulta y simultaneidad sería too5 limitado a los usuarios (40 ranuras de simultaneidad 8 ranuras disponibles por usuario mediumrc).

## <a name="selecting-proper-resource-class"></a>Selección de la clase de recurso correcta  
Clase de recursos de tooa de toopermanently asignar los usuarios, en lugar de cambiar sus clases de recursos, es una práctica recomendada. Por ejemplo, tablas de almacén de columnas de carga tooclustered crear índices de mayor calidad al asignar más memoria. tooensure que carga tiene acceso toohigher memoria, cree un usuario específico para cargar datos y asigna de forma permanente esta clase de recurso de usuario tooa superior.
Hay un par de toofollow de prácticas recomendada aquí. Como se mencionó anteriormente, SQL DW admite dos tipos de clase de recurso: estáticos y dinámicos.
### <a name="loading-best-practices"></a>Carga de procedimientos recomendados
1.  Si las expectativas de hello son cargas regulares cantidad de datos, una clase de recurso estático es una buena elección. Más adelante, cuando tooget el escalado más potencia de cálculo, almacenamiento de datos de hello podrán toorun más simultánea consulta out-of-the-box, como usuario de la carga de hello no consume más memoria.
2.  Si las expectativas de hello son mayores cargas en algunas ocasiones, una clase de recurso dinámico es una buena elección. Más adelante, cuando se escala ascendentemente tooget más potencia de cálculo, Hola carga usuario obtendrá más memoria out-of-the-box, por lo tanto, lo que permite Hola carga tooperform con mayor rapidez.

Hello memoria necesaria tooprocess cargas eficazmente depende Hola naturaleza de tabla Hola cargado y cantidad de Hola de procesamiento de datos. Por ejemplo, cargar datos en tablas CCI requiere que algunos grupos de filas de memoria toolet CCI alcanzar estado óptimo. Para obtener más información, vea índices de almacén de columnas de hello - Guía de la carga de datos.

Como práctica recomendada, se aconseja toouse como mínimo 200MB de memoria para las cargas.

### <a name="querying-best-practices"></a>Procedimientos recomendados sobre las consultas
Las consultas tienen requisitos diferentes en función de su complejidad. El aumento de memoria por consulta o aumentar la simultaneidad de hello son ambos métodos válidos tooaugment rendimiento global en función de las necesidades de consulta de Hola.
1.  Si las expectativas de hello son consultas normales y complejas (por ejemplo, toogenerate informes diarios y semanales) y no es necesario tootake ventajas de simultaneidad, una clase de recurso dinámico es una buena elección. Si el sistema de hello tiene más tooprocess de datos, escalar verticalmente el almacenamiento de datos de hello, por tanto, proporcionará automáticamente más ejecutando Hola consulta de usuario de toohello de la memoria.
2.  Si las expectativas de Hola son modelos de simultaneidad de variable o diurna (por ejemplo si se consulta la base de datos de Hola a través de un sitio web ampliamente accesible de la interfaz de usuario), una clase de recurso estático es una buena elección. Más adelante, cuando se escala ascendentemente toodata almacenamiento, usuario Hola asociado con la clase de recurso estático Hola configurará automáticamente y ser capaz de toorun consultas más simultáneas.

Selección de concesión de memoria adecuada según la necesidad de saludo de la consulta no es trivial, ya que depende de muchos factores, como la cantidad de Hola de datos consultados, naturaleza Hola de esquemas de tabla de hello y combinación de varios, selección y predicados de grupo. Desde la perspectiva general, asignar más memoria le permitirá toocomplete de consultas más rápido, pero se reduciría Hola simultaneidad general. Si la simultaneidad no es un problema, asignar una cantidad de memoria mayor de la necesaria no resulta perjudicial. toofine optimizar el rendimiento, tratando de distintas versiones de las clases de recursos puede ser necesario.

Puede usar los siguientes Hola almacenados toofigure procedimiento espera de concesión de memoria y simultaneidad por clase de recurso en un determinado hello y SLO clase más cercana mejor recurso para operaciones de CCI intensivo de memoria en la tabla CCI sin particiones en una clase de recurso determinado:

#### <a name="description"></a>Description:  
Este es el propósito de Hola de este procedimiento almacenado:  
1. toohelp usuario averiguar grant de simultaneidad y la memoria por clase de recurso en un objetivo determinado. Usuario necesita tooprovide NULL para el esquema y nombre de tabla para este tal y como se muestra en el siguiente ejemplo de Hola.  
2. toohelp usuario averiguar más cercano clase de recurso Hola recomendada para hello memoria intensed operaciones de CCI (carga, tabla de copia, volver a generar índice, etc.) en una tabla con particiones no de CCI a una clase de recurso determinado. Hola almacenado proc utiliza toofind del esquema de tabla out Hola concesión de memoria necesaria para este.

#### <a name="dependencies--restrictions"></a>Dependencias y restricciones:
- Este procedimiento almacenado no es requisito de memoria de toocalculate diseñada para la tabla de particiones de cci.    
- Este procedimiento almacenado no tiene requisitos de memoria en la cuenta de la parte SELECT de Hola de CTAS/INSERT-SELECT y se da por supuesto toobe una instrucción SELECT simple.
- Este procedimiento almacenado utiliza una tabla temporal, por lo que se puede utilizar en la sesión de Hola donde se creó este procedimiento almacenado.    
- Este procedimiento almacenado depende de ofertas actuales de hello (por ejemplo, configuración de hardware, configuración DMS) y si alguno de los cambia, a continuación, este procedimiento almacenado no funcionará correctamente.  
- Este procedimiento almacenado depende del límite de simultaneidad ofrecido actualmente y, si este cambiara, no funcionaría correctamente.  
- Este procedimiento almacenado depende de las ofertas de clase de recursos actuales y, si estas cambiaran, no funcionaría correctamente.  

>  [!NOTE]  
>  Si no se obtienen resultados después de ejecutar el procedimiento almacenado con los parámetros proporcionados, podrían darse dos circunstancias. <br />1. Algún parámetro del almacenamiento de datos contiene un valor de SLO no válido <br />2. O bien, no hay ninguna clase de recursos coincidente para la operación CCI, si se proporcionó el nombre de la tabla. <br />Por ejemplo, en DW100, concesión de memoria máxima disponible es 400MB y si el esquema de tabla es extensa suficiente toocross Hola requisito de 400MB.
      
#### <a name="usage-example"></a>Ejemplo de uso:
Sintaxis:  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Escriba un tooextract de parámetro NULL Hola DWU actual de hello DW DB o proporcionar cualquier admitido DWU en forma de Hola de 'DW100'
2. @SCHEMA_NAME:Proporcione un nombre de esquema de tabla de Hola
3. @TABLE_NAME:Proporcione un nombre de tabla de interés de Hola

Ejemplos de ejecución de este procedimiento almacenado:  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

Table1 usa Hola por encima de los ejemplos se pudo crear como sigue:  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Esta es la definición del procedimiento almacenado de hello:
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>Importancia de las consultas
Almacenamiento de datos SQL implementa las clases de recursos mediante el uso de grupos de cargas de trabajo. Hay un total de ocho grupos de cargas de trabajo que controlan el comportamiento de Hola de clases de recursos de hello en hello diversos tamaños de unidad. Para cualquier unidad, almacenamiento de datos SQL usa solo cuatro de ocho grupos de cargas de trabajo Hola. Esto tiene sentido porque se asigna cada grupo de cargas de trabajo tooone de cuatro clases de recursos: smallrc, mediumrc, largerc, o xlargerc. Hello importancia de la descripción de los grupos de cargas de trabajo de hello es que algunos de estos grupos de cargas de trabajo se establecen toohigher *importancia*. El nivel de importancia se usa para la programación de la CPU. Las consultas que se ejecutan con importancia alta obtendrán tres veces más ciclos de CPU que aquellas con importancia media. Por lo tanto, las asignaciones de espacio de simultaneidad también determinan la prioridad en la CPU. Si una consulta utiliza 16 o más espacios, se ejecuta con importancia alta.

Hello tabla siguiente muestran las asignaciones de importancia de Hola para cada grupo de cargas de trabajo.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>Importancia y ranuras de tooconcurrency de asignaciones de grupo de cargas de trabajo
| Grupos de carga de trabajo | Asignación de espacio de simultaneidad | MB/Distribución | Asignación de importancia |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |Mediano |
| SloDWGroupC01 |2 |200 |Mediano |
| SloDWGroupC02 |4 |400 |Mediano |
| SloDWGroupC03 |8 |800 |Mediano |
| SloDWGroupC04 |16 |1600 |Alto |
| SloDWGroupC05 |32 |3.200 |Alto |
| SloDWGroupC06 |64 |6.400 |Alto |
| SloDWGroupC07 |128 |12.800 |Alto |

De hello **asignación y el consumo de ranuras de simultaneidad** gráfico, puede ver que una DW500 usa 1, 4, 8 o ranuras de simultaneidad 16 para smallrc, mediumrc, largerc y xlargerc, respectivamente. Puede buscar esos valores en hello anterior importancia de hello toofind de gráfico para cada clase de recursos.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>Asignación de DW500 de tooimportance de clases de recursos
| clase de recursos | Grupo de cargas de trabajo | Espacios de simultaneidad usados | MB/Distribución | importancia |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |Mediano |
| mediumrc |SloDWGroupC02 |4 |400 |Mediano |
| largerc |SloDWGroupC03 |8 |800 |Mediano |
| xlargerc |SloDWGroupC04 |16 |1600 |Alto |
| staticrc10 |SloDWGroupC00 |1 |100 |Mediano |
| staticrc20 |SloDWGroupC01 |2 |200 |Mediano |
| staticrc30 |SloDWGroupC02 |4 |400 |Mediano |
| staticrc40 |SloDWGroupC03 |8 |800 |Mediano |
| staticrc50 |SloDWGroupC03 |16 |1600 |Alto |
| staticrc60 |SloDWGroupC03 |16 |1600 |Alto |
| staticrc70 |SloDWGroupC03 |16 |1600 |Alto |
| staticrc80 |SloDWGroupC03 |16 |1600 |Alto |

Puede usar Hola después toolook de consulta DMV en diferencias de Hola de asignación de recursos de memoria en detalle de perspectiva de hello del regulador de recursos de Hola o el uso activos e históricos tooanalyze de grupos de cargas de trabajo de Hola para solucionar el problema.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>Consultas que respetan los límites de simultaneidad
La mayoría de las consultas se rigen por las clases de recursos. Estas consultas deben caber dentro de consultas simultáneas de Hola y umbrales de espacio de simultaneidad. Un usuario no puede elegir tooexclude una consulta de modelo de ranura de simultaneidad de Hola.

tooreiterate, hello instrucciones siguientes respetan las clases de recursos:

* INSERT-SELECT
* UPDATE
* DELETE
* SELECT (al consultar las tablas de usuario)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* ALTER TABLE REBUILD
* CREATE INDEX
* CREATE CLUSTERED COLUMNSTORE INDEX
* CREATE TABLE AS SELECT (CTAS)
* Carga de datos
* Operaciones de movimiento de datos realizadas por hello servicio de movimiento de datos (DMS)

## <a name="query-exceptions-tooconcurrency-limits"></a>Límites de tooconcurrency de excepciones de consulta
Algunas consultas no respetan los recursos de hello clase toowhich Hola usuario está asignado. Estos límites de simultaneidad de las excepciones toohello se realizan cuando Hola memoria necesarios para un determinado comando hay pocos recursos, a menudo como comando hello es una operación de metadatos. objetivo de Hola de estas excepciones es tooavoid asignaciones de memoria mayor para las consultas que nunca será necesario. En estos casos, predeterminado Hola siempre se utiliza la clase de recursos pequeño (smallrc), independientemente de la clase de recurso real de hello asignado toohello usuario. Por ejemplo, `CREATE LOGIN` se ejecutará siempre en la clase smallrc. Hola recursos necesarios toofulfill esta operación son muy bajo, por lo que no consulta de sentido tooinclude hello en el modelo de ranura de simultaneidad de Hola.  Estas consultas no están también limitadas por límite de simultaneidad de usuarios de hello 32, límite de 1.024 sesiones de toohello sesión puede ejecutar un número ilimitado de estas consultas.

Hola siguiendo las instrucciones no respeta las clases de recursos:

* CREATE o DROP TABLE
* ALTER TABLE ... SWITCH, SPLIT o MERGE PARTITION
* ALTER INDEX DISABLE
* DROP INDEX
* CREATE, UPDATE o DROP STATISTICS
* TRUNCATE TABLE
* ALTER AUTHORIZATION
* CREATE LOGIN
* CREATE, ALTER o DROP USER
* CREATE, ALTER o DROP PROCEDURE
* CREATE o DROP VIEW
* INSERT VALUES
* SELECT (desde vistas del sistema y DMV)
* EXPLAIN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a> Ejemplo de cambio de una clase de recursos de usuario
1. **Crear el inicio de sesión:** abrir una conexión tooyour **maestro** en hello SQL server que hospeda la base de datos de almacenamiento de datos SQL de base de datos y ejecutar Hola siga los comandos.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > Es un toocreate buena idea un usuario en la base de datos maestra de Hola para los usuarios de almacenamiento de datos de SQL Azure. La creación de un usuario en master permite un toologin de usuario con herramientas como SSMS sin especificar un nombre de base de datos.  También les permite toouse Hola objeto explorer tooview todas las bases de datos en un servidor SQL server.  Para obtener más información sobre cómo crear y administrar usuarios, consulte [Proteger una base de datos en SQL Data Warehouse][Secure a database in SQL Data Warehouse].
   > 
   > 
2. **Crear usuario del almacén de datos SQL:** abrir una conexión toohello **almacenamiento de datos SQL** la base de datos y ejecute el siguiente comando de Hola.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **Conceder permisos:** Hola siguientes en el ejemplo se concede `CONTROL` en hello **almacenamiento de datos SQL** base de datos. `CONTROL`en hello el nivel de base de datos es Hola equivalente de db_owner en SQL Server.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **Aumentar la clase de recurso:** consulta de uso Hola siguiente tooadd un rol usuario tooa mayor carga de trabajo administración.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **Reducir la clase de recurso:** consulta de uso Hola siguiente tooremove un usuario de un rol de administración de cargas de trabajo.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > No es posible tooremove un usuario de smallrc.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>Detección de consulta en cola y otras DMV
Puede usar hello `sys.dm_pdw_exec_requests` consultas tooidentify DMV que esperan en una cola de simultaneidad. Las consultas que esperan un espacio de simultaneidad tendrán el estado de **suspendido**.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

Los roles de administración de cargas de trabajo se pueden ver con `sys.database_principals`.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

Hola después de consulta muestra el rol que está asignado cada usuario.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

Almacenamiento de datos de SQL tiene Hola siguientes tipos de espera:

* **LocalQueriesConcurrencyResourceType**: las consultas que residen fuera del marco de ranura de simultaneidad de Hola. Las funciones del sistema y las consultas DMV como `SELECT @@VERSION` son ejemplos de consultas locales.
* **UserConcurrencyResourceType**: las consultas que se encuentran dentro de hello simultaneidad ranura framework. Las consultas en tablas de usuario final representan ejemplos que usarían este tipo de recurso.
* **DmsConcurrencyResourceType**: se refiere a las esperas que son el resultado de operaciones de movimiento de datos.
* **BackupConcurrencyResourceType**: se refiere a una espera que indica que se está creando la copia de seguridad de una base de datos. valor máximo de Hola para este tipo de recurso es 1. Si varias copias de seguridad se han solicitado en hello mismo tiempo, Hola otros se pondrán en cola.

Hola `sys.dm_pdw_waits` DMV puede ser toosee usa los recursos que una solicitud está esperando.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

Hola `sys.dm_pdw_resource_waits` DMV muestra solo hello las esperas de recursos utilizadas por una consulta determinada. Tiempo de espera de recursos sólo mide el tiempo de hello esperando toobe de recursos proporcionado, como los opuestos toosignal espera tiempo, lo que es el momento de hello tarda Hola subyacente de la consulta SQL servidores tooschedule hello en hello CPU.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

Hola `sys.dm_pdw_wait_stats` DMV se puede utilizar para el análisis de tendencias históricas de esperas.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo administrar los usuarios y la seguridad de la base de datos, consulte [Proteger una base de datos en SQL Data Warehouse][Secure a database in SQL Data Warehouse]. Para obtener más información acerca de cómo mayores clases de recursos puede mejorar la calidad del índice de almacén de columnas agrupado, vea [volver a generar la calidad de segmento de índices tooimprove].

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[volver a generar la calidad de segmento de índices tooimprove]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->

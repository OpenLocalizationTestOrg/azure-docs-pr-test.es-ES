---
title: "información general sobre el criterio de referencia de base de datos SQL aaaAzure"
description: "Este tema describe Hola prueba comparativa de base de datos de SQL Azure usa en la medición de rendimiento de Hola de base de datos de SQL Azure."
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Información general sobre la prueba comparativa Base de datos SQL de Azure
## <a name="overview"></a>Información general
La Base de datos SQL de Microsoft Azure ofrece tres [niveles de servicio](sql-database-service-tiers.md) con varios niveles de rendimiento. Cada nivel de rendimiento proporciona un rendimiento cada vez mayor de creciente conjunto de recursos o 'power', diseñado toodeliver.

Es importante toobe tooquantify capaz de cómo traduce la potencia creciente de Hola de cada nivel de rendimiento en el rendimiento de la base de datos mayor. toodo que Microsoft ha desarrollado hello Azure SQL Database Benchmark (ASDB). criterio de referencia de Hello ejerce una mezcla de operaciones básicas que se encuentra en todas las cargas de trabajo OLTP. Medimos el rendimiento de hello conseguido para bases de datos que se ejecuta en cada nivel de rendimiento.

Hello recursos y la potencia de cada nivel de rendimiento y de nivel de servicio se expresan en términos de [unidades de transacción de base de datos (Dtu)](sql-database-what-is-a-dtu.md). Las Dtu proporcionan un modo capacidad relativa de hello toodescribe de un nivel de rendimiento basándose en una medición mezclada de CPU, memoria y lee y escribe las tasas que ofrece cada nivel de rendimiento. Duplica la tasa de DTU de Hola de una base de datos equivale power de base de datos de toodoubling Hola. prueba comparativa de Hello nos permite tooassess impacto de hello en el rendimiento de la base de datos de menor a mayor potencia que ofrece cada nivel de rendimiento realizando operaciones de base de datos real, mientras se escala el tamaño de base de datos, el número de usuarios y velocidades de transacción en proporción de hello toohello base de datos de toohello de recursos proporcionados.

Al expresar el rendimiento de Hola Hola básica de nivel de servicio con transacciones por hora, nivel de servicio Standard Hola usando transacciones por minuto y el nivel de servicio Premium de hello mediante transacciones por segundo, hace que resulte más fácil tooquickly relacionar Hola potencial de rendimiento de cada requisitos de toohello de nivel de servicio de una aplicación.

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>Correlación de rendimiento de base de datos de prueba comparativa resultados tooreal world
Es importante toounderstand ese ASDB, al igual que todas las pruebas comparativas, solo es representativo e indicativo. Hola transacción tasas de conseguir con las aplicaciones de la prueba comparativa de hello no se Hola igual a los que se pueden lograr con otras aplicaciones. prueba comparativa de Hello consta de una colección de diferentes tipos de transacción ejecutados en un esquema que contiene una variedad de tablas y tipos de datos. Mientras los ejercicios de la prueba comparativa de Hola Hola mismas operaciones básicas que son comunes tooall cargas de trabajo OLTP, no representa ninguna clase específica de la base de datos o aplicación. objetivo de Hello de la prueba comparativa de hello es tooprovide un rendimiento relativo de toohello de orientación razonable de una base de datos que se puede esperar cuando se escala hacia arriba o hacia abajo entre los niveles de rendimiento. En realidad, las bases de datos son de distintos tamaños y complejidad, tienen distintas combinaciones de cargas de trabajo y responden de maneras diferentes. Por ejemplo, una aplicación que haga un uso intensivo de ES podría alcanzar antes el umbral de ES, o una que haga un uso intensivo de la CPU podría alcanzar antes los límites de CPU. No hay ninguna garantía de que cualquier base de datos concreta se escale de hello que igual manera como prueba comparativa de hello en aumento de carga.

Hello prueba comparativa y su metodología se describen con más detalle a continuación.

## <a name="benchmark-summary"></a>Resumen de la prueba comparativa
El ASDB mide el rendimiento de Hola de una combinación de operaciones de base de datos básicas que ocurren con más frecuencia en cargas de trabajo (OLTP) de procesamiento de transacciones en línea. Aunque prueba comparativa de hello está diseñado con la informática en la cuenta en la nube, esquema de base de datos de hello, rellenado de datos y transacciones han sido diseñada toobe ampliamente representativo de los elementos básicos de hello suelen usados en las cargas de trabajo OLTP.

## <a name="schema"></a>Esquema
esquema de Hello es toohave diseñada suficiente toosupport una variedad y complejidad una amplia gama de operaciones. prueba comparativa de Hola se ejecuta en una base de datos compuesta por seis tablas. tablas de Hola se dividen en tres categorías: tamaño fijo, escala y de crecimiento. Existen dos tablas de tamaño fijo, tres tablas de escalado y una tabla de crecimiento. Las tablas de tamaño fijo tienen un número de filas constante. Tablas de escala presentan una cardinalidad proporcional toodatabase rendimiento, pero no cambia durante la prueba comparativa de Hola. Hola aumentando la tabla tiene un tamaño como tabla de escala en la carga inicial, pero, a continuación, cambia la cardinalidad de hello en curso de hello de la ejecución de prueba comparativa de hello tal y como se insertan o eliminan filas.

esquema Hello incluye una combinación de tipos de datos, que incluyen valores enteros, numéricos, de carácter y de fecha y hora. esquema de Hello incluye claves primarias y secundarias, pero no claves externas; es decir, hay ninguna restricción de integridad referencial entre tablas.

Un programa de generación de datos genera los datos de Hola de base de datos inicial de Hola. Los datos enteros y numéricos se generan con diversas estrategias. En algunos casos, los valores se distribuyen al azar a lo largo de un intervalo. En otros casos, un conjunto de valores es tooensure permutado aleatoriamente que se mantiene una distribución específica. Campos de texto se generan a partir de una lista ponderada de datos con aspecto real palabras tooproduce.

base de datos de Hola se dimensiona basándose en un "factor de escala". factor de escala de Hello (abreviado SF) determina la cardinalidad de Hola de hello escala y de crecimiento de las tablas. Tal y como se describe a continuación en Hola sección usuarios y velocidad, el tamaño de la base de datos de hello, el número de usuarios y el rendimiento máximo se escalan en proporción tooeach otros.

## <a name="transactions"></a>Transacciones
carga de trabajo de Hello consta de tipos de transacciones nueve, tal y como se muestra en la siguiente tabla se Hola. Cada transacción está diseñada toohighlight un conjunto determinado de características del sistema en el hardware de sistema y el motor de base de datos hello, con un alto contraste de Hola otras transacciones. Este enfoque resulta más fácil de impacto de hello tooassess de rendimiento de toooverall de diferentes componentes. Por ejemplo, la transacción de Hola "Lectura intensa" produce un número significativo de operaciones de lectura de disco.

| Tipo de transacción | Descripción |
| --- | --- |
| Lectura ligera |SELECT; en memoria; solo lectura |
| Lectura mediana |SELECT; principalmente en memoria; solo lectura |
| Lectura intensa |SELECT; principalmente no en memoria; solo lectura |
| Actualización ligera |UPDATE; en memoria; solo escritura |
| Actualización intensa |UPDATE; principalmente no en memoria; solo escritura |
| Inserción ligera |INSERT; en memoria; solo escritura |
| Inserción intensa |INSERT; principalmente no en memoria; solo escritura |
| Eliminar |DELETE; combinación de en memoria y no en memoria; solo lectura |
| CPU intensa |SELECT; en memoria; carga en CPU relativamente intensa; solo lectura |

## <a name="workload-mix"></a>Combinación de cargas de trabajo
Las transacciones se seleccionan aleatoriamente de una distribución ponderada con hello siguiente mezcla global. Hello mezcla global tiene una relación de lectura/escritura de aproximadamente 2:1.

| Tipo de transacción | % de combinación |
| --- | --- |
| Lectura ligera |35 |
| Lectura mediana |20 | |
| Lectura intensa |5 |
| Actualización ligera |20 | |
| Actualización intensa |3 |
| Inserción ligera |3 |
| Inserción intensa |2 |
| Eliminar |2 |
| CPU intensa |10 |

## <a name="users-and-pacing"></a>Usuarios y velocidad
carga de trabajo de prueba comparativa de Hola se controla desde una herramienta que envía transacciones a través de un conjunto de conexiones toosimulate Hola comportamiento de un número de usuarios simultáneos. Aunque todas las transacciones y las conexiones de hello son generadas a máquina, para simplificar nos referiremos conexiones toothese como "usuarios". Aunque cada usuario opera independientemente de los demás usuarios, todos los usuarios realizan Hola mismo ciclo de pasos que se muestra a continuación:

1. Establecer una conexión de base de datos.
2. Repetir hasta tooexit señalado:
   * Seleccionar una transacción aleatoriamente (a partir de una distribución ponderada).
   * Realizar transacciones de hello seleccionada y medir el tiempo de respuesta de Hola.
   * Esperar un retraso de velocidad.
3. Cierre la conexión de base de datos de Hola.
4. Salir.

Hola velocidad retraso (en el paso 2c) se selecciona aleatoriamente, pero con una distribución que tenga un promedio de 1,0 segundos. De este modo, cada usuario puede, en promedio, generar como máximo una transacción por segundo.

## <a name="scaling-rules"></a>Reglas de escalado
número de Hola de usuarios viene determinado por el tamaño de la base de datos de hello (en unidades de factor de escala). Hay un usuario por cada cinco unidades de factor de escala. Debido a Hola retraso del ritmo, un usuario puede generar como máximo una transacción por segundo, en promedio.

Por ejemplo, una base de datos que tenga un factor de escala 500 (SF=500) tendrá 100 usuarios y podrá alcanzar una velocidad máxima de 100 TPS. toodrive una mayor velocidad TPS requiere más usuarios y una base de datos mayor.

siguiente de la tabla de Hello muestra el número de Hola de usuarios sostenidos realmente para cada nivel de rendimiento y de nivel de servicio.

| Nivel de servicio (nivel de rendimiento) | Usuarios | Tamaño de base de datos |
| --- | --- | --- |
| Básica |5 |720 MB |
| Estándar (S0) |10 |1 GB |
| Estándar (S1) |20 | |2,1 GB |
| Estándar (S2) |50 |7,1 GB |
| Premium (P1) |100 |14 GB |
| Premium (P2) |200 |28 GB |
| Premium (P6/P3) |800 |114 GB |

## <a name="measurement-duration"></a>Duración de la medición
Una ejecución válida de la prueba comparativa precisa una duración de medición en estado fijo de al menos una hora.

## <a name="metrics"></a>Métricas
las métricas clave de Hello en la prueba comparativa de hello son rendimiento y tiempo de respuesta.

* El rendimiento es Hola de medición de rendimiento esencial en la prueba comparativa de Hola. El rendimiento se indica en transacciones por unidad de tiempo, contando todos los tipos de transacciones.
* El tiempo de respuesta es una medición de la previsibilidad del rendimiento. restricción del tiempo de respuesta de Hello varía según la clase de servicio, con las clases de servicio que tiene un requisito de tiempo de respuesta más riguroso, tal y como se muestra a continuación elevadas.

| Clase de servicio | Medición del rendimiento | Requisito del tiempo de respuesta |
| --- | --- | --- |
| Premium |Transacciones por segundo |Percentil 95 en 0,5 segundos |
| Standard |Transacciones por minuto |Percentil 90 en 1,0 segundo |
| Básica |Transacciones por hora |Percentil 80 en 2,0 segundos |

## <a name="conclusion"></a>Conclusión
Hola criterio de referencia de base de datos de SQL de Azure mide rendimiento relativo de Hola de dispuestos a lo largo del intervalo de Hola de niveles de servicio disponible y los niveles de rendimiento de base de datos SQL Azure. criterio de referencia de Hello ejerce una combinación de operaciones de base de datos básicas que ocurren con más frecuencia en cargas de trabajo (OLTP) de procesamiento de transacciones en línea. Mediante la medición de rendimiento real, prueba comparativa de hello proporciona una evaluación más significativa del impacto de hello en el rendimiento de cambiar el nivel de rendimiento de Hola que sería posible con solo enumerando los recursos de hello proporcionados por cada nivel, como la velocidad de CPU, tamaño de la memoria y e/s por segundo . Hola futuras, se continuará tooevolve Hola prueba comparativa toobroaden su ámbito y expanda datos Hola proporcionados.

## <a name="resources"></a>Recursos
[Introducción tooSQL base de datos](sql-database-technical-overview.md)

[Niveles de servicio y niveles de rendimiento](sql-database-service-tiers.md)

[Guía de rendimiento de Base de datos SQL de Azure para bases de datos únicas](sql-database-performance-guidance.md)

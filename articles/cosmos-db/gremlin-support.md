---
title: soporte de Cosmos DB Gremlin aaaAzure | Documentos de Microsoft
description: "Conocer Hola lenguaje Gremlin de TinkerPop de Apache, que las características y los pasos y está disponible en la base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Compatibilidad de Azure Cosmos DB con grafos Gremlin
Azure Cosmos DB admite el lenguaje de recorrido de grafos de [Apache Tinkerpop](http://tinkerpop.apache.org), [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), que es una API Graph para crear entidades de grafo y realizar operaciones de consulta de grafos. Puede usar hello Gremlin toocreate gráfico entidades language (vértices y bordes), modificar las propiedades de las entidades, realizar consultas y recorridos y eliminar entidades. 

Base de datos de Azure Cosmos pone preparada para la empresa características bases de datos de toograph. entre ellas, distribución global, escalado independiente del almacenamiento y la capacidad de proceso, latencias predecibles inferiores a 10 milisegundos, indexación automática y SLA del 99,99 %. Dado que base de datos de Azure Cosmos admite TinkerPop/Gremlin, puede migrar fácilmente aplicaciones escritas con otra base de datos de gráfico sin necesidad de cambios en el código toomake. Además, gracias a la compatibilidad con Gremlin, Azure Cosmos DB se integra perfectamente entornos de análisis habilitados para TinkerPop, tales como [Apache Spark GraphX](http://spark.apache.org/graphx/). 

En este artículo, se proporciona un tutorial rápido de Gremlin y enumerar las características de Gremlin hello y los pasos que se admiten en la vista previa de Hola de compatibilidad con la API de Graph.

## <a name="gremlin-by-example"></a>Gremlin con ejemplos
Vamos a usar un toounderstand de gráfico muestra cómo se pueden expresar consultas en Gremlin. Hello en la ilustración siguiente se muestra una aplicación empresarial que administra los datos sobre los usuarios, los intereses y los dispositivos en forma de Hola de un gráfico.  

![Base de datos de ejemplo que muestra personas, dispositivos e intereses](./media/gremlin-support/sample-graph.png) 

Este gráfico tiene Hola siguientes tipos de vértices (denominados "etiqueta" en Gremlin):

- Personas: gráfico de hello tiene tres personas, Round Robin, Thomas y Ben
- Intereses: Hola de acuerdo con su intereses, en este ejemplo, juegos de fútbol
- Dispositivos: los dispositivos de hello personas usan
- Sistemas operativos: sistemas operativos Hola destinados a dispositivos de Hola

Se representan las relaciones de hello entre estas entidades a través de hello después tipos/etiquetas de bordes:

- Conoce a: por ejemplo, "Thomas conoce a Robin"
- Interesado: intereses de hello toorepresent de personas de hello en nuestro gráfico, por ejemplo, "Ben está interesado en fútbol"
- RunsOS: Ejecuta el equipo portátil Hola del sistema operativo Windows
- Usos: toorepresent utiliza el dispositivo al que una persona. Por ejemplo, Robin usa un teléfono Motorola con número de serie 77.

Vamos a ejecutar algunas operaciones en este gráfico con hello [Gremlin consola](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console). También puede realizar estas operaciones mediante controladores de Gremlin de plataforma de Hola de su elección (Java, Node.js, Python o. NET).  Antes de adentrarnos en lo que se admite en la base de datos de Azure Cosmos, echemos un vistazo a unos tooget ejemplos familiarizado con la sintaxis de Hola.

Primero, echemos un vistazo a CRUD. Hello Gremlin instrucción siguiente inserta Hola vértices "Thomas" en el gráfico de hello:

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

A continuación, Hola sigue Gremlin instrucción inserta un borde "sabe" entre Thomas y Round Robin.

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

Hello consulta siguiente devuelve vértices de "persona" hello en orden descendente de sus nombres:
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

Donde brillan de gráficos es cuando necesite tooanswer preguntas como "qué sistemas operativos usan amigos de Thomas?". Puede ejecutar este tooget de recorrido Gremlin simple esa información en el gráfico de hello:

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
Ahora, veamos qué proporciona Azure Cosmos DB a los desarrolladores de Gremlin.

## <a name="gremlin-features"></a>Características de Gremlin
TinkerPop es una norma que abarca una amplia gama de tecnologías de grafos. Por lo tanto, tiene terminología estándar toodescribe qué características son proporcionadas por un proveedor de gráfico. Azure Cosmos DB proporciona una base de datos de grafos de escritura, persistente y de alta simultaneidad que se puede dividir entre varios servidores o clústeres. 

Hello siguiente tabla enumeran hello TinkerPop características implementadas por base de datos de Azure Cosmos: 

| Categoría | Implementación de Azure Cosmos DB |  Notas | 
| --- | --- | --- |
| Características de grafos | La versión preliminar proporciona persistencia y acceso simultáneo. Toosupport diseñada las transacciones | Pueden implementar los métodos de equipo mediante el conector de Spark Hola. |
| Características de variables | Admite valores Boolean, Integer, Byte, Double, Float, Integer, Long, String. | Admite tipos primitivos; es compatible con tipos complejos mediante el modelo de datos. |
| Características de vértices | Admite RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty.  | Permite crear, modificar y eliminar vértices. |
| Características de propiedades de vértices | StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Permite crear, modificar y eliminar propiedades de vértices. |
| Características de aristas | AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty | Permite crear, modificar y eliminar aristas. |
| Características de propiedades de aristas | Properties, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Permite crear, modificar y eliminar propiedades de aristas. |

## <a name="gremlin-wire-format-graphson"></a>Formato de alambre de Gremlin: GraphSON

Base de datos de Azure Cosmos usa hello [GraphSON formato](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) al devolver los resultados de las operaciones de Gremlin. GraphSON es el formato estándar de hello Gremlin para representar los vértices y bordes, propiedades (propiedades con varios valores y únicas) mediante JSON. 

Por ejemplo, hello fragmento de código siguiente muestra una representación de GraphSON de un vértice *devuelve toohello cliente* de base de datos de Azure Cosmos. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

propiedades de Hello utilizados por GraphSON para vértices son siguientes de hello:

| Propiedad | Descripción |
| --- | --- |
| id | Id. de Hola de vértice Hola. Debe ser único (en combinación con el valor de Hola de _partition si es aplicable) |
| label | etiqueta de Hello del vértice de Hola. Se trata de un tipo de entidad de hello toodescribe opcional y se utiliza. |
| type | Vértices toodistinguish usado desde documentos de gráfico no |
| propiedades | Contenedor de propiedades definidas por el usuario asociados a los vértices de Hola. Cada propiedad puede tener varios valores. |
| _partition (configurable) | clave de partición de Hello del vértice de Hola. Puede ser utilizado tooscale gráficos en servidores de toomultiple |
| outE | Contiene una lista de las aristas de un vértice. Almacenar información de proximidad de hello con vértices permite ejecutar rápidamente recorridos. Las aristas se agrupan en función de sus etiquetas. |

Y borde de hello contiene Hola después toohelp información con partes de tooother de navegación de gráfico de Hola.

| Propiedad | Descripción |
| --- | --- |
| id | Id. de Hello borde Hola. Debe ser único (en combinación con el valor de Hola de _partition si es aplicable) |
| label | etiqueta de Hello del borde de Hola. Esta propiedad es el tipo de relación de hello toodescribe opcional y se utiliza. |
| inV | Contiene una lista de vértices para una línea. Almacenar información de proximidad de hello con borde Hola permite ejecutar rápidamente recorridos. Los vértices se agrupan en función de sus etiquetas. |
| propiedades | Contenedor de propiedades definidas por el usuario asociada hello borde. Cada propiedad puede tener varios valores. |

Cada propiedad puede almacenar varios valores dentro de una matriz. 

| Propiedad | Descripción |
| --- | --- |
| value | valor de Hola de propiedad Hola

## <a name="gremlin-partitioning"></a>Particiones de Gremlin

En Azure Cosmos DB, los grafos se almacenan en contenedores que se pueden escalar independientemente en cuanto a almacenamiento y capacidad de proceso (expresada en solicitudes normalizadas por segundo). Cada contenedor debe definir una propiedad de clave de partición opcional, aunque recomendada, que determina el límite de una partición lógica para los datos relacionados. Cada vértice o arista debe tener una propiedad `id` que es única para las entidades dentro de ese valor de clave de partición. Hola detalles se tratan en [particiones en la base de datos de Azure Cosmos](partition-data.md).

Las operaciones de Gremlin funcionan perfectamente en los datos de grafos repartidos en varias particiones en Azure Cosmos DB. Sin embargo, es recomendable toochoose una clave de partición para los gráficos que se utiliza normalmente como un filtro en las consultas, tiene muchos valores distintos y frecuencia similar de obtener acceso a estos valores. 

## <a name="gremlin-steps"></a>Pasos de Gremlin
Ahora Echemos un vistazo a Hola pasos Gremlin compatibles con la base de datos de Azure Cosmos. Para una referencia completa de Gremlin, consulte la [referencia de TinkerPop](http://tinkerpop.apache.org/docs/current/reference).

| paso | Descripción | Documentación de TinkerPop 3.2. | Notas |
| --- | --- | --- | --- |
| `addE` | Agrega una arista entre dos vértices. | [Paso addE](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | Agrega un gráfico de toohello de vértices | [Paso addV](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest que todos los recorridos de hello devuelven un valor | [y un paso](http://tinkerpop.apache.org/docs/current/reference/#and-step). | |
| `as` | Un tooassign de modulador una salida de la variable toohello de un paso de paso | [paso as](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | Modulador de pasos que se usa con `group` y `order`. | [paso by](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | Devuelve el cruce seguro primera Hola que devuelve un resultado | [paso coalesce](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | Devuelve un valor constante. Se usa con `coalesce`.| [paso constant](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Devuelve el número de recorrido de Hola Hola | [paso count](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | Devuelve Hola valores con los duplicados de hello quitados | [paso dedup](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | Quita Hola valores (vértices/edge) | [paso drop](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | Actúa como una barrera que calcula el agregado de Hola de resultados| [paso fold](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | Grupos de Hola valores basados en etiquetas de hello especificadas| [paso group](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Usar propiedades de toofilter, vértices y bordes. Admite las variantes `hasLabel`, `hasId`, `hasNot` y `has`. | [paso has](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | Inserta valores en un flujo.| [paso inject](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Usar tooperform un filtro mediante una expresión booleana | [paso is](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | Usar toolimit un número de elementos en cruce seguro de Hola| [paso limit](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | Local contiene una sección de una subconsulta de recorrido, de forma similar tooa | [paso local](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | Usa la negación de hello tooproduce de un filtro | [paso not](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | Devuelve Hola resultado de hello especificado cruce seguro si produce un resultado else devuelve Hola elemento que realiza la llamada | [paso optional](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Garantiza al menos uno de los recorridos de hello devuelve un valor | [paso or](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | Muestra los resultados en hello especifican el criterio de ordenación | [paso order](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Devuelve Hola ruta de acceso completa de cruce seguro de Hola | [paso path](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | Propiedades de proyectos Hola como un mapa | [paso project](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Devuelve las propiedades de Hola Hola especifican las etiquetas | [paso properties](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | Filtros toohello especifica el intervalo de valores| [paso range](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Repeticiones Hola paso para hello un número especificado de veces. Se usa para crear bucles. | [paso repeat](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Utilizar resultados toosample de cruce seguro de Hola | [paso sample](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Utilizar resultados tooproject de cruce seguro de Hola |  [paso select](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Utilizada para los agregados antibloqueo de cruce seguro de Hola | [paso store](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | Agrega las rutas de acceso desde un vértice en un árbol. | [paso tree](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | Extrae un iterador como un paso.| [paso unfold](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | Combina los resultados de varios recorridos.| [paso union](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Incluye los pasos de hello necesarios para recorridos entre vértices y bordes `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, y `otherV` para | [pasos vertex](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Utilizar resultados toofilter de cruce seguro de Hola. Admite los operadores `eq`, `neq`, `lt`, `lte`, `gt`, `gte` y `between`  | [paso where](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

De forma predeterminada, el motor optimizado para escritura de Azure Cosmos DB admite la indexación automática de todas las propiedades dentro de vértices y aristas. Por lo tanto, las consultas con filtros de rango de las consultas, ordenación, o agregados en las propiedades se procesan del índice de Hola y servir de forma eficaz. Para más información sobre cómo funciona la indexación en Azure Cosmos DB, consulte nuestro artículo sobre la [indexación independiente del esquema](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).

## <a name="next-steps"></a>Pasos siguientes
* Empezar a compilar una aplicación de grafos [con nuestros SDK](create-graph-dotnet.md) 
* Más información sobre la [compatibilidad de Azure Cosmos DB con grafos](graph-introduction.md)

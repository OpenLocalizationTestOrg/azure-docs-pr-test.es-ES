---
title: consultas de aaaSQL para la API de documentos de base de datos de Azure Cosmos | Documentos de Microsoft
description: "Más información sobre la sintaxis SQL, los conceptos de base de datos y las consultas SQL para Azure Cosmos DB. Puede usar SQL como lenguaje de consulta JSON en Azure Cosmos DB."
keywords: consulta sql, consultas sql, sintaxis sql, lenguaje de consulta json, conceptos de base de datos y consultas sql, funciones de agregado
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>Consultas SQL para la API de DocumentDB de Azure Cosmos DB
Microsoft Azure Cosmos DB admite la consulta de documentos con SQL (lenguaje de consulta estructurado) como lenguaje de consulta de JSON. Cosmos DB realmente no tiene esquemas. En virtud de su compromiso toohello JSON modelo de datos directamente en el motor de base de datos de hello, proporciona la indexación automática de documentos JSON sin necesidad de esquema explícito o la creación de índices secundarios. 

Al diseñar el lenguaje de consulta de Hola para Cosmos DB, hemos tenido en cuenta dos objetivos:

* En lugar de crear un nuevo lenguaje de consulta JSON, deseamos toosupport SQL. SQL es uno de los lenguajes de consulta de hello más familiares y conocidos. SQL de Cosmos DB proporciona un modelo de programación formal para consultas enriquecidas en documentos JSON.
* Como JSON documento base de datos puede ejecutar JavaScript directamente en el motor de base de datos de hello, deseamos modelo de programación de JavaScript de toouse como base de hello para el lenguaje de consulta. Hola documentos API SQL se basa en el sistema de tipos de JavaScript, la evaluación de expresiones y la invocación de función. A su vez, esto proporciona un modelo de programación natural para proyecciones relacionales, navegación jerárquica por documentos JSON, autocombinaciones, consultas espaciales e invocación de funciones definidas por el usuario (UDF) escritas íntegramente en JavaScript, entre otras características. 

Creemos que estas capacidades son fricción de hello tooreducing clave entre la aplicación hello y base de datos de Hola y son cruciales para la productividad del desarrollador.

Se recomienda introducción, inspeccionando Hola después de vídeo, donde Aravind Ramachandran muestra las capacidades de creación de consultas de Cosmos DB y al visitar nuestro [Query Playground](http://www.documentdb.com/sql/demo), donde puede probar DB Cosmos y ejecutar consultas SQL en el conjunto de datos.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

A continuación, devolver toothis artículo, donde se comienza con un tutorial de consulta SQL que le guiará por algunos documentos sencillos de JSON y los comandos SQL.

## <a id="GettingStarted"></a>Introducción a los comandos SQL en Cosmos DB
toosee Cosmos base de datos SQL en trabajar, vamos a empezar con algunos documentos JSON simples y guiar algunas consultas sencillas con ella. Tenga en cuenta estos dos documentos JSON sobre dos familias. Con la base de datos de Cosmos, no necesitamos toocreate los esquemas o los índices secundarios explícitamente. Se simplemente necesita tooinsert Hola JSON documentos tooa colección DB Cosmos y posteriormente realiza una consulta. Aquí tenemos un simple del JSON documentos para hello familia Andersen, Hola principales, los elementos secundarios (y sus mascotas), dirección e información de registro. documento de Hello tiene cadenas, números, valores booleanos, matrices y las propiedades anidadas. 

**Documento**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

Aquí se muestra un segundo documento con una sutil diferencia: se usan `givenName` y `familyName` en lugar de `firstName` y `lastName`.

**Documento**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Ahora vamos a intentarlo algunas consultas contra este toounderstand datos algunos Hola los aspectos clave de SQL de la API de documentos. Por ejemplo, siguiente Hola consulta devuelve documentos de Hola que coincide con el campo de Id. de hello `AndersenFamily`. Puesto que es un `SELECT *`, resultado de hello de consulta de hello es documento JSON de hello completo:

**Consultar**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


Ahora considere la posibilidad de caso de Hola que necesitamos tooreformat Hola salida JSON en una forma diferente. Esta consulta proyectos JSON nuevo objeto con dos campos seleccionados, Name y City, cuando ciudad de la dirección hello tiene Hola mismo nombre como estado de Hola. En este caso, "NY, NY" coincide.

**Consultar**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**Resultados**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


consulta siguiente de Hello devuelve todos los nombres especificados de Hola de elementos secundarios de familia de hello cuyo identificador coincide con `WakefieldFamily` ordenadas por ciudad Hola de residencia.

**Consultar**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**Resultados**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


Nos gustaría toodraw atención tooa algunos aspectos importantes de hello Cosmos DB consultar lenguaje a través de ejemplos de Hola que hemos visto hasta ahora:  

* Como SQL de la API de DocumentDB funciona con valores JSON, trata entidades en forma de árbol en lugar de filas y columnas. Por lo tanto, el lenguaje de hello le permite hacer referencia toonodes del árbol de Hola en cualquier profundidad arbitraria, como `Node1.Node2.Node3…..Nodem`, similar toorelational SQL que hace referencia toohello dos referencia de una parte de `<table>.<column>`.   
* Hola estructurado funciona de lenguaje de consulta con los datos sin esquema. Por lo tanto, Hola tipo sistema necesidades toobe enlazados dinámicamente. Hello misma expresión puede producir distintos tipos en los distintos documentos. resultado de Hello de una consulta es un valor JSON válido, pero no se garantiza que toobe de un esquema fijo.  
* Cosmos DB solo admite documentos JSON estrictos. Esto significa expresiones y sistema de tipos de hello son toodeal restringida solo con los tipos JSON. Consulte toohello [especificación de JSON](http://www.json.org/) para obtener más detalles.  
* Una recopilación de Cosmos DB es un contenedor sin esquemas de documentos JSON. relaciones de Hello en entidades de datos dentro y entre documentos en una colección implícitamente se capturan de contención y no primary key y relaciones de clave externas. Se trata de un aspecto importante que vale la pena señalar a la luz de combinaciones de hello dentro de los documentos que se describe más adelante en este artículo.

## <a id="Indexing"></a> Indexación de Cosmos DB
Antes de entrar en hello sintaxis SQL de la API de documentos, merece la pena explorar Hola indización de diseño en la base de datos de Cosmos. 

Hola de índices de la base de datos sirve tooserve consultas en sus diversas formas y formas con el consumo de recursos mínimo (por ejemplo, CPU y de entrada/salida) al proporcionar un buen rendimiento y latencia baja. A menudo, elección de Hola de índice correcto de Hola para consultar una base de datos requiere mucho planeamiento y la experimentación. Este enfoque supone un desafío para las bases de datos sin esquema en los datos de hello tooa estricta del esquema no es conforme y evoluciona rápidamente. 

Por lo tanto, cuando se diseñó el subsistema de indización de base de datos de Cosmos hello, establecemos Hola siguientes objetivos:

* Indizar los documentos sin necesidad de esquema: Hola indización subsistema no requiere ninguna información de esquema ni realizar ninguna suposición acerca del esquema de documentos de Hola. 
* Compatibilidad con gran y eficaz consultas relacionales y jerárquicas: el índice Hola admite lenguaje de consulta de base de datos de Cosmos Hola eficazmente, incluida la compatibilidad para las proyecciones relacionales y jerárquicas.
* Compatibilidad con las consultas coherente en caso de un volumen sostenido de escrituras: escritura alto rendimiento las cargas de trabajo con consultas coherente, Hola índice se actualiza incrementalmente, eficaz y en línea en cara Hola de un volumen sostenido de escrituras. actualización de índice coherente de Hello es fundamental tooserve consultas de hello en el nivel de coherencia de hello en qué servicio de documento Hola Hola de configurada por el usuario.
* Compatibilidad con la arquitectura multiempresa: dado el modelo de basadas en reservas de hello para la regulación de recursos entre los inquilinos, se realizan las actualizaciones del índice dentro del presupuesto Hola de recursos del sistema (CPU, memoria y operaciones de entrada/salida por segundo) asignadas por la réplica. 
* Eficacia de almacenamiento: para obtener rentabilidad, almacenamiento sobrecarga de hello en el disco del índice de hello es limitada y de predicción. Esto es fundamental porque Cosmos DB permite Hola developer toomake basado en costos contrapartidas sobrecarga de índice en el rendimiento de las consultas toohello relación.  

Consulte toohello [ejemplos de base de datos de Azure Cosmos](https://github.com/Azure/azure-documentdb-net) en MSDN para ejemplos que muestran cómo tooconfigure Hola directiva de indexación de una colección. Supongamos ahora entraremos en detalles de Hola de hello sintaxis SQL de base de datos de Azure Cosmos.

## <a id="Basics"></a>Conceptos básicos de una consulta SQL de Azure Cosmos DB
Todas las consultas constan de una cláusula SELECT y cláusulas FROM y WHERE opcionales por estándares ANSI-SQL. Por lo general, para cada consulta, se enumera el origen de hello en la cláusula FROM de Hola. A continuación, Hola filtrar Hola de cláusula WHERE se aplica en hello origen tooretrieve un subconjunto de documentos JSON. Por último, se utiliza la cláusula SELECT Hola Hola tooproject solicitado valores JSON en hello seleccione lista.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>Cláusula FROM
Hola `FROM <from_specification>` cláusula es opcional, a menos que se filtra o proyecta más adelante en la consulta de hello origen Hola. Hola de esta cláusula sirve toospecify origen de datos de hello en qué Hola debe funcionar la consulta. Normalmente recolección completa de hello es origen hello, pero uno en su lugar, puede especificar un subconjunto del conjunto de Hola. 

Al igual que una consulta `SELECT * FROM Families` indica que la colección completa de las familias de hello es origen Hola sobre qué tooenumerate. Un identificador especial raíz puede ser usado toorepresent Hola colección en lugar de usar el nombre de la colección de Hola. Hello lista siguiente contiene reglas de Hola que se aplican por cada consulta.

* colección de Hello puede tener alias, como `SELECT f.id FROM Families AS f` o simplemente `SELECT f.id FROM Families f`. Aquí `f` es equivalente a hello `Families`. `AS`es un identificador de palabra clave opcional tooalias Hola.
* Una vez tiene un alias, no se puede enlazar el origen de Hola. Por ejemplo, `SELECT Families.id FROM Families f` es sintácticamente válida porque no se puede resolver el identificador de Hola "Familias" ya.
* Todas las propiedades que deben toobe al que hace referencia deben ser nombres completos. En ausencia de Hola de adherencia estricta del esquema, se trata de tooavoid ha aplicado los enlaces ambiguos. Por lo tanto, `SELECT id FROM Families f` es sintácticamente válida desde la propiedad de hello `id` no está enlazado.

### <a name="subdocuments"></a>Subdocumentos
origen de Hello también puede ser el subconjunto más pequeño de tooa reducida. Por ejemplo, tooenumerating sólo un subárbol en cada documento, subroot Hola se convertiría en origen hello, tal y como se muestra en el siguiente ejemplo de Hola:

**Consultar**

    SELECT * 
    FROM Families.children

**Resultados**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

Mientras Hola anteriormente en el ejemplo utiliza una matriz como origen de hello, un objeto también podría usarse como origen de hello, que es lo que se muestra en el siguiente ejemplo de Hola: cualquier valor JSON válido (no definido) que se pueden encontrar en el origen de Hola se considera para su inclusión en el resultado de hello de consulta de Hola. Si no dispone de algunas familias un `address.state` valor, se excluyen Hola del resultado de consulta.

**Consultar**

    SELECT * 
    FROM Families.address.state

**Resultados**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>Cláusula WHERE
Hola de cláusula WHERE (**`WHERE <filter_condition>`**) es opcional. Especifica Hola condiciones que deben satisfacer los documentos JSON de hello proporcionadas por el origen de hello en toobe orden incluido como parte del resultado de hello. Se debe evaluar cualquier documento JSON Hola especifica condiciones demasiado "true" toobe tienen en cuenta para el resultado de hello. Hola donde se utiliza la cláusula por nivel de índice de hello en orden toodetermine Hola absoluta subconjunto más pequeño de documentos de origen que pueden ser parte del resultado de hello. 

Hello consulta siguiente solicita los documentos que contienen una propiedad de nombre cuyo valor es `AndersenFamily`. Cualquier otro documento que no tiene una propiedad name, o donde no coincide con el valor de Hola `AndersenFamily` se excluye. 

**Consultar**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


ejemplo de Hola anterior mostró una consulta de igualdad simple. SQL de la API de DocumentDB también admite diversas expresiones escalares. Hola más utilizado son expresiones unarios y binarios. Las referencias de propiedad desde un objeto JSON origen hello también son expresiones válidas. 

Hola después de los operadores binarios es compatibles actualmente y puede utilizarse en consultas, como se muestra en hello en los ejemplos siguientes:  

<table>
<tr>
<td>Aritméticos</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>Bit a bit</td>    
<td>|, &, ^, <<, >>, >>> (desplazamiento a la derecha con relleno de ceros)</td>
</tr>
<tr>
<td>Lógicos</td>
<td>AND, OR, NOT</td>
</tr>
<tr>
<td>De comparación</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>Cadena</td>    
<td>|| (concatenar)</td>
</tr>
</table>  


Echemos un vistazo a algunas consultas usando operadores binarios.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


Hola operadores unarios +,-, ~ también son compatibles y no puede utilizarse dentro de consultas, como se muestra en el siguiente ejemplo de Hola:

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



Además toobinary y los operadores unarios, referencias de propiedad también se permiten. Por ejemplo, `SELECT * FROM Families f WHERE f.isRegistered` devuelve Hola documento JSON que contiene la propiedad de hello `isRegistered` donde el valor de la propiedad de hello es igual toohello JSON `true` valor. Cualquier otro valor (false, null, sin definir, `<number>`, `<string>`, `<object>`, `<array>`, etc.) lleva toohello documento de origen se excluye del resultado de hello. 

### <a name="equality-and-comparison-operators"></a>Operadores de igualdad y de comparación
Hello siguiente tabla muestra hello resultado de las comparaciones de igualdad en SQL de la API de documentos entre los dos tipos JSON.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>Op</strong>
         </td>
         <td valign="top">
            <strong>Undefined</strong>
         </td>
         <td valign="top">
            <strong>Null</strong>
         </td>
         <td valign="top">
            <strong>Booleano</strong>
         </td>
         <td valign="top">
            <strong>Número</strong>
         </td>
         <td valign="top">
            <strong>Cadena</strong>
         </td>
         <td valign="top">
            <strong>Objeto</strong>
         </td>
         <td valign="top">
            <strong>Matriz</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Undefined<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Null<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Booleano<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Número<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Cadena<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Objeto<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Matriz<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
      </tr>
   </tbody>
</table>

Para otros operadores de comparación como >, > =,! =, < y < =, hello se aplican las reglas siguientes:   

* La comparación entre los tipos da lugar a Undefined.
* La comparación entre dos objetos o dos matrices da lugar a Undefined.   

Si el resultado de hello de expresión escalar de hello en el filtro de hello es sin definir, documento correspondiente hello no se incluiría en el resultado de hello, ya que Undefined lógicamente no equipare demasiado "true".

### <a name="between-keyword"></a>Palabra clave BETWEEN
También puede utilizar consultas de tooexpress de hello BETWEEN palabra clave en intervalos de valores como en ANSI SQL. BETWEEN puede utilizarse con cadenas o números.

Por ejemplo, esta consulta devuelve todos los documentos familias en qué Hola grado del primer nodo secundario está entre 1-5 (ambos inclusive). 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

A diferencia de en ANSI-SQL, se puede utilizar también Hola BETWEEN cláusula en la cláusula FROM de hello como en el siguiente ejemplo de Hola.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

Para los tiempos de ejecución de consulta más rápidos, recuerde toocreate una directiva de indexación que usa un tipo de índice de intervalo con las propiedades/rutas numéricas que se filtran en la cláusula de hello BETWEEN. 

Hola principal diferencia entre utilizar BETWEEN en API de documentos y ANSI SQL es que se pueden expresar consultas por rango en Propiedades de tipos mixtos, por ejemplo, podría tener que "grado" ser un número (5) en algunos documentos y cadenas en otros ("grade4"). En estos casos, al igual que en JavaScript, una comparación entre dos resultados de diferentes tipos en "undefined" y documento de Hola se omitirán.

### <a name="logical-and-or-and-not-operators"></a>Operadores lógicos (Y, O y NO)
Los operadores lógicos operan en valores booleanos. Hola tablas lógicas de verdad para estos operadores se muestran en hello las tablas siguientes.

| OR | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |True |True |
| False |True |False |Undefined |
| Undefined |True |Undefined |Undefined |

| Y | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |False |Undefined |
| False |False |False |False |
| Undefined |Undefined |False |Undefined |

| NO |  |
| --- | --- |
| True |False |
| False |True |
| Undefined |Undefined |

### <a name="in-keyword"></a>Palabra clave IN
palabra clave IN de Hello puede ser usado toocheck si un valor especificado coincide con algún valor en una lista. Por ejemplo, esta consulta devuelve todos los documentos familias donde Id. de hello es uno de "WakefieldFamily" o "AndersenFamily". 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

Este ejemplo devuelve todos los documentos donde el estado de hello es uno de hello especificado valores.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>Operadores ternario (?) y de fusión (??)
operadores de ternario y Coalesce de Hello pueden ser expresiones condicionales toobuild usado, toopopular similar programación lenguajes como C# y JavaScript. 

operador ternario (?) de Hello puede ser muy útil cuando la creación de nuevas propiedades JSON en hello volar. Por ejemplo, ahora puede escribir niveles de clase de consultas tooclassify hello en un formato legible humano como principiante/intermedio/Advanced tal y como se muestra a continuación.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

También puede anidar Hola llamadas toohello (operador) como en la siguiente consulta de Hola.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

Como con otros operadores de consulta, si hello que se hace referencia en una expresión condicional Hola faltan propiedades en cualquier documento, si los tipos de Hola que se comparan son diferentes, a continuación, esos documentos se excluyen o en resultados de la consulta de Hola.

Hello Coalesce (?) puede ser usa tooefficiently comprobación presencia de Hola de una propiedad (conocido como) (es decir, si esta se ha definido) en un documento. Esto es útil cuando se consultan datos semiestructurados o de tipos combinados. Por ejemplo, esta consulta devuelve Hola "Apellidos" Si está presente, o hello "apellido" Si no están presente.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>Descriptor de acceso de propiedad entre comillas
También puede tener acceso a propiedades mediante el operador de la propiedad indicada de hello `[]`. Por ejemplo, `SELECT c.grade` and `SELECT c["grade"]` son equivalentes. Esta sintaxis es útil cuando necesita tooescape una propiedad que contiene espacios, caracteres especiales, u ocurre hello tooshare mismo nombre como una palabra clave SQL o una palabra reservada.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>Cláusula SELECT
cláusula SELECT Hello (**`SELECT <select_list>`**) es obligatorio y especifica qué valores se recuperan de la consulta de hello, igual que en ANSI SQL. subconjunto de Hola que se han filtrado encima de los documentos de origen de Hola se pasan en la fase de proyección de hello, donde hello especificada se recuperan valores JSON y se construye un nuevo objeto JSON, para cada entrada que se pasó en él. 

Hola de ejemplo siguiente muestra una consulta SELECT normal. 

**Consultar**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>Propiedades anidadas
En el siguiente ejemplo de Hola, nos estamos proyectar dos propiedades anidadas `f.address.state` y `f.address.city`.

**Consultar**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


Proyección también admite expresiones de JSON como se muestra en el siguiente ejemplo de Hola:

**Consultar**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


Echemos un vistazo a la función hello de `$1` aquí. Hola `SELECT` cláusula necesita toocreate un objeto JSON y puesto que se proporcionó ninguna clave, usamos los nombres de variable argumento implícito a partir de `$1`. Por ejemplo, esta consulta devuelve dos variables de argumentos implícitos, etiquetadas como `$1` and `$2`.

**Consultar**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>Establecimiento de alias
Ahora vamos a ampliar el ejemplo de Hola anteriormente con alias explícito de valores. TAL cual Hola palabra clave utilizada para el alias. Es opcional, como se muestra mientras que el valor de segundo Hola proyectar como `NameInfo`. 

En caso de que una consulta tiene dos propiedades con hello mismo nombre, alias deben ser toorename usa uno o ambos de Hola propiedades para que se elimina la ambigüedad en hello proyectada resultados.

**Consultar**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>Expresiones escalares
También hace referencia a tooproperty, también admite la cláusula SELECT Hola expresiones escalares como constantes, expresiones aritméticas, expresiones lógicas, etcetera. Por ejemplo, aquí hay una sencilla consulta "Hello World".

**Consultar**

    SELECT "Hello World"

**Resultados**

    [{
      "$1": "Hello World"
    }]


A continuación se muestra un ejemplo más complejo que usa una expresión escalar.

**Consultar**

    SELECT ((2 + 11 % 7)-2)/3    

**Resultados**

    [{
      "$1": 1.33333
    }]


En el siguiente ejemplo de Hola, resultado de hello de expresión escalar de hello es un valor booleano.

**Consultar**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**Resultados**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>Creación de objetos y matrices
Otra característica clave del lenguaje SQL de la API de DocumentDB es la creación de matrices u objetos. En el ejemplo anterior de hello, tenga en cuenta que hemos creado un nuevo objeto JSON. De forma similar, uno puede construir matrices de tal y como se muestra en hello en los ejemplos siguientes:

**Consultar**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**Resultados**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>Palabra clave VALUE
Hola **valor** (palabra clave) proporciona un valor de manera tooreturn JSON. Por ejemplo, las consultas de Hola se muestra a continuación devuelve Hola escalar `"Hello World"` en lugar de `{$1: "Hello World"}`.

**Consultar**

    SELECT VALUE "Hello World"

**Resultados**

    [
      "Hello World"
    ]


Hello consulta siguiente devuelve valor JSON de hello sin hello `"address"` etiqueta en los resultados de Hola.

**Consultar**

    SELECT VALUE f.address
    FROM Families f    

**Resultados**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

Hello en el ejemplo siguiente se amplía este tooshow cómo tooreturn valores primitivos de JSON (nivel de hello hoja del árbol JSON de hello). 

**Consultar**

    SELECT VALUE f.address.state
    FROM Families f    

**Resultados**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>Operador *
operador especial (*) Hello es documento de hello tooproject compatibles como-es. Cuando se utiliza, debe ser Hola proyecta solo campo. Aunque una consulta como `SELECT * FROM Families f` es válida, `SELECT VALUE * FROM Families f ` y `SELECT *, f.id FROM Families f ` no lo son.

**Consultar**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>Operador TOP
puede ser la palabra clave TOP de Hello usar toolimit Hola un número de valores de una consulta. Cuando se usa TOP junto con la cláusula ORDER BY hello, conjunto de resultados de hello es toohello limitado el primer número N de valores ordenados; en caso contrario, devuelve Hola primer N número de resultados en un orden indefinido. Como práctica recomendada, en una instrucción SELECT, utilice siempre una cláusula ORDER BY con la cláusula TOP Hola. Se trata de una única manera de hello toopredictably indicar qué filas están afectadas por la parte superior. 

**Consultar**

    SELECT TOP 1 * 
    FROM Families f 

**Resultados**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

TOP se puede usar con un valor constante (como se muestra anteriormente) o con un valor variable usando consultas con parámetros. Si desea obtener más información, consulte las consultas con parámetros que aparecen a continuación.

### <a id="Aggregates"></a>Funciones de agregado
También puede realizar agregaciones en hello `SELECT` cláusula. Las funciones de agregado realizan un cálculo en un conjunto de valores y devuelven un valor único. Por ejemplo, hello siguiente consulta devuelve Hola recuento de familias documentos dentro de la colección de Hola.

**Consultar**

    SELECT COUNT(1) 
    FROM Families f 

**Resultados**

    [{
        "$1": 2
    }]

También puede devolver valor escalar de Hola de hello agregado mediante el uso de hello `VALUE` palabra clave. Por ejemplo, hello siguiente consulta devuelve Hola recuento de valores como un único número:

**Consultar**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**Resultados**

    [ 2 ]

También puede realizar agregados en combinación con filtros. Por ejemplo, hello siguiente consulta devuelve Hola recuento de documentos con la dirección de hello en hello estado de Washington.

**Consultar**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**Resultados**

    [ 1 ]

Hello siguiente tabla muestra hello lista de funciones de agregado compatibles en la API de documentos. `SUM`y `AVG` se aplican a valores numéricos, mientras que `COUNT`, `MIN` y `MAX` se pueden aplicar a números, cadenas, y valores booleanos y NULL. 

| Uso | Descripción |
|-------|-------------|
| COUNT | Devuelve Hola número de elementos de la expresión de Hola. |
| SUM   | Devuelve Hola suma de todos los valores de hello en la expresión de Hola. |
| MÍN   | Devuelve Hola valor mínimo en expresión Hola. |
| MÁX   | Devuelve Hola valor máximo en expresión Hola. |
| MEDIA   | Devuelve Hola promedio de valores de hello en la expresión de Hola. |

También se pueden realizar agregados sobre resultados de Hola de una iteración de la matriz. Para más información, vea [Iteración de matriz en consultas](#Iteration).

> [!NOTE]
> Al usar hello Explorador de consulta del portal de Azure, tenga en cuenta que las consultas de agregación pueden devolver Hola resultados parcialmente agregados a través de una página de consulta. Hola SDK genera un único valor acumulado en todas las páginas. 
> 
> Orden en consultas de agregación de tooperform mediante código, se necesita .NET SDK 1.12.0, .NET Core SDK 1.1.0 o Java SDK 1.9.5 o superior.    
>

## <a id="OrderByClause"></a>Cláusula ORDER BY
Al igual que en ANSI SQL, puede incluir una cláusula Order By opcional al realizar la consulta. cláusula de Hello puede incluir en el que se deben recuperar los resultados de un pedido de Hola de toospecify de argumento ASC o DESC opcional.

Por ejemplo, aquí es una consulta que recupera familias en orden de nombre de ciudad residente Hola.

**Consultar**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**Resultados**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

Y aquí es una consulta que recupera familias en orden de fecha de creación, que se almacena como un número que representa Hola tiempo base, es decir, tiempo transcurrido desde el 1 de enero de 1970 en segundos.

**Consultar**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**Resultados**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>Conceptos avanzados de base de datos y consultas SQL

### <a id="Iteration"></a>Iteración
Se agregó una nueva construcción a través de hello **IN** palabra clave en la compatibilidad de documentos API SQL tooprovide para iterar por matrices JSON. origen de Hello FROM proporciona compatibilidad para la iteración. Puede empezar con el siguiente ejemplo de Hola:

**Consultar**

    SELECT * 
    FROM Families.children

**Resultados**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

Ahora Echemos un vistazo a otra consulta que realiza iteración en los elementos secundarios en la colección de Hola. Tenga en cuenta diferencia hello en la matriz de salida de hello. Este ejemplo divide `children` y reduce los resultados de hello en una sola matriz.  

**Consultar**

    SELECT * 
    FROM c IN Families.children

**Resultados**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

Esto puede resultar más toofilter usado en cada entrada de matriz de hello tal y como se muestra en el siguiente ejemplo de Hola individual:

**Consultar**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**Resultados**  

    [{
      "givenName": "Lisa"
    }]

También puede realizar la agregación sobre resultado de hello de iteración de la matriz. Por ejemplo, hello consulta siguiente cuenta Hola número de elementos secundarios entre todas las familias.

**Consultar**

    SELECT COUNT(child) 
    FROM child IN Families.children

**Resultados**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>Combinaciones
En una base de datos relacional, es importante Hola necesidad toojoin entre tablas. Su Hola lógico toodesigning corollary normalizado esquemas. Modelo de datos sin normalizar Hola de documentos de esquema se ocupa contrarias toothis, API de documentos. Esto es equivalente lógico de Hola de un "autocombinación".

sintaxis de Hola que admite el lenguaje de hello es la combinación de combinación < from_source2 > < from_source1 >... JOIN <from_sourceN>. Generalmente, esto devuelve un conjunto de **N** tuplas (tupla con **N** valores). Cada tupla tiene valores generados por sus respectivos conjuntos en iteración de todos los alias de colección. En otras palabras, se trata de un producto cruzado completo de conjuntos de hello participan en la combinación de Hola.

Hello en los ejemplos siguientes muestran cómo funciona la cláusula de combinación Hola. En el siguiente ejemplo de Hola, resultado de hello está vacía ya que hello producto cruzado de todos los documentos de origen y un conjunto vacío está vacío.

**Consultar**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**Resultados**  

    [{
    }]


En el siguiente ejemplo de Hola, combinación de hello es entre hello y raíz del documento hello `children` subroot. Es un producto cruzado entre dos objetos JSON. ausencia de Hola que los elementos secundarios es una matriz no es eficaz en hello combinación puesto que estamos trabajando con una única raíz que es la matriz de elementos secundarios de Hola. Por lo tanto, el resultado de hello contiene solo dos resultados, ya que el producto cruzado de todos los documentos con la matriz de Hola Hola produce exactamente un único documento.

**Consultar**

    SELECT f.id
    FROM Families f
    JOIN f.children

**Resultados**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


Hola de ejemplo siguiente muestra una combinación más convencional:

**Consultar**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**Resultados**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



Hello lo primero que toonote es ese hello `from_source` de hello **UNIR** cláusula es un iterador. Por lo tanto, el flujo de hello en este caso es como sigue:  

* Expanda cada elemento secundario **c** de matriz de Hola.
* Aplicar un producto cruzado con raíz Hola de documento de hello **f** con cada elemento secundario **c** que se acoplan en el primer paso de Hola.
* Por último, el objeto de raíz de Hola de proyecto **f** name (propiedad) independiente. 

primer documento de Hello (`AndersenFamily`) contiene un único elemento secundario, por lo que el conjunto de resultados de hello contiene sólo un único objeto toothis documento correspondiente. segundo documento de Hello (`WakefieldFamily`) contiene dos elementos secundarios. Por lo tanto, hello producto cruzado genera un objeto independiente para cada elemento secundario, lo que resulta en dos objetos, uno para cada documento de toothis secundarios correspondientes. raíz de Hello campos en ambos estos documentos son iguales, Hola como se esperaría en un producto cruzado.

Hola utilidad real de hello combinación es tooform tuplas desde el producto cruzado de hello en una forma que en caso contrario es difícil tooproject. Además, tal y como se ve en el siguiente ejemplo de Hola, puede filtrar en la combinación de Hola de una tupla Hola que permite el usuario eligió una condición satisface Hola tuplas general.

**Consultar**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**Resultados**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



Este ejemplo es una extensión natural del anterior ejemplo de Hola y realiza una combinación de tipo double. Por lo tanto, hello producto cruzado puede verse como Hola siguiente pseudocódigo:

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily` tiene un hijo que tiene una mascota. Por lo tanto, hello producto cruzado da como resultado una fila (1\*1\*1) de esta familia. La familia Wakefield tiene, sin embargo, dos hijos, pero solo uno, "Jesse", tiene mascotas. Pero Jesse tiene dos mascotas. Por lo tanto, hello producto cruzado genera 1\*1\*2 = 2 filas de esta familia.

En el siguiente ejemplo de Hola, hay un filtro adicional en `pet`. Esto excluye todas las tuplas de Hola donde hello mascota nombre no es "Instantáneas". Tenga en cuenta que estamos toobuild capaz de tuplas de matrices, filtrar por cualquiera de los elementos de Hola de tupla de hello y cualquier combinación de elementos de hello del proyecto. 

**Consultar**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**Resultados**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>Integración de JavaScript
Base de datos de Azure Cosmos proporciona un modelo de programación para ejecutar lógica de la aplicación de JavaScript que se basa directamente en las colecciones de hello en cuanto a los procedimientos almacenados y desencadenadores. Esto les proporciona:

* Operaciones de CRUD transaccionales de alto rendimiento de toodo de capacidad y consultas en documentos de una colección en virtud de la integración de JavaScript en tiempo de ejecución directamente en el motor de base de datos de Hola Hola. 
* Un modelo natural de flujo de control, ámbito variable, asignación e integración de primitivas de control de excepciones con transacciones de base de datos. Para obtener más detalles sobre la compatibilidad de base de datos de Azure Cosmos para la integración de JavaScript, por favor, consulte la documentación de programación del servidor de JavaScript de toohello.

### <a id="UserDefinedFunctions"></a>Funciones definidas por el usuario (UDF)
Junto con los tipos de hello ya definidos en este artículo, DocumentDB API SQL proporciona compatibilidad para las funciones definida por el usuario (UDF). En concreto, se admiten UDF escalares donde los desarrolladores de hello pueden pasar en cero o varios argumentos y devuelven un resultado único argumento. Cada uno de estos argumentos se comprueba para ver si se trata de valores JSON válidos.  

Hola sintaxis SQL de la API de documentos se extiende la lógica de la aplicación personalizada de toosupport uso de estas funciones definidas por el usuario. Las funciones definidas por el usuario pueden registrarse con la API de DocumentDB y, a continuación, se puede hacer referencia a ellas como parte de una consulta de SQL. De hecho, Hola UDF son exquisitely diseñado toobe invocado por las consultas. Como una opción toothis corollary, UDF no tiene el objeto de contexto de acceso toohello que Hola otras JavaScript tienen tipos (procedimientos almacenados y desencadenadores). Puesto que las consultas se ejecutan como de solo lectura, pueden ejecutarse en réplicas principales o secundarias. Por lo tanto, las UDF son toorun diseñado en las réplicas secundarias a diferencia de otros tipos de JavaScript.

A continuación se muestra un ejemplo de cómo se puede registrar una UDF en Hola DB Cosmos base de datos, en concreto en una colección de documentos.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

Hello en el ejemplo anterior se crea una UDF cuyo nombre es `REGEX_MATCH`. Acepta dos valores de cadena JSON `input` y `pattern` y comprueba si la primeras coincidencias de hello especifica el patrón de hello en segundo lugar Hola con función de JavaScript a String.Match.

Ahora podemos usar esta UDF en una consulta de una proyección. UDF se deben calificar con el prefijo entre mayúsculas y minúsculas de Hola "udf." cuando se las llama desde las consultas. 

> [!NOTE]
> Anterior too3/17/2015, Cosmos DB admite llamadas a UDF sin Hola "udf." al igual que SELECT REGEX_MATCH(). Este patrón de llamada está desusado.  
> 
> 

**Consultar**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**Resultados**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

Hola UDF también puede utilizarse dentro de un filtro como se muestra en el ejemplo de Hola siguiente, también está calificado con hello "udf." prefijo:

**Consultar**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**Resultados**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


Básicamente, las UDF son expresiones escalares válidas y pueden usarse en ambas proyecciones y filtros. 

tooexpand en potencia Hola de UDF, echemos un vistazo a otro ejemplo con una lógica condicional:

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


A continuación se muestra un ejemplo que ejercicios Hola UDF.

**Consultar**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**Resultados**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


Como hello showcase de ejemplos anteriores, las UDF integran potencia de Hola de lenguaje JavaScript con hello documentos API SQL tooprovide una interfaz programable enriquecida toodo procedimientos, condicional una lógica compleja con ayuda de Hola de integradas en tiempo de ejecución de JavaScript capacidades.

Documentos API SQL proporciona argumentos de hello toohello UDF para cada documento de origen de Hola Hola actual fase (cláusula WHERE o cláusula SELECT) de procesamiento Hola UDF. Hello resultado se incorpora Hola general canalización de ejecución sin problemas. Si propiedades hello tooby que se hace referencia Hola UDF parámetros no están disponibles en el valor JSON, Hola hello parámetro se considera como sin definir y, por tanto, Hola invocación UDF completamente se omite. De forma similar si el resultado de hello de hello UDF no está definido, no se incluye en el resultado de hello. 

En resumen, las UDF son lógica de negocios compleja de buenas herramientas toodo como parte de la consulta de Hola.

### <a name="operator-evaluation"></a>Evaluación de operadores
COSMOS DB, en virtud de Hola de ser una base de datos JSON dibuja parallels con operadores de JavaScript y su semántica de evaluación. Mientras la base de datos de Cosmos intenta toopreserve semántica de JavaScript en términos de soporte JSON, se desvía la evaluación de la operación de hello en algunos casos.

En SQL de la API de documentos, a diferencia de en SQL tradicional, tipos de Hola de valores a menudo no se conocen hasta que se recuperan valores de hello de base de datos. En orden tooefficiently ejecutar consultas, la mayoría de los operadores de Hola tienen estrictos requisitos de tipos. 

SQL de la API de DocumentDB no realiza conversiones implícitas a diferencia de JavaScript. Por ejemplo, una consulta como `SELECT * FROM Person p WHERE p.Age = 21` coincide con documentos que contienen una propiedad Age cuyo valor es 21. Cualquier otro documento cuya propiedad Age coincida con la cadena "21", u otras variaciones posiblemente infinitas, como "021", "21,0", "0021", "00021", etc. no producirán coincidencias. Se trata en cambio toohello JavaScript donde los valores de cadena de hello son toonumbers realiza una conversión implícita (en función de operador, por ejemplo: ==). Esta opción es fundamental para conseguir una coincidencia de índices eficaz en SQL de la API de DocumentDB. 

## <a name="parameterized-sql-queries"></a>Consultas SQL con parámetros
COSMOS DB admite consultas con parámetros expresados con hello familiarizado notación @. El uso de SQL con parámetros permite controlar y evitar de forma sólida la entrada por parte de los usuarios, impidiendo así la exposición accidental de datos a través de la inyección de código SQL. 

Por ejemplo, puede escribir una consulta que acepte los apellidos y el estado de la dirección como parámetros y, a continuación, ejecutarla para distintos valores de los parámetros mencionados en función de la entrada del usuario.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

Esta solicitud, a continuación, se puede enviar tooCosmos base de datos como una consulta con parámetros de JSON como se muestra a continuación.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

Hola argumento tooTOP puede establecerse utilizando consultas con parámetros como se muestra a continuación.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

Los valores de los parámetros pueden ser cualquier tipo de JSON válido (cadenas, números, booleanos, null o incluso matrices o JSON anidado). Además, como Cosmos DB no tiene ningún esquema, los parámetros no se validan respecto a ningún tipo.

## <a id="BuiltinFunctions"></a>Funciones integradas
Cosmos DB también admite un número de funciones integradas para operaciones comunes, que se pueden usar dentro de las consultas como funciones definidas por el usuario (UDF).

| Grupo de funciones          | Operaciones                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Funciones matemáticas  | ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN y TAN |
| Funciones de comprobación de tipos | IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE                                                           |
| Funciones de cadena        | CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING y UPPER       |
| Funciones de matriz         | ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH y ARRAY_SLICE                                                                                         |
| Funciones espaciales       | ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID y ST_ISVALIDDETAILED                                                                           | 

Si actualmente usa una función definida por el usuario (UDF) para el que ahora está disponible una función integrada, debe usar la función integrada correspondiente de hello tal y como se va toorun más rápida de toobe y mucho más eficaz. 

### <a name="mathematical-functions"></a>Funciones matemáticas
Hola funciones matemáticas cada realizan un cálculo, en función de los valores de entrada que se proporcionan como argumentos y devuelven un valor numérico. Esta es una tabla de las funciones matemáticas integradas admitidas.


| Uso | Descripción |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [ABS (num_expr)](#bk_abs) | Devuelve Hola valor absoluto (positivo) de hello especifica la expresión numérica. |
| [CEILING (num_expr)](#bk_ceiling) | Devuelve Hola valor entero más pequeño mayor o igual a, Hola expresión numérica especificada. |
| [FLOOR (num_expr)](#bk_floor) | Devuelve Hola mayor entero menor o igual toohello especifica la expresión numérica. |
| [EXP (num_expr)](#bk_exp) | Exponente de hello devuelve de hello especifica la expresión numérica. |
| [LOG (num_expr [,base])](#bk_log) | Devuelve el logaritmo de natural de Hola de hello especificados expresión numérica, o logaritmo hello mediante Hola especificados base |
| [LOG10 (num_expr)](#bk_log10) | Hola devuelve base 10 valores logarítmico de hello especifica la expresión numérica. |
| [ROUND (num_expr)](#bk_round) | Devuelve un valor numérico, redondeado toohello valor de entero más cercano. |
| [TRUNC (num_expr)](#bk_trunc) | Devuelve un valor numérico, el valor entero más cercano de toohello truncado. |
| [SQRT (num_expr)](#bk_sqrt) | Devuelve Hola cuadrado raíz de hello especificado expresión numérica. |
| [SQUARE (num_expr)](#bk_square) | Hola devuelve cuadrado de hello especifica la expresión numérica. |
| [POWER (num_expr, num_expr)](#bk_power) | Devuelve Hola power de hello especificado expresión numérica toohello valor especificado. |
| [SIGN (num_expr)](#bk_sign) | Expresión numérica especifica devuelve Hola inicio de sesión valor (-1, 0, 1) de Hola. |
| [ACOS (num_expr)](#bk_acos) | Ángulo de hello devuelve, en radianes, cuyo coseno es Hola expresión numérica especificada; También se denomina arco coseno. |
| [ASIN (num_expr)](#bk_asin) | Ángulo de hello devuelve, en radianes, cuyo seno es hello especifica expresión numérica. También se denomina arcoseno. |
| [ATAN (num_expr)](#bk_atan) | Ángulo de hello devuelve, en radianes, cuya tangente es hello especifica expresión numérica. También se denomina arcotangente. |
| [ATN2 (num_expr)](#bk_atn2) | Devuelve Hola ángulo, en radianes, entre el eje x positivo de Hola y rayo de Hola desde el punto de hello origen toohello (y, x), donde x e y son valores de hello de hello dos expresiones de tipo flotante especificado. |
| [COS (num_expr)](#bk_cos) | Devuelve Hola coseno trigonométrico Hola especifica el ángulo, en radianes, en hello expresión especificada. |
| [COT (num_expr)](#bk_cot) | Devuelve Hola cotangente trigonométrica Hola especifica el ángulo, en radianes, en hello especifica la expresión numérica. |
| [DEGREES (num_expr)](#bk_degrees) | Devuelve Hola ángulo correspondiente en grados para un ángulo especificado en radianes. |
| [PI ()](#bk_pi) | Devuelve Hola valor constante de PI. |
| [RADIANS (num_expr)](#bk_radians) | Devuelve radianes cuando se especifica una expresión numérica en grados. |
| [SIN (num_expr)](#bk_sin) | Devuelve Hola seno trigonométrico Hola especifica el ángulo, en radianes, en hello expresión especificada. |
| [TAN (num_expr)](#bk_tan) | Tangente de hello devuelve de expresión de entrada de hello, Hola la expresión especificada. |

Por ejemplo, ahora puede ejecutar las consultas como Hola siguiente:

**Consultar**

    SELECT VALUE ABS(-4)

**Resultados**

    [4]

Hola principal diferencia entre tooANSI de funciones en comparación de Cosmos DB SQL es que son toowork diseñado correctamente con los datos del esquema sin esquema y mixto. Por ejemplo, si tiene un documento donde falta la propiedad de tamaño de Hola o tiene un valor no numérico, como "desconocido", a continuación, documento hello es recién saltado por, en lugar de devolver un error.

### <a name="type-checking-functions"></a>Funciones de comprobación de tipos
funciones de comprobación de tipo Hello permiten a tipo de hello toocheck de una expresión dentro de las consultas SQL. Funciones de comprobación pueden ser de tipo usa el tipo de hello toodetermine de propiedades de los documentos en marcha de hello cuando se variable o desconocido. Esta es una tabla de las funciones de comprobación de tipos integradas admitidas.

<table>
<tr>
  <td><strong>Uso</strong></td>
  <td><strong>Descripción</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></td>
  <td>Devuelve un valor booleano que indica si el tipo de hello del valor de hello es una matriz.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></td>
  <td>Devuelve un valor booleano que indica si el tipo de hello del valor de hello es un valor booleano.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></td>
  <td>Devuelve un valor booleano que indica si el tipo de saludo del valor de hello es null.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></td>
  <td>Devuelve un valor booleano que indica si el tipo de hello del valor de hello es un número.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></td>
  <td>Devuelve un valor booleano que indica si el tipo de hello del valor de hello es un objeto JSON.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></td>
  <td>Devuelve un valor booleano que indica si el tipo de saludo del valor de hello es una cadena.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></td>
  <td>Devuelve un valor booleano que indica si la propiedad de Hola se ha asignado un valor.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></td>
  <td>Devuelve un valor booleano que indica si el tipo de saludo del valor de hello es una cadena, número, booleano o null.</td>
</tr>

</table>

Uso de estas funciones, ahora puede ejecutar las consultas como Hola siguiente:

**Consultar**

    SELECT VALUE IS_NUMBER(-4)

**Resultados**

    [true]

### <a name="string-functions"></a>Funciones de cadena
Hola siguientes funciones escalares realizan una operación sobre un valor de cadena de entrada y devuelven una cadena, valor numérico o booleano. A continuación se facilita una tabla de funciones de cadena integradas:

| Uso | Descripción |
| --- | --- |
| [LENGTH (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |Devuelve el número de caracteres de Hola Hola especifica la expresión de cadena |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |Devuelve una cadena que es el resultado de hello de concatenar dos o más valores de cadena. |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |Devuelve parte de una expresión de cadena. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |Devuelve un valor booleano que indica si primera expresión de cadena Hola termina con hello en segundo lugar |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |Devuelve un valor booleano que indica si primera expresión de cadena Hola termina con hello en segundo lugar |
| [CONTAINS (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |Devuelve un valor booleano que indica si primera expresión de cadena hello contiene hello en segundo lugar. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Devuelve Hola a partir de la posición de la primera aparición de hello de la segunda expresión de cadena Hola dentro de la primera expresión de cadena especificada de hello, o -1 si no se encuentra la cadena de Hola. |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |Devuelve Hola parte izquierda de una cadena con hello especificada número de caracteres. |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Hola devuelve parte derecha de una cadena con hello del número de caracteres especificado. |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |Devuelve una expresión de cadena después de quitar los espacios en blanco iniciales. |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |Devuelve una expresión de cadena después de truncar todos los espacios en blanco finales. |
| [LOWER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |Devuelve una expresión de cadena después de convertir toolowercase de datos de caracteres en mayúsculas. |
| [UPPER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |Devuelve una expresión de cadena después de convertir toouppercase de datos de carácter en minúscula. |
| [REPLACE (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |Reemplaza todas las apariciones de un valor de cadena especificado por otro valor de cadena. |
| [REPLICATE (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |Repite un valor de cadena un número especificado de veces. |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Devuelve Hola invirtiendo el orden de un valor de cadena. |

Uso de estas funciones, ahora puede ejecutar las consultas como Hola siguiente. Por ejemplo, puede devolver el nombre de familia de Hola en mayúsculas como se indica a continuación:

**Consultar**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**Resultados**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

O concatenar cadenas como en este ejemplo:

**Consultar**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**Resultados**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


Funciones de cadena también pueden utilizarse en Hola donde cláusula toofilter obtener los resultados, al igual que en el siguiente ejemplo de Hola:

**Consultar**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**Resultados**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>Funciones de matriz
Hola siguientes funciones escalares realiza una operación sobre un valor de entrada de matriz y devolución numérico, el valor booleano o de matriz. A continuación se facilita una tabla de funciones de matriz integradas:

| Uso | Descripción |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |Devuelve el número de elementos de Hola Hola especifica la expresión de matriz. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |Devuelve una matriz que es el resultado de hello de concatenar dos o más valores de la matriz. |
| [ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |Devuelve un valor booleano que indica si la matriz de hello contiene Hola valor especificado. Puede especificar si la coincidencia de hello es completa o parcial. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |Devuelve parte de una expresión de matriz. |

Funciones de matriz pueden ser matrices de toomanipulate usado en JSON. Por ejemplo, aquí es una consulta que devuelve todos los documentos donde uno de los elementos primarios de hello es "Robin Wakefield". 

**Consultar**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]

Puede especificar un fragmento parcial de elementos coincidentes en la matriz de Hola. Hello siguiente consulta busca todos los elementos primarios con hello `givenName` de `Robin`.

**Consultar**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]


Este es otro ejemplo que utiliza ARRAY_LENGTH tooget Hola número de hijos por familia.

**Consultar**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**Resultados**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>Funciones espaciales
COSMOS DB admite Hola siguiendo las funciones integradas de Open Geospatial Consortium (OGC) para realizar consultas geoespaciales. 

<table>
<tr>
  <td><strong>Uso</strong></td>
  <td><strong>Descripción</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr, point_expr)</td>
  <td>Devuelve la distancia de hello entre expresiones de punto de GeoJSON, polígono o LineString Hola dos.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Devuelve una expresión booleana que indica si es Hola primer GeoJSON objeto (punto, polígono o LineString) dentro de hello segundo GeoJSON objeto (punto, polígono o LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Devuelve una expresión booleana que indica si se intersecan Hola dos GeoJSON objetos especificados (punto, polígono o LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Devuelve un valor booleano que indica si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Devuelve un valor JSON que contiene un valor booleano si Hola especifica LineString, Polygon o punto de GeoJSON una expresión es válida y si no es válido, además Hola motivo como un valor de cadena.</td>
</tr>
</table>

Funciones espaciales pueden ser consultas de proximidad de tooperform utilizadas en los datos espaciales. Por ejemplo, aquí es una consulta que devuelve la que familia de todos los documentos que está dentro de 30 km de hello ubicación especificada mediante hello ST_DISTANCE función integrada. 

**Consultar**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]

Para más información sobre la compatibilidad geoespacial en Cosmos DB, consulte [Uso de datos geoespaciales en Azure Cosmos DB](geospatial.md), Que concluye funciones espaciales y Hola sintaxis SQL para la base de datos de Cosmos. Ahora Echemos un vistazo a cómo LINQ consultar funciona y cómo interactúa con la sintaxis de Hola que hemos visto hasta ahora.

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
LINQ es un modelo de programación de .NET que expresa cálculos como consultas de secuencias de objetos. COSMOS DB proporciona un toointerface de biblioteca de cliente con LINQ al facilitar una conversión entre los objetos JSON y .NET y una asignación entre un subconjunto de LINQ consulta tooCosmos DB consultas. 

Figura Hola siguiente muestra la arquitectura de Hola de admitir consultas LINQ usando la base de datos de Cosmos.  Con cliente de base de datos de Cosmos hello, los programadores pueden crear un **IQueryable** que directamente consultas Hola DB Cosmos consultar al proveedor, que luego convierte la consulta LINQ de hello en una consulta de base de datos de Cosmos del objeto. consulta de Hello, a continuación, se pasa toohello tooretrieve de servidor de base de datos de Cosmos un conjunto de resultados en formato JSON. Hola devuelve resultados son deserializados en un flujo de objetos de .NET en el lado del cliente de Hola.

![Arquitectura de consultas compatibles con LINQ que usa la API de DocumentDB: sintaxis SQL, lenguaje de consulta JSON, conceptos de base de datos y consultas SQL][1]

### <a name="net-and-json-mapping"></a>Asignación de .NET y JSON
asignación de Hello entre objetos .NET y documentos JSON es natural: se asigna a cada campo de miembro de datos tooa: objeto JSON, donde es el nombre del campo Hola asigna toohello "claves" parte del objeto de Hola y parte de "value" Hola se asignan de forma recursiva toohello parte de valor de objeto de Hola. Considere el siguiente ejemplo de Hola: objeto de familia de hello creado es documento JSON de toohello asignado tal y como se muestra a continuación. Y viceversa, documento JSON de hello es objeto de .NET de tooa de espera asignado.

**Clase de C#**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>Traducción de tooSQL LINQ
proveedor de consultas de base de datos de Cosmos Hola realiza una mejor asignación de esfuerzo de una consulta LINQ en una consulta SQL de la base de datos de Cosmos. Hola siguiendo la descripción, suponemos lector hello tiene un conocimiento básico de LINQ.

En primer lugar, para el sistema de tipos de hello, se admiten todos los tipos primitivos de JSON: tipos numéricos, boolean, string y null. Solo se admiten estos tipos JSON. Hola siguientes expresiones escalares es compatibles.

* Valores constantes: estos incluyen valores constantes de tipos de datos primitivos de hello en tiempo de Hola Hola consulta se evalúa.
* Expresiones de índice de propiedad/matriz: estas expresiones hacen referencia toohello propiedad de un objeto o un elemento de matriz.
  
     family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n es una variable int
* Expresiones aritméticas: entre estas se incluyen expresiones aritméticas comunes o valores numéricos y booleanos. Para la lista completa de hello, consulte Especificación de SQL toohello.
  
     2 * family.children[0].grade;    x + y;
* Expresión de comparación de cadena - puede tratarse comparar un valor de cadena de constante de cadena valor toosome.  
  
     mother.familyName == "Smith";    child.givenName == s; //s es una variable de cadena
* Expresión de creación de objetos o matrices: estas expresiones devuelven un objeto de tipo de valor compuesto o tipo anónimo o una matriz de estos objetos. Estos valores se pueden anidar.
  
     new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //un tipo anónimo con dos campos              
     new int[] { 3, child.grade, 5 };

### <a id="SupportedLinqOperators"></a>Lista de los operadores LINQ admitidos
Esta es una lista de los operadores LINQ compatibles en proveedor LINQ de hello incluido con hello documentos .NET SDK.

* **Seleccione**: proyecciones traducen toohello SQL SELECT incluida la construcción de objetos
* **Donde**: filtros traducir toohello WHERE de SQL y admite la traducción entre & &, || y! operadores SQL toohello
* **SelectMany**: permite el desenredo de la cláusula JOIN de SQL de matrices toohello. Puede ser usado toochain/anidar expresiones toofilter en elementos de matriz
* **OrderBy y OrderByDescending**: traduce tooORDER BY ascendente o descendente
* Los operadores **Count**, **Sum**, **Min**, **Max** y **Average** para la agregación y sus equivalentes asincrónicos **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** y **AverageAsync**.
* **CompareTo**: traduce toorange comparaciones. Se usa frecuentemente para las cadenas, debido a que no son comparables en .NET.
* **Tomar**: traduce toohello TOP de SQL para limitar los resultados de una consulta
* **Funciones matemáticas**: admite la traducción de. Abs, Acos, Asin de NET, Atan, Ceiling, Cos, Exp, Floor, registro, Log10, Pow, Round, inicio de sesión, Sin, Sqrt, Tan, truncar funciones integradas de toohello equivalente de SQL.
* **Funciones de cadena**: admite la traducción de. Concat, Contains, EndsWith de NET, IndexOf, recuento, ToLower, TrimStart, Replace, inversa, TrimEnd, StartsWith, SubString, ToUpper toohello equivalente funciones integradas de SQL.
* **Funciones de matriz**: admite la traducción de. Concat, Contains y recuento toohello equivalente SQL funciones integradas de NET.
* **Funciones de extensión geoespaciales**: admite la traducción de los métodos de código auxiliar distancia, en IsValid y IsValidDetailed toohello equivalente funciones integradas de SQL.
* **Extensión de la función definida por el usuario**: traducción admite de hello UserDefinedFunctionProvider.Invoke toohello correspondiente definido por el usuario función del método de código auxiliar.
* **Varios**: admite la traducción de hello coalesce y operadores condicionales. Puede traducir Contains tooString CONTAINS, ARRAY_CONTAINS o hello IN de SQL según el contexto.

### <a name="sql-query-operators"></a>Operadores de consulta SQL
Estos son algunos ejemplos que ilustran cómo algunos operadores de consulta LINQ estándar Hola se traducen las consultas de base de datos de tooCosmos.

#### <a name="select-operator"></a>Operador Select
sintaxis de Hello es `input.Select(x => f(x))`, donde `f` es una expresión escalar.

**Expresión lambda de LINQ**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**Expresión lambda de LINQ**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**Expresión lambda de LINQ**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>Operador SelectMany
sintaxis de Hello es `input.SelectMany(x => f(x))`, donde `f` es una expresión escalar que devuelve un tipo de colección.

**Expresión lambda de LINQ**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Operador Where
sintaxis de Hello es `input.Where(x => f(x))`, donde `f` es una expresión escalar, que devuelve un valor booleano.

**Expresión lambda de LINQ**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**Expresión lambda de LINQ**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>Composición de consultas SQL
Hola por encima de los operadores puede ser compuesto tooform consultas más eficaces. Puesto que la base de datos de Cosmos admite colecciones anidadas, composición Hola puede concatenar o anidado.

#### <a name="concatenation"></a>Concatenación
sintaxis de Hello es `input(.|.SelectMany())(.Select()|.Where())*`. Una consulta concatenada puede empezar por una consulta `SelectMany` opcional seguida de varios operadores `Select` o `Where`.

**Expresión lambda de LINQ**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**Expresión lambda de LINQ**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**Expresión lambda de LINQ**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**Expresión lambda de LINQ**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>Anidamiento
sintaxis de Hello es `input.SelectMany(x=>x.Q())` donde Q es un `Select`, `SelectMany`, o `Where` operador.

En una consulta anidada, consulta interna de hello es aplicado tooeach elemento de colección exterior Hola. Una característica importante es que esa consulta interna Hola puede hacer referencia toohello campos de elementos de Hola de colección exterior de hello como autocombinaciones.

**Expresión lambda de LINQ**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**Expresión lambda de LINQ**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**Expresión lambda de LINQ**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>Ejecución de consultas SQL
Cosmos DB expone recursos mediante la API de REST, que puede invocar cualquier lenguaje capaz de realizar solicitudes de HTTP/HTTPS. Además, Cosmos DB ofrece bibliotecas de programación para varios lenguajes populares como .NET, Node.js, JavaScript y Python. API de REST de Hola y Hola todas las distintas bibliotecas admiten consultas a través de SQL. Hola .NET SDK es compatible con LINQ asimismo consultar tooSQL.

Hola siguientes ejemplos se muestra cómo toocreate una consulta y enviarlo en una cuenta de base de datos de la base de datos de Cosmos.

### <a id="RestAPI"></a>API DE REST
Cosmos DB ofrece un modelo de programación RESTful sobre HTTP. Las cuentas de la base de datos pueden aprovisionarse usando una suscripción de Azure. modelo de recursos de base de datos de Cosmos Hola consta de un conjunto de recursos en una cuenta de base de datos, cada uno de los cuales es direccionable mediante un URI lógico y estable. Un conjunto de recursos es tooas que se hace referencia una fuente de distribución en este documento. Una cuenta de la base de datos consta de un conjunto de bases de datos, cada una incluyendo varias recopilaciones que, a su vez, contienen documentos, UDF y otros tipos de recursos.

modelo de interacción básica Hello con estos recursos es a través de verbos de hello HTTP GET, PUT, POST y DELETE con su interpretación estándar. verbo POST de Hola se utiliza para la creación de un nuevo recurso, para ejecutar un procedimiento almacenado o para emitir una consulta de base de datos de Cosmos. Las consultas siempre son operaciones de solo lectura sin efectos secundarios.

Hello en los ejemplos siguientes muestran una entrada para una consulta de DocumentDB API realizada en una colección que contiene dos documentos de ejemplo Hola que hemos visto hasta ahora. consulta de Hello tiene un filtro simple en la propiedad de nombre de hello JSON. Tenga en cuenta use Hola de hello `x-ms-documentdb-isquery` y Content-Type: `application/query+json` toodenote encabezados que Hola operación es una consulta.

**Solicitud**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**Resultados**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


Hola segundo ejemplo muestra una consulta más compleja que devuelve varios resultados de la combinación de Hola.

**Solicitud**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**Resultados**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


Si los resultados de una consulta no caben dentro de una sola página de resultados, Hola REST API devuelve un token de continuación a través de hello `x-ms-continuation-token` encabezado de respuesta. Los clientes pueden paginar resultados mediante la inclusión de encabezado de hello en los resultados siguientes. número de Hola de resultados por página también puede controlarse mediante hello `x-ms-max-item-count` encabezado de número. Si la consulta especificada de hello tiene una función de agregación como `COUNT`, a continuación, la página de consulta de hello puede devolver un valor parcial agregado a través de la página de Hola de resultados. los clientes de Hello debe realizar una agregación de segundo nivel a través de estos resultados tooproduce Hola resultados finales, por ejemplo, sumar los recuentos de hello devueltos en el recuento total de hello páginas individuales tooreturn Hola.

Directiva de coherencia de datos toomanage Hola para las consultas, use hello `x-ms-consistency-level` encabezado al igual que todas las solicitudes de API de REST. Para mantener la coherencia sesión, es necesario tooalso Hola de eco más reciente `x-ms-session-token` encabezado de Cookie de solicitud de consulta de Hola. Hello directiva de indexación consultado la colección también puede influir coherencia Hola de resultados de la consulta. No tiene valor predeterminado de hello indización de configuración de directiva, para las colecciones Hola índice siempre está actual con el contenido del documento de Hola y consulta los resultados coincidan con coherencia de hello elegido para los datos. Si hello directiva de indexación es tooLazy flexible, las consultas pueden devolver resultados obsoletos. Para más información, vea [Niveles de coherencia en Azure Cosmos DB][consistency-levels].

Si la directiva de indexación de hello configurado en la colección de hello no es compatible con la consulta especificada de hello, servidor de base de datos de Azure Cosmos Hola devuelve 400 "solicitud incorrecta". Esto se devuelve para las consultas por rango en rutas de acceso configuradas para búsquedas hash (igualdad) y rutas de acceso excluidas de forma explícita de los índices. Hola `x-ms-documentdb-query-enable-scan` encabezado puede ser especificado tooallow Hola consulta tooperform un examen cuando un índice no está disponible.

Puede obtener métricas detalladas en ejecución de la consulta estableciendo `x-ms-documentdb-populatequerymetrics` encabezado demasiado`True`. Para más información, vea, [Métricas de consulta de SQL para la API de DocumentDB de Azure Cosmos DB](documentdb-sql-query-metrics.md).

### <a id="DotNetSdk"></a>SDK de C# (.NET)
Hola .NET SDK es compatible con LINQ y SQL consultar. Hello en el ejemplo siguiente se muestra la consulta de filtro simple hello tooperform introdujo anteriormente en este documento.

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


En este ejemplo se comparan dos propiedades para igualdad en cada documento y se usan proyecciones anónimas. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Hola siguiente muestra las combinaciones, expresadas a través de LINQ SelectMany.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



cliente de .NET de Hello automáticamente recorre en iteración todas las páginas de Hola de resultados de la consulta en los bloques de foreach hello como se indicó anteriormente. consulta Hola opciones que se presentan en la sección de la API de REST de hello también están disponibles en Hola SDK de .NET con hello `FeedOptions` y `FeedResponse` las clases de hello CreateDocumentQuery método. número de Hola de páginas puede controlarse mediante hello `MaxItemCount` configuración. 

Puede controlar explícitamente la paginación mediante la creación de `IDocumentQueryable` con hello `IQueryable` objeto, a continuación, al leer la` ResponseContinuationToken` valores y pasándolos nuevo como `RequestContinuationToken` en `FeedOptions`. `EnableScanInQuery`puede ser el conjunto tooenable exámenes cuando no se admite la consulta Hola por directiva de indexación de hello configurado. Para las colecciones particionadas, puede usar `PartitionKey` toorun consulta de hello en una sola partición (aunque Cosmos DB puede extraer automáticamente esto de texto de la consulta de hello), y `EnableCrossPartitionQuery` ejecutan consultas de toorun que necesitan toobe en varias particiones. 

Consulte demasiado[ejemplos de .NET de base de datos de Azure Cosmos](https://github.com/Azure/azure-documentdb-net) para ver más ejemplos que contienen consultas. 

### <a id="JavaScriptServerSideApi"></a>API del servidor de JavaScript
COSMOS DB proporciona un modelo de programación para ejecutar lógica de la aplicación de JavaScript que se basa directamente en las colecciones de hello mediante procedimientos almacenados y desencadenadores. lógica de JavaScript de Hello registrado en el nivel de colección, a continuación, puede emitir las operaciones de base de datos en operaciones de hello en documentos de Hola de hello dado de la colección. Estas operaciones se incluyen en transacciones ACID ambientales.

Hello en el ejemplo siguiente se muestra cómo las consultas toouse hello queryDocuments en toomake Hola API de servidor de JavaScript desde dentro de procedimientos almacenados y desencadenadores.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>Referencias
1. [Introducción tooAzure Cosmos DB][introduction]
2. [Especificación de SQL de Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Ejemplos de .NET de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net)
4. [Niveles de coherencia de Azure Cosmos DB][consistency-levels]
5. SQL ANSI 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. Especificación de JavaScript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. Técnicas de evaluación de consultas para bases de datos de gran tamaño [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994
11. Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.
12. Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.
13. G. Graefe. marco de cascadas de Hola para optimizar la consulta. IEEE Data Eng. Bull., 18(3): 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md
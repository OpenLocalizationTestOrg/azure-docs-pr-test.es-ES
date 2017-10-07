---
title: "directivas de indización de base de datos de Cosmos aaaAzure | Documentos de Microsoft"
description: "Comprenda cómo funciona la indexación en Azure Cosmos DB. Obtenga información acerca de cómo tooconfigure y cambio Hola directiva de indexación de la indexación automática y un mayor rendimiento."
keywords: "funcionamiento de la indexación, indexación automática, indexación de base de datos"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>¿Cómo funcionan los datos del índice de Azure Cosmos DB?

De forma predeterminada, todos los datos de Azure Cosmos DB se indexan. Y mientras que muchos clientes están satisfechos toolet base de datos de Azure Cosmos controlan automáticamente todos los aspectos de la indización, base de datos de Azure Cosmos también permite especificar un personalizado **directiva de indexación** para las colecciones durante la creación. Directivas de indización de base de datos de Azure Cosmos son más flexibles y eficaces que los índices secundarios que se ofrecen en otras plataformas de base de datos, ya que permiten diseñar y personalizar la forma de hello del índice de hello sin sacrificar la flexibilidad del esquema. toolearn indización funcionamiento en la base de datos de Cosmos de Azure, debe entender que administrar la directiva de indización, puede realizar específica equilibrio entre la sobrecarga de almacenamiento del índice, escritura y rendimiento de la consulta y coherencia de la consulta.  

En este artículo, examinaremos un cierre base de datos de Azure Cosmos directivas de indexación, cómo puede personalizar la directiva de indexación y Hola asociado ventajas e inconvenientes. 

Después de leer este artículo, podrá hello tooanswer pueda siguientes preguntas:

* ¿Cómo puedo invalidar Hola propiedades tooinclude o excluir de la indización?
* ¿Cómo puedo configurar índice Hola eventual actualizaciones?
* ¿Cómo puedo configurar indización tooperform Order By o intervalo de consultas?
* ¿Cómo creo directiva de indexación del conjunto de cambios tooa?
* ¿Cómo se puede comparar el almacenamiento y el rendimiento de diferentes directivas de indexación?

## <a id="CustomizingIndexingPolicy"></a>Personalizar la directiva de indexación de Hola de una colección
Los desarrolladores pueden personalizar Hola ventajas y desventajas de almacenamiento, el rendimiento de escritura/consulta y la coherencia de la consulta, reemplazando directiva de indexación predeterminada hello en una colección de base de datos de Azure Cosmos y configurar Hola siguientes aspectos.

* **Inclusión y exclusión de documentos y rutas de acceso del índice y al índice**. Los desarrolladores pueden elegir determinado toobe documentos incluyen o excluyen de índice de hello en tiempo de Hola de insertar o reemplazarlos toohello colección. Los desarrolladores también pueden elegir tooinclude o excluir algunas propiedades JSON conocido como las rutas de acceso (incluidos los patrones de caracteres comodín) toobe indizar en documentos que se incluyen en un índice.
* **Configuración de distintos tipos de índice**. Para cada una de las rutas de acceso de hello incluida, los desarrolladores también pueden especificar el tipo de Hola de índice que requieren a través de una colección basada en sus datos y la carga de trabajo de consulta esperado y Hola numérico o cadena "precisión" para cada ruta de acceso.
* **Configuración de modos de actualización del índice**. Base de datos de Azure Cosmos admite tres modos de indización que se pueden configurar a través de la directiva en una colección de base de datos de Azure Cosmos de indización de Hola: coherente, Lazy y ninguno. 

Hola .NET código fragmento siguiente muestra cómo tooset una directiva de indexación personalizada durante la creación de hello de una colección. Aquí se establecer Directiva de hello con índice de intervalo para las cadenas y números en la precisión máxima de Hola. Esta directiva nos permite ejecutar consultas Order By en cadenas.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> esquema JSON de Hello para la directiva de indexación se cambió con la versión de Hola de versión de API de REST índices de intervalo toosupport 2015-06-03 de cadenas. SDK de .NET 1.2.0 y Java, Python y Node.js SDK 1.1.0 admiten el esquema de directiva nueva de Hola. SDK anterior usa API de REST versión 2015-04-08 hello y admite el esquema anterior de Hola de directiva de indización.
> 
> De forma predeterminada, Azure Cosmos DB indexa todas las propiedades de cadena en los documentos de forma coherente con un índice Hash y las propiedades numéricas con un índice de intervalo.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Personalizar la directiva de indexación de hello mediante el portal de Hola

Puede cambiar Hola directiva de una colección mediante el portal de Azure Hola de indización. Abra su cuenta de base de datos de Azure Cosmos Hola portal de Azure, seleccione la colección, en haga clic en el menú de navegación izquierdo hello **configuración**y, a continuación, haga clic en **directiva de indización**. Hola **directiva de indización** hoja, cambiar su directiva de indexación y, a continuación, haga clic en **Aceptar** toosave los cambios. 

### <a id="indexing-modes"></a>Modos de indexación de bases de datos
Base de datos de Azure Cosmos admite tres modos indización que se pueden configurar a través de hello indización de directiva para una colección de la base de datos de Azure Cosmos – coherente, Lazy y ninguno.

**Coherente**: si la directiva de la colección de una base de datos de Azure Cosmos se designa como "coherente", las consultas de hello en una determinada base de datos de Azure Cosmos de seguimiento de colección Hola mismo nivel de coherencia que se especifican para hello (es decir, seguro, limitado-obsolescencia, lecturas de punto sesión o final). índice de Hola se actualiza de forma sincrónica como parte de la actualización de documentos de hello (es decir, insert, replace, actualización y eliminación de un documento en una colección de base de datos de Azure Cosmos).  Indización coherente admite consultas coherente al costo de Hola de reducción de los posibles en el rendimiento de escritura. Esta reducción es una función de hello rutas de acceso únicas que necesitan toobe indizada y Hola "nivel de coherencia". El modo de indexación coherente está diseñado para cargas de trabajo de tipo "escribir rápidamente, consultar inmediatamente".

**Lazy**: rendimiento de ingesta de tooallow máximo del documento, se puede configurar una colección de base de datos de Azure Cosmos con coherencia diferida; las consultas de significado son coherentes. índice de Hola se actualiza de forma asincrónica cuando una colección de base de datos de Azure Cosmos está inactiva, es decir, capacidad de rendimiento de la colección de hello no es totalmente infrautilizado tooserve las solicitudes del usuario. Para cargas de trabajo de tipo "introducir ahora, consultar más adelante" que requieran ingesta de documentos sin obstáculos, es posible que el modo de indexación "diferido" sea el adecuado.

**Ninguna**: una colección marcada con el modo de indexación de "Ninguna" no tiene ningún índice asociado. Esto se suele usar si Azure Cosmos DB se emplea como almacenamiento de clave-valor y solo se puede acceder a los documentos mediante su propiedad de identificador. 

> [!NOTE]
> Hola configurar Directiva con "None" de indexación tiene Hola inconveniente de quitar todos los índices existentes. Úsela si los patrones de acceso solo requieren "id" o "vinculación automática".
> 
> 

Hola después el programa de ejemplo de cómo crea una colección de base de datos de Azure Cosmos mediante Hola .NET SDK con la indexación automática coherente en todas las inserciones de documento.

Hello en la tabla siguiente muestra hello coherencia de las consultas en función de modo de indexación de hello (coherente y Lazy) configurado para hello hello y colección coherencia nivel especificado para la solicitud de consulta de Hola. Esto aplica tooqueries realizadas mediante los SDK de interfaz - API de REST, o desde los procedimientos almacenados y desencadenadores. 

|Coherencia|Modo de indexación: coherente|Modo de indexación: diferido|
|---|---|---|
|Alta|Alta|Ocasional|
|De obsolescencia entrelazada|De obsolescencia entrelazada|Ocasional|
|Sesión|Sesión|Ocasional|
|Ocasional|Ocasional|Ocasional|

Azure Cosmos DB devuelve un error para las consultas realizadas en colecciones con el modo de indexación Ninguna. Todavía se pueden ejecutar las consultas como exámenes a través de hello explícita `x-ms-documentdb-enable-scan` encabezado en la API de REST de Hola o hello `EnableScanInQuery` solicitud utilizando la opción Hola .NET SDK. Algunas funciones de consulta, como ORDER BY, no se admiten como exámenes con `EnableScanInQuery`.

Hello tabla siguiente muestran Hola coherencia de las consultas en función de modo de indexación de hello (coherente, Lazy y ninguno) cuando se especifica EnableScanInQuery.

|Coherencia|Modo de indexación: coherente|Modo de indexación: diferido|Modo de indexación: ninguno|
|---|---|---|---|
|Alta|Alta|Ocasional|Alta|
|De obsolescencia entrelazada|De obsolescencia entrelazada|Ocasional|De obsolescencia entrelazada|
|Sesión|Sesión|Ocasional|Sesión|
|Ocasional|Ocasional|Ocasional|Ocasional|

Hola después el programa de ejemplo de código cómo crea una colección de base de datos de Azure Cosmos mediante Hola .NET SDK con la indización coherente en todas las inserciones de documento.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>Rutas de acceso del índice
Base de datos de Azure Cosmos modela documentos JSON y el índice de hello como árboles y permite tootune toopolicies para rutas de acceso de árbol de Hola. En los documentos, puede elegir qué rutas de acceso se deben incluir o excluir del índice. Esto puede ofrecer un rendimiento de escritura mejorado y el almacenamiento de índice inferior para los escenarios cuando los patrones de consulta de Hola se conocen de antemano.

Las rutas de acceso de índice iniciar con raíz (/) de Hola y normalmente finalizan con hello? operador de carácter comodín, lo que indica que hay varios valores posibles para el prefijo de Hola. ¿Por ejemplo, tooserve SELECT * FROM familias F WHERE F.familyName = "Andersen", debe incluir una ruta de acceso de índice para /familyName/? en la directiva de índice de la colección de Hola.

Las rutas de acceso de índice también pueden usar Hola * comportamiento de comodín operador toospecify Hola para las rutas de acceso de forma recursiva bajo prefijo Hola. Por ejemplo, / carga / * puede ser tooexclude usa todo el contenido en la propiedad de la carga de hello de la indización.

Estos son los patrones comunes de Hola para especificar las rutas de acceso del índice:

| Ruta de acceso                | Descripción/caso de uso                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | Ruta de acceso predeterminada de la recopilación. Recursiva y aplica toowhole árbol del documento.                                                                                                                                                                                                                                   |
| /prop/?             | Ruta de índice requerida tooserve consultas como Hola siguiente (con Hash o Range tipos, respectivamente):<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                       |
| /"prop"/*             | Ruta de acceso de índice para todas las rutas de acceso en la etiqueta especificada Hola. Funciona con las siguientes consultas de Hola<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5<br><br>SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"<br><br>SELECT FROM collection c ORDER BY c.prop         |
| /props/[]/?         | Ruta de índice requerida tooserve iteración y las consultas de combinación en las matrices de valores escalares como ["a", "b", "c"]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5                                                                         |
| /props/[]/subprop/? | Ruta de índice requerida tooserve iteración y consultas de combinación en las matrices de objetos, como [{subprop: "a"}, {subprop: "b"}]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"                                  |
| /prop/subprop/?     | Ruta de índice requerida tooserve consultas (con Hash o Range tipos, respectivamente):<br><br>SELECT FROM collection c WHERE c.prop.subprop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> Al configurar las rutas de acceso de índice personalizado, son regla de indexación predeterminada de toospecify necesario Hola de árbol de todo el documento de hello denotado por ruta de acceso especial de Hola "/ *". 
> 
> 

Hello en el ejemplo siguiente se configura una ruta de acceso específica con una indización de intervalo y un valor de precisión personalizado de 20 bytes:

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>Tipos de datos de índice, variantes y precisiones
Ahora que hemos llevado un vistazo a cómo las rutas de acceso de toospecify, echemos un vistazo en Opciones de hello, podemos utilizar tooconfigure Hola directiva de indexación de una ruta de acceso. Puede especificar una o más definiciones de indexación para cada ruta de acceso:

* Tipo de datos: **Cadena**, **Número** o **Punto**, **Polígono** o **LineString** (solo puede contener una entrada por tipo de datos y ruta de acceso).
* Variante de índice: **Hash** (consultas de igualdad), **Intervalo** (consultas de igualdad, de intervalo o por Order By), o **Espacial** (consultas espaciales) 
* Precisión: Índice de hash esto varía desde 1 too8 para cadenas y números no tiene valor predeterminado como 3. Para el índice de intervalo, este valor puede ser -1 (precisión mínima) y, para valores numéricos o de cadena, variar entre 1 y 100 (precisión máxima).

#### <a name="index-kind"></a>Tipo de índice
Azure Cosmos DB admite los tipos de índice Hash e Intervalo para cada ruta de acceso (que puede configurar para las cadenas, números o ambos).

* **Hash** admite consultas de igualdad y JOIN eficientes. Para la mayoría de los casos de uso, los índices de hash no es necesario una precisión mayor que el valor predeterminado de Hola de 3 bytes. El tipo de datos puede ser Cadena o Número.
* **Intervalo** admite consultas de igualdad, consultas de intervalo (con &gt;, &lt;, &gt;=, &lt;=, !=) y consultas Order By eficientes. De forma predeterminada, las consultas Order By también requieren una precisión índice máximo (-1). El tipo de datos puede ser Cadena o Número.

Base de datos de Azure Cosmos también admite tipo de índice espacial de Hola para cada ruta de acceso, que se pueden especificar para tipos de datos de punto, polígono o LineString Hola. valor de Hello en la ruta de acceso especificada de hello debe ser un fragmento de GeoJSON válido como `{"type": "Point", "coordinates": [0.0, 10.0]}`.

* **Espacial** admite consultas espaciales eficaces (internas y a distancia). El tipo de datos puede ser Punto, Polígono o LineString.

> [!NOTE]
> Azure Cosmos DB admite la indexación automática de puntos, polígonos y LineString.
> 
> 

Estos son tipos de índice de hello compatible y ejemplos de consultas que pueden ser utilizado tooserve:

| Tipo de índice | Descripción/caso de uso                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hash       | Hash over /prop/? (o /) puede ser hello tooserve usado las siguientes consultas eficazmente:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>Hash over /props/[]/? (o / o/props /) puede ser hello tooserve usado las siguientes consultas eficazmente:<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5                                                                                                                       |
| Intervalo      | Range over /prop/? (o /) puede ser hello tooserve usado las siguientes consultas eficazmente:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                                                                                                                                                              |
| Espacial     | Range over /prop/? (o /) puede ser hello tooserve usado las siguientes consultas eficazmente:<br><br>SELECT FROM collection c<br><br>WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40<br><br>SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --with indexing on points enabled<br><br>SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --with indexing on polygons enabled              |

De forma predeterminada, se devuelve un error para las consultas con operadores de intervalo como > = Si no hay ningún índice de intervalo (de cualquier precisión) en toosignal de orden que un examen podría ser la consulta de hello tooserve necesarios. Las consultas por rango pueden realizarse sin un índice de intervalo con el encabezado x-ms-documentdb-enable-examen de Hola Hola API de REST o la opción de solicitud de EnableScanInQuery de hello usando Hola .NET SDK. Si no hay ningún otro filtro de consulta de Hola que base de datos de Azure Cosmos pueden usar hello toofilter de índice en, no se devolverá ningún error.

Hola mismas reglas se aplican para las consultas espaciales. De forma predeterminada, se devuelve un error para las consultas espaciales, si no hay ningún índice espacial, y no hay ningún otro filtro que se pueda acceder desde el índice de Hola. Se pueden realizar como un análisis mediante x-ms-documentdb-enable-examen/EnableScanInQuery.

#### <a name="index-precision"></a>Índice de precisión
La precisión de índice permite lograr un equilibrio entre la sobrecarga de almacenamiento de índices y el rendimiento de las consultas. Para números, se recomienda usar la configuración de precisión predeterminada de Hola de -1 ("máximo"). Puesto que los números son 8 bytes en JSON, ésta es la configuración de tooa equivalente de 8 bytes. Seleccionar un valor inferior para precisión, por ejemplo, 1-7, significa que los valores dentro de algunos toohello de asignación de intervalos iguales la entrada de índice. Unidades de solicitud, por tanto, se reducirá el espacio de almacenamiento del índice, pero podría tener tooprocess varios documentos y, por consiguiente, es decir, a consumir más rendimiento ejecución de la consulta.

La configuración de la precisión del índice tiene una aplicación más práctica con intervalos de cadena. Puesto que las cadenas pueden ser cualquier longitud arbitraria, elección de Hola de precisión de índice Hola puede afectar el rendimiento de Hola de consultas por rango cadena y la cantidad de Hola de impacto en el índice de espacio de almacenamiento necesario. Los índices de intervalo de cadena pueden configurarse con 1-100 o -1 (“máxima”). Si desea que tooperform Order By consultas en las propiedades de cadena, debe especificar una precisión de -1 para las rutas de acceso correspondientes de Hola.

Los índices espaciales siempre utilizan precisión de índice de hello predeterminada para todos los tipos (puntos, LineStrings y polígonos) y no pueden ser reemplazada. 

Hola de ejemplo siguiente muestra cómo tooincrease una precisión de hello para el intervalo de índices en una colección usando Hola .NET SDK. 

**Creación de una colección con una precisión de índice personalizada**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Base de datos de Azure Cosmos devuelve un error cuando una consulta utiliza Order By, pero no tiene un índice de intervalo contra Hola consultado ruta de acceso con una precisión máxima de Hola. 
> 
> 

De forma similar las rutas de acceso se pueden excluir completamente de la indexación. Hola siguiente en el ejemplo se muestra cómo tooexclude toda una sección de hello documenta (conocido como) un subárbol) de la indización utilizando Hola "*" comodín.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>Opción de suscribirse o no a la indexación
Puede elegir si desea índice de la colección tooautomatically Hola todos los documentos. De forma predeterminada, todos los documentos se indexan automáticamente, pero puede elegir tooturn, apáguelo. Cuando se desactiva la indexación, solo se puede tener acceso a documentos a través de sus propios vínculos o mediante consultas con Id.

Con la indexación automática está desactivada, puede agregar todavía selectivamente solo índice de toohello de documentos específicos. Por el contrario, puede dejar la indización automática y elegir de forma selectiva tooexclude solo determinados documentos. Indización de encendido/apagado configuraciones son útiles cuando tiene solo un subconjunto de documentos que necesitan toobe consultar.

Por ejemplo, hello ejemplo siguiente se muestra cómo tooinclude un documento de forma explícita mediante hello [DocumentDB API .NET SDK](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) hello y [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) propiedad.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>Modificar directiva de indexación de Hola de una colección
Base de datos de Azure Cosmos permite directiva de indexación toohello de toomake cambios de una colección en marcha Hola. Un cambio en la indización de la directiva en una colección de base de datos de Azure Cosmos puede provocar cambios tooa en forma de Hola de índice Hola incluidos Hola se pueden indizar las rutas de acceso, su precisión, así como modelo de coherencia de hello del propio índice; Hola. Por lo tanto un cambio en la directiva de indexación, hecho requiere una transformación de índice antiguo hello en una nueva. 

**Transformaciones de índice en línea**

![Cómo funciona la indexación: transformaciones de índice en línea de Azure Cosmos DB](./media/indexing-policies/index-transformations.png)

Transformaciones de índice se realizan en línea, lo que significa que documentos de hello indizados por directiva antigua Hola se transforman eficazmente por la nueva directiva de hello **sin afectar a la disponibilidad de escritura de Hola o rendimiento aprovisionado hello** de colección de Hola. Hola coherencia de lectura y operaciones de escritura realizadas mediante Hola API de REST, SDK o desde dentro de procedimientos almacenados y desencadenadores no se ve afectado durante la transformación de índice. Esto significa que no hay ningún rendimiento aplicaciones tooyour degradación o tiempo de inactividad al cambiar una directiva de indexación.

Sin embargo, durante el tiempo de hello transformación de índice está en curso, las consultas son finalmente coherentes, independientemente de hello indización de configuración del modo (Consistent o Lazy). Esto también aplica tooqueries desde todas las interfaces: API de REST, SDK y desde los procedimientos almacenados y desencadenadores. Al igual que con Lazy indización, transformación de índice se realiza asincrónicamente en segundo plano de hello en las réplicas de hello mediante recursos de Hola de repuesto disponibles para una réplica dada. 

También se realizan transformaciones de índice **in situ** (en su lugar), es decir, base de datos de Azure Cosmos no mantiene dos copias del índice de Hola y Hola de intercambio índice antiguo out con hello uno nuevo. Esto significa que no se requiere ni se usa espacio adicional en disco en las colecciones mientras se realizan transformaciones de índice.

Cuando se cambia la directiva de indexación, cómo los cambios de hello son toomove aplicada de hello antiguo índice toohello nuevo uno dependen principalmente Hola indización más configuraciones del modo de modo que Hola otros valores como las rutas de acceso incluidos y excluidos, tipos de índice y precisiones. Si la directiva antigua y la nueva usan indexación coherente, Azure Cosmos DB realiza una transformación de índice en línea. No se puede aplicar otro cambio de directiva de indización con modo de indexación coherente mientras transformación Hola está en curso.

Sin embargo, puede mover tooLazy o None modo de indexación durante una transformación está en curso. 

* Al mover tooLazy, cambio de directiva del índice de Hola se convierte en efectivo inmediatamente y base de datos de Azure Cosmos inicia asincrónicamente volver a crear el índice de Hola. 
* Cuando mueve tooNone, a continuación, hello es quitar índice efectivo inmediatamente. Mover tooNone es útil cuando se desea toocancel un en curso transformación e inicie de nuevo con una directiva de indización diferente. 

Si usas Hola .NET SDK, se puede iniciar un cambio de directiva de indización mediante Hola nueva **ReplaceDocumentCollectionAsync** método y realizar un seguimiento Hola porcentaje de progreso de transformación de índice de hello mediante hello  **IndexTransformationProgress** propiedad respuesta desde un **ReadDocumentCollectionAsync** llamar. Otros SDK y API de REST de hello admiten métodos y propiedades equivalentes para realizar cambios de directiva de indización.

Este es un fragmento de código que muestra cómo toomodify una colección de la directiva de indización de tooLazy de modo de indización coherente.

**Modificar la directiva de indización de tooLazy coherente**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


Puede comprobar el progreso de Hola de una transformación de índice por ReadDocumentCollectionAsync que realiza la llamada, por ejemplo, tal y como se muestra a continuación.

**Seguimiento del progreso de transformación de índice**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

Puede quitar el índice de Hola para una colección moviendo toohello ninguno modo de indexación. Esto puede ser una herramienta útil operativa si desea toocancel una transformación en curso y se aplican inmediatamente una nueva.

**Quitar índice Hola para una colección**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

¿Cuando se realiza cambios de la directiva de indización colecciones de base de datos de Azure Cosmos tooyour? siguiente Hola es casos de uso más común de hello:

* Servir resultados coherentes durante el funcionamiento normal, pero revertir toolazy indización durante las importaciones de datos de forma masiva
* Empezar a usar nuevas características de indización en sus base de datos de Azure Cosmos colecciones actuales, por ejemplo, como geospatial consultar que requieren el tipo de índice espacial de Hola o Order By y la cadena de consultas por rango que necesitan Hola cadena tipo de índice de intervalo
* Seleccione mano Hola toobe propiedades indizada y modificarlos con el tiempo
* Optimizar el rendimiento de consultas de indización precisión tooimprove o reduzca el almacenamiento usado

> [!NOTE]
> Directiva de indexación de toomodify con ReplaceDocumentCollectionAsync, necesita versión > = 1.3.0 de hello SDK de .NET
> 
> Para toocomplete de transformación de índice correctamente, debe asegurarse de que hay suficiente espacio de almacenamiento libre disponible en la colección de Hola. Si la colección de hello alcanza su cuota de almacenamiento, se pausará la transformación de índice Hola. La transformación del índice se reanudará automáticamente una vez que haya espacio de almacenamiento disponible, por ejemplo, si elimina algunos documentos.
> 
> 

## <a name="performance-tuning"></a>Optimización del rendimiento
Hola DocumentDB APIs proporcionan información acerca de las métricas de rendimiento como utiliza almacenamiento de índice de Hola y rendimiento de hello costo (unidades de solicitud) para cada operación. Esta información puede ser toocompare usa varias directivas de indización y de optimizar el rendimiento.

cuota de almacenamiento de toocheck Hola y el uso de una colección, ejecutar una solicitud HEAD o GET en un recurso de colección de Hola e inspeccionar los encabezados de x-ms-solicitud-usage de Hola y Hola x-ms-solicitud-quota. Hola .NET SDK, Hola [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) y [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) propiedades en [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) contienen estos valores correspondientes .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


sobrecarga de hello toomeasure de indización en cada operación de escritura (crear, actualizar o eliminar), inspeccionar el encabezado x-ms-solicitud-cargo de hello (o equivalente hello [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) propiedad en [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) Hola .NET SDK) número de hello toomeasure de unidades de solicitud utilizado por estas operaciones.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>Especificación de la directiva de indización de toohello de cambios
Se introdujo un cambio en el esquema de Hola de directiva de indexación de 7 de julio de 2015 con la API de REST versión 2015-06-03. las clases correspondientes de Hello en las versiones SDK de hello tienen nuevo esquema de hello toomatch de implementaciones. 

Hola siguientes cambios se implementaron en hello especificación de JSON:

* La directiva de indexación admite índices de intervalo para las cadenas
* Cada ruta de acceso puede tener varias definiciones de índice, una para cada tipo de datos
* La precisión de la indexación admite 1-8 para números, 1-100 para las cadenas y -1 (precisión máxima)
* Segmentos de rutas de acceso no requieren una comilla doble tooescape cada ruta de acceso. Por ejemplo, ¿puede agregar una ruta de acceso para /title/? en lugar de /"title"/?
* que representa "todas las rutas de acceso" de ruta de acceso raíz Hola puede representarse como / * (además demasiado /)

Si tiene código que realiza la provisión colecciones con una directiva de indexación personalizada escrita con versión 1.1.0 de Hola .NET SDK o anterior, deberá toochange la aplicación de código toohandle estos cambios en la versión de orden toomove tooSDK 1.2.0. Si no tiene código que configura la directiva de indexación o planear toocontinue usando una versión anterior de SDK, se requiere ningún cambio.

Para obtener una comparación resulta muy práctica, aquí es un ejemplo Hola de directiva de indexación personalizado escrito mediante API de REST versión 2015-06-03 así como Hola anterior versión 2015-04-08.

**JSON de directiva de indexación anterior**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**JSON de directiva de indexación actual**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>Pasos siguientes
Siga los vínculos de hello siguientes para los ejemplos de administración de directivas de índice y toolearn más información sobre el lenguaje de consulta de Azure Cosmos DB.

1. [Ejemplos de código de administración de índices de la API .NET de DocumentDB](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [Operaciones de recopilación de la API de REST de DocumentDB](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [Consulta con SQL](documentdb-sql-query.md)


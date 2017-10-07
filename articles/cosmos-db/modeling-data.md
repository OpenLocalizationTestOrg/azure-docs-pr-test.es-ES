---
title: datos del documento aaaModeling para una base de datos NoSQL | Documentos de Microsoft
description: "Obtenga información sobre el modelado de datos para bases de datos NoSQL."
keywords: modelado de datos
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a>Modelado de datos del documento para bases de datos NoSQL
Mientras sin esquemas bases de datos, como la base de datos de Azure Cosmos facilitan super modelo de datos de tooyour tooembrace cambios todavía debe dedicar algún tiempo pensar sobre los datos. 

¿Cómo van toobe almacena datos? ¿Cómo son los datos de tooretrieve y consulta de curso de aplicación? ¿La aplicación realiza muchas operaciones de lectura o escritura? 

Después de leer este artículo, será hello tooanswer pueda siguientes preguntas:

* ¿Cómo debo pensar en un documento en una base de datos de documentos?
* ¿Qué es el modelado de datos y por qué tendría que importarme? 
* ¿Cómo es modelar los datos en una base de datos documento relacional tooa diferentes de base de datos?
* ¿Cómo expreso relaciones de datos en una base de datos no relacional?
* ¿Cuándo se puede incrustar los datos y cuándo puedo vincular toodata?

## <a name="embedding-data"></a>Incrustación de datos
Al comenzar a modelar los datos en un almacén de documentos, como la base de datos de Azure Cosmos, intente tootreat las entidades como **documentos independientes** representado en JSON.

Antes de adentrarnos demasiado, nos gustaría volver a realizar algunos pasos y echar un vistazo a cómo podríamos modelar algo en una base de datos relacional, un asunto con el que muchos de nosotros ya estamos familiarizados. Hello en el ejemplo siguiente se muestra cómo se podría almacenar una persona en una base de datos relacional. 

![Modelo de base de datos relacional](./media/documentdb-modeling-data/relational-data-model.png)

Cuando se trabaja con bases de datos relacionales, nos hemos ha aprendido para toonormalize años, normalizar, normalizar.

Normalizar los datos normalmente implica tomar una entidad, como una persona y presenta la información estructurada en toodiscrete partes de los datos. En el ejemplo de Hola anterior, una persona puede tener varios registros de detalle de contacto, así como varios registros de dirección. Podemos ir incluso un paso más allá y desglosar detalles de contacto extrayendo aún más campos comunes, como un tipo. Al igual que ocurre con la dirección, cada registro aquí tiene un tipo como *doméstico* o *empresarial*. 

Hola guiar local cuando la normalización de datos es demasiado**evitar el almacenamiento de datos redundantes** en cada registro y en su lugar, consulte toodata. En este ejemplo, tooread una persona, con todos sus detalles de contacto y las direcciones, necesita toouse combinaciones tooeffectively agregado los datos en tiempo de ejecución.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

La actualización de una única persona con su información de contacto y direcciones requiere operaciones de escritura en muchas tablas individuales. 

Ahora vamos a echar un vistazo a cómo se podría modelo Hola mismo datos como una entidad independiente en una base de datos del documento.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

Con el anterior de enfoque Hola ahora tenemos **sin normalizar** Hola registro persona donde se **incrustado** todos Hola información relacionada con la persona de toothis, como sus detalles de contacto y direcciones, en tooa único Documento JSON.
Además, dado que no nos estamos confinados tooa un esquema fijo que tenemos Hola flexibilidad toodo cosas con detalles de contacto de distintas formas completamente. 

La recuperación de un registro de la persona que completa de base de datos de hello es ahora una única operación en una sola colección y de un solo documento de lectura. La actualización de un registro de una persona, con su información de contacto y direcciones, es también una operación de escritura única frente a un documento único.

Al eliminar la normalización de datos, la aplicación puede necesitar tooissue menos las consultas y actualizaciones toocomplete operaciones comunes. 

### <a name="when-tooembed"></a>Cuando tooembed
Por lo general, use los modelos de datos de incrustación cuando:

* Existen relaciones de **inclusión** entre entidades.
* Existen relaciones de **uno a algunos** entre entidades.
* Existen datos incrustados que **cambian con poca frecuencia**.
* Existen datos incrustados que no crecerán **sin límites**.
* No hay datos incrustados **integral** toodata en un documento.

> [!NOTE]
> Los modelos de datos desnormalizados normalmente proporcionan un mejor rendimiento de **lectura** .
> 
> 

### <a name="when-not-tooembed"></a>Cuando no tooembed
Mientras Hola regla general en una base de datos de documento es toodenormalize todo el contenido y lo inserte todos los datos en tooa único documento, esto puede provocar situaciones toosome que deberían evitarse.

Seleccione este fragmento JSON.

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

Este podría el aspecto de una entidad de publicación con comentarios incrustados si se ha modelado un sistema, CMS o blog normales. problema con este ejemplo Hello es ese hello matriz comentarios es **unbounded**, lo que significa que no hay ningún número de toohello límite (práctico) de los comentarios puede tener cualquier mensaje único. Esto se convertirá en un problema como tamaño de saludo del documento de hello podría crecer significativamente.

Como tamaño de Hola de hello documento crece en datos de saludo capacidad tootransmit Hola sobre conexión de hello, así como la lectura y actualización documento hello, a escala, se verán afectado.

En este caso sería mejor hello tooconsider siguiendo el modelo.

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

Este modelo tiene comentarios más reciente de hello tres incrustados en hello contabilizar por sí mismo, que es una matriz con un límite fijo esta hora. Hello otros comentarios se agrupan en toobatches de 100 comentarios y se almacenan en documentos independientes. tamaño de Hola de lote de Hola se ha elegido como 100 porque nuestra aplicación ficticia permite Hola comentarios del usuario tooload 100 a la vez.  

Otro caso donde la incrustación de datos no son una buena idea es cuando Hola incrusta datos se utilizan con frecuencia en documentos y cambian con frecuencia. 

Seleccione este fragmento JSON.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

Esto podría representar la cartera de acciones de una persona. Información bursátil de tooembed Hola que hemos elegido en el documento de la cartera de tooeach. En un entorno donde está cambiando con frecuencia, los datos relacionados como una aplicación, de operaciones bursátiles incrustación de datos que cambian con frecuencia va toomean que está actualizando constantemente cada documento cartera cada vez que una cotización.

Es posible negociar con la acción *zaza* cientos de veces en un solo día y miles de usuarios pueden tener *zaza* en su cartera. Con un modelo de datos como Hola anterior tendríamos tooupdate varios miles de documentos de cartera muchas veces al día a la izquierda tooa sistema que no se escala muy bien. 

## <a id="Refer"></a>Datos de referencia
Por lo tanto, la incrustación de datos funciona bien en muchos casos, pero está claro que hay escenarios en los que la desnormalización de los datos provocará más problemas que ventajas. ¿Qué hacemos ahora? 

Bases de datos relacionales no son lugar solo Hola donde puede crear relaciones entre entidades. En una base de datos de documento puede tener información en un documento que está realmente relacionado toodata en otros documentos. Ahora, estoy no recomendando para incluso un minuto que se desarrollan sistemas que serían mejor base de datos relacional tooa adecuado en la base de datos de Azure Cosmos o cualquier otra base de datos del documento, pero relaciones simples son válidas y pueden ser muy útiles. 

Hola JSON siguiente elegimos el ejemplo de Hola a toouse de una cartera de cotizaciones anteriormente pero esta vez que nos referimos toohello elemento estándar en la cartera de hello en lugar de incrustarla. De esta manera, al elemento en existencias Hola cambia con frecuencia a lo largo de hello día Hola solo documento que necesite toobe actualizado es único documento de cotizaciones Hola. 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


Un inconveniente inmediata toothis aunque consiste si su aplicación es tooshow requiere información sobre cada acción que se mantiene al mostrar una cartera de una persona; en este caso se necesita toomake varios viajes toohello base de datos tooload Hola información para cada documento estándar. Aquí hemos realizado una decisión tooimprove Hola la eficacia de operaciones de escritura, que ocurrir con frecuencia a lo largo de día de hello, pero a su vez en peligro en hello operaciones de lectura que probablemente tengan menos impacto en el rendimiento de Hola de este sistema determinado.

> [!NOTE]
> Modelos de datos normalizados **puede requerir más ciclos de ida y** toohello server.
> 
> 

### <a name="what-about-foreign-keys"></a>¿Qué sucede con las claves externas?
Porque actualmente no hay ningún concepto de una restricción, clave externa o de otra manera, las relaciones entre documentos que tienen en los documentos son "puntos débiles" y no se comprobarán Hola propia base de datos. Si desea tooensure que Hola datos que hace referencia a un documento tooactually existe, deberá toodo esto en la aplicación, o mediante el uso de saludo del servidor desencadenadores o procedimientos almacenados en la base de datos de Azure Cosmos.

### <a name="when-tooreference"></a>Cuando tooreference
Por lo general, se deben utilizar modelos de datos normalizados cuando:

* Se realiza una representación de relaciones de **uno a varios** .
* Se realiza una representación de las relaciones de **muchos a muchos** .
* Los datos relacionados **cambian con frecuencia**.
* Puede **cancelarse el límite**de los datos de referencia.

> [!NOTE]
> Normalmente, la normalización proporciona un mejor rendimiento de **escritura** .
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>¿Dónde se puede colocar relación Hola?
crecimiento de Hola de relación de hello le ayudará a determinar en qué referencia del documento toostore Hola.

Si miramos Hola JSON siguiente que modela publicadores y libros.

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

Si es poco a poco con crecimiento limitado número Hola de libros de Hola por publicador, puede ser útil, a continuación, almacenar referencia del libro de hello dentro de documento de publisher Hola. Sin embargo, si el número de Hola de libros por publicador es ilimitado, este modelo de datos conduciría toomutable, aumentando las matrices, como en el documento de publicador de ejemplo de Hola anterior. 

Cambiar cosas alrededor de un bit haría resultado en un modelo que representa todavía Hola los mismos datos pero ahora evita estas grandes colecciones mutables.

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

Hola ejemplo anterior, hemos eliminado Hola colección sin enlazar en el documento de publisher Hola. En su lugar, basta con un publicador toohello referencia en cada documento del libro.

### <a name="how-do-i-model-manymany-relationships"></a>¿Cómo se puede modelar las relaciones de varios a varios?
En una base de datos relacional, las relaciones *varios a varios* modelan con frecuencia con tablas de unión, que simplemente unen registros de otras tablas. 

![Combinar tablas](./media/documentdb-modeling-data/join-table.png)

Es posible que tooreplicate tentado Hola lo mismo con documentos y crear un modelo de datos que busca a continuación toohello similar.

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

Esto funcionaría. Sin embargo, cargar a cualquier un autor con sus libros o cargar un libro con su autor, siempre requeriría al menos dos consultas adicionales en la base de datos de Hola. Una consulta toohello de unión de documento y, a continuación, otra consulta toofetch Hola documento real que se está combinando. 

Si todo lo que hace esta tabla de unión es combinar dos datos, ¿por qué no quitarla completamente?
Tenga en cuenta Hola siguiente.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

Ahora, si tuviera un autor, inmediatamente saber qué libros que han escrito y a la inversa si tuviera un documento de libro cargado sabría identificadores de Hola de autores de Hola. Esto ahorra esa consulta intermedia en la tabla de combinación de hello reducir el número de saludo del servidor de viajes de ida y la aplicación tiene toomake. 

## <a id="WrapUp"></a>Modelos de datos híbridos
Ya hemos observado la incrustación (o desnormalización) y el establecimiento de referencias (o normalización). Cada opción tiene sus ventajas y compromisos, como hemos visto. 

No siempre tiene toobe o o, no ser un poco toomix asustado cosas up. 

En función de los patrones de uso específicos y las cargas de trabajo pueden darse casos donde se incrusta la combinación de la aplicación y los datos que se hace referencia tiene sentido y podría responsable toosimpler la lógica de la aplicación con el servidor de menos de ida y vuelta al mismo tiempo mantienen un buen nivel de rendimiento .

Considere la posibilidad de hello después de JSON. 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

Aquí hemos (principalmente) seguimos modelo incrustados hello, donde los datos de otras entidades se incrustan en los documentos de nivel superior de hello, pero se hace referencia a otros datos. 

Si observa en el documento de la libreta de hello, podemos ver algunas interesantes campos cuando miramos matriz Hola de autores. Hay un *identificador* campo que es el campo de hello usamos documento de autor de toorefer tooan atrás, una práctica estándar en un modelo normalizado, pero, a continuación, también tiene *nombre* y *thumbnailUrl*. Se ha podido detenida simplemente con *Id. de* y deja Hola aplicación tooget cualquier información adicional sea necesario del documento de autor respectivos hello mediante Hola "enlace", pero dado que nuestra aplicación muestra el nombre del autor de Hola y un imagen en miniatura con cada libro muestra podemos guardar un servidor de toohello de ida y vuelta por libro en una lista por eliminar la normalización **algunos** datos del autor de Hola.

Por supuesto, si cambia el nombre del autor de Hola o deseaban tooupdate sus fotos tendríamos toogo una actualización todos los libros que publican alguna vez pero en nuestra aplicación, basado en la suposición de Hola que los autores no cambien sus nombres muy a menudo, es un diseño aceptable Decisión.  

En el ejemplo de Hola hay **calcula previamente agregados** valores toosave un procesamiento costoso en una operación de lectura. En el ejemplo de Hola, algunos de los datos de hello incrustados en el documento de autor Hola son datos que se calculan en tiempo de ejecución. Cada vez que se publica un nuevo libro, se crea un documento de libro **y** campo de hello countOfBooks está establecido el valor de tooa calculado según el número de Hola de documentos de libro que existen para un autor concreto. Esta optimización sería buena en sistemas muchos lecturas donde se pueden permitirse toodo cálculos en las escrituras en orden toooptimize lecturas.

Hola toohave capacidad un modelo con campos calculados previamente pueden evitarse porque admite la base de datos de Azure Cosmos **transacciones de documentos múltiple**. Muchos almacenes NoSQL no pueden realizar transacciones en documentos y defensa, por tanto, al tomar decisiones de diseño, como "siempre incrustar todo", debido a la limitación de toothis. Con Azure Cosmos DB, puede utilizar los desencadenadores del servidor o los procedimientos almacenados que insertan los libros y actualizan los autores dentro de una transacción ACID. Ahora no lo hace **tienen** tooembed todo el contenido de tooone documento simplemente toobe seguro de que los datos de forma coherentes.

## <a name="NextSteps"></a>Pasos siguientes
debe recordar más importantes de Hola de este artículo es toounderstand que modelado de datos en un mundo sin esquemas son tan importantes como nunca. 

Igual que no hay ningún toorepresent de manera única una parte de los datos en una pantalla, no hay ningún toomodel de forma única los datos. Tenga toounderstand su aplicación y cómo generará, consumir y procesar los datos de Hola. A continuación, aplicando algunos Hola instrucciones presentadas aquí se pueden establecer sobre la creación de un modelo que cubre Hola necesidades inmediatas de la aplicación. Cuando las aplicaciones necesitan toochange, puede aprovechar flexibilidad Hola de una base de datos sin esquemas tooembrace que cambian y evolucionar con facilidad el modelo de datos. 

toolearn más información acerca de la base de datos de Cosmos de Azure, consulte del servicio de toohello [documentación](https://azure.microsoft.com/documentation/services/cosmos-db/) página. 

toounderstand cómo tooshard los datos entre varias particiones, consulte demasiado[particiones de datos en la base de datos de Azure Cosmos](documentdb-partition-data.md). 

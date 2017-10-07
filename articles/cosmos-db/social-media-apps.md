---
title: "Patrón de diseño de Azure Cosmos DB: aplicaciones de redes sociales | Microsoft Docs"
description: "Obtenga información acerca de un modelo de diseño para las redes sociales aprovechando la flexibilidad de almacenamiento de Hola de base de datos de Azure Cosmos y otros servicios de Azure."
keywords: aplicaciones de redes sociales
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>Redes sociales y Azure Cosmos DB
Vivir en una sociedad enormemente interconectada significa que, en algún momento de la vida, uno formará parte de una **red social**. Se usa las redes sociales tookeep en contacto con tus amigos, compañeros de trabajo, familia o a veces tooshare nuestra pasión con usuarios con intereses comunes.

Como ingenieros o a los desarrolladores, tengamos que se pregunte cómo estas redes almacenar y nuestros datos se interconectan, podría haber incluso ha toocreate de trabajo que pidieron o arquitecto de una nueva red social para un nicho específico mercado o su propio. ¿Es decir, cuando Hola big pregunta que surge: cómo se almacenan todos estos datos?

Supongamos que queremos crear una red social nueva en la que los usuarios puedan publicar artículos y materiales como imágenes, vídeos o incluso música. En esta red social, los usuarios podrán comentar y valorar las publicaciones con fines de clasificación. Habrá una fuente de entradas que los usuarios se ven y ser capaz de toointeract con en la página de inicio del sitio Web principal de Hola. Esto no parezca muy complicada (al principio), pero para hello simplificar, vamos a parar ahí (podríamos profundizar en las fuentes de usuario personalizada afectadas por las relaciones, pero supera el objetivo de Hola de este artículo).

Entonces, ¿cómo y dónde almacenamos estos datos?

Muchos de los usuarios podrían tener experiencia en bases de datos SQL o como mínimo, tener noción de [de modelado de datos relacional](https://en.wikipedia.org/wiki/Relational_model) y es posible que vea tentado toostart dibujar algo parecido a esto:

![Diagrama que ilustra un modelo relacional relativo](./media/social-media-apps/social-media-apps-sql.png) 

Sin embargo, a pesar de ser una estructura de datos perfectamente normalizada, no sería posible escalarla. 

No me malinterpreten, he trabajado con bases de datos SQL toda mi vida y me parecen excelentes, pero, al igual que todos los modelos, prácticas y plataformas de software, no son perfectas para todos los escenarios.

¿Por qué no es mejor opción de Hola SQL en este escenario? Echemos un vistazo a la estructura de Hola de un solo elemento para exponer, si deseaba tooshow que publique en un sitio Web o aplicación, ¿tengo toodo una consulta con... tabla 8 combinaciones (!) tooshow solo un único post, ahora, imagen podría ver una secuencia de entradas que se cargaron dinámicamente y aparecen en pantalla de bienvenida y donde voy.

Podríamos, por supuesto, usar una instancia SQL humongous con suficiente toosolve power miles de consultas con estos tooserve muchas de las combinaciones nuestro contenido, pero realmente, ¿por qué se cuando una solución más sencilla existe?

## <a name="hello-nosql-road"></a>carretera de NoSQL Hola
En este artículo le ayudará a modelar datos de su plataforma sociales con una base de datos de SQL de Azure [base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) de una manera rentable y con el uso de otras características de base de datos de Azure Cosmos como hello [Gremlin API de Graph ](../cosmos-db/graph-introduction.md). Con un enfoque [NoSQL](https://en.wikipedia.org/wiki/NoSQL), almacenamiento de datos en formato JSON y la aplicación de [desnormalización](https://en.wikipedia.org/wiki/Denormalization), nuestra publicación, que antes era complicada, ahora puede transformarse en un único [documento](https://en.wikipedia.org/wiki/Document-oriented_database):


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

Además, puede obtenerse con una sola consulta y sin combinaciones. Esto es mucho más sencilla y directa y budget-wise, requiere menos recursos tooachieve mejores resultados.

Base de datos de Azure Cosmos se asegura de que todas las propiedades de hello están indizadas con su indización automática, lo que puede ser incluso [personalizada](indexing-policies.md). Hola sin esquemas enfoque nos permite almacenar documentos con diferentes y las estructuras dinámicas, quizás mañana que queremos toohave entradas de una lista de categorías o hashtags asociados a ellos, Cosmos DB controlará Hola nuevos documentos con hello agrega atributos con sin adicional trabajo necesario para nosotros.

Los comentarios en una publicación pueden tratarse del mismo modo que otras publicaciones con una propiedad primaria (esto simplifica la asignación de objetos). 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

Por otro lado, todas las interacciones sociales pueden almacenarse en un objeto independiente como contadores:

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

Para la creación de fuentes solo es necesario crear documentos que puedan contener una lista de identificadores de publicación con un orden de importancia determinado:

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

Podríamos tener una secuencia "más reciente" con entradas ordenadas por fecha de creación, una secuencia "más reciente" con los que se envía con más similares en hello últimas 24 horas, incluso podríamos implementamos una secuencia personalizada para cada usuario según la lógica como seguidores e intereses y todavía sería una lista de  las entradas. Es una cuestión de cómo toobuild estas listas, pero rendimiento de lectura de hello permanece sin problemas. Una vez que se adquiere una de estas listas, se emiten una base de datos de consulta única tooCosmos con hello [IN (operador)](documentdb-sql-query.md#WhereClause) tooobtain páginas de entradas a la vez.

Hola fuente secuencias podría generarse utilizando [servicios de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/) procesos en segundo plano: [Webjobs](../app-service-web/web-sites-create-web-jobs.md). Una vez que se crea una entrada de blog, el procesamiento en segundo plano puede activarse mediante el uso de [el almacenamiento de Azure](https://azure.microsoft.com/services/storage/) [colas](../storage/queues/storage-dotnet-how-to-use-queues.md) y trabajos Web desencadenado mediante hello [SDK de Webjobs de Azure](../app-service-web/websites-dotnet-webjobs-sdk.md), implementación Hola posteriores a la propagación en secuencias en función de nuestra propia lógica personalizada. 

Puntos y LIKE sobre una publicación puede procesarse de forma diferida usando este mismo toocreate de técnica un entorno coherente.

Con los seguidores es más complicado. COSMOS base de datos tiene un límite de tamaño máximo del documento y documentos de gran tamaño de lectura/escritura puede afectar a la escalabilidad de hello de la aplicación. Por esta razón, debería plantearse almacenar los seguidores como un documento con esta estructura:

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

Esto puede funcionar en un usuario con unos miles seguidores, pero si algunos famosos combina nuestra rangos, este enfoque llevará tooa tamaño de documento de gran tamaño y podría limitar tamaño del documento Hola finalmente llamadas.

toosolve, podemos usar un enfoque mixto. Como parte del documento de estadísticas de usuarios de hello podemos almacenar número Hola de seguidores de:

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

Y gráfico real de Hola de seguidores puede almacenarse con base de datos de Azure Cosmos [API de Graph Gremlin](../cosmos-db/graph-introduction.md), toocreate [vértices](http://mathworld.wolfram.com/GraphVertex.html) para cada usuario y [bordes](http://mathworld.wolfram.com/GraphEdge.html) que mantener hello " Relaciones se indica a continuación-A-B". Hello API Graph vamos a no sólo obtener seguidores de Hola de un determinado usuario sino crear consultas más complejas tooeven sugerir personas en común. Si se agrega Hola de gráfico toohello categorías de contenido que las personas como o disfrute, podemos iniciar tejido experiencias que incluyen detección inteligente de contenido, lo que sugiere contenido que los que se siga como, o buscar personas con quienes se tengamos que tienen mucho en común.

documento de Hello estadísticas de usuario puede seguir siendo toocreate usado tarjetas de interfaz de usuario de Hola o vistas previas de perfil rápido.

## <a name="hello-ladder-pattern-and-data-duplication"></a>Hola duplicación de datos y el patrón de "Escala"
Como puede que haya observado en el documento JSON de Hola que hace referencia a una entrada de blog, hay varias apariciones de un usuario. Y habría adivinado correctamente, que esto significa que información de Hola que representa un especificada por el usuario, esta desnormalización, podría estar presente en más de un lugar.

En orden tooallow para las consultas más rápidas, se incurre en la desduplicación de datos. problema de Hola con este efecto secundario es que si por alguna acción, cambian los datos de un usuario, necesitamos toofind todas las actividades de hello alguna vez ha y actualizar todos ellos. Lo cierto es que no parece muy práctico.

Estamos toosolve continuo, mediante la identificación de Hola atributos de clave de un usuario que se muestra en nuestra aplicación para cada actividad. Si se muestra una entrada de blog en nuestra aplicación visualmente y mostrar simplemente del creador de Hola y el nombre imagen, ¿por qué almacenar todos los datos del usuario de hello en atributo createdBy"hello"? Si cada comentario que mostramos imagen de usuario de hello, realmente no es necesario rest Hola de su información. Es donde entra en juego la algo que llamaré Hola "escalera pattern".

Tomemos como ejemplo información de usuario:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

Al examinar esta información, podemos detectar rápidamente cuál es información importante y cuál no lo es, creando así una "escalera":

![Diagrama de un modelo de escalera](./media/social-media-apps/social-media-apps-ladder.png)

paso más pequeño de Hola se denomina un UserChunk, parte mínima de hello de la información que identifica a un usuario y se usa para la desduplicación de datos. Al reducir el tamaño de Hola Hola duplicada tooonly Hola de información de datos "mostraremos", se reducirán las posibilidades de Hola de actualizaciones masivas.

paso intermedio de Hola se denomina usuario hello, resulta Hola a todos los datos de Hola que se utilizará en la mayoría de las consultas dependientes de rendimiento en la base de datos de Cosmos más graves y que se accede. Incluye información de hello representado por un UserChunk.

Hola más grande es hello usuario extendido. Incluye toda la información crítica usuario hello además de otros datos que realmente no requieren la lectura de toobe rápidamente o su uso es final (por ejemplo, proceso de inicio de sesión de hello). Estos datos pueden almacenarse fuera de Cosmos DB, en Azure SQL Database o en tablas de Azure Storage.

¿Por qué podría se dividir usuario Hola e incluso almacenar esta información en distintos lugares? Dado que desde un punto de vista del rendimiento, hello documentos hello más grandes, Hola costosa consultas Hola. Mantener documentos finos con hello derecho información toodo realiza consultas en todos los dependientes de rendimiento con su red social y almacén Hola otra información adicional para posibles escenarios como, modificaciones de perfil completo, los inicios de sesión, incluso la minería de datos para análisis de uso y Big Iniciativas de datos. Realmente no nos interesa si Hola recopilación de datos para minería de datos están más lentos porque se está ejecutando en la base de datos de SQL Azure, se han conciernen aunque los usuarios tengan una experiencia rápida y delgada. La apariencia de un usuario almacenado en Cosmos DB sería la siguiente:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

Asimismo, una solicitud Post tendría el aspecto siguiente:

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

Y cuando una operación de edición se produce en uno de los atributos de hello del fragmento de Hola se ve afectado, resulta fácil toofind documentos de hello afectado mediante el uso de las consultas que señalan toohello indizado atributos (seleccione * FROM envía p WHERE p.createdBy.id == "edited_user_id") y, a continuación, actualizar fragmentos de Hola.

## <a name="hello-search-box"></a>cuadro de búsqueda de Hola
Los usuarios generarán, con suerte, una gran cantidad de contenido. Y deberíamos estar tooprovide capaz de hello capacidad toosearch y buscar contenido que podría no ser directamente en sus secuencias de contenido, quizás porque no seguimos creadores de hello, o quizás que simplemente tratamos toofind esa entrada anterior que se realizó hace 6 meses.

Por suerte, y dado que usamos la base de datos de Azure Cosmos, podemos implementar con facilidad un motor de búsqueda con [búsqueda de Azure](https://azure.microsoft.com/services/search/) en un par de minutos y sin escribir una sola línea de código (distinto de hello Obviamente, Buscar proceso e interfaz de usuario).

¿Por qué es tan fácil?

Búsqueda de Azure implementa lo que llame a [indizadores](https://msdn.microsoft.com/library/azure/dn946891.aspx), procesos en segundo plano que enlace en los repositorios de datos y de modo automático agregar, actualizar o quitar los objetos en los índices de Hola. Son compatibles con [indexadores de Azure SQL Database](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [indexadores de Blobs de Azure](../search/search-howto-indexing-azure-blob-storage.md) y, afortunadamente, [indexadores de Cosmos DB](../search/search-howto-index-documentdb.md). Hello transición de información de base de datos de Cosmos tooAzure búsqueda es sencilla, como ambos almacenar la información en formato JSON, solo tenemos demasiado[crear nuestro índice](../search/search-create-index-portal.md) y asignar los atributos de nuestros documentos desea indizar y eso es todo, en cuestión de minutos (depende de tamaño de Hola de nuestros datos), todo el contenido estará disponible toobe buscado, solución de hello mejor búsqueda como servicio en la infraestructura de nube. 

Para obtener más información acerca de la búsqueda de Azure, puede visitar hello [tooSearch de guía de Autoestopista](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).

## <a name="hello-underlying-knowledge"></a>conocimiento subyacente Hola
Después de almacenar todo este contenido que crece y crece diariamente, podríamos pensar: ¿qué puedo hacer con todo este flujo de información de mis usuarios?

respuesta de Hello es sencillo: colocarla toowork y obtenga información acerca de él.

Pero, ¿qué podemos aprender? Algunos ejemplos fácil son [análisis de opiniones](https://en.wikipedia.org/wiki/Sentiment_analysis), contenido recomendaciones se basan en las preferencias del usuario o incluso un automatizadas moderador contenido que garantiza que todos los Hola contenido publicado en nuestra red social es seguro para Hola familia.

Ahora que tengo que enlazar, se podrá considerar probablemente necesita algunos doctorado en matemáticas ciencia tooextract estos patrones y la información de archivos y bases de datos simples, pero podría ser incorrecto.

[Aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/), parte del programa Hola a [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), es un servicio de nube totalmente administrado que le permite crear flujos de trabajo mediante algoritmos en una sencilla interfaz de arrastrar y colocar, sus propios algoritmos de código de hello en [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) o usar algunas de hello ya creado y listo toouse API como: [análisis de texto](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [moderador contenido](https://www.microsoft.com/moderator) o [recomendaciones](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve cualquier de estos escenarios de aprendizaje automático, podemos usar [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest Hola información procedente de diferentes orígenes y usar [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess Hola información y generar una salida que pueden ser procesados por aprendizaje automático de Azure.

Otra opción disponible es toouse [Microsoft Services cognitivos](https://www.microsoft.com/cognitive-services) tooanalyze nuestros usuarios contenidos; no solo podemos se entienda mejor (a través de analizar lo que escribe con [API de análisis de texto](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), pero También podríamos detectar contenido no deseado o maduro y actuar en consecuencia con [equipo Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api). Servicios cognitivos incluyen muchas soluciones de cuadro que no requieren ningún tipo de aprendizaje automático conocimiento toouse.

## <a name="a-planet-scale-social-experience"></a>Una experiencia social a escala mundial
Hay un último, pero no por ello menos importante, tema que abordaremos: la **escalabilidad**. Al diseñar una arquitectura que es fundamental que cada componente puede escalar por sí mismo, ya sea porque se necesitan tooprocess más datos o porque deseamos toohave una cobertura geográfica más grande (o ambos). Afortunadamente, llevar a cabo una tarea así de compleja es una **experiencia inmediata** con Cosmos DB.

Admite COSMOS DB [crear particiones dinámicas](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of-the-box mediante la creación automática de las particiones basadas en un determinado **clave de partición** (definido como uno de los atributos de hello en los documentos). Definir Hola correcta de clave de partición debe realizarse en tiempo de diseño y mantener en hello cuenta [prácticas recomendadas](../cosmos-db/partition-data.md#designing-for-partitioning) está disponible; en caso de hello de una experiencia sociales, la estrategia de partición debe estar alineada con forma de hello consultar (lecturas dentro de hello son deseables misma partición) y escritura (evitar "zonas activas" extendiendo escrituras en varias particiones). Algunas opciones son: las particiones basadas en una clave temporal (día/mes/semana), por categoría de contenido, por región geográfica, por usuario; todo realmente depende de cómo consultar datos de Hola y mostrarla en su experiencia sociales. 

Un aspecto interesante de vale la pena mencionar es que Cosmos DB ejecutará las consultas (incluidos [agregados](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) a través de todas las particiones de forma transparente, no es necesario tooadd ninguna lógica que crecen los datos.

Con el tiempo, a la larga el tráfico crecerá y su consumo de recursos (que se mide en [RU](request-units.md) o unidades de solicitud) aumentará. Leerá y escribirá con mayor frecuencia medida que crece su userbase y se inician la creación y lectura de contenido más; Hola capacidad de **ajuste de escala en el rendimiento** es vital. Aumentar nuestro RUs es muy fácil, podemos hacerlo con unos pocos clics en hello Portal de Azure o [emitir comandos a través de la API de hello](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).

![Escalado vertical y definición de una clave de partición](./media/social-media-apps/social-media-apps-scaling.png)

¿Qué ocurre si las cosas siguen mejorando y los usuarios de otra región, otro país u otro continente descubren su plataforma y comienzan a usarla? ¡Una gran sorpresa!

Pero, espere... pronto se da cuenta de su experiencia con la plataforma no es óptimo; únicamente son hasta ahora fuera de su región operativa que la latencia de hello es terrible y obviamente no gusto tooquit. ¡Si tan solo hubiese una forma sencilla de **extender su alcance global**! Y la hay.

COSMOS DB permite [los datos se replica globalmente](../cosmos-db/tutorial-global-distribution-documentdb.md) y de forma transparente con un par de clics y automáticamente selecciona entre las regiones disponibles de Hola desde su [código de cliente](../cosmos-db/tutorial-global-distribution-documentdb.md). Esto también significa que tiene [varias regiones de conmutación por error](regional-failover.md). 

Al replicar los datos de forma global, deberá toomake seguro de que los clientes pueden beneficiarse de ella. Si usas un front-end web o el acceso a las API desde clientes móviles, puede implementar [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) y clonar el servicio de aplicaciones de Azure en todas las regiones de hello deseado, mediante una [configuración de rendimiento](../app-service-web/web-sites-traffic-manager.md)toosupport la cobertura global extendida. Cuando los clientes tienen acceso a su front-end o las API, estarán toohello enrutado el servicio de aplicación más cercano, que a su vez, se conectará la réplica de base de datos de Cosmos local toohello.

![Agregar plataforma sociales de cobertura global tooyour](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>Conclusión
Este artículo intenta tooshed algunos claro en alternativas de Hola de crear las redes sociales completamente en Azure con los servicios de bajo costo y proporcionar excelentes resultados mediante el uso de hello fomentando de una distribución de datos y la solución de varias capas de almacenamiento denominada "Escala".

![Diagrama de interacción entre los servicios de Azure para redes sociales](./media/social-media-apps/social-media-apps-azure-solution.png)

verdad de Hello es que no hay ningún mágica para este tipo de escenarios, tiene Hola synergy creado por la combinación de hello de servicios excelentes que nos permiten experiencias inmejorables toobuild: Hola velocidad y ausencia de base de datos de Azure Cosmos tooprovide una gran aplicación sociales, inteligencia de Hello detrás de una solución de búsqueda de primera clase, como búsqueda de Azure, flexibilidad de hello de servicios de aplicaciones de Azure toohost no incluso aplicaciones independientes del lenguaje pero procesos en segundo plano eficaz y Hola puede expandir el almacenamiento de Azure y base de datos de SQL de Azure para almacenar grandes cantidades de datos y Hola potencia analítica de toocreate de aprendizaje automático de Azure conocimiento e inteligencia que puede proporcionar comentarios tooour procesos y nos ayudarán a entregar hello toohello derecha contenido derecho a los usuarios.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de los casos de uso de la base de datos de Cosmos, consulte [casos de uso de la base de datos común de Cosmos](use-cases.md).

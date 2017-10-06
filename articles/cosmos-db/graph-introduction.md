---
title: "Introducción tooAzure API de gráficos de Cosmos DB | Documentos de Microsoft"
description: "Obtenga información acerca de cómo puede usar base de datos de Azure Cosmos toostore, consulta y gráficos masivos de recorrido con una latencia baja con lenguaje de consulta de Hola Hola Gremlin gráfico de Apache TinkerPop."
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>Introducción tooAzure DB Cosmos: API Graph

[Base de datos de Azure Cosmos](introduction.md) es Hola servicio de base de datos distribuidos globalmente, varios modelos de Microsoft para aplicaciones de misión crítica. Proporciona la base de datos de Azure Cosmos [distribución global preparada](distribute-data-globally.md), [escalado flexible de rendimiento y almacenamiento](partition-data.md) latencias de milisegundo en todo el mundo, solo dígito se escriben en el percentil 99 de hello, [cinco niveles de coherencia bien definido](consistency-levels.md)y garantiza la alta disponibilidad, que están respaldados por [líderes en la industria SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de datos de Azure Cosmos [automáticamente los datos de índices](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sin necesidad de toodeal con administración de esquema y de índice. Sigue varios modelos y es compatible con los modelos de datos de documento, de clave-valor, de grafo y de columnas.

![Gremlin, grafo y Azure Cosmos DB](./media/graph-introduction/graph-gremlin.png)

Hola API Graph de Azure Cosmos DB proporciona:

- Modelado de gráficos
- API de recorrido
- Distribución global llave en mano
- Escalado flexible de almacenamiento y el rendimiento con menos de 10 ms de latencias de lectura y menos de 15 ms en percentil 99 Hola
- Indexación automática con disponibilidad de consulta instantánea
- Niveles de coherencia ajustables
- Acuerdos de nivel de servicio completo con disponibilidad del 99,99 %

tooquery base de datos de Azure Cosmos, puede usar hello [Apache TinkerPop](http://tinkerpop.apache.org) graph lenguaje recorrido, [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), o al igual que otros sistemas de gráfico compatibles con TinkerPop [Apache Spark GraphX](spark-connector-graph.md).

En este artículo se proporciona información general de API Graph de Azure Cosmos DB hello y explica cómo puede utilizarlo toostore masivos gráficos con miles de millones de vértices y bordes. Puede consultar gráficos Hola con una latencia milisegundo y evolucionar con facilidad esquema y estructura gráfica del saludo.

## <a name="graph-database"></a>Base de datos de gráfico
Datos tal y como aparece en el mundo real Hola naturalmente está conectados. El modelado de datos tradicional se centra en las entidades. Para muchas aplicaciones, también hay una necesidad toomodel o toomodel las entidades y relaciones de forma natural.

Un [gráfico](http://mathworld.wolfram.com/Graph.html) es una estructura que está formada por [vértices](http://mathworld.wolfram.com/GraphVertex.html) y [bordes](http://mathworld.wolfram.com/GraphEdge.html). Tanto los vértices como los bordes pueden tener un número arbitrario de propiedades. Los vértices denotan objetos discretos, como una persona, un lugar o un evento. Los bordes representan las relaciones entre vértices. Por ejemplo, es posible que una persona conozca a otra, haya participado en un evento y recientemente haya estado en una ubicación. Propiedades de expresan la información acerca de los bordes y los vértices de Hola. Algunas propiedades de ejemplo son un vértice con un nombre y una edad, y un borde con una marca de tiempo o un peso. En términos más formales, este modelo se conoce como [grafo de propiedades](http://tinkerpop.apache.org/docs/current/reference/#intro). Base de datos de Azure Cosmos admite modelo del gráfico de propiedad Hola.

Por ejemplo, el gráfico muestra las relaciones entre personas, dispositivos móviles, intereses y sistemas operativos de ejemplo de Hola siguiente.

![Base de datos de ejemplo que muestra personas, dispositivos e intereses](./media/graph-introduction/sample-graph.png)

Gráficos son útil toounderstand una amplia gama de conjuntos de datos de la ciencia, la tecnología y negocio. Las bases de datos de gráficos permiten modelar y almacenar gráficos de forma natural y eficaz, lo que las hace útiles para muchos escenarios. Suelen ser bases de datos NoSQL, ya que estos casos de uso también necesitan a menudo flexibilidad en el esquema y una iteración rápida.

Los grafos ofrecen una técnica de modelado de datos novedosa y eficaz. Pero este hecho por sí solo no es un toouse razón suficiente una base de datos del gráfico. Para muchos casos de uso y patrones que implican recorridos de gráfico, los gráficos superan el rendimiento de las bases de datos SQL y NoSQL tradicionales en órdenes de magnitud. Esta diferencia en rendimiento se amplía aún más al recorrer varias relaciones, como los amigos de mis amigos.

Puede combinar recorridos rápido Hola que proporcionan las bases de datos de gráfico con algoritmos de gráfico, como búsqueda de prioridad de profundidad, búsqueda de amplitud y el algoritmo de Dijkstra, toosolve problemas en distintos dominios como las redes sociales, administración de contenido, geospatial, y las recomendaciones.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Grafos a escala mundial con Azure Cosmos DB
Base de datos de Cosmos Azure es una base de datos de gráfico totalmente administrado que ofrece la distribución global, elástico de ajuste de escala de almacenamiento y rendimiento, la indexación automática y consulta, niveles de coherencia ajustables y compatibilidad para hello TinkerPop estándar.  

![Arquitectura de grafo de Azure Cosmos DB](./media/graph-introduction/cosmosdb-graph-architecture.png)

Base de datos de Azure Cosmos ofrece siguiente Hola diferencia capacidades cuando se comparan las bases de datos del gráfico de tooother de mercado de hello:

* Rendimiento y almacenamiento escalables de manera elástica

 Los gráficos de Hola mundo real necesitan tooscale más allá de la capacidad de Hola de un único servidor. Con Azure Cosmos DB, puede escalar sus grafos sin problemas en varios servidores. También puede escalar el rendimiento de Hola de su gráfico de forma independiente en función de los patrones de acceso. Base de datos de Azure Cosmos admite bases de datos de gráfico que se pueden escalar toovirtually tamaños de almacenamiento ilimitado y rendimiento aprovisionado.

* Replicación de varias regiones

 Base de datos de Azure Cosmos transparente replica regiones de datos tooall el gráfico que se han asociado a su cuenta. La replicación permite toodevelop aplicaciones que requieren acceso global toodata. Hay que en áreas de Hola de coherencia, disponibilidad, rendimiento y garantías correspondientes. Azure Cosmos DB proporciona conmutación por error regional transparente con las API de hospedaje múltiple. Elásticamente puede escalar el almacenamiento y rendimiento en todo el mundo de Hola.

* Consultas rápidas y recorridos con la sintaxis conocida de Gremlin

 Almacene vértices heterogéneos y bordes, y consulte estos documentos por medio de la sintaxis conocida de Gremlin. Base de datos de Cosmos Azure emplea un grado elevado de simultaneidad sin bloqueo, estructurado del registro indización tecnología tooautomatically índice todo el contenido. Esta función permite enriquecidas consultas en tiempo real y recorridos sin Hola necesitan toospecify sugerencias de esquema, los índices secundarios o vistas. Aprenda más en [Consulta de grafos mediante Gremlin](gremlin-support.md).

* Completamente administrada

 Base de datos de Azure Cosmos elimina Hola necesidad toomanage base de datos y máquina los recursos. Como un servicio de Microsoft Azure completamente administrado, no no necesidad toomanage las máquinas virtuales, implementar y configurar el software, administrar el ajuste de escala o, ocuparse de las actualizaciones de la capa de datos complejos. Se hacen copias de seguridad de todos los grafos, además de protegerlos ante errores regionales. Puede agregar fácilmente una cuenta de Azure Cosmos DB y aprovisionar capacidad a medida que la necesite, para poder concentrarse en su aplicación en lugar de en la operación y administración de la base de datos.

* Indexación automática

 De forma predeterminada, base de datos de Azure Cosmos automáticamente indiza todas las propiedades de hello en los nodos y bordes en el gráfico de hello y no esperan o requieren cualquier esquema o la creación de índices secundarios.

* Compatibilidad con Apache TinkerPop

 Azure DB Cosmos forma nativa es compatible con estándar de Apache TinkerPop de código abierto de Hola y se puede integrar con otros sistemas de gráfico TinkerPop habilitado. Por tanto, puede migrar fácilmente desde una base de datos de gráficos diferente, como Titan o Neo4j, o usar Azure Cosmos DB con marcos de análisis de gráficos como [Apache Spark GraphX](spark-connector-graph.md).

* Niveles de coherencia ajustables

 Seleccione en cinco bien definidos de coherencia niveles tooachieve un equilibrio óptimo entre coherencia y rendimiento. Para las consultas y las operaciones de lectura, Azure Cosmos DB ofrece cinco niveles de coherencia diferentes: segura, obsolescencia limitada, sesión, prefijo coherente y posible. Estos niveles de coherencia granular y bien definidos permiten toomake sonido contrapartidas entre coherencia, la disponibilidad y la latencia. Obtenga más información en [utilizando coherencia niveles toomaximize disponibilidad y el rendimiento en DocumentDB](consistency-levels.md).

Base de datos de Azure Cosmos puede usar varios modelos, como el documento y gráfico, dentro Hola contenedores mismas/bases de datos. Puede utilizar un documento colección toostore gráfico de datos paralelo con documentos. Puede usar ambas consultas SQL sobre JSON y Gremlin consultas tooquery Hola los mismos datos como un gráfico.

## <a name="getting-started"></a>Introducción
Puede usar hello Azure interfaz de línea de comandos (CLI), Powershell de Azure, u Hola portal de Azure con compatibilidad para las cuentas de base de datos de Azure Cosmos de graph API toocreate. Después de crear cuentas, hello portal de Azure proporciona un extremo de servicio, como `https://<youraccount>.graphs.azure.com`, que proporciona un front-end de WebSocket para Gremlin. Puede configurar las herramientas de TinkerPop compatible, como hello [Gremin consola](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), tooconnect toothis aplicaciones punto de conexión y compilación de Java, Node.js o cualquier controlador de cliente Gremlin.

Hello tabla siguiente se muestran a los controladores de Gremlin populares que se pueden usar con la base de datos de Azure Cosmos:

| Descargar | Documentación |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.js](https://www.npmjs.com/package/gremlin) |[Gremlin-JavaScript en Github](https://github.com/jbmusso/gremlin-javascript) |
| [Gremlin Console](https://tinkerpop.apache.org/downloads.html) |[Documentación de TinkerPop](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Base de datos de Azure Cosmos también proporciona una biblioteca de .NET que tiene los métodos de extensión de Gremlin sobre hello [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md) a través de NuGet. Esta biblioteca proporciona un servidor de Gremlin "en proceso" que se puede usar tooconnect directamente tooDocumentDB particiones de datos.

| Descargar | Documentación |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

Mediante el uso de hello [emulador de base de datos de Azure Cosmos](local-emulator.md), puede utilizar toodevelop de API Graph de Hola y probar localmente sin crear una suscripción de Azure o incurrir en los costos. Cuando esté satisfecho con cómo funciona la aplicación en el emulador de hello, puede cambiar una cuenta de base de datos de Azure Cosmos en nube de hello toousing.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Escenarios de compatibilidad con gráficos de Azure Cosmos DB
Estos son algunos escenarios donde se puede usar la compatibilidad con gráficos de Azure Cosmos DB:

* Redes sociales

 Al combinar datos sobre los clientes y sus interacciones con otras personas, puede desarrollar experiencias personalizadas, predecir el comportamiento de los clientes o conectar a personas con otras que tengan intereses similares. Base de datos de Azure Cosmos pueden toomanage usa redes sociales y realizar un seguimiento de los datos y las preferencias del usuario.

* Motores de recomendaciones

 Este escenario se usa normalmente en el sector minorista de Hola. Al combinar información sobre productos, usuarios e interacciones de usuario, como comprar, examinar o clasificar un artículo, puede generar recomendaciones personalizadas. Hola baja latencia y escala elástica, nativo compatibilidad de gráfico de base de datos de Azure Cosmos es ideal para el modelado de estas interacciones.

* Geoespaciales

 Muchas aplicaciones de telecomunicaciones, logística y planear sus viajes necesitan toofind una ubicación de interés dentro de un área o busque la ruta más corta/óptima de hello entre dos ubicaciones. Azure Cosmos DB es una opción natural para estos problemas.

* Internet de las cosas

 Con la red de Hola y las conexiones entre los dispositivos de IoT modelados como un gráfico, puede crear una mejor comprensión del estado de Hola de los dispositivos y los activos y obtenga información acerca de cómo los cambios en una parte de la red de hello posiblemente pueden afectar a otra parte.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de soporte técnico de gráfico en la base de datos de Cosmos de Azure, vea:

* Empezar a trabajar con hello [tutorial del gráfico de base de datos de Azure Cosmos](create-graph-dotnet.md).
* Obtenga información acerca de cómo demasiado[consultar los gráficos de la base de datos de Azure Cosmos con Gremlin](gremlin-support.md).

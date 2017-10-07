---
title: aaaAzure Cosmos DB modelo de recursos y conceptos | Documentos de Microsoft
description: "Obtenga información sobre el modelo jerárquico del Cosmos base de datos Azure de las bases de datos, colecciones, función definida por el usuario (UDF), documentos, recursos de toomanage de permisos y mucho más."
keywords: "Modelo jerárquico, cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Conceptos básicos y modelo jerárquico de recursos de Azure Cosmos DB
las entidades de base de datos que administra la base de datos de Azure Cosmos Hello son tooas que se hace referencia **recursos**. Cada recurso se identifica mediante un URI lógico. Puede interactuar con los recursos de hello mediante verbos HTTP estándar, encabezados de solicitud/respuesta y códigos de estado. 

Leyendo este artículo, podrá hello tooanswer pueda siguientes preguntas:

* ¿Qué es el modelo de recursos de Cosmos DB?
* ¿Qué sistema definido recursos como recursos toouser opuestos definido?
* ¿Cómo se puede dirigir un recurso?
* ¿Cómo se trabaja con las colecciones?
* ¿Cómo se trabaja con procedimientos almacenados, desencadenadores y Funciones definidas por el usuario (UDF)?

## <a name="hierarchical-resource-model"></a>Modelo jerárquico de recursos
Como hello siguiente diagrama se muestra, Hola DB Cosmos jerárquica **modelo de recursos** están compuestos de conjuntos de recursos en una cuenta de base de datos, cada uno de ellos direccionable a través de un URI lógico y estable. Un conjunto de recursos será tooas que se hace referencia una **fuente** en este artículo. 

> [!NOTE]
> Base de datos de Cosmos Azure ofrece un protocolo TCP muy eficaz que también es RESTful en su modelo de comunicación, disponible a través de hello [API de cliente de .NET de DocumentDB](documentdb-sdk-dotnet.md).
> 
> 

![Modelo jerárquico de recursos de Azure Cosmos DB][1]  
**Modelo jerárquico de recursos**   

toostart trabajar con los recursos, debe [crear una cuenta de base de datos](create-documentdb-dotnet.md) con su suscripción de Azure. Una cuenta de base de datos puede constar de un grupo de **bases de datos**, cada una con varias **colecciones**, que a su vez pueden contener **procedimientos almacenados, desencadenadores, UDF, documentos** y **datos adjuntos** relacionados. Una base de datos también tiene asociados **usuarios**, cada uno con un conjunto de **permisos** tooaccess colecciones, procedimientos almacenados, desencadenadores, las UDF, documentos o datos adjuntos. Mientras las bases de datos, usuarios, permisos y colecciones son recursos definidos por el sistema con esquemas, documentos y datos adjuntos conocidos con contenido arbitrario JSON definido por el usuario.  

| Recurso | Description |
| --- | --- |
| Cuenta de base de datos |Una cuenta de base de datos está asociada a un conjunto de bases de datos y una cantidad fija de almacenamiento de blobs para los datos adjuntos. Puede crear una o más cuentas de base de datos mediante su suscripción de Azure. Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/). |
| Base de datos |Una base de datos es un contenedor lógico de almacenamiento de documentos particionado en recopilaciones. Es también un contenedor de usuarios. |
| Usuario |Hola espacio de nombres lógico para definir el ámbito de permisos. |
| Permiso |Un token de autorización asociado a un usuario para el recurso específico de acceso tooa. |
| Colección |Una colección es un contenedor de documentos JSON y Hola asociadas lógica de la aplicación de JavaScript. Una colección es una entidad facturable, donde hello [costo](performance-levels.md) viene determinado por el nivel de rendimiento de hello asociado a la colección de Hola. Las colecciones pueden abarcar uno o más particiones/servidores y puede escalarse toohandle prácticamente ilimitados volúmenes de almacenamiento o de rendimiento. |
| Procedimiento almacenado |Lógica de aplicación escrita en JavaScript que se registra con una colección y ejecutar transaccionalmente dentro del motor de base de datos de Hola. |
| Desencadenador |Lógica de aplicaciones creada en JavaScript que se ejecuta antes o después de una operación de inserción, reemplazo o eliminación. |
| UDF |Lógica de aplicaciones creada en JavaScript. UDF habilitar toomodel un operador de consulta personalizada y, por tanto, amplían el lenguaje de consulta de API de documentos de hello core. |
| Documento |Contenido JSON definido por el usuario (arbitrario). De forma predeterminada, ningún esquema necesita toobe definido ni es necesario toobe índices secundarios proporcionados por hello todos los documentos agregan tooa colección. |
| Datos adjuntos |Los datos adjuntos son documentos especiales que contienen referencias y metadatos asociados con blobs/medios externos. desarrollador de Hello puede elegir blob de hello toohave administrado por la base de datos de Cosmos o guardarlo con un proveedor de servicio de blobs externo como OneDrive, Dropbox, etcetera. |

## <a name="system-vs-user-defined-resources"></a>Recursos del sistema frente a recursos definidos por el usuario
Los recursos como cuentas de base de datos, bases de datos, colecciones, usuarios, permisos, procedimientos almacenados, desencadenadores y UDF, tienen todos un esquema fijo y se denominan recursos del sistema. En contraste, los recursos, como documentos y datos adjuntos no tienen restricciones de esquema de Hola y son ejemplos de recursos definidos por el usuario. En Cosmos DB, tanto los recursos del sistema como los definidos por el usuario se representan y controlan como JSON compatibles con el estándar. Todos los recursos, sistema o definidas por usuarios tienen Hola propiedades comunes siguientes.

> [!NOTE]
> Tenga en cuenta que todas las propiedades generadas por el sistema en un recurso tienen un prefijo con subrayado (_) en su representación de JSON.
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>Propiedad</strong></p></td>
            <td valign="top"><p><strong>¿Configurable por el usuario o generada por el sistema?</strong></p></td>
            <td valign="top"><p><strong>Propósito</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>Generado por el sistema</p></td>
            <td valign="top"><p>Generados por el sistema, identificador único y jerárquico de recurso de Hola</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>Generado por el sistema</p></td>
            <td valign="top"><p>valor eTag del recurso de hello necesario para el control de simultaneidad optimista</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>Generado por el sistema</p></td>
            <td valign="top"><p>Última marca de tiempo actualizada del recurso de Hola</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>Generado por el sistema</p></td>
            <td valign="top"><p>URI direccionable único del recurso de Hola</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>Generado por el sistema</p></td>
            <td valign="top"><p>Nombre único del recurso de hello definido por el usuario (con hello misma partición clave-valor). Si el usuario de hello no especifica un Id., un identificador será generada por el sistema</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>Representación de conexión de los recursos
COSMOS DB no impone ninguna extensiones propias toohello estándar o especiales codificaciones de JSON; funciona con documentos conforme a JSON estándares.  

### <a name="addressing-a-resource"></a>Direccionamiento de un recurso
Todos los recursos se pueden diseccionar mediante URI. Hola valo hello **_self** propiedad de un recurso representa Hola URI relativo del recurso de Hola. Hello formato de hello URI consta de Hola /\<fuente\>/ segmentos de ruta de acceso de {_rid}:  

| Valor de hello _self | Descripción |
| --- | --- |
| /dbs |Fuente de bases de datos que hay en una cuenta de base de datos |
| /dbs/{dbName} |Base de datos con un identificador que coincida con el valor de Hola {dbName} |
| /dbs/{dbName}/colls/ |Fuente de colecciones que hay en una base de datos |
| /dbs/{dbName}/colls/{collName} |Colección con un identificador que coincida con el valor de Hola {collName} |
| /dbs/{dbName}/colls/{collName}/docs |Fuente de documentos que hay en una colección |
| /dbs/{dbName}/colls/{collName}/docs/{docId} |Documento con un identificador que coincida con el valor de Hola {doc} |
| /dbs/{dbName}/users/ |Fuente de usuarios que hay en una base de datos |
| /dbs/{dbName}/users/{userId} |Usuario con un identificador que coincida con el valor de Hola {user} |
| /dbs/{dbName}/users/{userId}/permissions |Fuente de permisos que hay en un usuario |
| /dbs/{dbName}/users/{userId}/permissions/{permissionId} |Permiso con un identificador que coincida con el valor de Hola {permiso} |

Cada recurso tiene un nombre único definido por el usuario expone a través de la propiedad de Id. de Hola. Nota: para los documentos, si Hola usuario no especifica un Id., nuestro SDK compatible generará automáticamente un identificador único para el documento de Hola. Id. de Hello es una cadena definida por el usuario, de los caracteres too256 que es único dentro del contexto de Hola de un recurso de nodo principal específico. 

Cada recurso también tiene un identificador de recurso jerárquica de generada por el sistema (también denominado tooas un RID), que está disponible a través de la propiedad de _rid Hola. Hola RID codifica la jerarquía completa de Hola de un recurso determinado y es que una representación interna cómoda utiliza tooenforce la integridad referencial de una manera distribuida. Hola RID es único dentro de una cuenta de base de datos y se usa internamente en DB Cosmos para enrutamiento eficaz sin necesidad de búsquedas de partición cruzado. los valores de Hello de propiedades de _rid de Hola y Hola _self son representaciones alternativas y canónicas de un recurso. 

compatibilidad de las API de REST de Hello direccionamiento de los recursos y el enrutamiento de solicitudes por Id. de Hola y propiedades de _rid de Hola.

## <a name="database-accounts"></a>Cuentas de la base de datos
Puede aprovisionar una o más cuentas de base de datos de Cosmos DB mediante su suscripción a Azure.

Puede crear y administrar cuentas de base de datos de base de datos de Cosmos a través del Portal de Azure de Hola en [http://portal.azure.com/](https://portal.azure.com/). Crear y administrar una cuenta de base de datos requiere acceso administrativo y solo se puede realizar con su suscripción de Azure. 

### <a name="database-account-properties"></a>Propiedades de la cuenta de base de datos
Como parte de aprovisionamiento y administración de una cuenta de base de datos puede configurar y leer Hola propiedades siguientes:  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Nombre de la propiedad</strong></p></td>
            <td valign="top"><p><strong>Descripción</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Directiva de coherencia</p></td>
            <td valign="top"><p>Establecer este nivel de coherencia de propiedad tooconfigure Hola predeterminada para todas las colecciones de hello en su cuenta de base de datos. Puede invalidar el nivel de coherencia de hello en forma de cada solicitud con el encabezado de solicitud de hello [x-ms-consistency-level]. <p><p>Tenga en cuenta que esta propiedad solo aplica toohello <i>recursos definidos por el usuario</i>. Todos los recursos definidos por el sistema son toosupport configurado lecturas/consultas con coherencia segura.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Claves de autorización</p></td>
            <td valign="top"><p>Estos son Hola principal y secundarias claves maestras y de solo lectura que proporcionan administrativos acceso tooall de recursos de hello en la cuenta de base de datos de Hola.</p></td>
        </tr>
    </tbody>
</table>

Tenga en cuenta que en suma tooprovisioning, configurar y administrar su cuenta de base de datos de hello Portal de Azure, mediante programación puede crear y administrar cuentas de base de datos de la base de datos de Cosmos mediante hello [API de REST de base de datos de Azure Cosmos](/rest/api/documentdb/) como así como [SDK de cliente](documentdb-sdk-dotnet.md).  

## <a name="databases"></a>Bases de datos
Una base de datos de la base de datos de Cosmos es un contenedor lógico de uno o más recopilaciones y los usuarios, como se muestra en hello siguiente diagrama. Puede crear cualquier número de bases de datos en un toooffer de asunto de cuenta de base de datos de Cosmos DB límites.  

![Modelo jerárquico de colecciones y cuenta de base de datos][2]  
**Una base de datos es un contenedor lógico de usuarios y colecciones**

Una base de datos puede contener almacenamiento de documentos prácticamente ilimitado y particionado en colecciones.

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Escala elástica de una base de datos de Cosmos DB
Una base de datos de la base de datos de Cosmos es elástico de manera predeterminada, que van desde unos toopetabytes GB de almacenamiento de documentos SSD de seguridad y rendimiento aprovisionado. 

A diferencia de una base de datos RDBMS tradicionales, una base de datos en la base de datos de Cosmos no está tooa ámbito único equipo. Con la base de datos de Cosmos como escala de su aplicación necesita toogrow, puede crear más colecciones, las bases de datos o ambos. De hecho, varias aplicaciones propias dentro de Microsoft han usado Cosmos DB a nivel de consumidor creando bases de datos de Cosmos DB extremadamente grandes conteniendo cada una miles de colecciones con terabytes de almacenamiento de documentos. Puede aumentar o reducir una base de datos agregando o quitando colecciones toomeet requisitos de escalado de la aplicación. 

Puede crear cualquier número de colecciones en una oferta de toohello de asunto de base de datos. Cada colección tiene un almacenamiento SSD de seguridad y el rendimiento aprovisionado para usted según el nivel de rendimiento seleccionados Hola.

Una base de datos de Cosmos DB también es un contenedor de usuarios. Un usuario, a su vez, es un espacio de nombres lógico para un conjunto de permisos que proporciona los datos adjuntos, documentos y toocollections específico de acceso y la autorización.  

Como con otros recursos en el modelo de recursos de base de datos de Cosmos hello, se pueden crear bases de datos, reemplazar, eliminar, leer o enumerado fácilmente con cualquier hello [API de REST](/rest/api/documentdb/) o cualquiera de hello [SDK de cliente](documentdb-sdk-dotnet.md). COSMOS DB garantiza la coherencia fuerte para leer o consultar los metadatos de Hola de un recurso de base de datos. Eliminar una base de datos automáticamente, se garantiza que no se puede obtener acceso a cualquiera de las colecciones de Hola o usuarios contenidos dentro de él.   

## <a name="collections"></a>Colecciones
Una colección de Cosmos DB es un contenedor de sus documentos JSON. 

### <a name="elastic-ssd-backed-document-storage"></a>Almacenamiento de documentos respaldado con SSD elástico
Una colección es elástica de forma intrínseca; crece y se reduce automáticamente a medida que agrega o elimina documentos. Las colecciones son recursos lógicos y pueden abarcar una o varios servidores o particiones físicos. número de Hola de particiones dentro de una colección viene determinado por base de datos de Cosmos según el tamaño de almacenamiento de Hola y rendimiento aprovisionado de saludo de la colección. Todas las particiones de Cosmos DB tienen una cantidad fija de almacenamiento con respaldo SSD asociado y se replican para ofrecer una alta disponibilidad. Administración de particiones es completamente administrado por base de datos de Azure Cosmos y no tiene un código complejo toowrite o administrar las particiones. Las colecciones de Cosmos DB ofrecen funcionalidades de almacenamiento y rendimiento **prácticamente ilimitadas** . 

### <a name="automatic-indexing-of-collections"></a>Indexación automática de las colecciones
Cosmos DB es un sistema de bases de datos verdadero libre de esquemas. No se supone ni requieren ningún esquema para los documentos de hello JSON. Si agrega la colección de documentos tooa, Cosmos DB indiza automáticamente y están disponibles para tooquery. La indexación automática de documentos sin requerir esquema o índices secundarios es una capacidad clave de Cosmos DB y se habilita mediante técnicas de mantenimiento de índices de escritura optimizada, sin bloqueo y estructuradas por registros. Cosmos DB es compatible con un volumen constante de operaciones de escritura muy rápidas mientras sigue dando servicio a consultas consistentes. Almacenamiento de documento y de índice son usado el almacenamiento de hello toocalculate utilizado por cada colección. Puede controlar Hola almacenamiento y rendimiento ventajas e inconvenientes asociados con una indización mediante la configuración de directiva de indexación de Hola de una colección. 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>Configuración de directiva de indexación de Hola de una colección
Hola directiva de cada colección de indización permite toomake rendimiento y almacenamiento ventajas e inconvenientes asociados con la indización. Hello siguientes opciones están disponible tooyou como parte de la configuración de índice:  

* Elija si colección Hola automáticamente indiza todos los documentos de Hola o no. De forma predeterminada, se indexan todos los documentos automáticamente. Puede elegir tooturn desactivar la indización automática y agregar de forma selectiva sólo el índice de toohello documentos concretos. Por el contrario, es posible elegir selectivamente tooexclude únicamente los documentos específicos. Puede lograr esto estableciendo Hola automática de las propiedades toobe true o false en hello indexingPolicy de una colección y uso del encabezado de solicitud de hello [x-ms-indexingdirective] al insertar, reemplazar o eliminar un documento.  
* Elija si tooinclude o excluir rutas de acceso específicas o patrones en los documentos de Hola índice. Puede conseguirlo mediante configuración includedPaths y excludedPaths en indexingPolicy Hola de una colección respectivamente. También puede configurar Hola almacenamiento y rendimiento ventajas e inconvenientes de intervalo y hash busca patrones de ruta de acceso específica. 
* Seleccione entre actualizaciones de índice sincrónica (consistente) y asincrónica (diferida). De forma predeterminada, el índice de Hola se actualiza sincrónicamente en cada Insertar, reemplazar o eliminar una colección de toohello de documento. Esto permite realizar consultas de hello toohonor Hola de mismo nivel de coherencia de lecturas del documento de Hola. Mientras DB Cosmos es de escritura optimizado y admite volúmenes sostenidos de escrituras de documento junto con el mantenimiento del índice sincrónico y que sirve al consultas coherente, puede configurar cierto tooupdate colecciones su índice de forma diferida. La indexación diferida aumenta aún más el rendimiento de escritura hello y es ideal para escenarios de ingesta de forma masiva para principalmente con muchas lecturas colecciones.

Hola directiva de indexación se puede cambiar mediante la ejecución de una operación PUT en la colección de Hola. Esto puede ser logra a través de hello [SDK del cliente](documentdb-sdk-dotnet.md), hello [Portal de Azure](https://portal.azure.com) o hello [API de REST](/rest/api/documentdb/).

### <a name="querying-a-collection"></a>Consulta de una colección
documentos de Hello dentro de una colección pueden tener esquemas arbitrarios y puede consultar documentos dentro de una colección sin proporcionar cualquier esquema o índices secundarios por adelantado. Puede consultar la colección de hello mediante hello [API de documentos de base de datos de Azure Cosmos: referencia de la sintaxis SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx), que proporciona operadores espaciales, relacional y jerárquicos enriquecidos y extensibilidad a través de la UDF basadas en JavaScript. Gramática JSON se permite para el modelado de documentos JSON como árboles con las etiquetas de los nodos de árbol de Hola. Esto lo aprovechan tanto las técnicas de indexación automática de la API de DocumentDB como el dialecto de SQL de la API de DocumentDB. Hola lenguaje de consulta de API de DocumetDB consta de tres aspectos principales:   

1. Un pequeño conjunto de operaciones de consulta que se asignan de forma natural toohello estructura de árbol como proyecciones y consultas jerárquicas. 
2. Un subconjunto de operaciones relacionales incluyendo composición, filtro, proyecciones, agregados y autocombinaciones. 
3. UDF basadas puramente en JavaScript que se funcionan con (1) y (2)  

modelo de consultas de base de datos de Cosmos Hola intenta toostrike un equilibrio entre la funcionalidad, la eficacia y la simplicidad. motor de base de datos de base de datos de Cosmos de Hola forma nativa se compila y ejecuta instrucciones de consulta SQL Hola. Puede consultar una colección utilizando hello [API de REST](/rest/api/documentdb/) o cualquiera de hello [SDK de cliente](documentdb-sdk-dotnet.md). Hola .NET SDK incluye un proveedor LINQ.

> [!TIP]
> Puede probar Hola API de DocumentDB y ejecutar consultas SQL contra nuestro conjunto de datos en hello [Query Playground](https://www.documentdb.com/sql/demo).
> 
> 

## <a name="multi-document-transactions"></a>Transacciones de documentos múltiples
Las transacciones de base de datos proporcionan un modelo de programación seguro y de predicción para tratar los datos de toohello cambios simultáneos. En RDBMS, lógica de negocios de toowrite de forma tradicional de hello es toowrite **procedimientos almacenados** o **desencadenadores** y entregarlo toohello servidor de base de datos para su ejecución transaccional. En RDBMS, programador de la aplicación hello es necesario toodeal con dos lenguajes de programación diferentes: 

* Hola (no transaccional) aplicación lenguaje de programación (por ejemplo, JavaScript, Python, C#, Java, etcetera.)
* T-SQL, transaccional lenguaje de programación Hola que se ejecuta de forma nativa en base de datos de Hola

En virtud de su profundo compromiso tooJavaScript y JSON directamente en el motor de base de datos de hello, base de datos de Cosmos proporciona un modelo de programación e intuitiva para ejecución de JavaScript basada en lógica de la aplicación directamente en las colecciones de hello en cuanto a los procedimientos almacenados y desencadenadores. Esto permite dos procedimientos siguientes de hello:

* Controlar la implementación eficaz de simultaneidad, recuperación, automática de indización de gráficos de objetos JSON de hello directamente en el motor de base de datos de Hola
* Expresar de forma natural flujo de control, la variable de ámbito, la asignación y la integración de primitivas con transacciones de bases de datos directamente en términos de lenguaje de programación de JavaScript de Hola de control de excepciones

lógica de JavaScript de Hello registrado en el nivel de colección, a continuación, puede emitir operaciones de base de datos en documentos de Hola de hello dado de la colección. DB COSMOS implícitamente Hola ajusta basadas en JavaScript, procedimientos almacenados y desencadenadores dentro de un ambiente transacciones ACID con aislamiento de instantánea a través de documentos dentro de una colección. Durante el transcurso de Hola de su ejecución, si Hola JavaScript produce una excepción, a continuación, Hola toda la transacción se anula. Hello resultante modelo de programación es muy sencilla pero eficaz. Los desarrolladores de JavaScript obtienen un modelo de programación “duradero” mientras siguen utilizando sus construcciones de lenguaje y primitivos de biblioteca familiares.   

Hello capacidad tooexecute JavaScript directamente dentro de la base de datos de hello motor Hola mismo espacio de direcciones como grupo de búferes de hello permite un rendimiento superior y ejecución transaccional de operaciones de base de datos en documentos de Hola de una colección. Además, motor de base de datos de base de datos de Cosmos hace un toohello profundo compromiso JSON y JavaScript elimina cualquier desigualdad de impedancia entre sistemas de tipos de Hola de aplicación y base de datos de Hola.   

Después de crear una colección, puede registrar los procedimientos almacenados, desencadenadores y UDF con una colección utilizando hello [API de REST](/rest/api/documentdb/) o cualquiera de hello [SDK de cliente](documentdb-sdk-dotnet.md). Tras el registro, puede hacer referencia a los mismos y ejecutarlos. Considere la posibilidad de siguiente Hola escrito completamente en JavaScript, código de hello siguiente toma dos argumentos (nombre de libro y nombre del autor) del procedimiento almacenado y crea un nuevo documento, las consultas para un documento y, a continuación, actualiza su – todo dentro de una transacción ACID implícita. En cualquier momento durante la ejecución de hello, si se produce una excepción de JavaScript, anula toda la transacción Hola.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

cliente de Hello puede "envíos" hello por encima de la base de datos de JavaScript lógica toohello para su ejecución transaccional a través de HTTP POST. Para obtener más información acerca del uso de los métodos HTTP, consulte [Interacciones RESTful con recursos de Azure Cosmos DB](https://msdn.microsoft.com/library/azure/mt622086.aspx). 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


Observe que, porque la base de datos de hello entiende JSON y JavaScript, no hay ningún sistema de tipo no coincidente, ningún "Asignación OR" o mágico de generación de código necesarios.   

Procedimientos almacenados y desencadenadores interactúan con un documentos hello y colección en una colección a través de un modelo de objetos bien definidas, que expone el contexto actual de colección de Hola.  

Las colecciones de hello API de documentos se pueden crear, eliminar, leer o enumerar fácilmente con cualquier hello [API de REST](/rest/api/documentdb/) o cualquiera de hello [SDK de cliente](documentdb-sdk-dotnet.md). Hola API de documentos siempre proporciona coherencia fuerte para leer o consultar los metadatos de Hola de una colección. Eliminar automáticamente una colección, se garantiza que no se puede tener acceso a cualquiera de los documentos de hello, datos adjuntos, procedimientos almacenados, desencadenadores y UDF incluidos en él.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>Procedimientos almacenados, desencadenadores y funciones definidas por el usuario (UDF)
Como se describe en la sección anterior de hello, puede escribir toorun de lógica de aplicación directamente dentro de una transacción dentro del motor de base de datos de Hola. lógica de la aplicación Hello puede escribirse completamente en JavaScript y se puede modelar como un procedimiento almacenado, desencadenador o una UDF. Hola código JavaScript en un procedimiento almacenado o un desencadenador puede insertar, reemplazar, eliminar, documentos de lectura o consultas dentro de una colección. En Hola otra parte, Hola JavaScript dentro de un UDF no se puede insertar, reemplazar o eliminar documentos. UDF enumerar documentos Hola de una consulta conjunto de resultados y generan otro conjunto de resultados. Para los servicios multiinquilino, Cosmos DB impone una estricta reserva basada en la gobernanza de los recursos. Cada procedimiento almacenado, desencadenador o una UDF Obtiene un cuanto fijo de toodo de recursos de sistema operativo su trabajo. Además, los procedimientos almacenados, desencadenadores o UDF no se pueden vincular con bibliotecas de JavaScript externas y están en la lista negra si superan los presupuestos de recursos de hello asignados toothem. Puede registrar, anular el registro de los procedimientos almacenados, desencadenadores o UDF con una colección mediante las API de REST de Hola.  Tras el registro de un procedimiento almacenado, desencadenador o UDF, se compila de forma previa y almacena como código byte que se ejecutará más tarde. Hola siguiente sección muestra cómo puede utilizar Hola Cosmos DB JavaScript SDK tooregister, ejecutar y anular el registro de un procedimiento almacenado, desencadenador y una UDF. Hola SDK de JavaScript es un contenedor simple hello [API de REST](/rest/api/documentdb/). 

### <a name="registering-a-stored-procedure"></a>Registro de un procedimiento almacenado
El registro de un procedimiento almacenado crea un nuevo recurso de procedimiento almacenado en una colección mediante POST HTTP.  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>Ejecución de un procedimiento almacenado
Ejecución de un procedimiento almacenado se realiza mediante la emisión de una solicitud HTTP POST con un recurso de procedimiento almacenado existente al pasar parámetros de procedimiento toohello Hola del cuerpo de solicitud.

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>Anulación del registro de un procedimiento almacenado
Anular el registro de un procedimiento almacenado es sencillo mediante la emisión de una solicitud HTTP DELETE en un recurso de procedimiento almacenado existente.   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>Registro de un desencadenador previo
El registro de un desencadenador se realiza creando un nuevo recurso de desencadenador en una colección mediante POST HTTP. Puede especificar si el desencadenador de hello es una anterior o un tipo de desencadenador y Hola post de operación se puede asociar con (por ejemplo, crear, reemplazar, Delete o todos).   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>Ejecución de un desencadenador previo
Ejecución de un desencadenador se debe especificar el nombre hello de un desencadenador existente en el momento de Hola de emitir la solicitud POST, PUT o DELETE de Hola de un recurso de documento a través del encabezado de solicitud de Hola.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>Anulación del registro de un desencadenador previo
Anular el registro de un desencadenador es sencillo mediante la emisión de una solicitud HTTP DELETE en un recurso de desencadenador existente.  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>Registro de una UDF
El registro de una UDF se realiza creando un nuevo recurso de UDF en una colección mediante POST HTTP.  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>Ejecutar un UDF como parte de la consulta de Hola
Una UDF puede especificarse como parte de la consulta SQL de Hola y se utiliza como un núcleo de Hola de manera tooextend [lenguaje de consulta SQL para hello documentos API](https://msdn.microsoft.com/library/azure/dn782250.aspx).

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>Anulación del registro de una UDF
Anular el registro de una UDF es sencillo mediante la emisión de una solicitud HTTP DELETE en un recurso de UDF existente.  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

Aunque los fragmentos de código de hello anteriores mostraron registro hello (POST), la anulación del registro (PUT), leer/lista (GET) y ejecución (POST) a través de hello [SDK de JavaScript](https://github.com/Azure/azure-documentdb-js), también puede usar hello [API de REST](/rest/api/documentdb/) u otros [SDK de cliente](documentdb-sdk-dotnet.md). 

## <a name="documents"></a>Documentos
Puede insertar, reemplazar, eliminar, leer, enumerar y consultar documentos JSON arbitrarios de una colección. COSMOS DB no impone ningún esquema y no requiere que los índices secundarios en toosupport de orden que las consultas en documentos de una colección. tamaño máximo de Hola para un documento es 2 MB.   

Al ser un servicio de base de datos totalmente abierto, Cosmos DB no crea ningún tipo de datos especializados, como fecha y hora, o codificaciones específicas para documentos JSON. Tenga en cuenta que Cosmos DB no requiere ningún especial JSON convenciones toocodify hello las relaciones entre varios documentos; sintaxis SQL de Hola de Cosmos DB proporciona a operadores de consulta relacional y jerárquica muy eficaces documentos tooquery y proyecto sin necesidad de toocodify relaciones entre los documentos con propiedades distintivas ni anotaciones especiales.  

Como con todos los demás recursos, se pueden crear documentos, reemplazar, eliminar, leer, enumerado y consultar fácilmente mediante las API de REST o cualquiera de hello [SDK de cliente](documentdb-sdk-dotnet.md). Eliminar un documento al instante libera Hola cuota correspondiente tooall de datos adjuntos de hello anidado. Hola lee el nivel de coherencia de documentos de sigue la directiva de coherencia de hello en la cuenta de base de datos de Hola. Esta directiva se puede reemplazar en función de la solicitud dependiendo de los requisitos de coherencia de datos de su aplicación. Al consultar documentos, Hola lee coherencia sigue Hola indización modo establecido en la colección de Hola. Para "coherente", esto sigue la directiva de coherencia de la cuenta de hello. 

## <a name="attachments-and-media"></a>Datos adjuntos y multimedia
COSMOS DB permite toostore blobs/medios binarios con la base de datos de Cosmos (máximo de 2 GB por cuenta) o tooyour multimedia de manera remota propio almacén. También permite toorepresent Hola metadatos de un medio de un documento especial denominado datos adjuntos. Datos adjuntos en la base de datos de Cosmos son un documento de (JSON) especial que referencias Hola multimedia o BLOBs almacenados en otro lugar. Datos adjuntos son simplemente un documento especial que captura Hola metadatos (por ejemplo, ubicación, autor, etc.) de un medio que se almacenan en un almacenamiento de información multimedia de manera remota. 

Considere la posibilidad de una aplicación de lectura social que usa anotaciones de Cosmos DB toostore tinta, y resalta los metadatos, incluidos los comentarios, marcadores, clasificaciones, etc. asociados para un libro electrónico de un usuario determinado similares/gustan.   

* Hello contenido del libro de hello propio se almacena de forma Hola medios o disponible como parte de la cuenta de base de datos de la base de datos de Cosmos o un almacén de multimedia de manera remota. 
* Una aplicación puede almacenar los metadatos de cada usuario como un documento distinto; por ejemplo, los metadatos de Joe para book1 se almacenan en un documento con la referencia /colls/joe/docs/book1. 
* Datos adjuntos que señala toohello páginas de contenido de un libro determinado de un usuario se almacenan en el documento correspondiente Hola p. ej., /colls/joe/docs/book1/chapter1, /colls/joe/docs/book1/chapter2 etcetera. 

Tenga en cuenta que los ejemplos de hello mencionados anteriormente usar la jerarquía de recursos de identificadores descriptivo tooconvey Hola. Se tiene acceso a recursos a través de hello las API de REST a través de identificadores de recurso único. 

En medios de Hola que está administrados por base de datos de Cosmos, propiedad de _media Hola de datos adjuntos de hello hará referencia a medios Hola por su identificador URI. COSMOS DB garantizará toogarbage media de hello recopilar cuando se quitan todas las referencias pendientes de Hola. COSMOS DB genera datos adjuntos de hello cuando cargue nuevos medios de Hola y rellenan hello _media toopoint toohello recién agregado medios automáticamente. Si elige media de hello toostore en un almacén de datos blob remoto administrado por el usuario (por ejemplo, OneDrive, almacenamiento de Azure, DropBox etcetera), todavía puede usar medios de los datos adjuntos tooreference Hola. En este caso, se crear datos adjuntos de hello usted mismo y rellenar la propiedad _media.   

Al igual que con todos los demás recursos, datos adjuntos pueden crearse, reemplazaron, eliminarán, leen o enumeran fácilmente utilizando las API de REST o cualquiera de los SDK de cliente de Hola. Como con documentos, de nivel de coherencia de los datos adjuntos de lectura Hola sigue la directiva de coherencia de hello en la cuenta de base de datos de Hola. Esta directiva se puede reemplazar en función de la solicitud dependiendo de los requisitos de coherencia de datos de su aplicación. Al consultar los datos adjuntos, Hola lee coherencia sigue Hola indización modo establecido en la colección de Hola. Para "coherente", esto sigue la directiva de coherencia de la cuenta de hello. 
 

## <a name="users"></a>Usuarios
Un usuario de Cosmos DB representa un espacio de nombres lógico para agrupar permisos. Un usuario de base de datos de Cosmos puede corresponder tooa usuario en un sistema de administración de identidad o un rol de aplicación predefinida. Para la base de datos de Cosmos, un usuario simplemente representa un toogroup abstracción un conjunto de permisos en una base de datos.   

Para implementar la arquitectura multiempresa en la aplicación, puede crear usuarios de base de datos de Cosmos que corresponde a los usuarios reales de tooyour o inquilinos de hello de la aplicación. A continuación, puede crear permisos para un usuario determinado que corresponden toohello el control de acceso a través de varias colecciones, documentos, datos adjuntos, etcetera.   

Ya que las aplicaciones deben tooscale con el crecimiento de usuarios, puede adoptar tooshard de diversas maneras los datos. Puede modelar cada usuario de la siguiente forma:   

* Cada usuario asigna tooa base de datos.
* Cada usuario asigna tooa colección. 
* Documentos correspondientes a los usuarios de toomultiple van colección tooa dedicado. 
* Documentos correspondientes a los usuarios de toomultiple van tooa conjunto de colecciones.   

Independientemente de la estrategia de particionamiento específica de Hola que elija, puede modelar los usuarios reales como los usuarios de base de datos de base de datos de Cosmos y asociar el usuario de tooeach permisos avanzados.  

![Colecciones de usuario][3]  
**Estrategias de partición y modelado de usuarios**

Como todos los demás recursos, los usuarios de base de datos de Cosmos pueden crearse, reemplazaron, eliminarán, leen o enumeran fácilmente utilizando las API de REST o cualquiera de los SDK de cliente de Hola. COSMOS DB siempre proporciona coherencia fuerte para leer o consultar los metadatos de Hola de un recurso de usuario. Es necesario aclarar que eliminar un usuario automáticamente se asegura de que no se puede tener acceso a ninguno de los permisos de hello incluidos en él. Aunque Hola DB Cosmos reclama cuota Hola de permisos de hello como parte del usuario de hello eliminado en segundo plano de hello, permisos de hello eliminado está disponible al instante nuevo para toouse.  

## <a name="permissions"></a>Permisos
Desde la perspectiva del control de acceso, los recursos como las cuentas de base de datos, las bases de datos, los usuarios y los permisos se consideran recursos *administrativos* , puesto que requieren permisos administrativos. En Hola otra parte, incluidas las colecciones de hello, documentos, datos adjuntos, procedimientos almacenados, desencadenadores, los recursos y UDF se con ámbito en una base de datos y se consideran *recursos de la aplicación*. Correspondiente toohello dos tipos de recursos y roles de Hola que tienen acceso a ellos (es decir, el Administrador de Hola y de usuario), modelo de autorización de hello define dos tipos de *las claves de acceso*: *clave maestra* y *clave de recurso*. clave maestra de Hello es una parte de la cuenta de base de datos de Hola y se proporciona para desarrolladores de toohello (o administrador) que está aprovisionando cuenta de base de datos de Hola. Dicha clave maestra tiene semántica de administrador, en que puede ser usado tooauthorize acceso tooboth administrativas y recursos de la aplicación. En cambio, una clave de recurso es una clave de acceso granular que permita acceso tooa *específico* recurso de la aplicación. Por lo tanto, captura la relación de hello entre usuario Hola de una base de datos y Hola permisos hello, usuario tiene para un recurso concreto (por ejemplo, colección, documentos, datos adjuntos, procedimiento almacenado, desencadenador o UDF).   

Hola única manera tooobtain que es una clave de recurso mediante la creación de un recurso de permiso en un usuario determinado. Tenga en cuenta que en orden toocreate o recuperar un permiso, una clave maestra se debe presentar en el encabezado de autorización de Hola. Un recurso de permiso une usuario de recurso, su acceso y Hola Hola. Después de crear un recurso de permiso, el usuario de hello solo necesita toopresent clave de recurso asociado hello en orden toogain acceso toohello relevante de recursos. Por lo tanto, una clave de recurso puede verse como una representación lógica y compacta de recurso de permiso de Hola.  

Al igual que con todos los demás recursos, permisos en la base de datos de Cosmos pueden crearse, reemplazaron, eliminarán, leen o enumeran fácilmente utilizando las API de REST o cualquiera de los SDK de cliente de Hola. COSMOS DB siempre proporciona coherencia fuerte para leer o consultar los metadatos de Hola de un permiso. 

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre cómo trabajar con recursos usando comandos HTTP en [interacciones RESTful con recursos de Cosmos DB](https://msdn.microsoft.com/library/azure/mt622086.aspx).

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png


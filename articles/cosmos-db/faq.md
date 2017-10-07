---
title: "aaaAzure DB Cosmos preguntas más frecuentes | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes sobre la base de datos de Azure Cosmos, un servicio de base de datos distribuidos globalmente, varios modelos. Obtenga más información sobre capacidad, niveles de rendimiento y escalado."
keywords: Database questions, frequently asked questions, documentdb, azure, Microsoft azure
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Preguntas más frecuentes sobre Azure Cosmos DB
## <a name="azure-cosmos-db-fundamentals"></a>Conceptos básicos de Azure Cosmos DB
### <a name="what-is-azure-cosmos-db"></a>¿Qué es Azure Cosmos DB?
Azure Cosmos DB es un servicio de base de datos de varios modelos distribuido de forma global que ofrece consultas enriquecidas de datos sin esquemas, ayuda a proporcionar un rendimiento configurable y de confianza, y posibilita un desarrollo rápido. Se se logra a través de una plataforma administrada que está respaldada por una potencia de Hola y alcance de Microsoft Azure. 

Base de datos de Azure Cosmos es la solución adecuada de hello juegos de web, móviles, y las aplicaciones de IoT cuando el rendimiento predecible, alta disponibilidad, baja latencia y un modelo de datos sin esquemas están requisitos clave. Ofrece flexibilidad de esquemas e indexación enriquecida, e incluye compatibilidad transaccional de documentos múltiples con JavaScript integrado. 

Para más preguntas de la base de datos, respuestas e instrucciones para implementar y usar este servicio, vea hello [página de documentación de la base de datos de Azure Cosmos](https://azure.microsoft.com/documentation/services/cosmos-db/).

### <a name="what-happened-toodocumentdb"></a>¿Qué problema tooDocumentDB?
Hola API de documentos es una de hello admitida las API y modelos de datos para la base de datos de Azure Cosmos. Además, Azure Cosmos DB ofrece compatibilidad con API Graph (versión preliminar), Table API (versión preliminar) y API de MongoDB. Para más información, vea [Preguntas de clientes de DocumentDB](#moving-to-cosmos-db).

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>¿Cómo obtengo toomy cuenta de DocumentDB Hola portal de Azure?
Hola portal de Azure, haga clic en el icono de base de datos de Azure Cosmos de hello en el panel izquierdo de Hola. Si tuviera una cuenta de DocumentDB antes, ahora tiene una cuenta de base de datos de Azure Cosmos, con la facturación de tooyour de ningún cambio.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>¿Qué casos de uso habitual de hello para la base de datos de Azure Cosmos?
Base de datos de Azure Cosmos es una buena elección para los juegos en dispositivos móviles, web, nuevo, y aplicaciones de IoT donde escala automática, un rendimiento predecible, el rápido orden de los tiempos de respuesta de milisegundo y Hola tooquery de capacidad sobre datos sin esquemas es importante. Base de datos de Azure Cosmos presta toorapid desarrollo y en la iteración continua de Hola de modelos de datos de aplicación. Las aplicaciones que administran contenido y datos generados por el usuario son [casos de uso comunes de Azure Cosmos DB](use-cases.md). 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>¿Cómo ofrece Azure Cosmos DB un rendimiento predecible?
A [unidad de solicitud](request-units.md) (RU) es la medida de Hola de rendimiento en la base de datos de Azure Cosmos. Un rendimiento de 1 RU corresponde rendimiento toohello de hello GET de un documento de 1 KB. Cada operación en la base de datos de Cosmos de Azure, incluidas las lecturas, escrituras, consultas SQL y las ejecuciones del procedimiento almacenado, tiene un valor de RU determinista que se basa en hello rendimiento requerido toocomplete Hola operación. En lugar de pensar en la CPU, las E/S y la memoria, y en cómo cada uno de estos aspectos afecta al rendimiento de la aplicación, es mejor que se centre en una unidad única de unidad de solicitud.

Cada contenedor de Azure Cosmos DB puede reservarse con rendimiento aprovisionado en términos de unidades de solicitud del rendimiento por segundo. Para las aplicaciones de cualquier escala, puede pruebas comparativas toomeasure de las solicitudes individuales de sus valores RU y aprovisionar un total de hello toohandle de contenedor de unidades de solicitud a través de todas las solicitudes. También puede ampliar o reducir el rendimiento de su contenedor como necesidades de Hola de evolucionar de la aplicación. Para obtener más información acerca de las unidades de solicitud y como ayuda para determinar el contenedor necesita, consulte [calcular las necesidades de rendimiento](request-units.md#estimating-throughput-needs) y pruebe hello [Calculadora de rendimiento](https://www.documentdb.com/capacityplanner). término de Hello *contenedor* aquí hace referencia la colección de API de documentos de toorefers tooa, graph API Graph, colección de API de MongoDB y tabla de API de tabla. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>¿Por qué Azure Cosmos DB admite varios modelos de datos, como pares clave-valor, columnas, documentos y gráficos?

Clave/valor (tabla), columna, documentos y datos de gráfico modelos son todas compatibles de forma nativa debido a Hola ARS (átomos, registros y las secuencias) para diseño de esa base de datos de Azure Cosmos se basa en. Átomos, registros y secuencias pueden toovarious fácilmente asignadas y proyectado modelos de datos. Hola API para un subconjunto de los modelos están disponibles en este momento (documentos, MongoDB, tabla y las API de Graph) y otros modelos de datos de tooadditional específico estará disponibles en Hola futuro.

Base de datos de Azure Cosmos tiene un esquema válido indización motor capaz de indización automáticamente todos los datos de Hola que introduce sin necesidad de ningún esquema ni índices secundarios del programador de Hola. motor de Hola se basa en un conjunto de diseños de lógica de índice (árbol invertido, columna,) que desacoplar el diseño de almacenamiento de Hola de índice de Hola y subsistemas de procesamiento de consultas. COSMOS DB también tiene un conjunto de protocolos de conexión y las API de hello capacidad toosupport de forma extensible y convertirlos eficazmente toohello core datos modelo (1) Hola índice lógico diseños y (2) lo que forma única capaz de admitir varios modelos de datos de forma nativa .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>¿Es compatible Azure Cosmos DB con HIPAA?
Sí, Azure Cosmos DB es compatible con HIPAA. HIPAA establece requisitos para hello utilizan, la divulgación de información y la protección de información de estado identificables individualmente. Para obtener más información, vea hello [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>¿Cuáles son los límites de almacenamiento de Hola de base de datos de Azure Cosmos?
No hay ningún límite toohello total de datos que un contenedor puede almacenar en la base de datos de Azure Cosmos.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>¿Cuáles son los límites de rendimiento de Hola de base de datos de Azure Cosmos?
No hay ninguna cantidad total de toohello de límite de rendimiento que puede admitir un contenedor de base de datos de Azure Cosmos. Hola idea clave es toodistribute la carga de trabajo aproximadamente uniformemente entre un número suficiente de las claves de partición.

### <a name="how-much-does-azure-cosmos-db-cost"></a>¿Cuánto cuesta Azure Cosmos DB?
Para obtener más información, consulte toohello [base de datos de Azure Cosmos detalles de precios](https://azure.microsoft.com/pricing/details/cosmos-db/) página. Azure cobra de uso de base de datos de Cosmos se determina por número de Hola de contenedores de aprovisionamiento, número de Hola de horas contenedores Hola estaban en línea y Hola aprovisionado el rendimiento para cada contenedor. término de Hello *contenedores* aquí hace referencia la colección de API de documentos toohello, graph API Graph, colección de API de MongoDB y tablas de la API de tabla. 

### <a name="is-a-free-account-available"></a>¿Existe una cuenta gratuita disponible?
Si está tooAzure nueva, puede registrarse para una [cuenta gratuita de Azure](https://azure.microsoft.com/free/), que encontrará 30 días y y un tootry de crédito todos los servicios de Azure de Hola. Si tiene una suscripción de Visual Studio, también son aptos para [libre créditos de Azure](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse para cualquier servicio de Azure. 

También puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) toodevelop y probar su aplicación localmente para liberar, sin necesidad de crear una suscripción de Azure. Cuando esté satisfecho con cómo funciona la aplicación en el emulador de base de datos de Azure Cosmos hello, puede cambiar una cuenta de base de datos de Azure Cosmos en nube de hello toousing.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>¿Cómo puedo obtener ayuda adicional con Azure Cosmos DB?
Si necesita ayuda, acérquese toous en [desbordamiento de la pila](http://stackoverflow.com/questions/tagged/azure-cosmosdb) o hello [foro de MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), o programar una conversación codo con el equipo de ingeniería de base de datos de Azure Cosmos hello mediante el envío de correo electrónico demasiado[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Configuración de Azure Cosmos DB
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>¿Cómo me registro en Azure Cosmos DB?
Base de datos de Cosmos Azure está disponible en hello portal de Azure. En primer lugar, regístrese para obtener una suscripción de Azure. Una vez se haya registrado, puede agregar una API de documentos, API de Graph (versión preliminar), la API de API de tabla (vista previa) o MongoDB cuenta tooyour suscripción de Azure.

### <a name="what-is-a-master-key"></a>¿Qué es una clave maestra?
Una clave maestra es un tooaccess de token de seguridad de todos los recursos para una cuenta. Usuarios con clave de hello tienen recursos de tooall de acceso de lectura y escritura en la cuenta de base de datos de Hola. Tenga cuidado cuando distribuya claves maestras. Hola claves de master principal y secundaria están disponibles en hello **claves** hoja de hello [portal de Azure][azure-portal]. Para más información sobre las claves, vea [Visualización, copia y regeneración de las claves de acceso](manage-account.md#keys).

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>¿Cuáles son las regiones de hello PreferredLocations se puede establecer en? 
Hola PreferredLocations valor se puede establecer tooany de hello Azure regiones en que Cosmos DB está disponible. Para obtener una lista de las regiones disponibles, vea [Regiones de Azure](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>¿Hay algo que debo tener en cuenta al distribuir los datos entre Hola mundo a través de hello centros de datos de Azure? 
Base de datos de Azure Cosmos está presente en todas las regiones de Azure, como Hola especificado en [regiones de Azure](https://azure.microsoft.com/regions/) página. Dado que es el servicio principal de hello, cada nuevo centro de datos tiene una presencia de la base de datos de Azure Cosmos. 

Al establecer una región, debe recordar que Cosmos DB respeta las nubes independientes y de administración pública. Es decir, si crea una cuenta en una región independiente, no puede replicarla fuera de dicha región. De manera similar, tampoco puede habilitar la replicación en otras ubicaciones independientes desde una cuenta externa. 

## <a name="develop-against-hello-documentdb-api"></a>Desarrollar con hello API de documentos

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>¿Cómo empezar a desarrollar contra Hola API de documentos?
API de documentos de Microsoft está disponible en hello [portal de Azure][azure-portal]. En primer lugar, debe registrarse para obtener una suscripción de Azure. Una vez que se registra para una suscripción de Azure, puede agregar documentos API contenedor tooyour suscripción de Azure. Para obtener instrucciones sobre cómo agregar una cuenta de Azure Cosmos DB, vea [Creación de una cuenta de base de datos de Azure Cosmos DB](create-documentdb-dotnet.md#create-account). Si tuviera una cuenta de DocumentDB Hola anteriores, ahora tiene una cuenta de base de datos de Azure Cosmos. 

[SDK](documentdb-sdk-dotnet.md) están disponibles para NET, Python, Node.js, JavaScript y Java. Los desarrolladores también pueden usar hello [API HTTP RESTful](/rest/api/documentdb/) toointeract con recursos de base de datos de Azure Cosmos desde varias plataformas y lenguajes.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>¿Puedo tener acceso a algunos tooget ejemplos listos para usar un punto de partida?
Ejemplos de hello documentos API [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), y [Python](documentdb-python-samples.md) SDK está disponible en GitHub.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>¿Es Hola soporte sin esquemas datos de base de datos de API de documentos?
Sí, Hola documentos API permite que los documentos JSON aplicaciones toostore arbitrarios sin definiciones de esquema o sugerencias. Datos están inmediatamente disponibles para consulta a través de la interfaz de consulta de base de datos SQL de Azure Cosmos Hola.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>¿Hola API de documentos admite transacciones ACID?
Sí, Hola API de documentos admite transacciones de entre documentos expresadas como desencadenadores y procedimientos almacenados de JavaScript. Las transacciones son ámbito tooa única partición dentro de cada colección y ejecuta con semántica ACID como "todo o nada," aislada de otras solicitudes de usuario y el código concurrentemente. Si se detectan excepciones mediante la ejecución de servidor hello de código de la aplicación de JavaScript, Hola toda la transacción se revierte. Para obtener más información sobre las transacciones, consulte [Transacciones del programa de base de datos](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>¿Qué es una colección?
Una colección es un grupo de documentos y su lógica de aplicación de JavaScript asociada. Una colección es una entidad facturable, donde hello [costo](performance-levels.md) viene determinado por el rendimiento de Hola y usado el almacenamiento. Las colecciones pueden abarcar uno o más servidores o las particiones y puede escalarse toohandle prácticamente ilimitados volúmenes de almacenamiento o de rendimiento.

Las colecciones también son entidades de facturación de hello para la base de datos de Azure Cosmos. Cada colección se factura por horas, en función de rendimiento aprovisionado hello y espacio de almacenamiento usado. Para más información, vea los [precios de Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>¿Cómo se crea una base de datos?
Puede crear bases de datos mediante el uso de hello [portal de Azure](https://portal.azure.com), tal y como se describe en [agregar una colección](create-documentdb-dotnet.md#create-collection), uno de hello [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md), o hello [delasAPIdeREST](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>¿Cómo se configuran los usuarios y los permisos?
Puede crear usuarios y permisos mediante uno de hello [SDK de API de base de datos de Cosmos](documentdb-sdk-dotnet.md) o hello [API de REST](/rest/api/documentdb/).  

### <a name="does-hello-documentdb-api-support-sql"></a>¿Hola API de documentos admite SQL?
Hola lenguaje de consulta SQL es un subconjunto mejorado de la funcionalidad de consulta de Hola que sea compatible con SQL. Hola lenguaje de consulta de base de datos SQL de Azure Cosmos proporciona operadores relacionales y jerárquicos enriquecidos y extensibilidad a través de funciones basadas en JavaScript, definido por el usuario (UDF). Gramática JSON se permite para el modelado de documentos JSON como árboles de nodos con la etiqueta, que usan técnicas de indización automática de la base de datos de Azure Cosmos hello y dialecto de consulta SQL Hola de base de datos de Azure Cosmos. Para obtener información sobre el uso de la gramática de SQL, vea hello [QueryDocumentDB] [ query] artículo.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>¿Es Hola funciones de agregación de SQL de compatibilidad de API de documentos?
Hola documentos API compatible con la agregación de baja latencia en cualquiera de ellas a través de las funciones de agregado `COUNT`, `MIN`, `MAX`, `AVG`, y `SUM` a través de hello gramática de SQL. Para más información, consulte [Funciones de agregado](documentdb-sql-query.md#Aggregates).

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>¿Cómo proporciona simultaneidad Hola API de documentos?
Hola documentos API es compatible con el control de simultaneidad optimista (OCC) a través de etiquetas de entidad HTTP o ETags. Cada recurso de la API de documentos tiene un valor ETag y Hola ETag se establece en el servidor de hello cada vez que se actualiza un documento. encabezado de ETag de Hola y el valor actual de Hola se incluyen en todos los mensajes de respuesta. ETags puede utilizarse con hello If-Match encabezado tooallow Hola servidor toodecide si se debe actualizar un recurso. Hola valor If-Match es toobe de valor de ETag Hola rebasa. Si Hola valor ETag coincide con servidor hello valor ETag, se actualiza el recurso de Hola. Si ya no es actual Hola ETag, servidor hello rechazará las operaciones de hello con un "HTTP 412 Error de condición previa" código de respuesta. cliente de Hello, a continuación, volver a captura Hola recursos tooacquire Hola el valor ETag actual para el recurso de Hola. Además, ETags puede utilizarse con toodetermine de encabezado If-None-Match de hello si es necesario capturar volver a un recurso.

toouse simultaneidad optimista en. NET, use hello [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) clase. Para obtener un ejemplo. NET, vea [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) en el ejemplo de Hola a DocumentManagement en GitHub.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>¿Cómo se puede realizar transacciones en hello API de documentos?
Hola documentos API es compatible con language integrated transacciones a través de desencadenadores y procedimientos almacenados de JavaScript. Todas las operaciones de base de datos contenidas en scripts se ejecutan con aislamiento de instantánea. Si es una colección única partición, ejecución de hello es colección toohello con ámbito. Si la colección de hello tiene particiones, la ejecución de hello está toodocuments ámbito con hello mismo valor de clave de partición dentro de la colección de Hola. Una instantánea de versiones del documento hello (ETags) se deja al principio de Hola de transacción de Hola y confirmada solo si el script de Hola se realiza correctamente. Si Hola JavaScript produce un error, se revierten las transacciones de Hola. Para más información, vea [Programación de JavaScript en el lado del servidor de Azure Cosmos DB](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>¿Cómo se pueden insertar documentos de forma masiva en Cosmos DB?
Hay dos maneras de insertar documentos de forma masiva en Azure Cosmos DB:

* herramienta de migración de datos Hello, como se describe en [herramienta de migración de base de datos para la base de datos de Azure Cosmos](import-data.md).
* Procedimientos almacenados, como se describe en [Programación de JavaScript en el lado del servidor de Azure Cosmos DB](programming.md).

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>¿Hola API de documentos admite el almacenamiento en caché de vínculo de recursos?
Sí. Como Azure Cosmos DB es un servicio RESTful, los vínculos de recursos son inmutables y se pueden almacenar en caché. Los clientes de la API de documentos pueden especificar un encabezado de "If-None-Match" para lecturas en cualquier tipo de recurso de documento o la colección y, a continuación, actualizar sus copias locales después de que ha cambiado la versión del servidor hello.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>¿Hay disponible una instancia local de la API de DocumentDB?
Sí. Hola [emulador de base de datos de Azure Cosmos](local-emulator.md) proporciona una emulación de alta fidelidad de hello servicio base de datos de Cosmos. Admite la funcionalidad que es idéntica tooAzure Cosmos DB, incluida la compatibilidad para crear y consultar documentos JSON, aprovisionamiento y ajuste de escala en las colecciones y ejecutar procedimientos almacenados y desencadenadores. Puede desarrollar y probar aplicaciones mediante el uso de hello Azure Cosmos DB emulador e implementarlos tooAzure en una escala global mediante la realización de una sola configuración cambiar toohello extremo de la conexión de base de datos de Azure Cosmos.

## <a name="develop-against-hello-api-for-mongodb"></a>Desarrollar con hello API para MongoDB
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>¿Qué es hello API de base de datos de Azure Cosmos para MongoDB?
Hola API de base de datos de Azure Cosmos para MongoDB es una capa de compatibilidad que permite que las aplicaciones tooeasily y transparente comunicarse con el motor de base de datos de base de datos de Azure Cosmos nativo hello mediante existente, admitido por la Comunidad Apache MongoDB APIs y controladores. Los desarrolladores pueden usar ahora MongoDB herramienta cadenas y las capacidades toobuild las aplicaciones existentes que aprovechan las ventajas de la base de datos de Azure Cosmos. Los desarrolladores pueden beneficiarse de capacidades únicas Hola de base de datos de Azure Cosmos, que incluyen mantenimiento de copia de seguridad, la indización automática, contratos de nivel de servicio respaldado financieramente (SLA) y así sucesivamente.

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>¿Cómo conecto toomy API de base de datos de MongoDB?
Hola toohello de tooconnect de manera más rápida API de base de datos de Azure Cosmos para MongoDB es toohead sobre toohello [portal de Azure](https://portal.azure.com). Tooyour cuenta y, a continuación, en el menú de navegación izquierdo de hello, haga clic en **inicio rápido**. Inicio rápido es Hola mejor manera tooget código fragmentos tooconnect tooyour base de datos. 

Azure Cosmos DB aplica estándares y requisitos de seguridad estrictos. Cuentas de base de datos de Cosmos Azure requieren autenticación y comunicación segura mediante SSL, por lo que realmente toouse TLSv1.2.

Para obtener más información, consulte [conectar tooyour API de base de datos de MongoDB](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>¿Existen otros códigos de error para una base de datos de la API de MongoDB?
En los códigos de error de MongoDB comunes de suma toohello, Hola MongoDB API tiene sus propios códigos de error específicos:


| Error               | Código  | Descripción  | Solución  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | número total de Hola de unidades de solicitud consumido ha superado la velocidad de unidad de solicitud de aprovisionamiento de hello para la recopilación de Hola y se ha limitado. | Considere la posibilidad de escalar el rendimiento de Hola de recopilación de Hola de hello portal de Azure o volver a intentar. |
| ExceededMemoryLimit | 16501 | Como un servicio multiempresa, operación Hola ha superado la asignación de memoria del cliente de Hola. | Reducir el ámbito de Hola de operación de Hola a través de los criterios de consulta más restrictivos o póngase en contacto con soporte técnico de hello [portal de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>Ejemplo: *&nbsp;&nbsp;&nbsp;&nbsp;db.getCollection('users').aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Desarrollar con hello API de tabla (vista previa)

### <a name="terms"></a>Términos 
base de datos de Azure Cosmos Hello: API de tabla (vista previa) se refiere toohello mejor oferta por base de datos de Azure Cosmos para compatibilidad con tablas anunciada en la compilación de 2017. 

tabla estándar de Hello SDK es tabla de almacenamiento de Azure existente Hola SDK. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>¿Cómo se puede usar la nueva oferta de API de tabla (vista previa) Hola? 
Hola API de tabla de base de datos de Azure Cosmos está disponible en hello [portal de Azure][azure-portal]. En primer lugar, debe registrarse para obtener una suscripción de Azure. Una vez se haya registrado, puede agregar un tooyour de cuenta de la API de tabla de base de datos de Azure Cosmos suscripción de Azure y, a continuación, agregue la cuenta de tooyour de tablas. 

Durante el período de vista previa de hello, cuando [SDK](../cosmos-db/table-sdk-dotnet.md) están disponibles para. NET, puede empezar a siguiendo hello [API tabla](../cosmos-db/create-table-dotnet.md) artículo de inicio rápido.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>¿Necesito una Hola de toouse SDK nuevas API de tabla (vista previa)? 
Sí, Hola [almacenamiento Premium tabla (vista previa) SDK de Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) está disponible en NuGet. Información adicional está disponible en hello [API de .NET de tabla de base de datos de Azure Cosmos: descargar y notas de la versión](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) página. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>¿Cómo se puede proporcionar comentarios sobre Hola SDK o errores?
Puede compartir sus comentarios en cualquiera de hello siguientes maneras:

* [UserVoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [Foro de MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>¿Qué es la cadena de conexión de Hola que necesito toouse tooconnect toohello API de tabla (vista previa)?
cadena de conexión de Hello es:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
Puede obtener la cadena de conexión de Hola desde la página de claves de Hola Hola portal de Azure. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>¿Cómo se puede invalidar los valores de configuración de Hola de opciones de solicitud de hello en hello nueva tabla API (versión preliminar)?
Para información sobre las opciones de configuración, vea [Funcionalidades de Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Puede cambiar configuración de hello agregándolas tooapp.config en la sección appSettings de hello en la aplicación de cliente de Hola.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>¿Existen cambios para los clientes que están utilizando Hola tabla estándar existente SDK?
Ninguno. No hay ningún cambio para los clientes nuevos o existentes que están utilizando la tabla estándar existente SDK de Hola. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>¿Cómo se pueden ver los datos de la tabla que se almacenan en la base de datos de Azure Cosmos para su uso con hello API de tabla (revisión)? 
Puede usar datos de saludo de hello toobrowse de portal de Azure. También puede utilizar Hola código de la API de tabla (vista previa) o herramientas de hello mencionadas en la siguiente respuesta de Hola. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>¿Las herramientas que funcionan con hello API de tabla (vista previa)? 
Puede usar la versión anterior de hello del explorador de Azure (0.8.9).

Herramientas con hello flexibilidad tootake una cadena de conexión en formato de hello especificado anteriormente puede admitir Hola nueva API de tabla (vista previa). Se proporciona una lista de herramientas de tabla en hello [herramientas de cliente de almacenamiento de Azure](../storage/common/storage-explorers.md) página. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>¿PowerShell o CLI de Azure funcionan con hello nueva tabla API (versión preliminar)?
Tenemos previsto tooadd compatibilidad con PowerShell y la CLI de Azure para la API de tabla (vista previa). 

### <a name="is-hello-concurrency-on-operations-controlled"></a>¿Es la simultaneidad de hello en operaciones controladas?
Sí, simultaneidad optimista se proporciona a través de uso de Hola de mecanismo de ETag Hola. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>¿Se hello modelo de consulta OData compatibles con entidades? 
Sí, Hola API de tabla (vista previa) admite las consultas de OData y consulta LINQ. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>¿Puedo conectar toohello tabla de Azure estándar y premium nuevas API de tabla (vista previa) en paralelo en hello Hola misma aplicación? 
Sí, puede conectarse mediante la creación de dos instancias independientes de hello CloudTableClient, uno que apunta tooits posee URI a través de la cadena de conexión de Hola.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>¿Cómo se puede migrar una existente tabla de Azure aplicación toothis nueva oferta de almacenamiento?
tootake aprovechar la nueva oferta de API de tabla hello en los datos de almacenamiento de tabla existentes, póngase en contacto con [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com). 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>¿Qué es la guía básica de Hola para este servicio y, cuando se le ofrece otra funcionalidad de API de tabla estándar?
Tenemos previsto tooadd compatibilidad con SAS tokens, contexto de servicio, estadísticas, cliente lado cifrado, análisis y otras características conforme avancemos hacia la disponibilidad general. Háganos sus comentarios en [UserVoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api). 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>¿Es la expansión de realizar para este servicio si, por ejemplo, empezar con el tamaño de almacenamiento de hello  *n*  GB de datos y Mis datos crecerá too1 TB con el tiempo? 
Base de datos de Azure Cosmos es tooprovide diseñado un almacenamiento ilimitado; a través del uso de Hola de escalado horizontal. servicio de Hello puede supervisar y aumentar el almacenamiento de forma eficaz. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>¿Cómo supervisar la oferta de la API de tabla (vista previa) de hello?
Puede usar hello API de tabla (vista previa) **métricas** panel toomonitor solicitudes y el uso de almacenamiento. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>¿Cómo se puede calcular el rendimiento de hello que necesito?
Puede usar Hola de toocalculate Estimador de hello capacidad TableThroughput necesario para las operaciones de Hola. Para más información, vea [Estimate Request Units and Data Storage](https://www.documentdb.com/capacityplanner) (Cálculo de unidades de solicitud y almacenamiento de datos). En general, puede representar la entidad como JSON y proporcionar números de Hola para las operaciones. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>¿Puedo usar Hola nueva API de tabla (vista previa) SDK localmente con emulator Hola?
Sí, puede usar Hola API de tabla (vista previa) con un emulador local hello cuando usas Hola nuevo SDK. nuevo emulador toodownload, vaya demasiado[Hola Use el emulador de base de datos de Azure Cosmos para desarrollo local y las pruebas](local-emulator.md). Hola StorageConnectionString valor en un archivo app.config debe toobe:

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>¿Puede mi aplicación existente funciona con hello API de tabla (vista previa)? 
área expuesta de Hola de hello nueva API de tabla (vista previa) es compatible con hello tabla estándar Azure SDK en hello crear, eliminar, actualizar y operaciones en hello .NET API de consulta existente. Asegúrese de que tiene una clave de fila, ya que Hola API de tabla (vista previa) requiere una clave de partición y una clave de fila. También planeamos tooadd más soporte técnico SDK conforme avancemos hacia la disponibilidad general de esta oferta de servicio.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>¿Necesito toomigrate mi toohello existente de las aplicaciones basadas en tablas de Azure SDK nueva si no deseo usar características de la API de tabla (vista previa) de toouse Hola?
No, se pueden crear y usar recursos de tabla estándar existentes sin interrupciones de ningún tipo. Sin embargo, si no utiliza Hola nueva API de tabla (vista previa), no se pueden beneficiar de índice automáticas de hello, opción de coherencia adicionales de Hola o distribución global. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>¿Cómo se agrega la replicación de datos de hello en premium Hola API de tabla (vista previa) en varias regiones de Azure?
Puede usar del portal de base de datos de Azure Cosmos hello [configuración de replicación global](tutorial-global-distribution-documentdb.md#portal) tooadd regiones que son adecuadas para la aplicación. toodevelop una aplicación distribuida globalmente, también debe agregar la aplicación con hello PreferredLocation información conjunto toohello región local para proporciona baja latencia de lectura. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>¿Cómo se cambia la región de escritura principal de hello para la cuenta de hello en premium Hola API de tabla (vista previa)?
Puede usar Hola base de datos de Azure Cosmos replicación global panel del portal tooadd una región y, a continuación, conmutar por error toohello necesario región. Para obtener instrucciones, vea [Developing with multi-region Azure Cosmos DB accounts](regional-failover.md) (Desarrollo con cuentas de Azure Cosmos DB de varias regiones). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>¿Cómo se configuran las regiones de lectura preferidas con una baja latencia al distribuir los datos? 
toohelp leer desde la ubicación local de hello, use la clave de PreferredLocation de hello en el archivo app.config de hello. Para las aplicaciones existentes, Hola API de tabla (vista previa) produce un error si se establece LocationMode. Quitar ese código, porque premium Hola API de tabla (vista previa) recoge esta información del archivo app.config de hello. Para más información, vea [Funcionalidades de Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>¿Cómo debo pensar sobre los niveles de coherencia en hello API de tabla (vista previa)? 
Azure Cosmos DB ofrece contrapartidas bien fundamentadas entre coherencia, disponibilidad y latencia. Base de datos de Azure Cosmos ofrece cinco niveles de coherencia tooTable desarrolladores de API (versión preliminar), por lo que puede elegir el modelo de coherencia derecho de hello en el nivel de tabla de Hola y realizar solicitudes individuales al consultar los datos de Hola. Al conectarse, el cliente puede especificar un nivel de coherencia. Puede cambiar el nivel de Hola a través de la configuración de app.config de Hola para valor de Hola de clave de TableConsistencyLevel Hola. 

Hola API de tabla (vista previa) proporciona baja latencia lee con "leer sus propias operaciones de escritura," con coherencia de la sesión como valor predeterminado de Hola. Para más información, consulte [Niveles de coherencia](consistency-levels.md). 

De forma predeterminada, el almacenamiento de tabla de Azure proporciona homogeneidad dentro de una región y coherencia Eventual en ubicaciones de hello secundaria. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>¿Ofrece Azure Cosmos DB más niveles de coherencia que las tablas estándar?
Sí, para obtener información acerca de cómo toobenefit de hello distribuye la naturaleza de la base de datos de Azure Cosmos, consulte [niveles de coherencia](consistency-levels.md). Dado que se proporcionan garantías para los niveles de coherencia de hello, puede utilizarlos con confianza. Para más información, vea [Funcionalidades de Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>¿Cuando se habilita la distribución global, cuánto tiempo toman los datos de hello tooreplicate?
Se confirmación datos Hola manera duradera en la región local Hola e inserción tooother regiones de datos de hello inmediatamente en cuestión de milisegundos. Esta replicación es dependiente sólo puntualmente Hola ida y vuelta (RTT) del centro de datos de Hola. toolearn más información acerca de la capacidad de distribución global de Hola de base de datos de Cosmos de Azure, consulte [base de datos de Azure Cosmos: un servicio de base de datos distribuidos globalmente en Azure](distribute-data-globally.md).

### <a name="can-hello-read-request-consistency-level-be-changed"></a>¿Nivel de coherencia de solicitud de lectura de Hola se puede cambiar?
Con la base de datos de Cosmos de Azure, puede establecer el nivel de coherencia de hello en el nivel de contenedor de hello (en la tabla de hello). Mediante el uso de hello SDK, puede cambiar nivel de hello, proporcionando el valor de hello para la clave de TableConsistencyLevel en el archivo app.config de hello. Hola los valores posibles son: Strong, Bounded Staleness, Session, prefijo coherente y Eventual. Para más información, vea [Niveles de coherencia de datos optimizables en Azure Cosmos DB](consistency-levels.md). idea clave Hello es que no se puede establecer coherencia de la solicitud de hello nivel en más de configuración de hello para la tabla de Hola. Por ejemplo, no puede establecer el nivel de coherencia de hello para la tabla de hello en Eventual y el nivel de coherencia de solicitud de hello en seguro. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>¿Cómo maneja cuenta de la API de tabla (vista previa) de hello premium conmutación por error si una región se bloquea? 
premium Hola API de tabla (vista previa) toma prestado de plataforma distribuidos globalmente de Hola de base de datos de Azure Cosmos. tooensure que la aplicación puede tolerar un tiempo de inactividad de centro de datos, habilite al menos una región más de cuenta de hello en el portal de base de datos de Azure Cosmos hello [desarrollar con cuentas de base de datos de Azure Cosmos varias regiones](regional-failover.md). Puede establecer la prioridad de Hola de región de hello mediante el portal de hello [desarrollar con cuentas de base de datos de Azure Cosmos varias regiones](regional-failover.md). 

Puede agregar tantas áreas como desee para la cuenta de hello y controlar dónde puede conmutar por error tooby proporciona una prioridad de conmutación por error. Por supuesto, la base de datos de hello toouse, necesita demasiado tooprovide una aplicación no existe. Al hacerlo, los clientes no experimentarán tiempo de inactividad. SDK de cliente de Hello es auto ubicación. Es decir, puede detectar la región Hola que está inactivo y conmutar por error automáticamente toohello nueva región.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>¿Está habilitada premium Hola API de tabla (vista previa) para las copias de seguridad?
Sí, premium Hola API de tabla (vista previa) toma prestado de plataforma de Hola de base de datos de Azure Cosmos para copias de seguridad. Se realizan copias de seguridad automáticamente. Para más información, vea [Copias de seguridad y restauración automáticas en línea con Azure Cosmos DB](online-backup-and-restore.md).

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>¿Hola API de tabla (vista previa) índice todos los atributos de una entidad de forma predeterminada?
Sí, todos los atributos de una entidad se indexan de forma predeterminada. Para más información, vea [Directivas de indexación de Azure Cosmos DB](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>¿Significa esto no tengo toocreate varias consultas de índices toosatisfy Hola? 
Sí, Azure Cosmos DB ofrece indexación automática de todos los atributos sin ninguna definición de esquema. Esta automatización libera a los desarrolladores toofocus en aplicación hello en lugar de en la administración y creación de índices. Para más información, vea [Directivas de indexación de Azure Cosmos DB](indexing-policies.md).

### <a name="can-i-change-hello-indexing-policy"></a>¿Puedo cambiar la directiva de indexación de hello?
Sí, puede cambiar la directiva de indexación de Hola proporcionando la definición del índice Hola. Para más información, vea [Funcionalidades de Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Necesita tooproperly codificar y configuración de Hola de escape. 

Json en formato de cadena en el archivo app.config de hello:
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>Azure DB Cosmos como una plataforma parece toohave muchas capacidades, como la ordenación, agregados, jerarquía y otras funcionalidades. ¿Agregará estas toohello funciones API de tabla? 
En la vista previa, Hola API de tabla proporciona Hola misma consulta funcionalidad como almacenamiento de tabla de Azure. Azure Cosmos DB también admite ordenación, agregados, consulta geoespacial, jerarquía y una amplia variedad de funciones integradas. Se proporcionará una funcionalidad adicional en hello API de tabla en una actualización de servicio futura. Para más información, vea, [Consultas SQL para la API de DocumentDB de Azure Cosmos DB](../documentdb/documentdb-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>¿Cuándo debo cambiar TableThroughput de Hola API de tabla (vista previa)?
Se deben cambiar TableThroughput cuando se cumple alguna de hello condiciones siguientes:
* Va a realizar una extracción, transformación y carga (ETL) de datos, o quiere tooupload una gran cantidad de datos en un período corto de tiempo. 
* Necesita más rendimiento del contenedor de hello en el back-end de Hola. Por ejemplo, verá que rendimiento hello usa es mayor que el rendimiento aprovisionado hello y está obteniendo limitados. Para más información, vea [Configuración del rendimiento para contenedores de Azure Cosmos DB](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>¿Puedo aumentar o reducir el rendimiento de saludo de la tabla de la API de tabla (vista previa)? 
Sí, puede usar el rendimiento del portal de base de datos de Azure Cosmos Hola escala panel tooscale Hola. Para más información, vea [Establecimiento del rendimiento](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>¿Existe un TableThroughput predeterminado que se establezca para tablas recién aprovisionadas?
Sí, si no invalide hello TableThroughput a través de app.config y no utilice un contenedor creado previamente en la base de datos de Azure Cosmos, servicio de hello crea una tabla con un rendimiento de 400.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>¿Hay algún cambio de precios para los clientes existentes de la API de tabla estándar de hello?
Ninguno. No hay ningún cambio de precio para los clientes existentes de Standard Table API. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>¿Cómo se calcula el precio de Hola para hello API de tabla (vista previa)? 
precio de Hello depende de hello asignado TableThroughput. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>¿Cómo se puede controlar cualquier limitación en las tablas de Hola de API de tabla (vista previa) de la oferta? 
Si tasa de solicitud de hello supera la capacidad de Hola de rendimiento aprovisionado Hola de contenedor subyacente hello, obtendrá un error y Hola SDK volverá a intentar Hola llamada mediante la aplicación de directiva de reintentos de Hola.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>¿Por qué necesito un rendimiento además de PartitionKey y RowKey tootake aprovechar oferta de API de tabla (vista previa) de hello premium de base de datos de Azure Cosmos toochoose?
Base de datos de Azure Cosmos establece un rendimiento de manera predeterminada para el contenedor si no se proporciona uno en el archivo app.config de hello. 

Azure Cosmos DB ofrece garantías de rendimiento y latencia con límites superiores por operación. Esta garantía es posible cuando el motor de hello puede aplicar la regulación de las operaciones del inquilino de Hola. Establecer TableThroughput garantiza que obtendrá Hola garantiza el rendimiento y la latencia, porque la plataforma Hola reserva esta capacidad y garantiza el funcionamiento correcto. 

Mediante el uso de especificación de rendimiento de hello, elásticamente puede cambiarlo toobenefit de estacionalidad hello de la aplicación, satisfacer necesidades de rendimiento de Hola y ahorrar costes.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>SDK de almacenamiento de Azure ha sido muy económica para mí, dado que tengo que pagar solo datos de hello toostore y raramente de consulta. nueva oferta de base de datos de Azure Cosmos Hola parece toobe me está cargando aunque no he realizado una sola transacción ni almacena nada. ¿Puede explicarse?

Base de datos de Azure Cosmos es toobe diseñado un sistema basado en SLA, distribuido globalmente con garantías de disponibilidad, latencia y rendimiento. Al reservar el rendimiento en la base de datos de Azure Cosmos, se garantiza que, a diferencia de rendimiento de Hola de otros sistemas. Azure Cosmos DB ofrece funcionalidades adicionales que los clientes han solicitado, como índices secundarios y distribución global. Durante el período de vista previa de hello, se proporcionan un modelo de rendimiento optimizado y, finalmente, tenemos previsto tooprovide un modelo de almacenamiento optimizado toomeet necesidades de nuestros clientes. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>Nunca aparece una notificación de “cuota completa" (que indica que una partición está completa) cuando se ingieren datos en Table Storage. Con hello API de tabla (vista previa), aparece un mensaje. ¿Esto ofrece limitarme y forzar me toochange mi aplicación existente?

Azure Cosmos DB es un sistema basado en contratos de nivel de servicio que ofrece escalado ilimitado con garantías de latencia, rendimiento, disponibilidad y coherencia. tooensure garantiza un rendimiento premium, asegúrese de que el tamaño de los datos y el índice son escalables y fáciles de administrar. límite de 10 GB de Hello en número de Hola de entidades o elementos por la clave de partición es tooensure que es proporcionar un gran rendimiento de búsqueda y consulta. tooensure que la aplicación se escala bien, incluso para el almacenamiento de Azure, se recomienda que se *no* crear una partición activa por almacenar toda la información en una partición y realizar consultas sobre estos. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>¿Por lo que PartitionKey y RowKey son necesarios con Hola nueva API de tabla (vista previa)? 
Sí. Porque el área expuesta de Hola de hello API de tabla (vista previa) está toothat similar de hello SDK de almacenamiento de tabla, clave de partición de hello proporciona una manera eficaz toodistribute Hola de datos. clave de fila de Hello es único dentro de esa partición. Hola toobe de necesidades de clave de fila está presente y no puede ser null, como en Hola SDK estándar. longitud de Hola de RowKey es 255 bytes y longitud de Hola de PartitionKey es 100 bytes (pronto toobe aumentar too1 KB). 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>¿Cuáles son los mensajes de error de Hola para hello API de tabla (vista previa)?
Dado que esta versión preliminar es compatible con la tabla estándar de hello, la mayoría de los errores de hello asignará toohello errores de tabla estándar de Hola. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>¿Por qué obtener limitada cuando intento toocreate mucha tablas uno tras otro en hello API de tabla (vista previa)?
Azure Cosmos DB es un sistema basado en contratos de nivel de servicio que ofrece garantías de latencia, rendimiento, disponibilidad y coherencia. Dado que es un sistema de aprovisionamiento, se reservan recursos tooguarantee estos requisitos. tasa rápido Hola de creación de tablas se detecta y limitada. Se recomienda que examine tasa de Hola de creación de tablas y bajarlo a que no requiere herramientas que 5 por minuto. Recuerde que Hola API de tabla (vista previa) es un sistema de aprovisionamiento. momento de Hello aprovisionarla, se iniciará toopay para él. 

## <a name="develop-against-hello-graph-api-preview"></a>Desarrollar con hello API Graph (versión preliminar)
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>¿Cómo puedo aplicar funcionalidad Hola de API de Graph (versión preliminar) tooAzure Cosmos DB?
Puede usar una funcionalidad de Hola de tooapply de biblioteca de extensión de la API de Graph (versión preliminar). Esta biblioteca se denomina Microsoft Azure Graphs y está disponible en NuGet. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Parece que admite el lenguaje de cruce seguro de hello Gremlin gráfico. ¿Tiene pensado tooadd más formas de consulta?
Sí, tenemos previsto tooadd otros mecanismos de consulta en hello futuras. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>¿Cómo se puede usar la nueva oferta de API de Graph (versión preliminar) Hola? 
Hola de introducción, completa tooget [API Graph](../cosmos-db/create-graph-dotnet.md) artículo de inicio rápido.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>Preguntas de clientes de DocumentDB
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>¿Por qué se está moviendo tooAzure Cosmos DB? 

Azure DB Cosmos es bisiesto big siguiente de hello en distribuidos globalmente, bases de datos de nube a escala. Como cliente de documentos, ahora tiene acceso toohello importante sistema y las capacidades ofrecidas por base de datos de Azure Cosmos.

Base de datos de Azure Cosmos se inició como "Proyecto Florence" en los puntos débiles de 2010 tooaddress Hola se enfrentan los desarrolladores en la creación de aplicaciones a gran escala en Microsoft. desafíos de Hello de la creación de aplicaciones distribuidas globalmente no son tooMicrosoft único, por lo que hemos realizado Hola primera generación de esta tecnología disponible en los desarrolladores de 2015 tooAzure en forma de Hola de documentos de Azure. 

Desde ese momento, hemos agregado nuevas características e incorporado nuevas funcionalidades significativas. Base de datos de Azure Cosmos es resultado de hello. Como parte de esta versión de Azure Cosmos DB, los clientes de DocumentDB (con sus datos) se convierten automáticamente en clientes de Azure Cosmos DB. Estas capacidades están en áreas de Hola de motor de base de datos central de hello, así como distribución global, escalabilidad elástica y SLA líderes en la industria y completas. En concreto, hicimos evolucionar mapa de hello base de datos de Azure Cosmos base de datos motor tooefficiently todos los modelos de datos muy popular, sistemas de tipos y las API toohello subyacente modelo de datos de base de datos de Azure Cosmos. 

Hola manifestación de desarrollador orientado actual de este trabajo es Hola nueva compatibilidad con [Gremlin](../cosmos-db/graph-introduction.md) y [API de almacenamiento de tablas](../cosmos-db/table-introduction.md). Y simplemente Hola inicio. Tenemos previsto tooadd otras API populares y modelos de datos más recientes con el tiempo, con los avances más rendimiento y almacenamiento a escala global. 

Es importante toopoint out que hello DocumentDB [dialecto SQL](../documentdb/documentdb-sql-query.md) siempre ha sido solo uno de hello muchas API que Hola subyacente Azure Cosmos DB puede admitir. Para los desarrolladores que utilizan un servicio completamente administrado, como la base de datos de Azure Cosmos, hello solo interfaz toohello servicio es hello las API expuestas por el servicio de Hola. Nada cambia realmente para los clientes existentes de DocumentDB. En la base de datos de Azure Cosmos, obtendrá exactamente Hola que ofrece el mismo SQL API que documentos. Y ahora (y en hello futuras), puede tener acceso a otras capacidades previamente inaccesibles 

Otra manifestación de nuestro trabajo continuo es base hello extendido global y elástica la escalabilidad del rendimiento y almacenamiento. Hemos realizado varias mejoras fundamentales toohello subsistema de distribución global. Uno de hello muchas características desarrollador orientado es Hola prefijo coherente modelo de coherencia, lo que hace un total cinco modelos de coherencia bien definido. Publicaremos muchas más funcionalidades interesantes a medida que vayan tomando forma. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>¿Qué necesito tooensure toodo que los recursos de DocumentDB continúan toorun en la base de datos de Azure Cosmos?

No debe toomake ningún cambio en absoluto. Los recursos de DocumentDB ahora son recursos de base de datos de Azure Cosmos y no había ninguna interrupción del servicio de hello cuando se produjo este movimiento.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>¿Qué cambios se necesita toomake para mi toowork de aplicación con la base de datos de Azure Cosmos?

No hay ningún toomake cambios. Las clases, los espacios de nombres y los paquetes NuGet no han cambiado. Como siempre, se recomienda que mantenga el SDK de la ventaja de tootake toodate de hello últimas características y mejoras. 

### <a name="whats-changed-in-hello-azure-portal"></a>¿Qué ha cambiado en hello portal de Azure?

Documentos ya no aparece en el portal de Hola como un servicio de Azure. En su lugar es un nuevo icono de la base de datos de Azure Cosmos, como se muestra en hello después de la imagen. Todas las colecciones están disponibles tal y como se encontraban antes y aún puede escalar el rendimiento, cambiar la coherencia y supervisar los contratos de nivel de servicio. se han mejorado las capacidades de Hola de explorador de datos (vista previa). Ahora puede ver y editar documentos, crear y ejecutar consultas y trabajar con procedimientos almacenados, desencadenadores y UDF desde una sola página, como se muestra en hello después de imagen: 

![hoja de colecciones de base de datos de Azure Cosmos Hola](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>¿Existen cambios toopricing?

No, costo de Hola de ejecutar la aplicación en la base de datos de Azure Cosmos es Hola igual que estaba antes.

### <a name="are-there-changes-toohello-slas"></a>¿Son existen cambios toohello SLA?

No, Hola SLA de disponibilidad, coherencia, la latencia y rendimiento se modifican y se siguen mostrando en el portal de Hola. Para más información, vea [Contrato de nivel de servicio para Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/).
   
![Aplicación de tareas pendientes con datos de ejemplo](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md

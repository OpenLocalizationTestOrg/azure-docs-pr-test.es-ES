---
title: aaaExpire datos en la base de datos de Azure Cosmos con hora toolive | Documentos de Microsoft
description: "Con TTL, base de datos de Microsoft Azure Cosmos proporciona documentos toohave Hola capacidad que se purgan automáticamente del sistema de hello tras un período de tiempo."
services: cosmos-db
documentationcenter: 
keywords: tiempo toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Punto de expirar datos en colecciones de base de datos de Azure Cosmos automáticamente con hora toolive
Las aplicaciones pueden generar y almacenar enormes cantidades de datos. Algunos de estos datos, como los datos de eventos, los registros y la información de sesión de usuario que se generan automáticamente, solo son útiles durante un tiempo finito. Una vez datos Hola se convierte en exceso toohello las necesidades de aplicación hello es toopurge seguro para estos datos y reducir las necesidades de almacenamiento de Hola de una aplicación.

Con "tiempo toolive" o TTL, base de datos de Microsoft Azure Cosmos proporciona documentos de toohave de capacidad de hello purgados de base de datos de hello automáticamente tras un período de tiempo. tiempo predeterminado de Hello toolive se puede establecer en el nivel de colección de Hola y se reemplaza en una base de cada documento. Una vez que se establece el TTL, como un valor predeterminado de la colección o en un nivel de documento, Cosmos DB quita automáticamente los documentos que existen después de ese período de tiempo, en segundos, desde que se modificaron por última vez.

Tiempo toolive en la base de datos de Cosmos usa un desplazamiento con respecto al documento Hola se modificó por última vez. toodo este equipo de TI usa hello `_ts` campo que se encuentra en cada documento. campo de _ts Hello es una hora y fecha que representan Hola de estilo unix época marca de tiempo. Hola `_ts` campo se actualiza cada vez que se modifica un documento. 

## <a name="ttl-behavior"></a>Comportamiento de TTL
característica TTL Hola se controla mediante propiedades TTL en dos niveles: nivel de colección de Hola y de nivel de documento de Hola. valores de Hello se establecen en segundos y se tratan como una diferencia de hello `_ts` ese documento Hola se modificó por última vez en.

1. DefaultTTL para la recopilación de Hola
   
   * Si falta (o conjunto toonull), documentos no se eliminan automáticamente.
   * Si está presente y el valor de hello es "-1" = infinito: no caducan documentos de forma predeterminada
   * Si está presente y el valor de hello es un número ("n"): documentos expiran "n" segundos después de la última modificación
2. Período de vida para los documentos de hello: 
   
   * Propiedad solo es aplicable si está presente para la colección principal de Hola DefaultTTL.
   * Invalida el valor de DefaultTTL de hello para la recopilación de hello primario.

Tan pronto como documento de hello ha expirado (`ttl`  +  `_ts` > = hora actual del servidor), documento Hola se marca como "expirada". No se permitirá ninguna operación en estos documentos después de este momento y se excluirá de los resultados de Hola de las consultas realizadas. documentos de Hola se eliminan físicamente en el sistema de Hola y se eliminan en segundo plano de hello según la ocasión en un momento posterior. Esto no utilizar cualquier [unidades de solicitud (RUs)](request-units.md) de asignación de la colección de Hola.

Hola anteriormente lógica se pueden mostrar en hello después de matriz:

|  | DefaultTTL falta o no se establece en la colección de Hola | DefaultTTL = -1 en la colección | DefaultTTL = "n" en la colección |
| --- |:--- |:--- |:--- |
| Falta TTL en el documento |Nada toooverride en el nivel de documento desde el documento de Hola y de colección no disponen del concepto de TTL. |Ningún documento de esta colección caducará. |documentos de Hello en esta colección expira cuando transcurre el intervalo n. |
| TTL = -1 en el documento |Nada toooverride en nivel de documento de hello puesto que no define la colección de Hola Hola propiedad DefaultTTL que puede invalidar un documento. Período de vida de un documento es sin interpretado por el sistema de Hola. |Ningún documento de esta colección caducará. |documento de Hello con TTL =-1 en esta colección nunca expirará. Todos los demás documentos caducarán después del intervalo "n". |
| TTL = n en documentos |Nada toooverride en nivel de documento de Hola. Período de vida de un documento en sin interpretado por el sistema de Hola. |documento de Hello con TTL = caducará n a n de intervalo, en segundos. Otros documentos heredarán el intervalo de -1 y no caducarán nunca. |documento de Hello con TTL = caducará n a n de intervalo, en segundos. Otros documentos hereda "n" el intervalo de recopilación de Hola. |

## <a name="configuring-ttl"></a>Configuración de TTL
De forma predeterminada, el tiempo toolive está deshabilitada de forma predeterminada en todas las colecciones de base de datos de Cosmos y en todos los documentos.

## <a name="enabling-ttl"></a>Habilitación del TTL
tooenable TTL en una colección o documentos de hello dentro de una colección, debe tooset Hola DefaultTTL propiedad un tooeither colección -1 o un número positivo distinto de cero. Configuración de medios de hello DefaultTTL demasiado-1 que de forma predeterminada todos los documentos de la colección de hello residirá indefinidamente pero Hola servicio base de datos de Cosmos debe supervisar esta colección para los documentos que ha reemplazado este valor predeterminado.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Configuración del TTL predeterminado en una colección
En un nivel de colección son tooconfigure capaz de un tiempo predeterminado toolive. Hola tooset TTL en una colección, debe tooprovide un número positivo distinto de cero que indica el período de hello, en segundos, tooexpire todos los documentos de la colección de hello después Hola modificó por última vez la marca de tiempo del documento de hello (`_ts`). O bien, puede establecer Hola predeterminada demasiado-1, lo que implica que todos los documentos que se inserta en la colección de toohello residirá indefinidamente de forma predeterminada.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>Configuración del TTL en un documento
Además toosetting un TTL predeterminado en una colección puede establecer TTL específico en un nivel de documento. Esto invalidará predeterminado Hola de colección de Hola.

* Hola tooset TTL en un documento, deberá tooprovide un número positivo distinto de cero que indica Hola período, en segundos, aparece el documento de hello tooexpire después de hello modificó por última vez la marca de tiempo del documento de hello (`_ts`).
* Si un documento no tiene ningún campo TTL, a continuación, Hola predeterminado de la colección de Hola se aplicará.
* Si el TTL se deshabilita en el nivel de colección de hello, se omitirán campo TTL de hello en el documento de hello hasta que el TTL se vuelve a habilitar en la colección de Hola.

Este es un fragmento de código que muestra cómo tooset Hola expiración del período de vida en un documento:

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>Extensión del TTL en un documento existente
Puede restablecer Hola TTL en un documento, realice cualquier operación de escritura en el documento de Hola. Esto establecerá hello `_ts` toohello hora actual y toohello de cuenta regresiva de hello en el documento fecha de expiración, según lo establecido por hello `ttl`, comenzará de nuevo. Si desea toochange hello `ttl` de un documento, puede actualizar el campo Hola tal y como haría con cualquier otro campo configurable.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>Eliminación del TTL de un documento
Si se ha establecido un valor de TTL en un documento y ya no desea que ese tooexpire de documento, a continuación, puede recuperar el documento de hello, quitar campo TTL de Hola y reemplazar documento hello en el servidor de Hola. Cuando se quita el campo TTL de Hola de documento de hello, se aplicarán predeterminado Hola de colección de Hola. toostop un documento de caduca y no se hereda de la colección de Hola deberá tooset Hola TTL valor demasiado-1.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>Deshabilitación de TTL
toodisable TTL por completo en una colección y el fondo de hello Detener proceso desde busca documentos caducados propiedad DefaultTTL de hello en la colección de hello debe eliminarse. Al eliminar esta propiedad es diferente de si se establece demasiado-1. Establecer nuevos documentos de demasiado-1 significa agrega colección toohello residirá indefinidamente, pero puede invalidar esta opción en los documentos específicos en la colección de Hola. Quitar esta propiedad por completo de la colección de Hola significa que ningún documento va a expirar, incluso si hay documentos que han invalidado explícitamente un valor predeterminado anterior.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>P+F
**¿Cuánto me costará el TTL?**

No hay ningún toosetting costo adicional un período de vida de un documento.

**¿Durante cuánto tiempo tardará toodelete un documento una vez Hola TTL está activo?**

documentos de Hello expiran inmediatamente una vez hello TTL está activo y no será accesible a través de CRUD o las API de consulta. 

**¿Afectará el TTL en un documento a los cargos de RU?**

No, no se producirá ningún impacto en los cargos de RU por las eliminaciones de documentos expirados mediante TTL en Cosmos DB.

**¿Aplica función TTL de hello solo tooentire documentos o puedo expirar la valores de propiedad de documento individual?**

TTL aplica a todo el documento toohello. Si desea que tooexpire solamente una parte de un documento, a continuación, se recomienda que extraer parte Hola Hola documento principal en tooa documento "vinculados" y, a continuación, utilizar el valor de TTL en ese documento extraída.

**¿Tienen características TTL de Hola indización requisitos específicos?**

Sí. Hola colección debe tener [conjunto de la directiva de indización](indexing-policies.md) tooeither Consistent o Lazy. Tratar tooset DefaultTTL en una colección con una indización de tooNone de conjunto, se producirá un error, así como que se está probando tooturn desactivar la indización en una colección que tiene un DefaultTTL ya establecido.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la base de datos de Cosmos de Azure, consulte servicio toohello [ *documentación* ](https://azure.microsoft.com/documentation/services/cosmos-db/) página.


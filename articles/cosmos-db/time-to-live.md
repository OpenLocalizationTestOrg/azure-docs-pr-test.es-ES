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
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="41a48-104">Punto de expirar datos en colecciones de base de datos de Azure Cosmos automáticamente con hora toolive</span><span class="sxs-lookup"><span data-stu-id="41a48-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="41a48-105">Las aplicaciones pueden generar y almacenar enormes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="41a48-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="41a48-106">Algunos de estos datos, como los datos de eventos, los registros y la información de sesión de usuario que se generan automáticamente, solo son útiles durante un tiempo finito.</span><span class="sxs-lookup"><span data-stu-id="41a48-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="41a48-107">Una vez datos Hola se convierte en exceso toohello las necesidades de aplicación hello es toopurge seguro para estos datos y reducir las necesidades de almacenamiento de Hola de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="41a48-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="41a48-108">Con "tiempo toolive" o TTL, base de datos de Microsoft Azure Cosmos proporciona documentos de toohave de capacidad de hello purgados de base de datos de hello automáticamente tras un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="41a48-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="41a48-109">tiempo predeterminado de Hello toolive se puede establecer en el nivel de colección de Hola y se reemplaza en una base de cada documento.</span><span class="sxs-lookup"><span data-stu-id="41a48-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="41a48-110">Una vez que se establece el TTL, como un valor predeterminado de la colección o en un nivel de documento, Cosmos DB quita automáticamente los documentos que existen después de ese período de tiempo, en segundos, desde que se modificaron por última vez.</span><span class="sxs-lookup"><span data-stu-id="41a48-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="41a48-111">Tiempo toolive en la base de datos de Cosmos usa un desplazamiento con respecto al documento Hola se modificó por última vez.</span><span class="sxs-lookup"><span data-stu-id="41a48-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="41a48-112">toodo este equipo de TI usa hello `_ts` campo que se encuentra en cada documento.</span><span class="sxs-lookup"><span data-stu-id="41a48-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="41a48-113">campo de _ts Hello es una hora y fecha que representan Hola de estilo unix época marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="41a48-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="41a48-114">Hola `_ts` campo se actualiza cada vez que se modifica un documento.</span><span class="sxs-lookup"><span data-stu-id="41a48-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="41a48-115">Comportamiento de TTL</span><span class="sxs-lookup"><span data-stu-id="41a48-115">TTL behavior</span></span>
<span data-ttu-id="41a48-116">característica TTL Hola se controla mediante propiedades TTL en dos niveles: nivel de colección de Hola y de nivel de documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="41a48-117">valores de Hello se establecen en segundos y se tratan como una diferencia de hello `_ts` ese documento Hola se modificó por última vez en.</span><span class="sxs-lookup"><span data-stu-id="41a48-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="41a48-118">DefaultTTL para la recopilación de Hola</span><span class="sxs-lookup"><span data-stu-id="41a48-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="41a48-119">Si falta (o conjunto toonull), documentos no se eliminan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="41a48-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="41a48-120">Si está presente y el valor de hello es "-1" = infinito: no caducan documentos de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="41a48-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="41a48-121">Si está presente y el valor de hello es un número ("n"): documentos expiran "n" segundos después de la última modificación</span><span class="sxs-lookup"><span data-stu-id="41a48-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="41a48-122">Período de vida para los documentos de hello:</span><span class="sxs-lookup"><span data-stu-id="41a48-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="41a48-123">Propiedad solo es aplicable si está presente para la colección principal de Hola DefaultTTL.</span><span class="sxs-lookup"><span data-stu-id="41a48-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="41a48-124">Invalida el valor de DefaultTTL de hello para la recopilación de hello primario.</span><span class="sxs-lookup"><span data-stu-id="41a48-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="41a48-125">Tan pronto como documento de hello ha expirado (`ttl`  +  `_ts` > = hora actual del servidor), documento Hola se marca como "expirada".</span><span class="sxs-lookup"><span data-stu-id="41a48-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="41a48-126">No se permitirá ninguna operación en estos documentos después de este momento y se excluirá de los resultados de Hola de las consultas realizadas.</span><span class="sxs-lookup"><span data-stu-id="41a48-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="41a48-127">documentos de Hola se eliminan físicamente en el sistema de Hola y se eliminan en segundo plano de hello según la ocasión en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="41a48-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="41a48-128">Esto no utilizar cualquier [unidades de solicitud (RUs)](request-units.md) de asignación de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="41a48-129">Hola anteriormente lógica se pueden mostrar en hello después de matriz:</span><span class="sxs-lookup"><span data-stu-id="41a48-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="41a48-130">DefaultTTL falta o no se establece en la colección de Hola</span><span class="sxs-lookup"><span data-stu-id="41a48-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="41a48-131">DefaultTTL = -1 en la colección</span><span class="sxs-lookup"><span data-stu-id="41a48-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="41a48-132">DefaultTTL = "n" en la colección</span><span class="sxs-lookup"><span data-stu-id="41a48-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="41a48-133">Falta TTL en el documento</span><span class="sxs-lookup"><span data-stu-id="41a48-133">TTL Missing on document</span></span> |<span data-ttu-id="41a48-134">Nada toooverride en el nivel de documento desde el documento de Hola y de colección no disponen del concepto de TTL.</span><span class="sxs-lookup"><span data-stu-id="41a48-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="41a48-135">Ningún documento de esta colección caducará.</span><span class="sxs-lookup"><span data-stu-id="41a48-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="41a48-136">documentos de Hello en esta colección expira cuando transcurre el intervalo n.</span><span class="sxs-lookup"><span data-stu-id="41a48-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="41a48-137">TTL = -1 en el documento</span><span class="sxs-lookup"><span data-stu-id="41a48-137">TTL = -1 on document</span></span> |<span data-ttu-id="41a48-138">Nada toooverride en nivel de documento de hello puesto que no define la colección de Hola Hola propiedad DefaultTTL que puede invalidar un documento.</span><span class="sxs-lookup"><span data-stu-id="41a48-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="41a48-139">Período de vida de un documento es sin interpretado por el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="41a48-140">Ningún documento de esta colección caducará.</span><span class="sxs-lookup"><span data-stu-id="41a48-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="41a48-141">documento de Hello con TTL =-1 en esta colección nunca expirará.</span><span class="sxs-lookup"><span data-stu-id="41a48-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="41a48-142">Todos los demás documentos caducarán después del intervalo "n".</span><span class="sxs-lookup"><span data-stu-id="41a48-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="41a48-143">TTL = n en documentos</span><span class="sxs-lookup"><span data-stu-id="41a48-143">TTL = n on document</span></span> |<span data-ttu-id="41a48-144">Nada toooverride en nivel de documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="41a48-145">Período de vida de un documento en sin interpretado por el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="41a48-146">documento de Hello con TTL = caducará n a n de intervalo, en segundos.</span><span class="sxs-lookup"><span data-stu-id="41a48-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="41a48-147">Otros documentos heredarán el intervalo de -1 y no caducarán nunca.</span><span class="sxs-lookup"><span data-stu-id="41a48-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="41a48-148">documento de Hello con TTL = caducará n a n de intervalo, en segundos.</span><span class="sxs-lookup"><span data-stu-id="41a48-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="41a48-149">Otros documentos hereda "n" el intervalo de recopilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="41a48-150">Configuración de TTL</span><span class="sxs-lookup"><span data-stu-id="41a48-150">Configuring TTL</span></span>
<span data-ttu-id="41a48-151">De forma predeterminada, el tiempo toolive está deshabilitada de forma predeterminada en todas las colecciones de base de datos de Cosmos y en todos los documentos.</span><span class="sxs-lookup"><span data-stu-id="41a48-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="41a48-152">Habilitación del TTL</span><span class="sxs-lookup"><span data-stu-id="41a48-152">Enabling TTL</span></span>
<span data-ttu-id="41a48-153">tooenable TTL en una colección o documentos de hello dentro de una colección, debe tooset Hola DefaultTTL propiedad un tooeither colección -1 o un número positivo distinto de cero.</span><span class="sxs-lookup"><span data-stu-id="41a48-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="41a48-154">Configuración de medios de hello DefaultTTL demasiado-1 que de forma predeterminada todos los documentos de la colección de hello residirá indefinidamente pero Hola servicio base de datos de Cosmos debe supervisar esta colección para los documentos que ha reemplazado este valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="41a48-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="41a48-155">Configuración del TTL predeterminado en una colección</span><span class="sxs-lookup"><span data-stu-id="41a48-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="41a48-156">En un nivel de colección son tooconfigure capaz de un tiempo predeterminado toolive.</span><span class="sxs-lookup"><span data-stu-id="41a48-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="41a48-157">Hola tooset TTL en una colección, debe tooprovide un número positivo distinto de cero que indica el período de hello, en segundos, tooexpire todos los documentos de la colección de hello después Hola modificó por última vez la marca de tiempo del documento de hello (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="41a48-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="41a48-158">O bien, puede establecer Hola predeterminada demasiado-1, lo que implica que todos los documentos que se inserta en la colección de toohello residirá indefinidamente de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="41a48-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="41a48-159">Configuración del TTL en un documento</span><span class="sxs-lookup"><span data-stu-id="41a48-159">Setting TTL on a document</span></span>
<span data-ttu-id="41a48-160">Además toosetting un TTL predeterminado en una colección puede establecer TTL específico en un nivel de documento.</span><span class="sxs-lookup"><span data-stu-id="41a48-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="41a48-161">Esto invalidará predeterminado Hola de colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="41a48-162">Hola tooset TTL en un documento, deberá tooprovide un número positivo distinto de cero que indica Hola período, en segundos, aparece el documento de hello tooexpire después de hello modificó por última vez la marca de tiempo del documento de hello (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="41a48-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="41a48-163">Si un documento no tiene ningún campo TTL, a continuación, Hola predeterminado de la colección de Hola se aplicará.</span><span class="sxs-lookup"><span data-stu-id="41a48-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="41a48-164">Si el TTL se deshabilita en el nivel de colección de hello, se omitirán campo TTL de hello en el documento de hello hasta que el TTL se vuelve a habilitar en la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="41a48-165">Este es un fragmento de código que muestra cómo tooset Hola expiración del período de vida en un documento:</span><span class="sxs-lookup"><span data-stu-id="41a48-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

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


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="41a48-166">Extensión del TTL en un documento existente</span><span class="sxs-lookup"><span data-stu-id="41a48-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="41a48-167">Puede restablecer Hola TTL en un documento, realice cualquier operación de escritura en el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="41a48-168">Esto establecerá hello `_ts` toohello hora actual y toohello de cuenta regresiva de hello en el documento fecha de expiración, según lo establecido por hello `ttl`, comenzará de nuevo.</span><span class="sxs-lookup"><span data-stu-id="41a48-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="41a48-169">Si desea toochange hello `ttl` de un documento, puede actualizar el campo Hola tal y como haría con cualquier otro campo configurable.</span><span class="sxs-lookup"><span data-stu-id="41a48-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="41a48-170">Eliminación del TTL de un documento</span><span class="sxs-lookup"><span data-stu-id="41a48-170">Removing TTL from a document</span></span>
<span data-ttu-id="41a48-171">Si se ha establecido un valor de TTL en un documento y ya no desea que ese tooexpire de documento, a continuación, puede recuperar el documento de hello, quitar campo TTL de Hola y reemplazar documento hello en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="41a48-172">Cuando se quita el campo TTL de Hola de documento de hello, se aplicarán predeterminado Hola de colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="41a48-173">toostop un documento de caduca y no se hereda de la colección de Hola deberá tooset Hola TTL valor demasiado-1.</span><span class="sxs-lookup"><span data-stu-id="41a48-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="41a48-174">Deshabilitación de TTL</span><span class="sxs-lookup"><span data-stu-id="41a48-174">Disabling TTL</span></span>
<span data-ttu-id="41a48-175">toodisable TTL por completo en una colección y el fondo de hello Detener proceso desde busca documentos caducados propiedad DefaultTTL de hello en la colección de hello debe eliminarse.</span><span class="sxs-lookup"><span data-stu-id="41a48-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="41a48-176">Al eliminar esta propiedad es diferente de si se establece demasiado-1.</span><span class="sxs-lookup"><span data-stu-id="41a48-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="41a48-177">Establecer nuevos documentos de demasiado-1 significa agrega colección toohello residirá indefinidamente, pero puede invalidar esta opción en los documentos específicos en la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="41a48-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="41a48-178">Quitar esta propiedad por completo de la colección de Hola significa que ningún documento va a expirar, incluso si hay documentos que han invalidado explícitamente un valor predeterminado anterior.</span><span class="sxs-lookup"><span data-stu-id="41a48-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="41a48-179">P+F</span><span class="sxs-lookup"><span data-stu-id="41a48-179">FAQ</span></span>
<span data-ttu-id="41a48-180">**¿Cuánto me costará el TTL?**</span><span class="sxs-lookup"><span data-stu-id="41a48-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="41a48-181">No hay ningún toosetting costo adicional un período de vida de un documento.</span><span class="sxs-lookup"><span data-stu-id="41a48-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="41a48-182">**¿Durante cuánto tiempo tardará toodelete un documento una vez Hola TTL está activo?**</span><span class="sxs-lookup"><span data-stu-id="41a48-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="41a48-183">documentos de Hello expiran inmediatamente una vez hello TTL está activo y no será accesible a través de CRUD o las API de consulta.</span><span class="sxs-lookup"><span data-stu-id="41a48-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="41a48-184">**¿Afectará el TTL en un documento a los cargos de RU?**</span><span class="sxs-lookup"><span data-stu-id="41a48-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="41a48-185">No, no se producirá ningún impacto en los cargos de RU por las eliminaciones de documentos expirados mediante TTL en Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="41a48-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="41a48-186">**¿Aplica función TTL de hello solo tooentire documentos o puedo expirar la valores de propiedad de documento individual?**</span><span class="sxs-lookup"><span data-stu-id="41a48-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="41a48-187">TTL aplica a todo el documento toohello.</span><span class="sxs-lookup"><span data-stu-id="41a48-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="41a48-188">Si desea que tooexpire solamente una parte de un documento, a continuación, se recomienda que extraer parte Hola Hola documento principal en tooa documento "vinculados" y, a continuación, utilizar el valor de TTL en ese documento extraída.</span><span class="sxs-lookup"><span data-stu-id="41a48-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="41a48-189">**¿Tienen características TTL de Hola indización requisitos específicos?**</span><span class="sxs-lookup"><span data-stu-id="41a48-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="41a48-190">Sí.</span><span class="sxs-lookup"><span data-stu-id="41a48-190">Yes.</span></span> <span data-ttu-id="41a48-191">Hola colección debe tener [conjunto de la directiva de indización](indexing-policies.md) tooeither Consistent o Lazy.</span><span class="sxs-lookup"><span data-stu-id="41a48-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="41a48-192">Tratar tooset DefaultTTL en una colección con una indización de tooNone de conjunto, se producirá un error, así como que se está probando tooturn desactivar la indización en una colección que tiene un DefaultTTL ya establecido.</span><span class="sxs-lookup"><span data-stu-id="41a48-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41a48-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41a48-193">Next steps</span></span>
<span data-ttu-id="41a48-194">toolearn más información acerca de la base de datos de Cosmos de Azure, consulte servicio toohello [ *documentación* ](https://azure.microsoft.com/documentation/services/cosmos-db/) página.</span><span class="sxs-lookup"><span data-stu-id="41a48-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>


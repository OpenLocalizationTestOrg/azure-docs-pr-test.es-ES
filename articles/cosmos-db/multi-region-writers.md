---
title: arquitecturas de base de datos maestra aaaMulti con base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodesign arquitecturas de aplicación con local lee y escribe en varias regiones geográficas con base de datos de Azure Cosmos."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="aa1e7-103">Arquitecturas de bases de datos de replicación global con varios maestros con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aa1e7-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="aa1e7-104">Base de datos de Azure Cosmos admite listo para usar [replicación global](distribute-data-globally.md), lo cual permite hacer toomultiple regiones de datos de toodistribute con acceso de baja latencia en cualquier parte de la carga de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="aa1e7-105">Este modelo se utiliza normalmente para las cargas de trabajo del publicador o el consumidor cuando hay un redactor en una única región geográfica y lectores distribuidos globalmente en otras regiones (lectura).</span><span class="sxs-lookup"><span data-stu-id="aa1e7-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="aa1e7-106">También puede utilizar replicación global compatible de Azure Cosmos base de datos con toobuild de aplicaciones en el que se distribuyen globalmente lectores y escritores.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="aa1e7-107">En este documento se describe un patrón que permite lograr un acceso de lectura y escritura local para redactores distribuidos con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="aa1e7-108"><a id="ExampleScenario"></a>Publicación de contenido: un escenario de ejemplo</span><span class="sxs-lookup"><span data-stu-id="aa1e7-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="aa1e7-109">Echemos un vistazo a una toodescribe de escenario de mundo real cómo puede usar los patrones de distribuidos globalmente varios-region/multi-maestro lectura y escritura con la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="aa1e7-110">Considere la posibilidad de una plataforma de publicación de contenido basada en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="aa1e7-111">Estos son algunos requisitos que debe cumplir esta plataforma para una experiencia del usuario excelente para publicadores y consumidores.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="aa1e7-112">Los autores y los suscriptores se distribuyen en Hola a todos</span><span class="sxs-lookup"><span data-stu-id="aa1e7-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="aa1e7-113">Los autores deben publicar la región (cerca) local tootheir de artículos (escritura)</span><span class="sxs-lookup"><span data-stu-id="aa1e7-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="aa1e7-114">Los autores tienen lectores/suscriptores de los artículos que se distribuyen en todo el mundo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="aa1e7-115">Los suscriptores deben recibir una notificación cuando se publican artículos nuevos.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="aa1e7-116">Los suscriptores deben ser capaz de tooread artículos de su región local.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="aa1e7-117">También deben ser capaz de tooadd revisiones toothese artículos.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="aa1e7-118">Nadie, incluido el autor de Hola de artículos de hello debe ser capaz de ver que todos Hola revisiones tooarticles adjunto de un área local.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="aa1e7-119">Suponiendo que millones de los consumidores y editores con miles de millones de artículos, pronto tenemos problemas de hello tooconfront de escala junto con para garantizar la localidad de acceso.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="aa1e7-120">Al igual que con la mayoría de los problemas de escalabilidad, solución de Hola se encuentra en una buena estrategia de partición.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="aa1e7-121">A continuación, vamos a observar cómo toomodel artículos, revise y notificaciones como documentos, configuran cuentas de base de datos de Azure Cosmos e implementar una capa de acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="aa1e7-122">Si desea que toolearn más información sobre la creación de particiones y las claves de partición, vea [particiones y ajuste de escala en la base de datos de Azure Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="aa1e7-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="aa1e7-123"><a id="ModelingNotifications"></a>Modelado de notificaciones</span><span class="sxs-lookup"><span data-stu-id="aa1e7-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="aa1e7-124">Las notificaciones son usuario de tooa específico de fuentes de datos.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="aa1e7-125">Por lo tanto, los patrones de acceso de Hola para los documentos de las notificaciones están siempre en contexto Hola de usuario único.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="aa1e7-126">Por ejemplo, podría "registrar un usuario de notificación tooa" o "capturar todas las notificaciones para un usuario determinado".</span><span class="sxs-lookup"><span data-stu-id="aa1e7-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="aa1e7-127">Por lo tanto, Hola idóneo de clave de partición para este tipo sería `UserId`.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="aa1e7-128"><a id="ModelingSubscriptions"></a>Modelado de suscripciones</span><span class="sxs-lookup"><span data-stu-id="aa1e7-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="aa1e7-129">Las suscripciones se pueden crear para diversos criterios, como una categoría específica de artículos de interés o un publicador específico.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="aa1e7-130">Por lo tanto, Hola `SubscriptionFilter` es una buena elección para la clave de partición.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <span data-ttu-id="aa1e7-131"><a id="ModelingArticles"></a>Modelado de artículos</span><span class="sxs-lookup"><span data-stu-id="aa1e7-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="aa1e7-132">Una vez que se identifica un artículo a través de notificaciones, las consultas posteriores se basan normalmente en hello `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="aa1e7-133">Elegir `Article.Id` como partición clave hello, por tanto, proporciona una distribución recomendada de Hola para almacenar los artículos dentro de una colección de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="aa1e7-134"><a id="ModelingReviews"></a>Modelado de revisiones</span><span class="sxs-lookup"><span data-stu-id="aa1e7-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="aa1e7-135">Como artículos, revisiones principalmente se escriben y leer en el contexto de Hola de artículo.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="aa1e7-136">Elegir `ArticleId` como clave de partición proporciona la mejor distribución y un acceso eficaz a las revisiones asociadas al artículo.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <span data-ttu-id="aa1e7-137"><a id="DataAccessMethods"></a>Métodos de nivel de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="aa1e7-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="aa1e7-138">Ahora Echemos un vistazo a los datos principales Hola necesitamos tooimplement de métodos de acceso.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="aa1e7-139">Esta es la lista de Hola de métodos que Hola `ContentPublishDatabase` necesita:</span><span class="sxs-lookup"><span data-stu-id="aa1e7-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="aa1e7-140"><a id="Architecture"></a>Configuración de la cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aa1e7-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="aa1e7-141">tooguarantee local las lecturas y escrituras, se deben crear particiones de datos no solo en la clave de partición, pero también se basa en el patrón de acceso geográfica hello en regiones.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="aa1e7-142">modelo de Hello depende de tener una cuenta de base de datos de base de datos de Azure Cosmos de replicación geográfica para cada región.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="aa1e7-143">Por ejemplo, con dos regiones, a continuación se muestra una configuración para operaciones de escritura en varias regiones:</span><span class="sxs-lookup"><span data-stu-id="aa1e7-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="aa1e7-144">Nombre de cuenta</span><span class="sxs-lookup"><span data-stu-id="aa1e7-144">Account Name</span></span> | <span data-ttu-id="aa1e7-145">Región de escritura</span><span class="sxs-lookup"><span data-stu-id="aa1e7-145">Write Region</span></span> | <span data-ttu-id="aa1e7-146">Región de lectura</span><span class="sxs-lookup"><span data-stu-id="aa1e7-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="aa1e7-147">Hello diagrama siguiente muestra cómo se realizan las lecturas y escrituras en una aplicación típica con este programa de instalación:</span><span class="sxs-lookup"><span data-stu-id="aa1e7-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Arquitectura con varios maestros de Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="aa1e7-149">Este es un fragmento de código que muestra cómo tooinitialize Hola clientes en un capa DAL ejecutando Hola `West US` región.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

<span data-ttu-id="aa1e7-150">Con hello precede el programa de instalación, capa de acceso a datos de hello puede reenviar todas las escrituras toohello cuenta local en función de donde se implementa.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="aa1e7-151">Las lecturas se realizan mediante la lectura del tanto cuentas tooget Hola global en vista de datos.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="aa1e7-152">Este enfoque puede ser extendidos tooas muchas regiones según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="aa1e7-153">Por ejemplo, la siguiente es una configuración con tres regiones geográficas:</span><span class="sxs-lookup"><span data-stu-id="aa1e7-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="aa1e7-154">Nombre de cuenta</span><span class="sxs-lookup"><span data-stu-id="aa1e7-154">Account Name</span></span> | <span data-ttu-id="aa1e7-155">Región de escritura</span><span class="sxs-lookup"><span data-stu-id="aa1e7-155">Write Region</span></span> | <span data-ttu-id="aa1e7-156">Región de lectura 1</span><span class="sxs-lookup"><span data-stu-id="aa1e7-156">Read Region 1</span></span> | <span data-ttu-id="aa1e7-157">Región de lectura 2</span><span class="sxs-lookup"><span data-stu-id="aa1e7-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="aa1e7-158"><a id="DataAccessImplementation"></a>Implementación del nivel de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="aa1e7-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="aa1e7-159">Ahora Echemos un vistazo a la implementación de Hola de capa de acceso a datos hello (DAL) para una aplicación con dos áreas de escritura.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="aa1e7-160">Hola DAL debe implementar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="aa1e7-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="aa1e7-161">Crear varias instancias de `DocumentClient` para cada cuenta.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="aa1e7-162">Con dos regiones, cada instancia del nivel DAL tiene elementos `writeClient` y `readClient`.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="aa1e7-163">En función de la región de hello implementada de la aplicación hello, configurar los extremos de Hola para `writeclient` y `readClient`.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="aa1e7-164">Por ejemplo, hello DAL se implementa en `West US` utiliza `contentpubdatabase-usa.documents.azure.com` para llevar a cabo escrituras.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="aa1e7-165">Hola DAL se implementa en `NorthEurope` utiliza `contentpubdatabase-europ.documents.azure.com` para operaciones de escritura.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="aa1e7-166">Con hello precede el programa de instalación, se pueden implementar métodos de acceso a datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="aa1e7-167">Escribir operaciones reenvían Hola escritura toohello correspondiente `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

<span data-ttu-id="aa1e7-168">Para leer las notificaciones y las revisiones, debe leer desde las regiones y los resultados de unión Hola tal y como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="aa1e7-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

<span data-ttu-id="aa1e7-169">Por lo tanto, al elegir una buena clave de creación de particiones y una creación de particiones estática basada en cuentas, puede lograr que las lecturas y escrituras locales en varias regiones usen Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="aa1e7-170"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa1e7-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="aa1e7-171">En este artículo, se describe cómo puede usar los patrones de lectura y escritura en varias regiones distribuidos globalmente con Azure Cosmos DB, y usar la publicación de contenido como un escenario de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="aa1e7-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="aa1e7-172">Más información sobre la compatibilidad de Azure Cosmos DB con la [distribución global](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="aa1e7-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="aa1e7-173">Más información sobre las [conmutaciones por error manuales y automáticas en Azure Cosmos DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="aa1e7-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="aa1e7-174">Más información sobre la [coherencia global con Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="aa1e7-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="aa1e7-175">Desarrollar con varias regiones, con hello [base de datos de Azure Cosmos: API de documentos](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="aa1e7-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="aa1e7-176">Desarrollar con varias regiones, con hello [base de datos de Azure Cosmos: API de MongoDB](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="aa1e7-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="aa1e7-177">Desarrollar con varias regiones, con hello [base de datos de Azure Cosmos: API de tabla](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="aa1e7-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>

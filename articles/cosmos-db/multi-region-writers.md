---
title: Arquitecturas de bases de datos con varios maestros con Azure Cosmos DB | Documentos de Microsoft
description: "Obtenga información sobre cómo diseñar arquitecturas de aplicaciones con lecturas y escrituras locales en varias regiones geográficas con Azure Cosmos DB."
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
ms.openlocfilehash: cf1482ae7b1070023703f5dbe861d151f5d64fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="0f39a-103">Arquitecturas de bases de datos de replicación global con varios maestros con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0f39a-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="0f39a-104">Azure Cosmos DB admite la [replicación global](distribute-data-globally.md) inmediata, que permite distribuir datos en varias regiones con un acceso de baja latencia en cualquier parte de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0f39a-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="0f39a-105">Este modelo se utiliza normalmente para las cargas de trabajo del publicador o el consumidor cuando hay un redactor en una única región geográfica y lectores distribuidos globalmente en otras regiones (lectura).</span><span class="sxs-lookup"><span data-stu-id="0f39a-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="0f39a-106">También puede usar la compatibilidad con la replicación global de Azure Cosmos DB para compilar aplicaciones en las que los redactores y lectores están distribuidos globalmente.</span><span class="sxs-lookup"><span data-stu-id="0f39a-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="0f39a-107">En este documento se describe un patrón que permite lograr un acceso de lectura y escritura local para redactores distribuidos con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0f39a-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="0f39a-108"><a id="ExampleScenario"></a>Publicación de contenido: un escenario de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0f39a-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="0f39a-109">Echemos un vistazo a un escenario real para describir cómo puede usar patrones de lectura y escritura con varios maestros y varias regiones distribuidos globalmente con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0f39a-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="0f39a-110">Considere la posibilidad de una plataforma de publicación de contenido basada en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0f39a-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="0f39a-111">Estos son algunos requisitos que debe cumplir esta plataforma para una experiencia del usuario excelente para publicadores y consumidores.</span><span class="sxs-lookup"><span data-stu-id="0f39a-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="0f39a-112">Los autores y los suscriptores se distribuyen en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="0f39a-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="0f39a-113">Los autores deben publicar (escribir) artículos en su región local (más cercana)</span><span class="sxs-lookup"><span data-stu-id="0f39a-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="0f39a-114">Los autores tienen lectores/suscriptores de los artículos que se distribuyen en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="0f39a-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="0f39a-115">Los suscriptores deben recibir una notificación cuando se publican artículos nuevos.</span><span class="sxs-lookup"><span data-stu-id="0f39a-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="0f39a-116">Los suscriptores deben poder leer artículos desde su región local.</span><span class="sxs-lookup"><span data-stu-id="0f39a-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="0f39a-117">También deben poder agregar revisiones a estos artículos.</span><span class="sxs-lookup"><span data-stu-id="0f39a-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="0f39a-118">Cualquiera, incluido al autor de los artículos, debe poder ver todas las revisiones asociadas a los artículos desde una región local.</span><span class="sxs-lookup"><span data-stu-id="0f39a-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="0f39a-119">Si damos por supuesto millones de consumidores y publicadores con miles de millones de artículos, pronto tendremos que hacer frente a problemas de escala y para garantizar un acceso local.</span><span class="sxs-lookup"><span data-stu-id="0f39a-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="0f39a-120">Al igual que con la mayoría de los problemas de escalabilidad, la solución se encuentra en una buena estrategia de creación de particiones.</span><span class="sxs-lookup"><span data-stu-id="0f39a-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="0f39a-121">A continuación, veamos cómo modelar artículos, revisiones y notificaciones como documentos, configurar cuentas de Azure Cosmos DB e implementar una capa de acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="0f39a-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="0f39a-122">Si desea obtener más información sobre la creación de particiones y las claves de partición, consulte [Partición y escalado en Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="0f39a-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="0f39a-123"><a id="ModelingNotifications"></a>Modelado de notificaciones</span><span class="sxs-lookup"><span data-stu-id="0f39a-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="0f39a-124">Las notificaciones son fuentes de datos específicos de un usuario.</span><span class="sxs-lookup"><span data-stu-id="0f39a-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="0f39a-125">Por lo tanto, los patrones de acceso para los documentos de notificaciones están siempre en el contexto de un único usuario.</span><span class="sxs-lookup"><span data-stu-id="0f39a-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="0f39a-126">Por ejemplo, podría enviar una notificación a un usuario o capturar todas las notificaciones para un determinado usuario.</span><span class="sxs-lookup"><span data-stu-id="0f39a-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="0f39a-127">Por lo tanto, la opción óptima de clave de creación de particiones para este tipo sería `UserId`.</span><span class="sxs-lookup"><span data-stu-id="0f39a-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="0f39a-128"><a id="ModelingSubscriptions"></a>Modelado de suscripciones</span><span class="sxs-lookup"><span data-stu-id="0f39a-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="0f39a-129">Las suscripciones se pueden crear para diversos criterios, como una categoría específica de artículos de interés o un publicador específico.</span><span class="sxs-lookup"><span data-stu-id="0f39a-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="0f39a-130">Por lo tanto, `SubscriptionFilter` es una buena elección para la clave de partición.</span><span class="sxs-lookup"><span data-stu-id="0f39a-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="0f39a-131"><a id="ModelingArticles"></a>Modelado de artículos</span><span class="sxs-lookup"><span data-stu-id="0f39a-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="0f39a-132">Una vez que se identifica un artículo mediante las notificaciones, las consultas posteriores se basan normalmente en `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="0f39a-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="0f39a-133">Por tanto, elegir `Article.Id` como clave de partición proporciona la mejor distribución para almacenar artículos dentro de una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0f39a-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="0f39a-134"><a id="ModelingReviews"></a>Modelado de revisiones</span><span class="sxs-lookup"><span data-stu-id="0f39a-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="0f39a-135">Al igual que los artículos, las revisiones suelen escribirse y leerse en el contexto del artículo.</span><span class="sxs-lookup"><span data-stu-id="0f39a-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="0f39a-136">Elegir `ArticleId` como clave de partición proporciona la mejor distribución y un acceso eficaz a las revisiones asociadas al artículo.</span><span class="sxs-lookup"><span data-stu-id="0f39a-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
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

## <span data-ttu-id="0f39a-137"><a id="DataAccessMethods"></a>Métodos de nivel de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="0f39a-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="0f39a-138">Ahora echaremos un vistazo a los principales métodos de acceso a datos que es necesario para implementar.</span><span class="sxs-lookup"><span data-stu-id="0f39a-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="0f39a-139">Esta es la lista de métodos que `ContentPublishDatabase` necesita:</span><span class="sxs-lookup"><span data-stu-id="0f39a-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="0f39a-140"><a id="Architecture"></a>Configuración de la cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0f39a-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="0f39a-141">Para garantizar lecturas y escrituras locales, debemos crear particiones para los datos basadas no solo en la clave de partición, sino también en el patrón de acceso geográfico en regiones.</span><span class="sxs-lookup"><span data-stu-id="0f39a-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="0f39a-142">El modelo se basa en tener una cuenta de base de datos de Azure Cosmos DB georeplicada para cada región.</span><span class="sxs-lookup"><span data-stu-id="0f39a-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="0f39a-143">Por ejemplo, con dos regiones, a continuación se muestra una configuración para operaciones de escritura en varias regiones:</span><span class="sxs-lookup"><span data-stu-id="0f39a-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="0f39a-144">Nombre de cuenta</span><span class="sxs-lookup"><span data-stu-id="0f39a-144">Account Name</span></span> | <span data-ttu-id="0f39a-145">Región de escritura</span><span class="sxs-lookup"><span data-stu-id="0f39a-145">Write Region</span></span> | <span data-ttu-id="0f39a-146">Región de lectura</span><span class="sxs-lookup"><span data-stu-id="0f39a-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="0f39a-147">En el diagrama siguiente se muestra cómo se realizan las lecturas y escrituras en una aplicación típica con esta configuración:</span><span class="sxs-lookup"><span data-stu-id="0f39a-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Arquitectura con varios maestros de Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="0f39a-149">En el siguiente fragmento de código se muestra cómo inicializar los clientes de un DAL que se ejecuta en la región `West US`.</span><span class="sxs-lookup"><span data-stu-id="0f39a-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
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

<span data-ttu-id="0f39a-150">Con la configuración anterior, el nivel de acceso a datos puede reenviar todas las escrituras a la cuenta local en función de dónde se implemente.</span><span class="sxs-lookup"><span data-stu-id="0f39a-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="0f39a-151">Las lecturas se realizan mediante la lectura de ambas cuentas para obtener una visión global de los datos.</span><span class="sxs-lookup"><span data-stu-id="0f39a-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="0f39a-152">Este enfoque se puede extender a tantas regiones como sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0f39a-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="0f39a-153">Por ejemplo, la siguiente es una configuración con tres regiones geográficas:</span><span class="sxs-lookup"><span data-stu-id="0f39a-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="0f39a-154">Nombre de cuenta</span><span class="sxs-lookup"><span data-stu-id="0f39a-154">Account Name</span></span> | <span data-ttu-id="0f39a-155">Región de escritura</span><span class="sxs-lookup"><span data-stu-id="0f39a-155">Write Region</span></span> | <span data-ttu-id="0f39a-156">Región de lectura 1</span><span class="sxs-lookup"><span data-stu-id="0f39a-156">Read Region 1</span></span> | <span data-ttu-id="0f39a-157">Región de lectura 2</span><span class="sxs-lookup"><span data-stu-id="0f39a-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="0f39a-158"><a id="DataAccessImplementation"></a>Implementación del nivel de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="0f39a-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="0f39a-159">Ahora echaremos un vistazo a la implementación del nivel de acceso a datos (DAL) para una aplicación con dos regiones de escritura.</span><span class="sxs-lookup"><span data-stu-id="0f39a-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="0f39a-160">El nivel de acceso a datos debe implementar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0f39a-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="0f39a-161">Crear varias instancias de `DocumentClient` para cada cuenta.</span><span class="sxs-lookup"><span data-stu-id="0f39a-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="0f39a-162">Con dos regiones, cada instancia del nivel DAL tiene elementos `writeClient` y `readClient`.</span><span class="sxs-lookup"><span data-stu-id="0f39a-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="0f39a-163">En función de la región de la aplicación implementada, configure los puntos de conexión `writeclient` y `readClient`.</span><span class="sxs-lookup"><span data-stu-id="0f39a-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="0f39a-164">Por ejemplo, el nivel DAL implementado en `West US` utiliza `contentpubdatabase-usa.documents.azure.com` para realizar escrituras.</span><span class="sxs-lookup"><span data-stu-id="0f39a-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="0f39a-165">El nivel DAL implementado en `NorthEurope` utiliza `contentpubdatabase-europ.documents.azure.com` para las operaciones de escritura.</span><span class="sxs-lookup"><span data-stu-id="0f39a-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="0f39a-166">Con la configuración anterior, se pueden implementar los métodos de acceso de datos.</span><span class="sxs-lookup"><span data-stu-id="0f39a-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="0f39a-167">Las operaciones de escritura reenvían la escritura al elemento `writeClient` correspondiente.</span><span class="sxs-lookup"><span data-stu-id="0f39a-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

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

<span data-ttu-id="0f39a-168">Para leer las notificaciones y las revisiones, debe leer de ambas regiones y unir los resultados, como se muestra en el fragmento siguiente:</span><span class="sxs-lookup"><span data-stu-id="0f39a-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

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

<span data-ttu-id="0f39a-169">Por lo tanto, al elegir una buena clave de creación de particiones y una creación de particiones estática basada en cuentas, puede lograr que las lecturas y escrituras locales en varias regiones usen Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0f39a-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="0f39a-170"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f39a-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="0f39a-171">En este artículo, se describe cómo puede usar los patrones de lectura y escritura en varias regiones distribuidos globalmente con Azure Cosmos DB, y usar la publicación de contenido como un escenario de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0f39a-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="0f39a-172">Más información sobre la compatibilidad de Azure Cosmos DB con la [distribución global](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="0f39a-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="0f39a-173">Más información sobre las [conmutaciones por error manuales y automáticas en Azure Cosmos DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="0f39a-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="0f39a-174">Más información sobre la [coherencia global con Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="0f39a-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="0f39a-175">Desarrollar con varias regiones mediante [Azure Cosmos DB: DocumentDB API](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="0f39a-175">Develop with multiple regions using the [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="0f39a-176">Desarrollar con varias regiones mediante [Azure Cosmos DB: MongoDB API](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="0f39a-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="0f39a-177">Desarrollar con varias regiones mediante [Azure Cosmos DB: Table API](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="0f39a-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>

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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Arquitecturas de bases de datos de replicación global con varios maestros con Azure Cosmos DB
Base de datos de Azure Cosmos admite listo para usar [replicación global](distribute-data-globally.md), lo cual permite hacer toomultiple regiones de datos de toodistribute con acceso de baja latencia en cualquier parte de la carga de trabajo de Hola. Este modelo se utiliza normalmente para las cargas de trabajo del publicador o el consumidor cuando hay un redactor en una única región geográfica y lectores distribuidos globalmente en otras regiones (lectura). 

También puede utilizar replicación global compatible de Azure Cosmos base de datos con toobuild de aplicaciones en el que se distribuyen globalmente lectores y escritores. En este documento se describe un patrón que permite lograr un acceso de lectura y escritura local para redactores distribuidos con Azure Cosmos DB.

## <a id="ExampleScenario"></a>Publicación de contenido: un escenario de ejemplo
Echemos un vistazo a una toodescribe de escenario de mundo real cómo puede usar los patrones de distribuidos globalmente varios-region/multi-maestro lectura y escritura con la base de datos de Azure Cosmos. Considere la posibilidad de una plataforma de publicación de contenido basada en Azure Cosmos DB. Estos son algunos requisitos que debe cumplir esta plataforma para una experiencia del usuario excelente para publicadores y consumidores.

* Los autores y los suscriptores se distribuyen en Hola a todos 
* Los autores deben publicar la región (cerca) local tootheir de artículos (escritura)
* Los autores tienen lectores/suscriptores de los artículos que se distribuyen en todo el mundo de Hola. 
* Los suscriptores deben recibir una notificación cuando se publican artículos nuevos.
* Los suscriptores deben ser capaz de tooread artículos de su región local. También deben ser capaz de tooadd revisiones toothese artículos. 
* Nadie, incluido el autor de Hola de artículos de hello debe ser capaz de ver que todos Hola revisiones tooarticles adjunto de un área local. 

Suponiendo que millones de los consumidores y editores con miles de millones de artículos, pronto tenemos problemas de hello tooconfront de escala junto con para garantizar la localidad de acceso. Al igual que con la mayoría de los problemas de escalabilidad, solución de Hola se encuentra en una buena estrategia de partición. A continuación, vamos a observar cómo toomodel artículos, revise y notificaciones como documentos, configuran cuentas de base de datos de Azure Cosmos e implementar una capa de acceso a datos. 

Si desea que toolearn más información sobre la creación de particiones y las claves de partición, vea [particiones y ajuste de escala en la base de datos de Azure Cosmos](partition-data.md).

## <a id="ModelingNotifications"></a>Modelado de notificaciones
Las notificaciones son usuario de tooa específico de fuentes de datos. Por lo tanto, los patrones de acceso de Hola para los documentos de las notificaciones están siempre en contexto Hola de usuario único. Por ejemplo, podría "registrar un usuario de notificación tooa" o "capturar todas las notificaciones para un usuario determinado". Por lo tanto, Hola idóneo de clave de partición para este tipo sería `UserId`.

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

## <a id="ModelingSubscriptions"></a>Modelado de suscripciones
Las suscripciones se pueden crear para diversos criterios, como una categoría específica de artículos de interés o un publicador específico. Por lo tanto, Hola `SubscriptionFilter` es una buena elección para la clave de partición.

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

## <a id="ModelingArticles"></a>Modelado de artículos
Una vez que se identifica un artículo a través de notificaciones, las consultas posteriores se basan normalmente en hello `Article.Id`. Elegir `Article.Id` como partición clave hello, por tanto, proporciona una distribución recomendada de Hola para almacenar los artículos dentro de una colección de base de datos de Azure Cosmos. 

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

## <a id="ModelingReviews"></a>Modelado de revisiones
Como artículos, revisiones principalmente se escriben y leer en el contexto de Hola de artículo. Elegir `ArticleId` como clave de partición proporciona la mejor distribución y un acceso eficaz a las revisiones asociadas al artículo. 

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

## <a id="DataAccessMethods"></a>Métodos de nivel de acceso a datos
Ahora Echemos un vistazo a los datos principales Hola necesitamos tooimplement de métodos de acceso. Esta es la lista de Hola de métodos que Hola `ContentPublishDatabase` necesita:

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Configuración de la cuenta de Azure Cosmos DB
tooguarantee local las lecturas y escrituras, se deben crear particiones de datos no solo en la clave de partición, pero también se basa en el patrón de acceso geográfica hello en regiones. modelo de Hello depende de tener una cuenta de base de datos de base de datos de Azure Cosmos de replicación geográfica para cada región. Por ejemplo, con dos regiones, a continuación se muestra una configuración para operaciones de escritura en varias regiones:

| Nombre de cuenta | Región de escritura | Región de lectura |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

Hello diagrama siguiente muestra cómo se realizan las lecturas y escrituras en una aplicación típica con este programa de instalación:

![Arquitectura con varios maestros de Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

Este es un fragmento de código que muestra cómo tooinitialize Hola clientes en un capa DAL ejecutando Hola `West US` región.
    
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

Con hello precede el programa de instalación, capa de acceso a datos de hello puede reenviar todas las escrituras toohello cuenta local en función de donde se implementa. Las lecturas se realizan mediante la lectura del tanto cuentas tooget Hola global en vista de datos. Este enfoque puede ser extendidos tooas muchas regiones según sea necesario. Por ejemplo, la siguiente es una configuración con tres regiones geográficas:

| Nombre de cuenta | Región de escritura | Región de lectura 1 | Región de lectura 2 |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>Implementación del nivel de acceso a datos
Ahora Echemos un vistazo a la implementación de Hola de capa de acceso a datos hello (DAL) para una aplicación con dos áreas de escritura. Hola DAL debe implementar Hola pasos:

* Crear varias instancias de `DocumentClient` para cada cuenta. Con dos regiones, cada instancia del nivel DAL tiene elementos `writeClient` y `readClient`. 
* En función de la región de hello implementada de la aplicación hello, configurar los extremos de Hola para `writeclient` y `readClient`. Por ejemplo, hello DAL se implementa en `West US` utiliza `contentpubdatabase-usa.documents.azure.com` para llevar a cabo escrituras. Hola DAL se implementa en `NorthEurope` utiliza `contentpubdatabase-europ.documents.azure.com` para operaciones de escritura.

Con hello precede el programa de instalación, se pueden implementar métodos de acceso a datos de Hola. Escribir operaciones reenvían Hola escritura toohello correspondiente `writeClient`.

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

Para leer las notificaciones y las revisiones, debe leer desde las regiones y los resultados de unión Hola tal y como se muestra en el siguiente fragmento de código de hello:

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

Por lo tanto, al elegir una buena clave de creación de particiones y una creación de particiones estática basada en cuentas, puede lograr que las lecturas y escrituras locales en varias regiones usen Azure Cosmos DB.

## <a id="NextSteps"></a>Pasos siguientes
En este artículo, se describe cómo puede usar los patrones de lectura y escritura en varias regiones distribuidos globalmente con Azure Cosmos DB, y usar la publicación de contenido como un escenario de ejemplo.

* Más información sobre la compatibilidad de Azure Cosmos DB con la [distribución global](distribute-data-globally.md)
* Más información sobre las [conmutaciones por error manuales y automáticas en Azure Cosmos DB](regional-failover.md)
* Más información sobre la [coherencia global con Azure Cosmos DB](consistency-levels.md)
* Desarrollar con varias regiones, con hello [base de datos de Azure Cosmos: API de documentos](tutorial-global-distribution-documentdb.md)
* Desarrollar con varias regiones, con hello [base de datos de Azure Cosmos: API de MongoDB](tutorial-global-distribution-MongoDB.md)
* Desarrollar con varias regiones, con hello [base de datos de Azure Cosmos: API de tabla](tutorial-global-distribution-table.md)

---
title: Modelado de datos del documento para una base de datos NoSQL | Microsoft Docs
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
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="a133a-104">Modelado de datos del documento para bases de datos NoSQL</span><span class="sxs-lookup"><span data-stu-id="a133a-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="a133a-105">Mientras que las bases de datos libres de esquemas, como Azure Cosmos DB, facilitan notablemente la adopción de cambios en el modelo de datos, debe dedicar algo de tiempo a pensar en los datos.</span><span class="sxs-lookup"><span data-stu-id="a133a-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="a133a-106">¿Cómo se van a almacenar los datos?</span><span class="sxs-lookup"><span data-stu-id="a133a-106">How is data going to be stored?</span></span> <span data-ttu-id="a133a-107">¿Cómo la aplicación va a recuperar y consultar los datos?</span><span class="sxs-lookup"><span data-stu-id="a133a-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="a133a-108">¿La aplicación realiza muchas operaciones de lectura o escritura?</span><span class="sxs-lookup"><span data-stu-id="a133a-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="a133a-109">Después de leer este artículo, podrá responder a las siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="a133a-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="a133a-110">¿Cómo debo pensar en un documento en una base de datos de documentos?</span><span class="sxs-lookup"><span data-stu-id="a133a-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="a133a-111">¿Qué es el modelado de datos y por qué tendría que importarme?</span><span class="sxs-lookup"><span data-stu-id="a133a-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="a133a-112">¿Cómo es el modelado de datos en una base de datos de documentos distinta de una base de datos relacional?</span><span class="sxs-lookup"><span data-stu-id="a133a-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="a133a-113">¿Cómo expreso relaciones de datos en una base de datos no relacional?</span><span class="sxs-lookup"><span data-stu-id="a133a-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="a133a-114">¿Cuándo se incrustan datos y cuándo realizo vinculaciones a los datos?</span><span class="sxs-lookup"><span data-stu-id="a133a-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="a133a-115">Incrustación de datos</span><span class="sxs-lookup"><span data-stu-id="a133a-115">Embedding data</span></span>
<span data-ttu-id="a133a-116">Al comenzar a modelar datos en un almacén de documentos, como Azure Cosmos DB, intente tratar las entidades como **documentos independientes** representados en JSON.</span><span class="sxs-lookup"><span data-stu-id="a133a-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="a133a-117">Antes de adentrarnos demasiado, nos gustaría volver a realizar algunos pasos y echar un vistazo a cómo podríamos modelar algo en una base de datos relacional, un asunto con el que muchos de nosotros ya estamos familiarizados.</span><span class="sxs-lookup"><span data-stu-id="a133a-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="a133a-118">En el ejemplo siguiente se muestra puede almacenarse una persona en una base de datos relacional.</span><span class="sxs-lookup"><span data-stu-id="a133a-118">The following example shows how a person might be stored in a relational database.</span></span> 

![Modelo de base de datos relacional](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="a133a-120">Al trabajar con bases de datos relacionales, hemos aprendido durante años a normalizar constantemente.</span><span class="sxs-lookup"><span data-stu-id="a133a-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="a133a-121">La normalización de los datos implica normalmente tomar una entidad, como una persona, y dividirla en piezas de datos discretas.</span><span class="sxs-lookup"><span data-stu-id="a133a-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="a133a-122">En el ejemplo anterior, una persona puede tener varios registros de información de contacto, así como varios registros de dirección.</span><span class="sxs-lookup"><span data-stu-id="a133a-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="a133a-123">Podemos ir incluso un paso más allá y desglosar detalles de contacto extrayendo aún más campos comunes, como un tipo.</span><span class="sxs-lookup"><span data-stu-id="a133a-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="a133a-124">Al igual que ocurre con la dirección, cada registro aquí tiene un tipo como *doméstico* o *empresarial*.</span><span class="sxs-lookup"><span data-stu-id="a133a-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="a133a-125">La premisa principal cuando se normalizan datos es la de **evitar el almacenamiento de datos redundantes** en cada registro y, en su lugar, hacer referencia a los datos.</span><span class="sxs-lookup"><span data-stu-id="a133a-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="a133a-126">En este ejemplo, para leer a una persona, con toda su información de contacto y direcciones, tendrá que utilizar CONEXIONES para agregar de forma eficaz los datos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a133a-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="a133a-127">La actualización de una única persona con su información de contacto y direcciones requiere operaciones de escritura en muchas tablas individuales.</span><span class="sxs-lookup"><span data-stu-id="a133a-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="a133a-128">Ahora veamos cómo modelamos los mismos datos como una entidad independiente en una base de datos de documentos.</span><span class="sxs-lookup"><span data-stu-id="a133a-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="a133a-129">Mediante el enfoque anterior, ahora hemos **desnormalizado** el registro de la persona en el que hemos **incrustado** toda la información relacionada con esta persona, como su información de contacto y direcciones, en un único documento JSON.</span><span class="sxs-lookup"><span data-stu-id="a133a-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="a133a-130">Además, puesto que no estamos limitados a un esquema fijo, contamos con la flexibilidad para hacer cosas como tener información de contacto de formas diferentes por completo.</span><span class="sxs-lookup"><span data-stu-id="a133a-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="a133a-131">Recuperar un registro de persona completa de la base de datos es ahora una única operación de lectura frente a una colección única y para un documento único.</span><span class="sxs-lookup"><span data-stu-id="a133a-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="a133a-132">La actualización de un registro de una persona, con su información de contacto y direcciones, es también una operación de escritura única frente a un documento único.</span><span class="sxs-lookup"><span data-stu-id="a133a-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="a133a-133">Mediante la desnormalización de datos, es posible que la aplicación tenga que emitir menos consultas y actualizaciones para completar operaciones frecuentes.</span><span class="sxs-lookup"><span data-stu-id="a133a-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="a133a-134">Cuándo se debe realizar la incrustación</span><span class="sxs-lookup"><span data-stu-id="a133a-134">When to embed</span></span>
<span data-ttu-id="a133a-135">Por lo general, use los modelos de datos de incrustación cuando:</span><span class="sxs-lookup"><span data-stu-id="a133a-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="a133a-136">Existen relaciones de **inclusión** entre entidades.</span><span class="sxs-lookup"><span data-stu-id="a133a-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="a133a-137">Existen relaciones de **uno a algunos** entre entidades.</span><span class="sxs-lookup"><span data-stu-id="a133a-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="a133a-138">Existen datos incrustados que **cambian con poca frecuencia**.</span><span class="sxs-lookup"><span data-stu-id="a133a-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="a133a-139">Existen datos incrustados que no crecerán **sin límites**.</span><span class="sxs-lookup"><span data-stu-id="a133a-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="a133a-140">Existen datos incrustados que se **integran** en los datos en un documento.</span><span class="sxs-lookup"><span data-stu-id="a133a-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="a133a-141">Los modelos de datos desnormalizados normalmente proporcionan un mejor rendimiento de **lectura** .</span><span class="sxs-lookup"><span data-stu-id="a133a-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="a133a-142">Cuándo no se debe incrustar</span><span class="sxs-lookup"><span data-stu-id="a133a-142">When not to embed</span></span>
<span data-ttu-id="a133a-143">Puesto que la regla general en una base de datos de documentos es desnormalizarlo todo e incrustar todos los datos en un único documento, es posible que se produzcan situaciones que se deben evitar.</span><span class="sxs-lookup"><span data-stu-id="a133a-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="a133a-144">Seleccione este fragmento JSON.</span><span class="sxs-lookup"><span data-stu-id="a133a-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="a133a-145">Este podría el aspecto de una entidad de publicación con comentarios incrustados si se ha modelado un sistema, CMS o blog normales.</span><span class="sxs-lookup"><span data-stu-id="a133a-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="a133a-146">El problema con este ejemplo es que la matriz de comentarios **no está limitada**, lo que significa que no hay ningún límite (práctico) para el número de comentarios que puede tener cualquier publicación única.</span><span class="sxs-lookup"><span data-stu-id="a133a-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="a133a-147">Esto será un problema, ya que el tamaño del documento puede aumentar notablemente.</span><span class="sxs-lookup"><span data-stu-id="a133a-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="a133a-148">Puesto que el tamaño del documento aumenta la capacidad de transmisión de los datos a través de la conexión, así como la lectura y actualización del documento, a escala, se producirá un impacto en ellos.</span><span class="sxs-lookup"><span data-stu-id="a133a-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="a133a-149">En este caso sería mejor tener en cuenta el siguiente modelo.</span><span class="sxs-lookup"><span data-stu-id="a133a-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
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

<span data-ttu-id="a133a-150">Este modelo tiene los tres últimos comentarios insertados en la propia publicación, que es una matriz con un límite fijo esta vez.</span><span class="sxs-lookup"><span data-stu-id="a133a-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="a133a-151">Los demás comentarios se agrupan en lotes de 100 comentarios y se almacenan en documentos independientes.</span><span class="sxs-lookup"><span data-stu-id="a133a-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="a133a-152">El tamaño del lote se ha seleccionado como 100, puesto que nuestra aplicación ficticia permite al usuario cargar 100 comentarios a la vez.</span><span class="sxs-lookup"><span data-stu-id="a133a-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="a133a-153">Otro caso en el que la incrustación de datos no es una buena opción es cuando los datos incrustados se utilizan a menudo en documentos y cambian con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="a133a-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="a133a-154">Seleccione este fragmento JSON.</span><span class="sxs-lookup"><span data-stu-id="a133a-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="a133a-155">Esto podría representar la cartera de acciones de una persona.</span><span class="sxs-lookup"><span data-stu-id="a133a-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="a133a-156">Hemos elegido incrustar la información de las acciones en cada documento de la cartera.</span><span class="sxs-lookup"><span data-stu-id="a133a-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="a133a-157">En un entorno donde los datos relacionados cambian con frecuencia, como una aplicación de comercio bursátil, la incrustación de datos que cambian con frecuencia significará que está actualizando constantemente cada documento de la cartera cada vez que se negocia una acción.</span><span class="sxs-lookup"><span data-stu-id="a133a-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="a133a-158">Es posible negociar con la acción *zaza* cientos de veces en un solo día y miles de usuarios pueden tener *zaza* en su cartera.</span><span class="sxs-lookup"><span data-stu-id="a133a-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="a133a-159">Con un modelo de datos como el anterior, tendríamos que actualizar miles de documentos de cartera varias veces al día, por lo que daría lugar a una escalación del sistema no muy buena.</span><span class="sxs-lookup"><span data-stu-id="a133a-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="a133a-160"><a id="Refer"></a>Datos de referencia</span><span class="sxs-lookup"><span data-stu-id="a133a-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="a133a-161">Por lo tanto, la incrustación de datos funciona bien en muchos casos, pero está claro que hay escenarios en los que la desnormalización de los datos provocará más problemas que ventajas.</span><span class="sxs-lookup"><span data-stu-id="a133a-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="a133a-162">¿Qué hacemos ahora?</span><span class="sxs-lookup"><span data-stu-id="a133a-162">So what do we do now?</span></span> 

<span data-ttu-id="a133a-163">Las bases de datos relacionales no son el único lugar donde puede crear relaciones entre entidades.</span><span class="sxs-lookup"><span data-stu-id="a133a-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="a133a-164">En una base de datos de documentos puede tener información en un documento que realmente se relacione con los datos en otros documentos.</span><span class="sxs-lookup"><span data-stu-id="a133a-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="a133a-165">No soy partidario ahora de dedicar ni un solo minuto a crear sistemas que podrían ser más adecuados para una base de datos relacional en Azure Cosmos DB o cualquier otra base de datos de documentos, ya que las relaciones simples son correctas y pueden ser muy útiles.</span><span class="sxs-lookup"><span data-stu-id="a133a-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="a133a-166">En el siguiente JSON hemos optado por utilizar el ejemplo de una cartera de acciones anteriores, pero esta vez hacemos referencia al artículo comercial en la cartera en lugar de incrustarlo.</span><span class="sxs-lookup"><span data-stu-id="a133a-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="a133a-167">De esa forma, cuando el artículo comercial cambia frecuentemente a lo largo del día, el único documento que tiene que actualizarse es el documento de acciones único.</span><span class="sxs-lookup"><span data-stu-id="a133a-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

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


<span data-ttu-id="a133a-168">Sin embargo, una desventaja de este enfoque inmediato es si la aplicación es necesaria para mostrar información sobre cada acción que se mantiene al mostrar la cartera de una persona; en este caso necesitaría realizar varios viajes a la base de datos para cargar la información de cada documento de acciones.</span><span class="sxs-lookup"><span data-stu-id="a133a-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="a133a-169">Aquí hemos tomado una decisión de mejorar la eficacia de las operaciones de escritura, que se producen con frecuencia a lo largo del día, pero a su vez, se comprometen las operaciones de lectura que potencialmente tienen un menor impacto en el rendimiento de este sistema en particular.</span><span class="sxs-lookup"><span data-stu-id="a133a-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="a133a-170">Los modelos de datos normalizados **pueden requerir varios viajes de ida y vuelta** al servidor.</span><span class="sxs-lookup"><span data-stu-id="a133a-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="a133a-171">¿Qué sucede con las claves externas?</span><span class="sxs-lookup"><span data-stu-id="a133a-171">What about foreign keys?</span></span>
<span data-ttu-id="a133a-172">Puesto que actualmente no hay ningún concepto de restricción, clave externa o de otra índole, las relaciones entre documentos que tienen en los documentos son efectivamente "puntos débiles" y la base de datos no los comprobará.</span><span class="sxs-lookup"><span data-stu-id="a133a-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="a133a-173">Si desea asegurarse de que los datos a los que hace referencia un documento existen realmente, debe hacerlo en la aplicación o mediante el uso de desencadenadores de servidor o procedimientos almacenados en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a133a-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="a133a-174">Cuándo se debe establecer referencias</span><span class="sxs-lookup"><span data-stu-id="a133a-174">When to reference</span></span>
<span data-ttu-id="a133a-175">Por lo general, se deben utilizar modelos de datos normalizados cuando:</span><span class="sxs-lookup"><span data-stu-id="a133a-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="a133a-176">Se realiza una representación de relaciones de **uno a varios** .</span><span class="sxs-lookup"><span data-stu-id="a133a-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="a133a-177">Se realiza una representación de las relaciones de **muchos a muchos** .</span><span class="sxs-lookup"><span data-stu-id="a133a-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="a133a-178">Los datos relacionados **cambian con frecuencia**.</span><span class="sxs-lookup"><span data-stu-id="a133a-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="a133a-179">Puede **cancelarse el límite**de los datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="a133a-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="a133a-180">Normalmente, la normalización proporciona un mejor rendimiento de **escritura** .</span><span class="sxs-lookup"><span data-stu-id="a133a-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="a133a-181">¿Dónde coloco la relación?</span><span class="sxs-lookup"><span data-stu-id="a133a-181">Where do I put the relationship?</span></span>
<span data-ttu-id="a133a-182">El crecimiento de la relación le ayudará a determinar en qué documento almacenar la referencia.</span><span class="sxs-lookup"><span data-stu-id="a133a-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="a133a-183">Si observamos el JSON siguiente que sirve como modelo para los publicadores y los libros.</span><span class="sxs-lookup"><span data-stu-id="a133a-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="a133a-184">Si el número de libros por publicador es reducido con un crecimiento limitado, almacenar la referencia del libro dentro del documento del publicador puede ser útil.</span><span class="sxs-lookup"><span data-stu-id="a133a-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="a133a-185">Sin embargo, si el número de libros por publicador no tiene un límite, este modelo de datos llevaría provocaría matrices crecientes y mutables como ocurre en el documento de publicador de ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="a133a-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="a133a-186">Cambiar las cosas un poco provocaría la creación de un modelo que seguiría representando los mismos datos, pero que evitaría esas grandes colecciones mutables.</span><span class="sxs-lookup"><span data-stu-id="a133a-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="a133a-187">En el ejemplo anterior, hemos eliminado la colección ilimitada en el documento del publicador.</span><span class="sxs-lookup"><span data-stu-id="a133a-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="a133a-188">En su lugar, solo tenemos una referencia al publicador en cada documento del libro.</span><span class="sxs-lookup"><span data-stu-id="a133a-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="a133a-189">¿Cómo se puede modelar las relaciones de varios a varios?</span><span class="sxs-lookup"><span data-stu-id="a133a-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="a133a-190">En una base de datos relacional, las relaciones *varios a varios* modelan con frecuencia con tablas de unión, que simplemente unen registros de otras tablas.</span><span class="sxs-lookup"><span data-stu-id="a133a-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Combinar tablas](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="a133a-192">Podría verse tentado a replicar lo mismo con documentos y producir un modelo de datos que tenga un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="a133a-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="a133a-193">Esto funcionaría.</span><span class="sxs-lookup"><span data-stu-id="a133a-193">This would work.</span></span> <span data-ttu-id="a133a-194">Sin embargo, cargar un autor con sus libros o cargar un libro con su autor siempre requeriría al menos dos consultas adicionales en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a133a-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="a133a-195">Una consulta para el documento de unión y, a continuación, otra consulta para capturar el documento real que se está uniendo.</span><span class="sxs-lookup"><span data-stu-id="a133a-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="a133a-196">Si todo lo que hace esta tabla de unión es combinar dos datos, ¿por qué no quitarla completamente?</span><span class="sxs-lookup"><span data-stu-id="a133a-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="a133a-197">Tenga en cuenta lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="a133a-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="a133a-198">Ahora, si tuviera un autor, sabría de inmediato qué libros ha escrito y, a la inversa, si tuviera un documento del libro cargado sabría los identificadores de los autores.</span><span class="sxs-lookup"><span data-stu-id="a133a-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="a133a-199">Esto ahorra la consulta intermedia de la tabla de unión, por lo que se reduce el número de viajes de ida y vuelta al servidor que tiene que realizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a133a-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="a133a-200"><a id="WrapUp"></a>Modelos de datos híbridos</span><span class="sxs-lookup"><span data-stu-id="a133a-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="a133a-201">Ya hemos observado la incrustación (o desnormalización) y el establecimiento de referencias (o normalización). Cada opción tiene sus ventajas y compromisos, como hemos visto.</span><span class="sxs-lookup"><span data-stu-id="a133a-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="a133a-202">No tiene por qué ser siempre una u otra. No tenga miedo de mezclarlas un poco.</span><span class="sxs-lookup"><span data-stu-id="a133a-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="a133a-203">En función de las cargas de trabajo y los diseños de uso específico de la aplicación, es posible que existan casos en los que mezclar los datos de referencia e incrustados tenga sentido y puede generar una lógica de aplicación más simple con menos viajes de ida y vuelta de servidor a la vez que se sigue manteniendo un buen nivel de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a133a-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="a133a-204">Considere el siguiente JSON.</span><span class="sxs-lookup"><span data-stu-id="a133a-204">Consider the following JSON.</span></span> 

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

<span data-ttu-id="a133a-205">Aquí hemos seguido principalmente el modelo de incrustación, donde los datos de otras entidades se incrustan en el documento de nivel superior, pero se establece la referencia en otros datos.</span><span class="sxs-lookup"><span data-stu-id="a133a-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="a133a-206">Si observa el documento del libro, podemos ver algunos campos interesantes cuando nos centramos en la matriz de autores.</span><span class="sxs-lookup"><span data-stu-id="a133a-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="a133a-207">Hay un campo *id* que es el campo que se utiliza para volver a hacer referencia a un documento de autor, una práctica estándar en un modelo normalizado, pero también tenemos *name* y *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="a133a-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="a133a-208">Podríamos habernos parado en *id* y dejar la aplicación para obtener información adicional que necesita a partir del documento de autor correspondiente mediante el "vínculo", pero como nuestra aplicación muestra el nombre del autor y una imagen en miniatura con cada libro mostrado, podemos ahorrar un viaje de ida y vuelta al servidor por libro en una lista mediante la desnormalización de **algunos** datos del autor.</span><span class="sxs-lookup"><span data-stu-id="a133a-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="a133a-209">Por supuesto, si cambia el nombre del autor o desean actualizar sus fotos, tendríamos que realizar una actualización de cada libro publicado, pero para nuestra aplicación, que se basa en la suposición de que los autores no cambian sus nombres muy a menudo, se trata de una decisión de diseño aceptable.</span><span class="sxs-lookup"><span data-stu-id="a133a-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="a133a-210">En el ejemplo hay valores de **adiciones calculadas previamente** para ahorrar un procesamiento costoso en una operación de lectura.</span><span class="sxs-lookup"><span data-stu-id="a133a-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="a133a-211">En el ejemplo, algunos de los datos incrustados en el documento del autor son datos que se calculan en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a133a-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="a133a-212">Cada vez que se publica un nuevo libro, se crea un documento de libro **y** el campo countOfBooks se establece en un valor calculado en función del número de documentos de libro que existen para un autor concreto.</span><span class="sxs-lookup"><span data-stu-id="a133a-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="a133a-213">Esta optimización sería adecuada en sistemas en los que se realizan muchas operaciones de lectura, donde podemos permitirnos hacer cálculos en las escrituras para optimizarlas.</span><span class="sxs-lookup"><span data-stu-id="a133a-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="a133a-214">La capacidad de tener un modelo con campos calculados previamente es posible porque Azure Cosmos DB admite **transacciones de varios documentos**.</span><span class="sxs-lookup"><span data-stu-id="a133a-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="a133a-215">Muchos almacenes NoSQL no pueden realizar transacciones en documentos y, por lo tanto, recomiendan las decisiones de diseño, por ejemplo, "siempre incrustar todo", debido a esa limitación.</span><span class="sxs-lookup"><span data-stu-id="a133a-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="a133a-216">Con Azure Cosmos DB, puede utilizar los desencadenadores del servidor o los procedimientos almacenados que insertan los libros y actualizan los autores dentro de una transacción ACID.</span><span class="sxs-lookup"><span data-stu-id="a133a-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="a133a-217">Ahora no **tiene** que incrustar todo en un documento para asegurarse de que los datos sigan siendo coherentes.</span><span class="sxs-lookup"><span data-stu-id="a133a-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="a133a-218"><a name="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a133a-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="a133a-219">Lo más importante de este artículo es comprender que el modelado de datos en un mundo sin esquemas es más importante que nunca.</span><span class="sxs-lookup"><span data-stu-id="a133a-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="a133a-220">Como no hay ninguna manera única de representar un elemento de datos en una pantalla, no hay una única forma de modelar los datos.</span><span class="sxs-lookup"><span data-stu-id="a133a-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="a133a-221">Necesita comprender la aplicación y saber cómo producirá, consumirá y procesará los datos.</span><span class="sxs-lookup"><span data-stu-id="a133a-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="a133a-222">A continuación, mediante la aplicación de algunas directrices presentadas aquí, puede crear un modelo que aborde las necesidades inmediatas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a133a-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="a133a-223">Cuando las aplicaciones necesitan cambiar, puede aprovechar la flexibilidad de una base de datos sin esquemas para adoptar ese cambio y que el modelo de datos evolucione con facilidad.</span><span class="sxs-lookup"><span data-stu-id="a133a-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="a133a-224">Para más información sobre Azure Cosmos DB, consulte la página de [documentación](https://azure.microsoft.com/documentation/services/cosmos-db/) del servicio.</span><span class="sxs-lookup"><span data-stu-id="a133a-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="a133a-225">Para comprender cómo particionar los datos en varias particiones, consulte [Partición de datos en Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="a133a-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 

---
title: datos del documento aaaModeling para una base de datos NoSQL | Documentos de Microsoft
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
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="fed31-104">Modelado de datos del documento para bases de datos NoSQL</span><span class="sxs-lookup"><span data-stu-id="fed31-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="fed31-105">Mientras sin esquemas bases de datos, como la base de datos de Azure Cosmos facilitan super modelo de datos de tooyour tooembrace cambios todavía debe dedicar algún tiempo pensar sobre los datos.</span><span class="sxs-lookup"><span data-stu-id="fed31-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="fed31-106">¿Cómo van toobe almacena datos?</span><span class="sxs-lookup"><span data-stu-id="fed31-106">How is data going toobe stored?</span></span> <span data-ttu-id="fed31-107">¿Cómo son los datos de tooretrieve y consulta de curso de aplicación?</span><span class="sxs-lookup"><span data-stu-id="fed31-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="fed31-108">¿La aplicación realiza muchas operaciones de lectura o escritura?</span><span class="sxs-lookup"><span data-stu-id="fed31-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="fed31-109">Después de leer este artículo, será hello tooanswer pueda siguientes preguntas:</span><span class="sxs-lookup"><span data-stu-id="fed31-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="fed31-110">¿Cómo debo pensar en un documento en una base de datos de documentos?</span><span class="sxs-lookup"><span data-stu-id="fed31-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="fed31-111">¿Qué es el modelado de datos y por qué tendría que importarme?</span><span class="sxs-lookup"><span data-stu-id="fed31-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="fed31-112">¿Cómo es modelar los datos en una base de datos documento relacional tooa diferentes de base de datos?</span><span class="sxs-lookup"><span data-stu-id="fed31-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="fed31-113">¿Cómo expreso relaciones de datos en una base de datos no relacional?</span><span class="sxs-lookup"><span data-stu-id="fed31-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="fed31-114">¿Cuándo se puede incrustar los datos y cuándo puedo vincular toodata?</span><span class="sxs-lookup"><span data-stu-id="fed31-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="fed31-115">Incrustación de datos</span><span class="sxs-lookup"><span data-stu-id="fed31-115">Embedding data</span></span>
<span data-ttu-id="fed31-116">Al comenzar a modelar los datos en un almacén de documentos, como la base de datos de Azure Cosmos, intente tootreat las entidades como **documentos independientes** representado en JSON.</span><span class="sxs-lookup"><span data-stu-id="fed31-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="fed31-117">Antes de adentrarnos demasiado, nos gustaría volver a realizar algunos pasos y echar un vistazo a cómo podríamos modelar algo en una base de datos relacional, un asunto con el que muchos de nosotros ya estamos familiarizados.</span><span class="sxs-lookup"><span data-stu-id="fed31-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="fed31-118">Hello en el ejemplo siguiente se muestra cómo se podría almacenar una persona en una base de datos relacional.</span><span class="sxs-lookup"><span data-stu-id="fed31-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![Modelo de base de datos relacional](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="fed31-120">Cuando se trabaja con bases de datos relacionales, nos hemos ha aprendido para toonormalize años, normalizar, normalizar.</span><span class="sxs-lookup"><span data-stu-id="fed31-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="fed31-121">Normalizar los datos normalmente implica tomar una entidad, como una persona y presenta la información estructurada en toodiscrete partes de los datos.</span><span class="sxs-lookup"><span data-stu-id="fed31-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="fed31-122">En el ejemplo de Hola anterior, una persona puede tener varios registros de detalle de contacto, así como varios registros de dirección.</span><span class="sxs-lookup"><span data-stu-id="fed31-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="fed31-123">Podemos ir incluso un paso más allá y desglosar detalles de contacto extrayendo aún más campos comunes, como un tipo.</span><span class="sxs-lookup"><span data-stu-id="fed31-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="fed31-124">Al igual que ocurre con la dirección, cada registro aquí tiene un tipo como *doméstico* o *empresarial*.</span><span class="sxs-lookup"><span data-stu-id="fed31-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="fed31-125">Hola guiar local cuando la normalización de datos es demasiado**evitar el almacenamiento de datos redundantes** en cada registro y en su lugar, consulte toodata.</span><span class="sxs-lookup"><span data-stu-id="fed31-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="fed31-126">En este ejemplo, tooread una persona, con todos sus detalles de contacto y las direcciones, necesita toouse combinaciones tooeffectively agregado los datos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fed31-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="fed31-127">La actualización de una única persona con su información de contacto y direcciones requiere operaciones de escritura en muchas tablas individuales.</span><span class="sxs-lookup"><span data-stu-id="fed31-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="fed31-128">Ahora vamos a echar un vistazo a cómo se podría modelo Hola mismo datos como una entidad independiente en una base de datos del documento.</span><span class="sxs-lookup"><span data-stu-id="fed31-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="fed31-129">Con el anterior de enfoque Hola ahora tenemos **sin normalizar** Hola registro persona donde se **incrustado** todos Hola información relacionada con la persona de toothis, como sus detalles de contacto y direcciones, en tooa único Documento JSON.</span><span class="sxs-lookup"><span data-stu-id="fed31-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="fed31-130">Además, dado que no nos estamos confinados tooa un esquema fijo que tenemos Hola flexibilidad toodo cosas con detalles de contacto de distintas formas completamente.</span><span class="sxs-lookup"><span data-stu-id="fed31-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="fed31-131">La recuperación de un registro de la persona que completa de base de datos de hello es ahora una única operación en una sola colección y de un solo documento de lectura.</span><span class="sxs-lookup"><span data-stu-id="fed31-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="fed31-132">La actualización de un registro de una persona, con su información de contacto y direcciones, es también una operación de escritura única frente a un documento único.</span><span class="sxs-lookup"><span data-stu-id="fed31-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="fed31-133">Al eliminar la normalización de datos, la aplicación puede necesitar tooissue menos las consultas y actualizaciones toocomplete operaciones comunes.</span><span class="sxs-lookup"><span data-stu-id="fed31-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="fed31-134">Cuando tooembed</span><span class="sxs-lookup"><span data-stu-id="fed31-134">When tooembed</span></span>
<span data-ttu-id="fed31-135">Por lo general, use los modelos de datos de incrustación cuando:</span><span class="sxs-lookup"><span data-stu-id="fed31-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="fed31-136">Existen relaciones de **inclusión** entre entidades.</span><span class="sxs-lookup"><span data-stu-id="fed31-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="fed31-137">Existen relaciones de **uno a algunos** entre entidades.</span><span class="sxs-lookup"><span data-stu-id="fed31-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="fed31-138">Existen datos incrustados que **cambian con poca frecuencia**.</span><span class="sxs-lookup"><span data-stu-id="fed31-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="fed31-139">Existen datos incrustados que no crecerán **sin límites**.</span><span class="sxs-lookup"><span data-stu-id="fed31-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="fed31-140">No hay datos incrustados **integral** toodata en un documento.</span><span class="sxs-lookup"><span data-stu-id="fed31-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="fed31-141">Los modelos de datos desnormalizados normalmente proporcionan un mejor rendimiento de **lectura** .</span><span class="sxs-lookup"><span data-stu-id="fed31-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="fed31-142">Cuando no tooembed</span><span class="sxs-lookup"><span data-stu-id="fed31-142">When not tooembed</span></span>
<span data-ttu-id="fed31-143">Mientras Hola regla general en una base de datos de documento es toodenormalize todo el contenido y lo inserte todos los datos en tooa único documento, esto puede provocar situaciones toosome que deberían evitarse.</span><span class="sxs-lookup"><span data-stu-id="fed31-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="fed31-144">Seleccione este fragmento JSON.</span><span class="sxs-lookup"><span data-stu-id="fed31-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="fed31-145">Este podría el aspecto de una entidad de publicación con comentarios incrustados si se ha modelado un sistema, CMS o blog normales.</span><span class="sxs-lookup"><span data-stu-id="fed31-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="fed31-146">problema con este ejemplo Hello es ese hello matriz comentarios es **unbounded**, lo que significa que no hay ningún número de toohello límite (práctico) de los comentarios puede tener cualquier mensaje único.</span><span class="sxs-lookup"><span data-stu-id="fed31-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="fed31-147">Esto se convertirá en un problema como tamaño de saludo del documento de hello podría crecer significativamente.</span><span class="sxs-lookup"><span data-stu-id="fed31-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="fed31-148">Como tamaño de Hola de hello documento crece en datos de saludo capacidad tootransmit Hola sobre conexión de hello, así como la lectura y actualización documento hello, a escala, se verán afectado.</span><span class="sxs-lookup"><span data-stu-id="fed31-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="fed31-149">En este caso sería mejor hello tooconsider siguiendo el modelo.</span><span class="sxs-lookup"><span data-stu-id="fed31-149">In this case it would be better tooconsider hello following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
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

<span data-ttu-id="fed31-150">Este modelo tiene comentarios más reciente de hello tres incrustados en hello contabilizar por sí mismo, que es una matriz con un límite fijo esta hora.</span><span class="sxs-lookup"><span data-stu-id="fed31-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="fed31-151">Hello otros comentarios se agrupan en toobatches de 100 comentarios y se almacenan en documentos independientes.</span><span class="sxs-lookup"><span data-stu-id="fed31-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="fed31-152">tamaño de Hola de lote de Hola se ha elegido como 100 porque nuestra aplicación ficticia permite Hola comentarios del usuario tooload 100 a la vez.</span><span class="sxs-lookup"><span data-stu-id="fed31-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="fed31-153">Otro caso donde la incrustación de datos no son una buena idea es cuando Hola incrusta datos se utilizan con frecuencia en documentos y cambian con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="fed31-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="fed31-154">Seleccione este fragmento JSON.</span><span class="sxs-lookup"><span data-stu-id="fed31-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="fed31-155">Esto podría representar la cartera de acciones de una persona.</span><span class="sxs-lookup"><span data-stu-id="fed31-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="fed31-156">Información bursátil de tooembed Hola que hemos elegido en el documento de la cartera de tooeach.</span><span class="sxs-lookup"><span data-stu-id="fed31-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="fed31-157">En un entorno donde está cambiando con frecuencia, los datos relacionados como una aplicación, de operaciones bursátiles incrustación de datos que cambian con frecuencia va toomean que está actualizando constantemente cada documento cartera cada vez que una cotización.</span><span class="sxs-lookup"><span data-stu-id="fed31-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="fed31-158">Es posible negociar con la acción *zaza* cientos de veces en un solo día y miles de usuarios pueden tener *zaza* en su cartera.</span><span class="sxs-lookup"><span data-stu-id="fed31-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="fed31-159">Con un modelo de datos como Hola anterior tendríamos tooupdate varios miles de documentos de cartera muchas veces al día a la izquierda tooa sistema que no se escala muy bien.</span><span class="sxs-lookup"><span data-stu-id="fed31-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="fed31-160"><a id="Refer"></a>Datos de referencia</span><span class="sxs-lookup"><span data-stu-id="fed31-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="fed31-161">Por lo tanto, la incrustación de datos funciona bien en muchos casos, pero está claro que hay escenarios en los que la desnormalización de los datos provocará más problemas que ventajas.</span><span class="sxs-lookup"><span data-stu-id="fed31-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="fed31-162">¿Qué hacemos ahora?</span><span class="sxs-lookup"><span data-stu-id="fed31-162">So what do we do now?</span></span> 

<span data-ttu-id="fed31-163">Bases de datos relacionales no son lugar solo Hola donde puede crear relaciones entre entidades.</span><span class="sxs-lookup"><span data-stu-id="fed31-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="fed31-164">En una base de datos de documento puede tener información en un documento que está realmente relacionado toodata en otros documentos.</span><span class="sxs-lookup"><span data-stu-id="fed31-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="fed31-165">Ahora, estoy no recomendando para incluso un minuto que se desarrollan sistemas que serían mejor base de datos relacional tooa adecuado en la base de datos de Azure Cosmos o cualquier otra base de datos del documento, pero relaciones simples son válidas y pueden ser muy útiles.</span><span class="sxs-lookup"><span data-stu-id="fed31-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="fed31-166">Hola JSON siguiente elegimos el ejemplo de Hola a toouse de una cartera de cotizaciones anteriormente pero esta vez que nos referimos toohello elemento estándar en la cartera de hello en lugar de incrustarla.</span><span class="sxs-lookup"><span data-stu-id="fed31-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="fed31-167">De esta manera, al elemento en existencias Hola cambia con frecuencia a lo largo de hello día Hola solo documento que necesite toobe actualizado es único documento de cotizaciones Hola.</span><span class="sxs-lookup"><span data-stu-id="fed31-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

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


<span data-ttu-id="fed31-168">Un inconveniente inmediata toothis aunque consiste si su aplicación es tooshow requiere información sobre cada acción que se mantiene al mostrar una cartera de una persona; en este caso se necesita toomake varios viajes toohello base de datos tooload Hola información para cada documento estándar.</span><span class="sxs-lookup"><span data-stu-id="fed31-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="fed31-169">Aquí hemos realizado una decisión tooimprove Hola la eficacia de operaciones de escritura, que ocurrir con frecuencia a lo largo de día de hello, pero a su vez en peligro en hello operaciones de lectura que probablemente tengan menos impacto en el rendimiento de Hola de este sistema determinado.</span><span class="sxs-lookup"><span data-stu-id="fed31-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="fed31-170">Modelos de datos normalizados **puede requerir más ciclos de ida y** toohello server.</span><span class="sxs-lookup"><span data-stu-id="fed31-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="fed31-171">¿Qué sucede con las claves externas?</span><span class="sxs-lookup"><span data-stu-id="fed31-171">What about foreign keys?</span></span>
<span data-ttu-id="fed31-172">Porque actualmente no hay ningún concepto de una restricción, clave externa o de otra manera, las relaciones entre documentos que tienen en los documentos son "puntos débiles" y no se comprobarán Hola propia base de datos.</span><span class="sxs-lookup"><span data-stu-id="fed31-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="fed31-173">Si desea tooensure que Hola datos que hace referencia a un documento tooactually existe, deberá toodo esto en la aplicación, o mediante el uso de saludo del servidor desencadenadores o procedimientos almacenados en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fed31-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="fed31-174">Cuando tooreference</span><span class="sxs-lookup"><span data-stu-id="fed31-174">When tooreference</span></span>
<span data-ttu-id="fed31-175">Por lo general, se deben utilizar modelos de datos normalizados cuando:</span><span class="sxs-lookup"><span data-stu-id="fed31-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="fed31-176">Se realiza una representación de relaciones de **uno a varios** .</span><span class="sxs-lookup"><span data-stu-id="fed31-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="fed31-177">Se realiza una representación de las relaciones de **muchos a muchos** .</span><span class="sxs-lookup"><span data-stu-id="fed31-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="fed31-178">Los datos relacionados **cambian con frecuencia**.</span><span class="sxs-lookup"><span data-stu-id="fed31-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="fed31-179">Puede **cancelarse el límite**de los datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="fed31-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="fed31-180">Normalmente, la normalización proporciona un mejor rendimiento de **escritura** .</span><span class="sxs-lookup"><span data-stu-id="fed31-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="fed31-181">¿Dónde se puede colocar relación Hola?</span><span class="sxs-lookup"><span data-stu-id="fed31-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="fed31-182">crecimiento de Hola de relación de hello le ayudará a determinar en qué referencia del documento toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="fed31-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="fed31-183">Si miramos Hola JSON siguiente que modela publicadores y libros.</span><span class="sxs-lookup"><span data-stu-id="fed31-183">If we look at hello JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

<span data-ttu-id="fed31-184">Si es poco a poco con crecimiento limitado número Hola de libros de Hola por publicador, puede ser útil, a continuación, almacenar referencia del libro de hello dentro de documento de publisher Hola.</span><span class="sxs-lookup"><span data-stu-id="fed31-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="fed31-185">Sin embargo, si el número de Hola de libros por publicador es ilimitado, este modelo de datos conduciría toomutable, aumentando las matrices, como en el documento de publicador de ejemplo de Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="fed31-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="fed31-186">Cambiar cosas alrededor de un bit haría resultado en un modelo que representa todavía Hola los mismos datos pero ahora evita estas grandes colecciones mutables.</span><span class="sxs-lookup"><span data-stu-id="fed31-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="fed31-187">Hola ejemplo anterior, hemos eliminado Hola colección sin enlazar en el documento de publisher Hola.</span><span class="sxs-lookup"><span data-stu-id="fed31-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="fed31-188">En su lugar, basta con un publicador toohello referencia en cada documento del libro.</span><span class="sxs-lookup"><span data-stu-id="fed31-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="fed31-189">¿Cómo se puede modelar las relaciones de varios a varios?</span><span class="sxs-lookup"><span data-stu-id="fed31-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="fed31-190">En una base de datos relacional, las relaciones *varios a varios* modelan con frecuencia con tablas de unión, que simplemente unen registros de otras tablas.</span><span class="sxs-lookup"><span data-stu-id="fed31-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Combinar tablas](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="fed31-192">Es posible que tooreplicate tentado Hola lo mismo con documentos y crear un modelo de datos que busca a continuación toohello similar.</span><span class="sxs-lookup"><span data-stu-id="fed31-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="fed31-193">Esto funcionaría.</span><span class="sxs-lookup"><span data-stu-id="fed31-193">This would work.</span></span> <span data-ttu-id="fed31-194">Sin embargo, cargar a cualquier un autor con sus libros o cargar un libro con su autor, siempre requeriría al menos dos consultas adicionales en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fed31-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="fed31-195">Una consulta toohello de unión de documento y, a continuación, otra consulta toofetch Hola documento real que se está combinando.</span><span class="sxs-lookup"><span data-stu-id="fed31-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="fed31-196">Si todo lo que hace esta tabla de unión es combinar dos datos, ¿por qué no quitarla completamente?</span><span class="sxs-lookup"><span data-stu-id="fed31-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="fed31-197">Tenga en cuenta Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="fed31-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="fed31-198">Ahora, si tuviera un autor, inmediatamente saber qué libros que han escrito y a la inversa si tuviera un documento de libro cargado sabría identificadores de Hola de autores de Hola.</span><span class="sxs-lookup"><span data-stu-id="fed31-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="fed31-199">Esto ahorra esa consulta intermedia en la tabla de combinación de hello reducir el número de saludo del servidor de viajes de ida y la aplicación tiene toomake.</span><span class="sxs-lookup"><span data-stu-id="fed31-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="fed31-200"><a id="WrapUp"></a>Modelos de datos híbridos</span><span class="sxs-lookup"><span data-stu-id="fed31-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="fed31-201">Ya hemos observado la incrustación (o desnormalización) y el establecimiento de referencias (o normalización). Cada opción tiene sus ventajas y compromisos, como hemos visto.</span><span class="sxs-lookup"><span data-stu-id="fed31-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="fed31-202">No siempre tiene toobe o o, no ser un poco toomix asustado cosas up.</span><span class="sxs-lookup"><span data-stu-id="fed31-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="fed31-203">En función de los patrones de uso específicos y las cargas de trabajo pueden darse casos donde se incrusta la combinación de la aplicación y los datos que se hace referencia tiene sentido y podría responsable toosimpler la lógica de la aplicación con el servidor de menos de ida y vuelta al mismo tiempo mantienen un buen nivel de rendimiento .</span><span class="sxs-lookup"><span data-stu-id="fed31-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="fed31-204">Considere la posibilidad de hello después de JSON.</span><span class="sxs-lookup"><span data-stu-id="fed31-204">Consider hello following JSON.</span></span> 

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

<span data-ttu-id="fed31-205">Aquí hemos (principalmente) seguimos modelo incrustados hello, donde los datos de otras entidades se incrustan en los documentos de nivel superior de hello, pero se hace referencia a otros datos.</span><span class="sxs-lookup"><span data-stu-id="fed31-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="fed31-206">Si observa en el documento de la libreta de hello, podemos ver algunas interesantes campos cuando miramos matriz Hola de autores.</span><span class="sxs-lookup"><span data-stu-id="fed31-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="fed31-207">Hay un *identificador* campo que es el campo de hello usamos documento de autor de toorefer tooan atrás, una práctica estándar en un modelo normalizado, pero, a continuación, también tiene *nombre* y *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="fed31-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="fed31-208">Se ha podido detenida simplemente con *Id. de* y deja Hola aplicación tooget cualquier información adicional sea necesario del documento de autor respectivos hello mediante Hola "enlace", pero dado que nuestra aplicación muestra el nombre del autor de Hola y un imagen en miniatura con cada libro muestra podemos guardar un servidor de toohello de ida y vuelta por libro en una lista por eliminar la normalización **algunos** datos del autor de Hola.</span><span class="sxs-lookup"><span data-stu-id="fed31-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="fed31-209">Por supuesto, si cambia el nombre del autor de Hola o deseaban tooupdate sus fotos tendríamos toogo una actualización todos los libros que publican alguna vez pero en nuestra aplicación, basado en la suposición de Hola que los autores no cambien sus nombres muy a menudo, es un diseño aceptable Decisión.</span><span class="sxs-lookup"><span data-stu-id="fed31-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="fed31-210">En el ejemplo de Hola hay **calcula previamente agregados** valores toosave un procesamiento costoso en una operación de lectura.</span><span class="sxs-lookup"><span data-stu-id="fed31-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="fed31-211">En el ejemplo de Hola, algunos de los datos de hello incrustados en el documento de autor Hola son datos que se calculan en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fed31-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="fed31-212">Cada vez que se publica un nuevo libro, se crea un documento de libro **y** campo de hello countOfBooks está establecido el valor de tooa calculado según el número de Hola de documentos de libro que existen para un autor concreto.</span><span class="sxs-lookup"><span data-stu-id="fed31-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="fed31-213">Esta optimización sería buena en sistemas muchos lecturas donde se pueden permitirse toodo cálculos en las escrituras en orden toooptimize lecturas.</span><span class="sxs-lookup"><span data-stu-id="fed31-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="fed31-214">Hola toohave capacidad un modelo con campos calculados previamente pueden evitarse porque admite la base de datos de Azure Cosmos **transacciones de documentos múltiple**.</span><span class="sxs-lookup"><span data-stu-id="fed31-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="fed31-215">Muchos almacenes NoSQL no pueden realizar transacciones en documentos y defensa, por tanto, al tomar decisiones de diseño, como "siempre incrustar todo", debido a la limitación de toothis.</span><span class="sxs-lookup"><span data-stu-id="fed31-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="fed31-216">Con Azure Cosmos DB, puede utilizar los desencadenadores del servidor o los procedimientos almacenados que insertan los libros y actualizan los autores dentro de una transacción ACID.</span><span class="sxs-lookup"><span data-stu-id="fed31-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="fed31-217">Ahora no lo hace **tienen** tooembed todo el contenido de tooone documento simplemente toobe seguro de que los datos de forma coherentes.</span><span class="sxs-lookup"><span data-stu-id="fed31-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="fed31-218"><a name="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fed31-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="fed31-219">debe recordar más importantes de Hola de este artículo es toounderstand que modelado de datos en un mundo sin esquemas son tan importantes como nunca.</span><span class="sxs-lookup"><span data-stu-id="fed31-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="fed31-220">Igual que no hay ningún toorepresent de manera única una parte de los datos en una pantalla, no hay ningún toomodel de forma única los datos.</span><span class="sxs-lookup"><span data-stu-id="fed31-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="fed31-221">Tenga toounderstand su aplicación y cómo generará, consumir y procesar los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fed31-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="fed31-222">A continuación, aplicando algunos Hola instrucciones presentadas aquí se pueden establecer sobre la creación de un modelo que cubre Hola necesidades inmediatas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fed31-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="fed31-223">Cuando las aplicaciones necesitan toochange, puede aprovechar flexibilidad Hola de una base de datos sin esquemas tooembrace que cambian y evolucionar con facilidad el modelo de datos.</span><span class="sxs-lookup"><span data-stu-id="fed31-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="fed31-224">toolearn más información acerca de la base de datos de Cosmos de Azure, consulte del servicio de toohello [documentación](https://azure.microsoft.com/documentation/services/cosmos-db/) página.</span><span class="sxs-lookup"><span data-stu-id="fed31-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="fed31-225">toounderstand cómo tooshard los datos entre varias particiones, consulte demasiado[particiones de datos en la base de datos de Azure Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="fed31-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 

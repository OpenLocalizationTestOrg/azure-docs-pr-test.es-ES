---
title: Activos de aaaManaging y entidades relacionadas con el SDK de .NET de servicios multimedia
description: "Obtenga información acerca de cómo toomanage activos y las entidades relacionadas con Hola SDK de servicios multimedia para. NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="a5a01-103">Administración de activos y entidades relacionadas con el SDK de Servicios multimedia para .NET</span><span class="sxs-lookup"><span data-stu-id="a5a01-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5a01-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a5a01-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="a5a01-105">REST</span><span class="sxs-lookup"><span data-stu-id="a5a01-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="a5a01-106">Este tema muestra cómo toomanage servicios multimedia de Azure entidades con. NET.</span><span class="sxs-lookup"><span data-stu-id="a5a01-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="a5a01-107">A partir del 1 de abril de 2017, cualquier registro de trabajo en su cuenta de más de 90 días se eliminarán automáticamente, junto con sus registros de tarea asociados, incluso si el número total de Hola de registros está por debajo de la cuota máxima de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5a01-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="a5a01-108">Por ejemplo, el 1 de abril de 2017, todos los registros de trabajo de la cuenta que sean anteriores al 31 de diciembre de 2016 se eliminarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a5a01-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="a5a01-109">Si necesita información de trabajo o tarea hello tooarchive, puede usar código de hello descrito en este tema.</span><span class="sxs-lookup"><span data-stu-id="a5a01-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5a01-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a5a01-110">Prerequisites</span></span>

<span data-ttu-id="a5a01-111">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a5a01-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="a5a01-112">Obtención de una referencia de recurso</span><span class="sxs-lookup"><span data-stu-id="a5a01-112">Get an Asset Reference</span></span>
<span data-ttu-id="a5a01-113">Una tarea frecuente es tooget un activo existente tooan de referencia en los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a5a01-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="a5a01-114">Hola, ejemplo de código siguiente muestra cómo puede obtener una referencia de activos de colección de activos de hello en servidor hello objeto de contexto, tomando como base un Hola de Id. de activo siguiendo el ejemplo de código utiliza una consulta Linq tooget un objeto de IAsset referencia tooan existente.</span><span class="sxs-lookup"><span data-stu-id="a5a01-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a><span data-ttu-id="a5a01-115">Lista de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="a5a01-115">List All Assets</span></span>
<span data-ttu-id="a5a01-116">A medida que aumenta el número de Hola de activos que tienen en el almacenamiento, resulta útil toolist sus activos.</span><span class="sxs-lookup"><span data-stu-id="a5a01-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="a5a01-117">Hola, ejemplo de código siguiente muestra cómo tooiterate a través de Hola colección activos en el objeto de contexto de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="a5a01-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="a5a01-118">Con cada activo, ejemplo de código de hello también escribe algunos de su consola toohello de valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="a5a01-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="a5a01-119">Por ejemplo, cada recurso puede contener muchos archivos multimedia.</span><span class="sxs-lookup"><span data-stu-id="a5a01-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="a5a01-120">ejemplo de código de Hello escribe todos los archivos asociados a cada recurso.</span><span class="sxs-lookup"><span data-stu-id="a5a01-120">hello code example writes out all files associated with each asset.</span></span>

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a><span data-ttu-id="a5a01-121">Obtención de una referencia de trabajo</span><span class="sxs-lookup"><span data-stu-id="a5a01-121">Get a Job Reference</span></span>

<span data-ttu-id="a5a01-122">Cuando se trabaja con las tareas en el código de servicios multimedia de procesamiento, suelen necesitar tooget un trabajo existente de referencia tooan tomando como base un Hola Id. ejemplo de código siguiente muestra cómo tooget una tooan IJob de referencia de objeto de colección de trabajos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5a01-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="a5a01-123">Puede necesitar tooget una referencia de trabajo al iniciar un trabajo de codificación de larga duración y necesita toocheck el estado del trabajo de hello en un subproceso.</span><span class="sxs-lookup"><span data-stu-id="a5a01-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="a5a01-124">En casos como este, al método hello devuelve desde un subproceso, deberá tooretrieve un trabajo de tooa referencia actualizada.</span><span class="sxs-lookup"><span data-stu-id="a5a01-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a><span data-ttu-id="a5a01-125">Lista de trabajos y recursos</span><span class="sxs-lookup"><span data-stu-id="a5a01-125">List Jobs and Assets</span></span>
<span data-ttu-id="a5a01-126">Una tarea relacionada importante es activos toolist con su trabajo asociado en los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a5a01-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="a5a01-127">Hello ejemplo de código siguiente muestra cómo toolist cada objeto IJob y, a continuación, muestra propiedades acerca de trabajo hello, todas las tareas relacionadas, todas las entradas de activos para cada trabajo, y todos los activos de salida.</span><span class="sxs-lookup"><span data-stu-id="a5a01-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="a5a01-128">código de Hello en este ejemplo puede ser útil para muchas otras tareas.</span><span class="sxs-lookup"><span data-stu-id="a5a01-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="a5a01-129">Por ejemplo, si desea que los activos de salida de hello toolist desde uno o más trabajos de codificación que haya ejecutado anteriormente, este código muestra cómo tooaccess Hola había salida activos.</span><span class="sxs-lookup"><span data-stu-id="a5a01-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="a5a01-130">Cuando tenga un recurso de salida tooan de referencia, puede entregar hello tooother contenido usuarios o aplicaciones descargándolo o proporcionando direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="a5a01-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="a5a01-131">Para obtener más información sobre las opciones de entrega de recursos, consulte [entregar activos con hello SDK de servicios multimedia para .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="a5a01-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a><span data-ttu-id="a5a01-132">Lista de todas las directivas de acceso</span><span class="sxs-lookup"><span data-stu-id="a5a01-132">List all Access Policies</span></span>
<span data-ttu-id="a5a01-133">En Servicios multimedia, puede definir una directiva de acceso en un recurso o sus archivos.</span><span class="sxs-lookup"><span data-stu-id="a5a01-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="a5a01-134">Una directiva de acceso define los permisos de Hola para un archivo o un recurso (el tipo de acceso y la duración de hello).</span><span class="sxs-lookup"><span data-stu-id="a5a01-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="a5a01-135">En el código de Servicios multimedia, normalmente se define una directiva de acceso mediante la creación de un objeto IAccessPolicy y, a continuación, su asociación a un recurso existente.</span><span class="sxs-lookup"><span data-stu-id="a5a01-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="a5a01-136">A continuación, cree un objeto ILocator, que le permite proporcionar acceso directo tooassets en los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a5a01-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="a5a01-137">proyecto de Visual Studio de Hola que se incluye en esta serie de documentación contiene varios ejemplos de código que muestran cómo toocreate y asignar acceso tooassets directivas y localizadores.</span><span class="sxs-lookup"><span data-stu-id="a5a01-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="a5a01-138">Hola siguiendo el ejemplo de código muestra cómo toolist todas las directivas de acceso al servidor hello y tipo de Hola de muestra de permisos asociadas a cada uno.</span><span class="sxs-lookup"><span data-stu-id="a5a01-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="a5a01-139">Directivas de acceso de otra manera útil tooview es toolist todos los objetos de ILocator en el servidor de hello y, a continuación, para cada localizador, puede enumerar su directiva de acceso asociada mediante su propiedad AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="a5a01-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a><span data-ttu-id="a5a01-140">Directivas de limitación del acceso</span><span class="sxs-lookup"><span data-stu-id="a5a01-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="a5a01-141">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a5a01-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a5a01-142">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="a5a01-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="a5a01-143">Por ejemplo, puede crear un conjunto de directivas genérico con hello después el código que se ejecute sólo una vez en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5a01-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="a5a01-144">Puede registrar el archivo de registro de identificadores tooa para su uso posterior:</span><span class="sxs-lookup"><span data-stu-id="a5a01-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="a5a01-145">A continuación, puede usar Hola existente identificadores en el código similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5a01-145">Then, you can use hello existing IDs in your code like this:</span></span>

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a><span data-ttu-id="a5a01-146">Enumerar todos los localizadores</span><span class="sxs-lookup"><span data-stu-id="a5a01-146">List All Locators</span></span>
<span data-ttu-id="a5a01-147">Un localizador es una dirección URL que proporciona una ruta de acceso directo tooaccess un activo, junto con los activos de toohello de permisos de acuerdo con la directiva de acceso asociada del localizador de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5a01-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="a5a01-148">Cada activo puede tener una colección de objetos ILocator asociados a él en su propiedad Locators.</span><span class="sxs-lookup"><span data-stu-id="a5a01-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="a5a01-149">contexto de servidor Hello también tiene una colección de localizadores que contiene todos los localizadores.</span><span class="sxs-lookup"><span data-stu-id="a5a01-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="a5a01-150">Hello ejemplo de código siguiente enumera todos los localizadores en servidor hello.</span><span class="sxs-lookup"><span data-stu-id="a5a01-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="a5a01-151">Para cada servidor muestra hello Id. de recurso relacionados de Hola y directiva de acceso.</span><span class="sxs-lookup"><span data-stu-id="a5a01-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="a5a01-152">También muestra tipo hello de permisos, fecha de expiración de Hola y activos de toohello de ruta de acceso completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5a01-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="a5a01-153">Tenga en cuenta que un recurso de tooan de ruta de acceso de ubicación es solo un base activo de toohello de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a5a01-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="a5a01-154">toocreate que una ruta de acceso directo tooindividual archivos que puede navegar un usuario o aplicación, el código debe agregar Hola archivo específico toohello localizador ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="a5a01-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="a5a01-155">Para obtener más información acerca de cómo toodo, vea el tema de hello [entregar activos con hello SDK de servicios multimedia para .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="a5a01-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="a5a01-156">Enumeración de grandes colecciones de entidades</span><span class="sxs-lookup"><span data-stu-id="a5a01-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="a5a01-157">Cuando se consultan las entidades, hay un límite de 1000 entidades devueltas al mismo tiempo porque pública v2 REST limita los resultados de too1000 de resultados de consulta.</span><span class="sxs-lookup"><span data-stu-id="a5a01-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="a5a01-158">Necesitará toouse Skip y Take para enumerar las grandes colecciones de entidades.</span><span class="sxs-lookup"><span data-stu-id="a5a01-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="a5a01-159">Hola después de la función recorre en bucle todos los trabajos de Hola Hola proporcionada la cuenta de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a5a01-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="a5a01-160">Servicios multimedia devuelve 1000 trabajos en la colección de trabajos.</span><span class="sxs-lookup"><span data-stu-id="a5a01-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="a5a01-161">función Hello hace que el uso de Skip y tomar toomake seguro de que todos los trabajos enumerados (en caso de que tenga más de 1000 trabajos en su cuenta).</span><span class="sxs-lookup"><span data-stu-id="a5a01-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a><span data-ttu-id="a5a01-162">Eliminación de un recurso</span><span class="sxs-lookup"><span data-stu-id="a5a01-162">Delete an Asset</span></span>
<span data-ttu-id="a5a01-163">Hola de ejemplo siguiente elimina un activo.</span><span class="sxs-lookup"><span data-stu-id="a5a01-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="a5a01-164">Eliminación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="a5a01-164">Delete a Job</span></span>
<span data-ttu-id="a5a01-165">toodelete un trabajo, debe comprobar estado de Hola de trabajo de hello como se indica en la propiedad de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5a01-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="a5a01-166">Los trabajos finalizados o cancelados pueden eliminarse, mientras que los trabajos que se encuentran en otros estados, por ejemplo, en cola, programado o en proceso, se deben cancelar primero y, a continuación, se pueden eliminar.</span><span class="sxs-lookup"><span data-stu-id="a5a01-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="a5a01-167">Hello ejemplo de código siguiente muestra un método para eliminar un trabajo comprobando los Estados de trabajo y, a continuación, eliminar al estado de hello finalice o se cancele.</span><span class="sxs-lookup"><span data-stu-id="a5a01-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="a5a01-168">Este código depende de la sección anterior de hello en este tema para obtener un trabajo de tooa de referencia: obtener una referencia de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a5a01-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a><span data-ttu-id="a5a01-169">Eliminación de una directiva de acceso</span><span class="sxs-lookup"><span data-stu-id="a5a01-169">Delete an Access Policy</span></span>
<span data-ttu-id="a5a01-170">Hello ejemplo de código siguiente muestra cómo tooget una directiva de acceso de referencia tooan basada en un Id. de directiva y, a continuación, toodelete Hola directiva.</span><span class="sxs-lookup"><span data-stu-id="a5a01-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="a5a01-171">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="a5a01-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a5a01-172">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a5a01-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


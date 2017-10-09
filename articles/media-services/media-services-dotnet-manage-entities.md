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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Administración de activos y entidades relacionadas con el SDK de Servicios multimedia para .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

Este tema muestra cómo toomanage servicios multimedia de Azure entidades con. NET. 

>[!NOTE]
> A partir del 1 de abril de 2017, cualquier registro de trabajo en su cuenta de más de 90 días se eliminarán automáticamente, junto con sus registros de tarea asociados, incluso si el número total de Hola de registros está por debajo de la cuota máxima de Hola. Por ejemplo, el 1 de abril de 2017, todos los registros de trabajo de la cuenta que sean anteriores al 31 de diciembre de 2016 se eliminarán automáticamente. Si necesita información de trabajo o tarea hello tooarchive, puede usar código de hello descrito en este tema.

## <a name="prerequisites"></a>Requisitos previos

Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Obtención de una referencia de recurso
Una tarea frecuente es tooget un activo existente tooan de referencia en los servicios multimedia. Hola, ejemplo de código siguiente muestra cómo puede obtener una referencia de activos de colección de activos de hello en servidor hello objeto de contexto, tomando como base un Hola de Id. de activo siguiendo el ejemplo de código utiliza una consulta Linq tooget un objeto de IAsset referencia tooan existente.

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

## <a name="list-all-assets"></a>Lista de todos los recursos
A medida que aumenta el número de Hola de activos que tienen en el almacenamiento, resulta útil toolist sus activos. Hola, ejemplo de código siguiente muestra cómo tooiterate a través de Hola colección activos en el objeto de contexto de servidor hello. Con cada activo, ejemplo de código de hello también escribe algunos de su consola toohello de valores de propiedad. Por ejemplo, cada recurso puede contener muchos archivos multimedia. ejemplo de código de Hello escribe todos los archivos asociados a cada recurso.

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

## <a name="get-a-job-reference"></a>Obtención de una referencia de trabajo

Cuando se trabaja con las tareas en el código de servicios multimedia de procesamiento, suelen necesitar tooget un trabajo existente de referencia tooan tomando como base un Hola Id. ejemplo de código siguiente muestra cómo tooget una tooan IJob de referencia de objeto de colección de trabajos de Hola.

Puede necesitar tooget una referencia de trabajo al iniciar un trabajo de codificación de larga duración y necesita toocheck el estado del trabajo de hello en un subproceso. En casos como este, al método hello devuelve desde un subproceso, deberá tooretrieve un trabajo de tooa referencia actualizada.

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

## <a name="list-jobs-and-assets"></a>Lista de trabajos y recursos
Una tarea relacionada importante es activos toolist con su trabajo asociado en los servicios multimedia. Hello ejemplo de código siguiente muestra cómo toolist cada objeto IJob y, a continuación, muestra propiedades acerca de trabajo hello, todas las tareas relacionadas, todas las entradas de activos para cada trabajo, y todos los activos de salida. código de Hello en este ejemplo puede ser útil para muchas otras tareas. Por ejemplo, si desea que los activos de salida de hello toolist desde uno o más trabajos de codificación que haya ejecutado anteriormente, este código muestra cómo tooaccess Hola había salida activos. Cuando tenga un recurso de salida tooan de referencia, puede entregar hello tooother contenido usuarios o aplicaciones descargándolo o proporcionando direcciones URL. 

Para obtener más información sobre las opciones de entrega de recursos, consulte [entregar activos con hello SDK de servicios multimedia para .NET](media-services-deliver-streaming-content.md).

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

## <a name="list-all-access-policies"></a>Lista de todas las directivas de acceso
En Servicios multimedia, puede definir una directiva de acceso en un recurso o sus archivos. Una directiva de acceso define los permisos de Hola para un archivo o un recurso (el tipo de acceso y la duración de hello). En el código de Servicios multimedia, normalmente se define una directiva de acceso mediante la creación de un objeto IAccessPolicy y, a continuación, su asociación a un recurso existente. A continuación, cree un objeto ILocator, que le permite proporcionar acceso directo tooassets en los servicios multimedia. proyecto de Visual Studio de Hola que se incluye en esta serie de documentación contiene varios ejemplos de código que muestran cómo toocreate y asignar acceso tooassets directivas y localizadores.

Hola siguiendo el ejemplo de código muestra cómo toolist todas las directivas de acceso al servidor hello y tipo de Hola de muestra de permisos asociadas a cada uno. Directivas de acceso de otra manera útil tooview es toolist todos los objetos de ILocator en el servidor de hello y, a continuación, para cada localizador, puede enumerar su directiva de acceso asociada mediante su propiedad AccessPolicy.

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
    
## <a name="limit-access-policies"></a>Directivas de limitación del acceso 

>[!NOTE]
> Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga). 

Por ejemplo, puede crear un conjunto de directivas genérico con hello después el código que se ejecute sólo una vez en la aplicación. Puede registrar el archivo de registro de identificadores tooa para su uso posterior:

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

A continuación, puede usar Hola existente identificadores en el código similar al siguiente:

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

## <a name="list-all-locators"></a>Enumerar todos los localizadores
Un localizador es una dirección URL que proporciona una ruta de acceso directo tooaccess un activo, junto con los activos de toohello de permisos de acuerdo con la directiva de acceso asociada del localizador de Hola. Cada activo puede tener una colección de objetos ILocator asociados a él en su propiedad Locators. contexto de servidor Hello también tiene una colección de localizadores que contiene todos los localizadores.

Hello ejemplo de código siguiente enumera todos los localizadores en servidor hello. Para cada servidor muestra hello Id. de recurso relacionados de Hola y directiva de acceso. También muestra tipo hello de permisos, fecha de expiración de Hola y activos de toohello de ruta de acceso completa de Hola.

Tenga en cuenta que un recurso de tooan de ruta de acceso de ubicación es solo un base activo de toohello de dirección URL. toocreate que una ruta de acceso directo tooindividual archivos que puede navegar un usuario o aplicación, el código debe agregar Hola archivo específico toohello localizador ruta de acceso. Para obtener más información acerca de cómo toodo, vea el tema de hello [entregar activos con hello SDK de servicios multimedia para .NET](media-services-deliver-streaming-content.md).

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

## <a name="enumerating-through-large-collections-of-entities"></a>Enumeración de grandes colecciones de entidades
Cuando se consultan las entidades, hay un límite de 1000 entidades devueltas al mismo tiempo porque pública v2 REST limita los resultados de too1000 de resultados de consulta. Necesitará toouse Skip y Take para enumerar las grandes colecciones de entidades. 

Hola después de la función recorre en bucle todos los trabajos de Hola Hola proporcionada la cuenta de servicios multimedia. Servicios multimedia devuelve 1000 trabajos en la colección de trabajos. función Hello hace que el uso de Skip y tomar toomake seguro de que todos los trabajos enumerados (en caso de que tenga más de 1000 trabajos en su cuenta).

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

## <a name="delete-an-asset"></a>Eliminación de un recurso
Hola de ejemplo siguiente elimina un activo.

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>Eliminación de un trabajo
toodelete un trabajo, debe comprobar estado de Hola de trabajo de hello como se indica en la propiedad de estado de Hola. Los trabajos finalizados o cancelados pueden eliminarse, mientras que los trabajos que se encuentran en otros estados, por ejemplo, en cola, programado o en proceso, se deben cancelar primero y, a continuación, se pueden eliminar.

Hello ejemplo de código siguiente muestra un método para eliminar un trabajo comprobando los Estados de trabajo y, a continuación, eliminar al estado de hello finalice o se cancele. Este código depende de la sección anterior de hello en este tema para obtener un trabajo de tooa de referencia: obtener una referencia de trabajo.

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


## <a name="delete-an-access-policy"></a>Eliminación de una directiva de acceso
Hello ejemplo de código siguiente muestra cómo tooget una directiva de acceso de referencia tooan basada en un Id. de directiva y, a continuación, toodelete Hola directiva.

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



## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


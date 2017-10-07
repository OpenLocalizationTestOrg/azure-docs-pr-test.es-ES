---
title: aaaSet y recuperar el objeto de propiedades y metadatos de almacenamiento de Azure | Documentos de Microsoft
description: "Almacenamiento de metadatos personalizados en los objetos de Almacenamiento de Azure y establecimiento y recuperación de propiedades del sistema."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="f8d13-103">Establecimiento y recuperación de propiedades y metadatos</span><span class="sxs-lookup"><span data-stu-id="f8d13-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="f8d13-104">Objetos de propiedades del sistema de Ayuda de almacenamiento de Azure y los metadatos definidos por el usuario además datos toohello que contienen.</span><span class="sxs-lookup"><span data-stu-id="f8d13-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="f8d13-105">En este artículo se describe las propiedades de sistema de administración y los metadatos definidos por el usuario con hello [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="f8d13-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="f8d13-106">**Propiedades del sistema**: en cada recurso de almacenamiento existen propiedades del sistema.</span><span class="sxs-lookup"><span data-stu-id="f8d13-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="f8d13-107">Algunas se pueden leer o establecer, mientras que otras son de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="f8d13-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="f8d13-108">Tras bastidores de hello, algunas propiedades del sistema corresponden toocertain los encabezados HTTP estándares.</span><span class="sxs-lookup"><span data-stu-id="f8d13-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="f8d13-109">biblioteca de cliente de almacenamiento de Azure Hola mantiene por usted.</span><span class="sxs-lookup"><span data-stu-id="f8d13-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="f8d13-110">**Metadatos definidos por el usuario**: metadatos definidos por el usuario son metadatos que se especifican en un recurso determinado en forma de Hola de un par nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="f8d13-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="f8d13-111">Puede usar valores de metadatos toostore adicionales con un recurso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f8d13-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="f8d13-112">Estos valores de metadatos adicionales para sus propios fines únicamente y no afectan a cómo se comporta el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8d13-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="f8d13-113">El proceso de recuperación de los valores de propiedad y metadatos de un recurso de almacenamiento consta de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="f8d13-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="f8d13-114">Para poder leer estos valores, debe capturarlos explícitamente por llamada hello **FetchAttributes** método.</span><span class="sxs-lookup"><span data-stu-id="f8d13-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8d13-115">No se rellenan los valores de propiedad y los metadatos para un recurso de almacenamiento, a menos que se llame a uno de hello **FetchAttributes** métodos.</span><span class="sxs-lookup"><span data-stu-id="f8d13-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="f8d13-116">Recibirá un mensaje `400 Bad Request` si algún par de nombre/valor contiene caracteres no ASCII.</span><span class="sxs-lookup"><span data-stu-id="f8d13-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="f8d13-117">Pares de nombre/valor de metadatos son encabezados HTTP válidos por lo que debe cumplir las restricciones de tooall que rigen los encabezados HTTP.</span><span class="sxs-lookup"><span data-stu-id="f8d13-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="f8d13-118">Por ello, se recomienda que utilice la codificación de direcciones URL o codificación Base64 para nombres y valores que contengan caracteres no ASCII.</span><span class="sxs-lookup"><span data-stu-id="f8d13-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="f8d13-119">Establecimiento y recuperación de propiedades</span><span class="sxs-lookup"><span data-stu-id="f8d13-119">Setting and retrieving properties</span></span>
<span data-ttu-id="f8d13-120">valores de propiedad tooretrieve llamada hello **FetchAttributes** método en las propiedades de hello toopopulate de blob o contenedor, a continuación, leer valores de hello.</span><span class="sxs-lookup"><span data-stu-id="f8d13-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="f8d13-121">propiedades de tooset en un objeto, especifique el valor de la propiedad de Hola y después llamar a hello **SetProperties** método.</span><span class="sxs-lookup"><span data-stu-id="f8d13-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="f8d13-122">Hello ejemplo de código siguiente crea un contenedor, a continuación, escribe algunos de su ventana de consola de tooa de valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="f8d13-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="f8d13-123">Establecer y recuperar metadatos</span><span class="sxs-lookup"><span data-stu-id="f8d13-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="f8d13-124">Puede especificar metadatos como uno o más pares nombre-valor en un recurso de blob o contenedor.</span><span class="sxs-lookup"><span data-stu-id="f8d13-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="f8d13-125">metadatos de tooset, agregar pares de nombre-valor toohello **metadatos** colección en el recurso de hello, a continuación, llamar a hello **SetMetadata** Hola de método toosave valores toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="f8d13-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="f8d13-126">nombre de Hola de sus metadatos debe cumplir las convenciones de nomenclatura toohello para identificadores de C#.</span><span class="sxs-lookup"><span data-stu-id="f8d13-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="f8d13-127">Hello ejemplo de código siguiente establece metadatos en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="f8d13-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="f8d13-128">Un valor se establece mediante la colección hello **agregar** método.</span><span class="sxs-lookup"><span data-stu-id="f8d13-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="f8d13-129">Hello otro valor se establece mediante la sintaxis del valor de clave implícita.</span><span class="sxs-lookup"><span data-stu-id="f8d13-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="f8d13-130">Ambos son válidos.</span><span class="sxs-lookup"><span data-stu-id="f8d13-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="f8d13-131">metadatos de tooretrieve, llamada hello **FetchAttributes** método en su hello toopopulate blob o contenedor **metadatos** colección, a continuación, leer valores de hello, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8d13-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="f8d13-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8d13-132">Next steps</span></span>
* [<span data-ttu-id="f8d13-133">Documentación de referencia de la biblioteca cliente de Azure Storage para .NET</span><span class="sxs-lookup"><span data-stu-id="f8d13-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="f8d13-134">Paquete de NuGet de la biblioteca cliente de Azure Storage para .NET</span><span class="sxs-lookup"><span data-stu-id="f8d13-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)

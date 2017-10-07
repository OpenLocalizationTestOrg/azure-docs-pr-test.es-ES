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
# <a name="set-and-retrieve-properties-and-metadata"></a>Establecimiento y recuperación de propiedades y metadatos

Objetos de propiedades del sistema de Ayuda de almacenamiento de Azure y los metadatos definidos por el usuario además datos toohello que contienen. En este artículo se describe las propiedades de sistema de administración y los metadatos definidos por el usuario con hello [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Propiedades del sistema**: en cada recurso de almacenamiento existen propiedades del sistema. Algunas se pueden leer o establecer, mientras que otras son de solo lectura. Tras bastidores de hello, algunas propiedades del sistema corresponden toocertain los encabezados HTTP estándares. biblioteca de cliente de almacenamiento de Azure Hola mantiene por usted.

* **Metadatos definidos por el usuario**: metadatos definidos por el usuario son metadatos que se especifican en un recurso determinado en forma de Hola de un par nombre-valor. Puede usar valores de metadatos toostore adicionales con un recurso de almacenamiento. Estos valores de metadatos adicionales para sus propios fines únicamente y no afectan a cómo se comporta el recurso de Hola.

El proceso de recuperación de los valores de propiedad y metadatos de un recurso de almacenamiento consta de dos pasos. Para poder leer estos valores, debe capturarlos explícitamente por llamada hello **FetchAttributes** método.

> [!IMPORTANT]
> No se rellenan los valores de propiedad y los metadatos para un recurso de almacenamiento, a menos que se llame a uno de hello **FetchAttributes** métodos.
>
> Recibirá un mensaje `400 Bad Request` si algún par de nombre/valor contiene caracteres no ASCII. Pares de nombre/valor de metadatos son encabezados HTTP válidos por lo que debe cumplir las restricciones de tooall que rigen los encabezados HTTP. Por ello, se recomienda que utilice la codificación de direcciones URL o codificación Base64 para nombres y valores que contengan caracteres no ASCII.
>

## <a name="setting-and-retrieving-properties"></a>Establecimiento y recuperación de propiedades
valores de propiedad tooretrieve llamada hello **FetchAttributes** método en las propiedades de hello toopopulate de blob o contenedor, a continuación, leer valores de hello.

propiedades de tooset en un objeto, especifique el valor de la propiedad de Hola y después llamar a hello **SetProperties** método.

Hello ejemplo de código siguiente crea un contenedor, a continuación, escribe algunos de su ventana de consola de tooa de valores de propiedad.

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

## <a name="setting-and-retrieving-metadata"></a>Establecer y recuperar metadatos
Puede especificar metadatos como uno o más pares nombre-valor en un recurso de blob o contenedor. metadatos de tooset, agregar pares de nombre-valor toohello **metadatos** colección en el recurso de hello, a continuación, llamar a hello **SetMetadata** Hola de método toosave valores toohello servicio.

> [!NOTE]
> nombre de Hola de sus metadatos debe cumplir las convenciones de nomenclatura toohello para identificadores de C#.
>
>

Hello ejemplo de código siguiente establece metadatos en un contenedor. Un valor se establece mediante la colección hello **agregar** método. Hello otro valor se establece mediante la sintaxis del valor de clave implícita. Ambos son válidos.

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

metadatos de tooretrieve, llamada hello **FetchAttributes** método en su hello toopopulate blob o contenedor **metadatos** colección, a continuación, leer valores de hello, como se muestra en el siguiente ejemplo de Hola.

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

## <a name="next-steps"></a>Pasos siguientes
* [Documentación de referencia de la biblioteca cliente de Azure Storage para .NET](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Paquete de NuGet de la biblioteca cliente de Azure Storage para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)

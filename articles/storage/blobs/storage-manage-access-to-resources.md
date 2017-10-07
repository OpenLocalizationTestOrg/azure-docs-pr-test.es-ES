---
title: "acceso aaaEnable público de lectura para los contenedores y blobs en almacenamiento de blobs de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomake contenedores y blobs disponibles para el acceso anónimo y cómo tooaccess ellos mediante programación."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: dd8ffdb39a66aa06f65ad3cdd4315d47c117f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>Administrar blobs y acceso de lectura anónimo toocontainers
Puede habilitar el acceso de lectura anónimo y público tooa contenedor y sus blobs en almacenamiento de blobs de Azure. Al hacerlo, puede conceder acceso de solo lectura a los recursos de toothese sin compartir la clave de cuenta y sin necesidad de una firma de acceso compartido (SAS).

Acceso de lectura público es mejor para escenarios donde desea que ciertas blobs tooalways esté disponible para el acceso de lectura anónimo. Para un control más minucioso, puede crear una firma de acceso compartido. Firmas de acceso compartido le permiten acceso tooprovide restringido mediante permisos diferentes, durante un período de tiempo específico. Para obtener más información sobre la creación de firmas de acceso compartido, vea [Uso de firmas de acceso compartido (SAS) en Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>Conceder a los usuarios anónimos permisos toocontainers y blobs
De forma predeterminada, un contenedor y cualquiera de sus blobs puede tener acceso a solo el propietario Hola de cuenta de almacenamiento de Hola. contenedor de tooa de permisos de lectura de los usuarios anónimos toogive y sus blobs, puede establecer Hola permisos tooallow público el acceso al contenedor. Los usuarios anónimos pueden leer los blobs dentro de un contenedor es accesible públicamente sin autenticar la solicitud de Hola.

Puede configurar un contenedor con hello los siguientes permisos:

* **Acceso no público de lectura:** Hola contenedor y sus blobs son accesibles solo por propietario hello de la cuenta de almacenamiento. Éste es Hola predeterminado para todos los contenedores nuevo.
* **Acceso solo para blobs público de lectura:** Blobs de hello contenedor pueden leerse mediante una solicitud anónima, pero los datos del contenedor no están disponibles. Los clientes anónimos no pueden enumerar blobs de hello en el contenedor de Hola.
* **Acceso de lectura público completo**: todos los datos del contenedor y de los blobs se pueden leer mediante una solicitud anónima. Los clientes pueden enumerar blobs en el contenedor de Hola por una solicitud anónima, pero no pueden enumerar contenedores dentro de la cuenta de almacenamiento de Hola.

Puede usar los siguientes permisos del contenedor de tooset de Hola:

* [Portal de Azure](https://portal.azure.com)
* [Azure PowerShell](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [CLI de Azure 2.0](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* Mediante programación, mediante una de las bibliotecas de cliente de almacenamiento de Hola o hello API de REST

### <a name="set-container-permissions-in-hello-azure-portal"></a>Establecer permisos del contenedor en hello portal de Azure
permisos del contenedor tooset Hola [portal de Azure](https://portal.azure.com), siga estos pasos:

1. Abra su **cuenta de almacenamiento** hoja en el portal de Hola. Puede encontrar la cuenta de almacenamiento seleccionando **cuentas de almacenamiento** en la hoja de menús del portal principal de Hola.
1. En **servicio BLOB** en la hoja de menú de hello, seleccione **contenedores**.
1. Haga doble clic en la fila de contenedor de Hola o del contenedor de Hola de hello seleccione puntos suspensivos tooopen **menú contextual**.
1. Seleccione **directiva de acceso** en el menú contextual de Hola.
1. Seleccione un **tipo de acceso** de hello menú desplegable.

    ![Cuadro de diálogo Editar metadatos del contenedor](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>Establecimiento de los permisos del contenedor con .NET
tooset permisos para un contenedor con C# y Hola biblioteca cliente de almacenamiento para. NET, en primer lugar recuperar los permisos existentes del contenedor de Hola Hola llamada **GetPermissions** método. Hola de conjunto, a continuación, **PublicAccess** propiedad hello **BlobContainerPermissions** objeto devuelto por hello **GetPermissions** método. Por último, llame hello **SetPermissions** método con hello actualiza permisos.

Hola siguiente ejemplo establece permisos del contenedor de hello toofull acceso de lectura público. acceso de lectura de tooset permisos toopublic para blobs únicamente, establecer hello **PublicAccess** propiedad demasiado**BlobContainerPublicAccessType.Blob**. conjunto de todos los permisos para usuarios anónimos, tooremove Hola propiedad demasiado**BlobContainerPublicAccessType.Off**.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>Acceso anónimo a contenedores y blobs
Un cliente que tiene acceso a contenedores y blobs de forma anónima puede utilizar constructores que no requieren credenciales. Hello en los ejemplos siguientes muestra algunas formas distintas de recursos del servicio Blob tooreference forma anónima.

### <a name="create-an-anonymous-client-object"></a>Creación de un objeto de cliente anónimo
Puede crear un nuevo objeto de cliente de servicio para el acceso anónimo al proporcionar extremo del servicio de Blob de hello para la cuenta de hello. Sin embargo, también debe conocer el nombre de Hola de un contenedor en esa cuenta a la que está disponible para el acceso anónimo.

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a>Referencia a un contenedor de forma anónima
Si tiene un contenedor de tooa de dirección URL de Hola que está disponible de forma anónima, utilizarla contenedor de hello tooreference directamente.

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a>Referencia a un blob de forma anónima
Si dispone de blob de tooa de dirección URL de Hola que está disponible para el acceso anónimo, puede hacer referencia directamente con esa dirección URL de blob de hello:

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>Funciones que los usuarios tooanonymous disponibles
Hello en la tabla siguiente muestra qué operaciones pueden ser llamadas por los usuarios anónimos cuando ACL del contenedor se establece el acceso público de tooallow.

| Operación REST | Permiso con acceso de lectura público completo | Permiso con acceso de lectura público para solo para los blobs |
| --- | --- | --- |
| List Containers |Solo el propietario |Solo el propietario |
| Create Container |Solo el propietario |Solo el propietario |
| Get Container Properties |Todo |Solo el propietario |
| Get Container Metadata |Todo |Solo el propietario |
| Set Container Metadata |Solo el propietario |Solo el propietario |
| Get Container ACL |Solo el propietario |Solo el propietario |
| Set Container ACL |Solo el propietario |Solo el propietario |
| Delete Container |Solo el propietario |Solo el propietario |
| List Blobs |Todo |Solo el propietario |
| Put Blob |Solo el propietario |Solo el propietario |
| Get Blob |Todo |Todo |
| Get Blob Properties |Todo |Todo |
| Set Blob Properties |Solo el propietario |Solo el propietario |
| Get Blob Metadata |Todo |Todo |
| Set Blob Metadata |Solo el propietario |Solo el propietario |
| Put Block |Solo el propietario |Solo el propietario |
| Get Block List (solo bloques confirmados) |Todo |Todo |
| Get Block List (solo bloques sin confirmar o todos los bloques) |Solo el propietario |Solo el propietario |
| Put Block List |Solo el propietario |Solo el propietario |
| Delete Blob |Solo el propietario |Solo el propietario |
| Copia de blobs |Solo el propietario |Solo el propietario |
| Instantánea de blob |Solo el propietario |Solo el propietario |
| Lease Blob |Solo el propietario |Solo el propietario |
| Put Page |Solo el propietario |Solo el propietario |
| Get Page Ranges |Todo |Todo |
| Append Blob |Solo el propietario |Solo el propietario |

## <a name="next-steps"></a>Pasos siguientes

* [Autenticación de hello servicios de almacenamiento de Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [Uso de Firmas de acceso compartido (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Delegación de acceso con una firma de acceso compartido](https://msdn.microsoft.com/library/azure/ee395415.aspx)

---
title: "expiración de aaaManage de blobs de almacenamiento de Azure en red CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de las opciones de Hola para controlar el período de vida para los blobs en almacenamiento en caché de CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>Administración de la expiración de Azure Storage Blob en la red CDN de Azure
> [!div class="op_single_selector"]
> * [Azure Web Apps/Cloud Services, ASP.NET o IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure Storage Blob service](cdn-manage-expiration-of-blob-content.md)
> 
> 

Hola [servicio blob](../storage/common/storage-introduction.md#blob-storage) en [el almacenamiento de Azure](../storage/common/storage-introduction.md) uno de varios orígenes basado en Azure se integra con la red CDN de Azure.  Cualquier contenido de blob accesible públicamente se puede almacenar en caché en la red CDN de Azure hasta que transcurra su tiempo de vida (TTL).  Hello TTL determina hello [ *Cache-Control* encabezado](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en respuesta Hola HTTP desde el almacenamiento de Azure.

> [!TIP]
> No puede elegir tooset ningún período de vida de un blob.  En este caso, la red CDN de Azure aplica automáticamente un valor predeterminado de TTL de siete días.
> 
> Para obtener más información acerca del funcionamiento de CDN de Azure toospeed tooblobs de acceso y otros archivos, vea hello [información general sobre la red CDN de Azure](cdn-overview.md).
> 
> Para obtener más detalles sobre Hola servicio de blob de almacenamiento de Azure, consulte [conceptos del servicio Blob](https://msdn.microsoft.com/library/dd179376.aspx). 
> 
> 

Este tutorial muestra varias maneras que puede establecer Hola TTL en un blob en el almacenamiento de Azure.  

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) es uno de hello formas más rápida y más eficaces tooadminister los servicios de Azure.  Hola de uso `Get-AzureStorageBlob` tooget cmdlet un blob de toohello referencia, a continuación, establezca hello `.ICloudBlob.Properties.CacheControl` propiedad. 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> También puede usar PowerShell[administrar los perfiles de red CDN y puntos de conexión](cdn-manage-powershell.md).
> 
> 

## <a name="azure-storage-client-library-for-net"></a>Biblioteca de cliente de Almacenamiento de Azure para .NET
tooset un blob del TTL con. NET, use hello [biblioteca de cliente de almacenamiento de Azure para .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) propiedad.

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> Hay muchos más ejemplos de código de .NET en hello [ejemplos de almacenamiento de blobs de Azure para .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 
> 

## <a name="other-methods"></a>Otros métodos
* [Interfaz de la línea de comandos de Azure](../cli-install-nodejs.md)
  
    Al cargar el blob de hello, establecer hello *cacheControl* propiedad mediante hello `-p` cambiar.  Este ejemplo establece tooone hora (3600 segundos) de hello TTL.
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [API de REST de servicios de Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    Explícitamente conjunto hello *x-ms---control de caché blob* propiedad en un [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [colocar la lista de bloques](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), o [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) solicitud.
* Herramientas de administración de almacenamiento de terceros
  
    Algunas herramientas de administración del almacenamiento de Azure de terceros permiten hello tooset *CacheControl* propiedad blobs. 

## <a name="testing-hello-cache-control-header"></a>Hola prueba *Cache-Control* encabezado
Puede comprobar fácilmente Hola TTL de los blobs.  Mediante el explorador [herramientas de desarrollo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), probar que el blob es incluidos hello *Cache-Control* encabezado de respuesta.  También puede utilizar una herramienta como **wget**, [Postman](https://www.getpostman.com/), o [Fiddler](http://www.telerik.com/fiddler) encabezados de respuesta de tooexamine Hola.

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga información sobre hello *Cache-Control* encabezado](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [Obtenga información acerca de cómo toomanage caducidad del contenido del servicio de nube en la red CDN de Azure](cdn-manage-expiration-of-cloud-service-content.md)


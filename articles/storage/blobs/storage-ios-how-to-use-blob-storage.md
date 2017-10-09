---
title: aaaHow toouse almacenamiento de blobs de Azure de iOS | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a>¿Cómo toouse almacenamiento de blobs de iOS
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general
En este artículo le mostrará cómo tooperform escenarios comunes con almacenamiento de blobs de Microsoft Azure. ejemplos de Hello están escritos en Objective C y usar hello [biblioteca de cliente de almacenamiento de Azure para iOS](https://github.com/Azure/azure-storage-ios). Hello escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs. Para obtener más información sobre los blobs, vea hello [pasos](#next-steps) sección. También puede descargar hello [aplicación de ejemplo](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly vea Hola el uso de almacenamiento de Azure en una aplicación de iOS.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Importar biblioteca de iOS de almacenamiento de Azure de hello en la aplicación
Puede importar biblioteca de iOS de almacenamiento de Azure de hello en la aplicación mediante hello [CocoaPod de almacenamiento de Azure](https://cocoapods.org/pods/AZSClient) o mediante la importación de hello **Framework** archivo. CocoaPod es hello recomendada manera, ya que facilita la integración biblioteca hello, sin embargo importar desde archivo de framework hello es menos intrusivo para el proyecto existente.

toouse esta biblioteca, deberá Hola siguientes:
- iOS 8+
- Xcode 7+

## <a name="cocoapod"></a>CocoaPod
1. Si aún no lo ha hecho lo ha hecho, [CocoaPods instalar](https://guides.cocoapods.org/using/getting-started.html#toc_3) en el equipo, abra una ventana de terminal y ejecutando el siguiente comando de Hola
    
    ```shell   
    sudo gem install cocoapods
    ```

2. A continuación, en directorio del proyecto hello (directorio de Hola que contiene el archivo .xcodeproj), cree un nuevo archivo denominado _Podfile_(sin extensión de archivo). Agregar Hola después too_Podfile_ y guardar.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. En la ventana de terminal de hello, navegue hello ejecución siguiente comando y directorio del proyecto toohello

    ```shell    
    pod install
    ```

4. Si el archivo .xcodeproj está abierto en Xcode, ciérrelo. En el archivo de proyecto de proyecto directorio abierto Hola recién creado que tendrá la extensión de .xcworkspace de Hola. Se trata de un archivo hello en que trabajará desde para ahora.

## <a name="framework"></a>marco
Hola otra forma de biblioteca de hello toouse es el marco de trabajo de toobuild Hola de manualmente:

1. Primero, descarga u Hola clon [repositorio de almacenamiento de azure de ios](https://github.com/azure/azure-storage-ios).
2. Vaya a *azure-storage-ios* -> *Lib* -> *Biblioteca de cliente de Azure Storage* y abra `AZSClient.xcodeproj` en Xcode.
3. En hello superior izquierda de Xcode, cambio Hola active esquema de "Biblioteca de cliente de almacenamiento de Azure" demasiado "Framework".
4. Compile el proyecto de hello (⌘ + B). Se crea un archivo `AZSClient.framework` en el escritorio.

A continuación, puede importar el archivo de framework de hello en la aplicación haciendo Hola siguiente:

1. Cree un proyecto nuevo o abra un proyecto existente en Xcode.
2. Hola de arrastrar y colocar `AZSClient.framework` en su navegador de proyecto de Xcode.
3. Seleccione *Copy items if needed* (Copiar elementos si es necesario) y haga clic en *Finish* (Finalizar).
4. Haga clic en el proyecto en el panel de navegación izquierdo Hola y Hola *General* ficha en parte superior de hello del editor de hello del proyecto.
5. En hello *vinculado marcos y bibliotecas* sección, haga clic en el botón de agregar hello (+).
6. En la lista Hola de bibliotecas suministradas ya, busque `libxml2.2.tbd` y agregue el proyecto de tooyour.

## <a name="import-hello-library"></a>Hola biblioteca de importación 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Si usas Swift, necesitará toocreate un encabezado de protocolo de puente e Importar < AZSClient/AZSClient.h > no existe:

1. Crear un archivo de encabezado `Bridging-Header.h`y agregue Hola por encima de la instrucción import.
2. Vaya toohello *configuración de generación* ficha y busque *el encabezado de protocolo de puente Objective-C*.
3. Haga doble clic en el campo de Hola de *el encabezado de protocolo de puente Objective-C* y agregue el archivo de encabezado tooyour de hello ruta de acceso:`ProjectName/Bridging-Header.h`
4. Xcode ha recogido tooverify de proyecto (⌘ + B) Hola de compilación que Hola encabezado de protocolo de puente.
5. Empezar a usar la biblioteca de hello directamente en cualquier archivo Swift, no es necesario para las instrucciones de importación.

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Operaciones asincrónicas
> [!NOTE]
> Todos los métodos que realizan una solicitud de servicio de hello son operaciones asincrónicas. En los ejemplos de código de hello, encontrará que estos métodos tienen un controlador de finalización. Se ejecutará el código del controlador de finalización de hello **después** completar la solicitud de saludo. Código después de que se ejecutará el controlador de finalización de hello **mientras** Hola se ha solicitado realizar.
> 
> 

## <a name="create-a-container"></a>Crear un contenedor
Todos los blobs del Almacenamiento de Azure deben residir en un contenedor. Hello en el ejemplo siguiente se muestra cómo toocreate un contenedor, llamar *newcontainer*, en la cuenta de almacenamiento, si aún no existe. Al elegir un nombre para el contenedor, esté atento a Hola nomenclatura reglas mencionadas anteriormente.

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

Puede confirmar que esto funciona examinando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) y comprobar que *newcontainer* está en la lista de Hola de contenedores de la cuenta de almacenamiento.

## <a name="set-container-permissions"></a>Establecimiento de los permisos del contenedor
De manera predeterminada, los permisos de un contenedor se configuran para el acceso **Privado** . Sin embargo, los contenedores proporcionan varias opciones diferentes para acceder a ellos:

* **Privada**: solo el propietario Hola cuenta pueden leer los datos de contenedor y blob.
* **Blob**: los datos de los blobs de este contenedor se pueden leer a través de una solicitud anónima, pero los datos del contenedor no están disponibles. Los clientes no pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima.
* **Contenedor**: los datos del contenedor y de los blobs se pueden leer mediante una solicitud anónima. Los clientes pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima, pero no pueden enumerar contenedores dentro de la cuenta de almacenamiento de Hola.

Hello en el ejemplo siguiente se muestra cómo toocreate un contenedor con **contenedor** tener acceso a permisos, lo que permiten el acceso público, de solo lectura para todos los usuarios Hola Internet:

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
Como se mencionó en hello [conceptos del servicio de Blob](#blob-service-concepts) sección, almacenamiento de blobs ofrece tres tipos diferentes de blobs: blobs en bloques, blobs en anexos y blobs en páginas. biblioteca de iOS de almacenamiento de Azure de Hello es compatible con los tres tipos de blobs. En la mayoría de los casos, blob en bloques es hello recomendada toouse de tipo.

Hola de ejemplo siguiente muestra cómo tooupload un bloque de blobs de un NSString. Si un blob con el mismo nombre ya existe en este contenedor de hello, se sobrescribirá el contenido de Hola de este blob.

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

Puede confirmar que esto funciona examinando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) y comprobación de ese contenedor hello, *containerpublic*, contiene el blob de hello, *sampleblob*. En este ejemplo, se utiliza un contenedor público para que también pueda comprobar que esta aplicación ha funcionado por va toohello blobs URI:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

Además toouploading un blob en bloques de un NSString, existen métodos similares para NSData, NSInputStream o un archivo local.

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
Hello en el ejemplo siguiente se muestra cómo toolist todos los blobs en un contenedor. Al realizar esta operación, tenga en cuenta de hello parámetros siguientes:     

* **continuationToken** -Hola representa token de continuación donde debe comenzar la operación de lista de Hola. Si no se proporciona ningún token, se enumerarán blobs desde el principio de Hola. Puede enumerar cualquier cantidad de blobs, desde cero una tooa establezca máximo. Aunque este método no devuelve ningún resultado, si `results.continuationToken` no es nulo, puede haber más blobs en el servicio de Hola que no se han enumerado.
* **prefijo** -puede especificar hello toouse de prefijo de la lista de blobs. Solo se enumerarán los blobs que comiencen por dicho prefijo.
* **useFlatBlobListing** : como se mencionó en hello [escribir el nombre y la referencia a contenedores y blobs](#naming-and-referencing-containers-and-blobs) sección, aunque Hola servicio Blob es un esquema de almacenamiento sin formato, puede crear una jerarquía virtual asignando un BLOB con la ruta de acceso información. Sin embargo, actualmente no se admiten listas que no sean planas. Esta característica estará disponible próximamente. Por el momento, este valor debe ser **SÍ**.
* **blobListingDetails** -puede especificar qué tooinclude elementos al enumerar los blobs
  * _AZSBlobListingDetailsNone_: solo muestra los blobs confirmados y no devuelve los metadatos de blob.
  * _AZSBlobListingDetailsSnapshots_: muestra los blobs confirmados y las instantáneas de blob.
  * _AZSBlobListingDetailsMetadata_: recupera metadatos del blob para cada blob devuelvan en la lista de Hola.
  * _AZSBlobListingDetailsUncommittedBlobs_: muestra los blobs confirmados y sin confirmar.
  * _AZSBlobListingDetailsCopy_: incluir copia propiedades de anuncio Hola.
  * _AZSBlobListingDetailsAll_: muestra todos los blobs confirmados, blobs sin confirmar e instantáneas disponibles. Además, se devuelven todos los metadatos y estados de copia de dichos blobs.
* **maxResults** -Hola número máximo de resultados tooreturn para esta operación. Utilice -1 toonot establece un límite.
* **completionHandler** -bloque de Hola de tooexecute de código con resultados de Hola de hello operación de lista.

En este ejemplo, un método auxiliar es toorecursively usado llamada Hola list blobs (método) cada vez que se devuelve un token de continuación.

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a>Descarga de un blob
Hola siguiente ejemplo se muestra cómo toodownload un objeto de NSString tooa de blob.

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a>Eliminar un blob
Hola siguiente ejemplo se muestra cómo toodelete un blob.

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a>un contenedor de blobs
Hola siguiente ejemplo se muestra cómo toodelete un contenedor.

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido cómo toouse almacenamiento de blobs de iOS, siga estas toolearn de vínculos más información acerca de la biblioteca de iOS de Hola y Hola servicio de almacenamiento.

* [Biblioteca de cliente de almacenamiento de Azure para iOS](https://github.com/azure/azure-storage-ios)
* [Documentación de referencia de iOS del Almacenamiento de Azure](http://azure.github.io/azure-storage-ios/)
* [API de REST de servicios de almacenamiento de Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage)

Si tiene alguna pregunta sobre esta biblioteca, cree libre toopost tooour [foro de Azure de MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) o [desbordamiento de la pila](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Si tiene sugerencias sobre características para el almacenamiento de Azure, publique demasiado[comentarios de almacenamiento de Azure](https://feedback.azure.com/forums/217298-storage/).


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
ms.openlocfilehash: 474c4263a4bfbd61bfa39e4fdb01ddd9c3829c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="ab8c5-103">¿Cómo toouse almacenamiento de blobs de iOS</span><span class="sxs-lookup"><span data-stu-id="ab8c5-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="ab8c5-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ab8c5-104">Overview</span></span>
<span data-ttu-id="ab8c5-105">En este artículo le mostrará cómo tooperform escenarios comunes con almacenamiento de blobs de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="ab8c5-106">ejemplos de Hello están escritos en Objective C y usar hello [biblioteca de cliente de almacenamiento de Azure para iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="ab8c5-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="ab8c5-107">Hello escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="ab8c5-108">Para obtener más información sobre los blobs, vea hello [pasos](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="ab8c5-109">También puede descargar hello [aplicación de ejemplo](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly vea Hola el uso de almacenamiento de Azure en una aplicación de iOS.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="ab8c5-110">Importar biblioteca de iOS de almacenamiento de Azure de hello en la aplicación</span><span class="sxs-lookup"><span data-stu-id="ab8c5-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="ab8c5-111">Puede importar biblioteca de iOS de almacenamiento de Azure de hello en la aplicación mediante hello [CocoaPod de almacenamiento de Azure](https://cocoapods.org/pods/AZSClient) o mediante la importación de hello **Framework** archivo.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="ab8c5-112">CocoaPod es hello recomendada manera, ya que facilita la integración biblioteca hello, sin embargo importar desde archivo de framework hello es menos intrusivo para el proyecto existente.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="ab8c5-113">toouse esta biblioteca, deberá Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="ab8c5-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="ab8c5-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="ab8c5-114">iOS 8+</span></span>
- <span data-ttu-id="ab8c5-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="ab8c5-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="ab8c5-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="ab8c5-116">CocoaPod</span></span>
1. <span data-ttu-id="ab8c5-117">Si aún no lo ha hecho lo ha hecho, [CocoaPods instalar](https://guides.cocoapods.org/using/getting-started.html#toc_3) en el equipo, abra una ventana de terminal y ejecutando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="ab8c5-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="ab8c5-118">A continuación, en directorio del proyecto hello (directorio de Hola que contiene el archivo .xcodeproj), cree un nuevo archivo denominado _Podfile_(sin extensión de archivo).</span><span class="sxs-lookup"><span data-stu-id="ab8c5-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="ab8c5-119">Agregar Hola después too_Podfile_ y guardar.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="ab8c5-120">En la ventana de terminal de hello, navegue hello ejecución siguiente comando y directorio del proyecto toohello</span><span class="sxs-lookup"><span data-stu-id="ab8c5-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="ab8c5-121">Si el archivo .xcodeproj está abierto en Xcode, ciérrelo.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="ab8c5-122">En el archivo de proyecto de proyecto directorio abierto Hola recién creado que tendrá la extensión de .xcworkspace de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="ab8c5-123">Se trata de un archivo hello en que trabajará desde para ahora.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="ab8c5-124">marco</span><span class="sxs-lookup"><span data-stu-id="ab8c5-124">Framework</span></span>
<span data-ttu-id="ab8c5-125">Hola otra forma de biblioteca de hello toouse es el marco de trabajo de toobuild Hola de manualmente:</span><span class="sxs-lookup"><span data-stu-id="ab8c5-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="ab8c5-126">Primero, descarga u Hola clon [repositorio de almacenamiento de azure de ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="ab8c5-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="ab8c5-127">Vaya a *azure-storage-ios* -> *Lib* -> *Biblioteca de cliente de Azure Storage* y abra `AZSClient.xcodeproj` en Xcode.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="ab8c5-128">En hello superior izquierda de Xcode, cambio Hola active esquema de "Biblioteca de cliente de almacenamiento de Azure" demasiado "Framework".</span><span class="sxs-lookup"><span data-stu-id="ab8c5-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="ab8c5-129">Compile el proyecto de hello (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="ab8c5-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="ab8c5-130">Se crea un archivo `AZSClient.framework` en el escritorio.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="ab8c5-131">A continuación, puede importar el archivo de framework de hello en la aplicación haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab8c5-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="ab8c5-132">Cree un proyecto nuevo o abra un proyecto existente en Xcode.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="ab8c5-133">Hola de arrastrar y colocar `AZSClient.framework` en su navegador de proyecto de Xcode.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="ab8c5-134">Seleccione *Copy items if needed* (Copiar elementos si es necesario) y haga clic en *Finish* (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="ab8c5-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="ab8c5-135">Haga clic en el proyecto en el panel de navegación izquierdo Hola y Hola *General* ficha en parte superior de hello del editor de hello del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="ab8c5-136">En hello *vinculado marcos y bibliotecas* sección, haga clic en el botón de agregar hello (+).</span><span class="sxs-lookup"><span data-stu-id="ab8c5-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="ab8c5-137">En la lista Hola de bibliotecas suministradas ya, busque `libxml2.2.tbd` y agregue el proyecto de tooyour.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="ab8c5-138">Hola biblioteca de importación</span><span class="sxs-lookup"><span data-stu-id="ab8c5-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="ab8c5-139">Si usas Swift, necesitará toocreate un encabezado de protocolo de puente e Importar < AZSClient/AZSClient.h > no existe:</span><span class="sxs-lookup"><span data-stu-id="ab8c5-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="ab8c5-140">Crear un archivo de encabezado `Bridging-Header.h`y agregue Hola por encima de la instrucción import.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="ab8c5-141">Vaya toohello *configuración de generación* ficha y busque *el encabezado de protocolo de puente Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="ab8c5-142">Haga doble clic en el campo de Hola de *el encabezado de protocolo de puente Objective-C* y agregue el archivo de encabezado tooyour de hello ruta de acceso:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="ab8c5-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="ab8c5-143">Xcode ha recogido tooverify de proyecto (⌘ + B) Hola de compilación que Hola encabezado de protocolo de puente.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="ab8c5-144">Empezar a usar la biblioteca de hello directamente en cualquier archivo Swift, no es necesario para las instrucciones de importación.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="ab8c5-145">Operaciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="ab8c5-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="ab8c5-146">Todos los métodos que realizan una solicitud de servicio de hello son operaciones asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="ab8c5-147">En los ejemplos de código de hello, encontrará que estos métodos tienen un controlador de finalización.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="ab8c5-148">Se ejecutará el código del controlador de finalización de hello **después** completar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="ab8c5-149">Código después de que se ejecutará el controlador de finalización de hello **mientras** Hola se ha solicitado realizar.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="ab8c5-150">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="ab8c5-150">Create a container</span></span>
<span data-ttu-id="ab8c5-151">Todos los blobs del Almacenamiento de Azure deben residir en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="ab8c5-152">Hello en el ejemplo siguiente se muestra cómo toocreate un contenedor, llamar *newcontainer*, en la cuenta de almacenamiento, si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="ab8c5-153">Al elegir un nombre para el contenedor, esté atento a Hola nomenclatura reglas mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

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

<span data-ttu-id="ab8c5-154">Puede confirmar que esto funciona examinando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) y comprobar que *newcontainer* está en la lista de Hola de contenedores de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="ab8c5-155">Establecimiento de los permisos del contenedor</span><span class="sxs-lookup"><span data-stu-id="ab8c5-155">Set Container Permissions</span></span>
<span data-ttu-id="ab8c5-156">De manera predeterminada, los permisos de un contenedor se configuran para el acceso **Privado** .</span><span class="sxs-lookup"><span data-stu-id="ab8c5-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="ab8c5-157">Sin embargo, los contenedores proporcionan varias opciones diferentes para acceder a ellos:</span><span class="sxs-lookup"><span data-stu-id="ab8c5-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="ab8c5-158">**Privada**: solo el propietario Hola cuenta pueden leer los datos de contenedor y blob.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="ab8c5-159">**Blob**: los datos de los blobs de este contenedor se pueden leer a través de una solicitud anónima, pero los datos del contenedor no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="ab8c5-160">Los clientes no pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="ab8c5-161">**Contenedor**: los datos del contenedor y de los blobs se pueden leer mediante una solicitud anónima.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="ab8c5-162">Los clientes pueden enumerar blobs en el contenedor de hello mediante una solicitud anónima, pero no pueden enumerar contenedores dentro de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="ab8c5-163">Hello en el ejemplo siguiente se muestra cómo toocreate un contenedor con **contenedor** tener acceso a permisos, lo que permiten el acceso público, de solo lectura para todos los usuarios Hola Internet:</span><span class="sxs-lookup"><span data-stu-id="ab8c5-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

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

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ab8c5-164">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ab8c5-164">Upload a blob into a container</span></span>
<span data-ttu-id="ab8c5-165">Como se mencionó en hello [conceptos del servicio de Blob](#blob-service-concepts) sección, almacenamiento de blobs ofrece tres tipos diferentes de blobs: blobs en bloques, blobs en anexos y blobs en páginas.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="ab8c5-166">biblioteca de iOS de almacenamiento de Azure de Hello es compatible con los tres tipos de blobs.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="ab8c5-167">En la mayoría de los casos, blob en bloques es hello recomendada toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="ab8c5-168">Hola de ejemplo siguiente muestra cómo tooupload un bloque de blobs de un NSString.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="ab8c5-169">Si un blob con el mismo nombre ya existe en este contenedor de hello, se sobrescribirá el contenido de Hola de este blob.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

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

<span data-ttu-id="ab8c5-170">Puede confirmar que esto funciona examinando hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) y comprobación de ese contenedor hello, *containerpublic*, contiene el blob de hello, *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="ab8c5-171">En este ejemplo, se utiliza un contenedor público para que también pueda comprobar que esta aplicación ha funcionado por va toohello blobs URI:</span><span class="sxs-lookup"><span data-stu-id="ab8c5-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="ab8c5-172">Además toouploading un blob en bloques de un NSString, existen métodos similares para NSData, NSInputStream o un archivo local.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="ab8c5-173">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ab8c5-173">List hello blobs in a container</span></span>
<span data-ttu-id="ab8c5-174">Hello en el ejemplo siguiente se muestra cómo toolist todos los blobs en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="ab8c5-175">Al realizar esta operación, tenga en cuenta de hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="ab8c5-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="ab8c5-176">**continuationToken** -Hola representa token de continuación donde debe comenzar la operación de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="ab8c5-177">Si no se proporciona ningún token, se enumerarán blobs desde el principio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="ab8c5-178">Puede enumerar cualquier cantidad de blobs, desde cero una tooa establezca máximo.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="ab8c5-179">Aunque este método no devuelve ningún resultado, si `results.continuationToken` no es nulo, puede haber más blobs en el servicio de Hola que no se han enumerado.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="ab8c5-180">**prefijo** -puede especificar hello toouse de prefijo de la lista de blobs.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="ab8c5-181">Solo se enumerarán los blobs que comiencen por dicho prefijo.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="ab8c5-182">**useFlatBlobListing** : como se mencionó en hello [escribir el nombre y la referencia a contenedores y blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) sección, aunque Hola servicio Blob es un esquema de almacenamiento sin formato, puede crear una jerarquía virtual asignando un BLOB con la ruta de acceso información.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="ab8c5-183">Sin embargo, actualmente no se admiten listas que no sean planas.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="ab8c5-184">Esta característica estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-184">This feature is coming soon.</span></span> <span data-ttu-id="ab8c5-185">Por el momento, este valor debe ser **SÍ**.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="ab8c5-186">**blobListingDetails** -puede especificar qué tooinclude elementos al enumerar los blobs</span><span class="sxs-lookup"><span data-stu-id="ab8c5-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="ab8c5-187">_AZSBlobListingDetailsNone_: solo muestra los blobs confirmados y no devuelve los metadatos de blob.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="ab8c5-188">_AZSBlobListingDetailsSnapshots_: muestra los blobs confirmados y las instantáneas de blob.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="ab8c5-189">_AZSBlobListingDetailsMetadata_: recupera metadatos del blob para cada blob devuelvan en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="ab8c5-190">_AZSBlobListingDetailsUncommittedBlobs_: muestra los blobs confirmados y sin confirmar.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="ab8c5-191">_AZSBlobListingDetailsCopy_: incluir copia propiedades de anuncio Hola.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="ab8c5-192">_AZSBlobListingDetailsAll_: muestra todos los blobs confirmados, blobs sin confirmar e instantáneas disponibles. Además, se devuelven todos los metadatos y estados de copia de dichos blobs.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="ab8c5-193">**maxResults** -Hola número máximo de resultados tooreturn para esta operación.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="ab8c5-194">Utilice -1 toonot establece un límite.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="ab8c5-195">**completionHandler** -bloque de Hola de tooexecute de código con resultados de Hola de hello operación de lista.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="ab8c5-196">En este ejemplo, un método auxiliar es toorecursively usado llamada Hola list blobs (método) cada vez que se devuelve un token de continuación.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="ab8c5-197">Descarga de un blob</span><span class="sxs-lookup"><span data-stu-id="ab8c5-197">Download a blob</span></span>
<span data-ttu-id="ab8c5-198">Hola siguiente ejemplo se muestra cómo toodownload un objeto de NSString tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="ab8c5-199">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="ab8c5-199">Delete a blob</span></span>
<span data-ttu-id="ab8c5-200">Hola siguiente ejemplo se muestra cómo toodelete un blob.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-200">hello following example shows how toodelete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="ab8c5-201">un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="ab8c5-201">Delete a blob container</span></span>
<span data-ttu-id="ab8c5-202">Hola siguiente ejemplo se muestra cómo toodelete un contenedor.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-202">hello following example shows how toodelete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ab8c5-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab8c5-203">Next steps</span></span>
<span data-ttu-id="ab8c5-204">Ahora que ha aprendido cómo toouse almacenamiento de blobs de iOS, siga estas toolearn de vínculos más información acerca de la biblioteca de iOS de Hola y Hola servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ab8c5-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="ab8c5-205">Biblioteca de cliente de almacenamiento de Azure para iOS</span><span class="sxs-lookup"><span data-stu-id="ab8c5-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="ab8c5-206">Documentación de referencia de iOS del Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ab8c5-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="ab8c5-207">API de REST de servicios de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ab8c5-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="ab8c5-208">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ab8c5-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="ab8c5-209">Si tiene alguna pregunta sobre esta biblioteca, cree libre toopost tooour [foro de Azure de MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) o [desbordamiento de la pila](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="ab8c5-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="ab8c5-210">Si tiene sugerencias sobre características para el almacenamiento de Azure, publique demasiado[comentarios de almacenamiento de Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="ab8c5-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>


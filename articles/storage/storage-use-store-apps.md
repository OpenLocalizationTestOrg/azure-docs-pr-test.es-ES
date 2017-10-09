---
title: aaaUse almacenamiento de Azure en aplicaciones de la tienda de Windows | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una tienda Windows aplicación que utiliza el almacenamiento de Azure Blob, cola, tabla o archivo."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="e882d-103">Cómo toouse el almacenamiento de Azure en aplicaciones de la tienda de Windows</span><span class="sxs-lookup"><span data-stu-id="e882d-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="e882d-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e882d-104">Overview</span></span>
<span data-ttu-id="e882d-105">Esta guía muestra cómo tooget se inicia con el desarrollo de aplicaciones de la tienda de Windows que usa el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e882d-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="e882d-106">Descarga de las herramientas necesarias</span><span class="sxs-lookup"><span data-stu-id="e882d-106">Download required tools</span></span>
* <span data-ttu-id="e882d-107">[Visual Studio](https://www.visualstudio.com/downloads/) resulta fácil toobuild, depurar, localizar, empaquetar e implementar aplicaciones de la tienda de Windows.</span><span class="sxs-lookup"><span data-stu-id="e882d-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="e882d-108">Se requiere Visual Studio 2012 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e882d-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="e882d-109">Hola [biblioteca de cliente de almacenamiento de Azure](https://www.nuget.org/packages/WindowsAzure.Storage) proporciona una biblioteca de clases en tiempo de ejecución de Windows para trabajar con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e882d-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="e882d-110">[WCF datos servicios herramientas para aplicaciones tienda Windows](http://www.microsoft.com/download/details.aspx?id=30714) amplía la experiencia de hello Agregar referencia de servicio con el soporte técnico de OData del lado cliente para aplicaciones de la tienda de Windows en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e882d-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="e882d-111">Desarrollo de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e882d-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="e882d-112">Preparación</span><span class="sxs-lookup"><span data-stu-id="e882d-112">Getting ready</span></span>
<span data-ttu-id="e882d-113">Cree un nuevo proyecto de aplicaciones de la Tienda Windows en Visual Studio 2012 o posterior:</span><span class="sxs-lookup"><span data-stu-id="e882d-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="e882d-115">A continuación, agregue una biblioteca de cliente de almacenamiento de Azure de referencia toohello haciendo clic en **referencias**, haga clic en **Agregar referencia**y, a continuación, examinar toohello biblioteca de cliente de almacenamiento de Windows Runtime que descargar:</span><span class="sxs-lookup"><span data-stu-id="e882d-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="e882d-117">Con biblioteca Hola con hello Blob y servicios de cola</span><span class="sxs-lookup"><span data-stu-id="e882d-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="e882d-118">En este punto, la aplicación es servicios de Azure Blob y cola de hello toocall listo.</span><span class="sxs-lookup"><span data-stu-id="e882d-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="e882d-119">Agregue los siguiente hello **con** instrucciones para que se pueden hacer referencia directamente a los tipos de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="e882d-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="e882d-120">A continuación, agregue una página de tooyour de botón.</span><span class="sxs-lookup"><span data-stu-id="e882d-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="e882d-121">Agregar Hola después código tooits **haga clic en** eventos y modificar su método de controlador de eventos mediante hello [palabra clave async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="e882d-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="e882d-122">Este código supone que hay dos variables de cadena, *accountName* y *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="e882d-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="e882d-123">Representan nombre Hola de su clave de cuenta de hello y cuenta de almacenamiento que está asociado a esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="e882d-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="e882d-124">Compile y ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e882d-124">Build and run hello application.</span></span> <span data-ttu-id="e882d-125">Haga clic en botón Hola comprobará si un contenedor denominado *container1* existe en su cuenta y crearla si no es así.</span><span class="sxs-lookup"><span data-stu-id="e882d-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="e882d-126">Usar la biblioteca de hello con hello servicio tabla</span><span class="sxs-lookup"><span data-stu-id="e882d-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="e882d-127">Tipos que son toocommunicate usado con el servicio de la tabla de Azure de hello dependen de WCF Data Services para la biblioteca de aplicación de tienda Windows hello.</span><span class="sxs-lookup"><span data-stu-id="e882d-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="e882d-128">A continuación, agregue que una referencia toohello requiere bibliotecas WCF mediante el uso de Hola Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="e882d-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="e882d-130">Usar hello después comando toopoint ubicación toohello del Administrador de paquetes en el equipo:</span><span class="sxs-lookup"><span data-stu-id="e882d-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="e882d-131">Este comando agregará automáticamente todas las referencias necesarias tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="e882d-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="e882d-132">Si no desea toouse Hola consola de administrador de paquetes, puede agregar carpeta de NuGet de servicios de datos de WCF de hello en la lista de toohello de equipo local de orígenes de paquetes y, a continuación, agregar referencia de Hola a través de hello interfaz de usuario, como se describe en [administración de uso de paquetes de NuGet Hola diálogo](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="e882d-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="e882d-133">Cuando se hace referencia a paquetes de NuGet de servicios de datos de WCF de hello, cambie el código de hello en el botón **haga clic en** eventos:</span><span class="sxs-lookup"><span data-stu-id="e882d-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="e882d-134">Este código comprueba si la tabla con el nombre *table1* existe en su cuenta y, a continuación, se crea si no existiera.</span><span class="sxs-lookup"><span data-stu-id="e882d-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="e882d-135">También puede agregar una referencia tooMicrosoft.WindowsAzure.Storage.Table.dll, que está disponible en el mismo paquete que descargó de Hola.</span><span class="sxs-lookup"><span data-stu-id="e882d-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="e882d-136">Esta biblioteca contiene una funcionalidad adicional como consultas genéricas y de serialización basadas en reflejo.</span><span class="sxs-lookup"><span data-stu-id="e882d-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="e882d-137">Tenga en cuenta que esta biblioteca no es compatible con JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e882d-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png

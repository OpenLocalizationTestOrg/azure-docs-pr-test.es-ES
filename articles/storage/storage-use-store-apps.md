---
title: Uso de Azure Storage en las aplicaciones de la Tienda Windows | Microsoft Docs
description: "Obtenga información acerca de cómo crear una aplicación de la Tienda Windows que usa Almacenamiento de blobs, Almacenamiento de colas, Almacenamiento de tablas o Almacenamiento de archivos de Azure."
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
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="c11aa-103">Uso de Almacenamiento de Azure en las aplicaciones de la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="c11aa-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="c11aa-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c11aa-104">Overview</span></span>
<span data-ttu-id="c11aa-105">Esta guía le muestra cómo comenzar con el desarrollo de una aplicación de la Tienda Windows que haga uso del almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c11aa-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="c11aa-106">Descarga de las herramientas necesarias</span><span class="sxs-lookup"><span data-stu-id="c11aa-106">Download required tools</span></span>
* <span data-ttu-id="c11aa-107">[Visual Studio](https://www.visualstudio.com/downloads/) hace que sea fácil compilar, depurar, localizar, empaquetar e implementar aplicaciones de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="c11aa-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="c11aa-108">Se requiere Visual Studio 2012 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c11aa-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="c11aa-109">La [Biblioteca de cliente de Almacenamiento de Azure](https://www.nuget.org/packages/WindowsAzure.Storage) proporciona una biblioteca de clases en tiempo de ejecución de Windows para trabajar con Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c11aa-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="c11aa-110">[Herramientas de servicios de datos WCF para aplicaciones de la Tienda Windows](http://www.microsoft.com/download/details.aspx?id=30714) amplía la experiencia de incorporación de referencias de servicios gracias a la compatibilidad de OData del lado cliente en aplicaciones de la Tienda Windows en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c11aa-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="c11aa-111">Desarrollo de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c11aa-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="c11aa-112">Preparación</span><span class="sxs-lookup"><span data-stu-id="c11aa-112">Getting ready</span></span>
<span data-ttu-id="c11aa-113">Cree un nuevo proyecto de aplicaciones de la Tienda Windows en Visual Studio 2012 o posterior:</span><span class="sxs-lookup"><span data-stu-id="c11aa-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="c11aa-115">A continuación, agregue una referencia a la biblioteca de cliente de Almacenamiento de Azure; para ello, haga clic con el botón derecho en **Referencias**, a continuación, en **Agregar referencia** y vaya a la biblioteca de cliente de Almacenamiento para Windows en tiempo de ejecución que ha descargado:</span><span class="sxs-lookup"><span data-stu-id="c11aa-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="c11aa-117">Uso de la biblioteca con los servicios BLOB y Cola</span><span class="sxs-lookup"><span data-stu-id="c11aa-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="c11aa-118">En este momento, la aplicación está preparada para llamar a los servicios Blob de Azure y Cola.</span><span class="sxs-lookup"><span data-stu-id="c11aa-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="c11aa-119">Agregue las siguientes instrucciones **using** de manera que pueda hacerse referencia directamente a los tipos de Almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="c11aa-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="c11aa-120">A continuación, agregue un botón a la página.</span><span class="sxs-lookup"><span data-stu-id="c11aa-120">Next, add a button to your page.</span></span> <span data-ttu-id="c11aa-121">Agregue el siguiente código al evento **Click** y modifique el método del controlador de eventos con la palabra clave [async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="c11aa-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="c11aa-122">Este código supone que hay dos variables de cadena, *accountName* y *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="c11aa-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="c11aa-123">Representan el nombre de la cuenta de almacenamiento y la clave de la cuenta que está asociada con esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="c11aa-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="c11aa-124">Compile y ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c11aa-124">Build and run the application.</span></span> <span data-ttu-id="c11aa-125">Si hace clic en el botón, se comprobará si existe un contenedor con el nombre *container1* en la cuenta y se creará si no existiera.</span><span class="sxs-lookup"><span data-stu-id="c11aa-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="c11aa-126">Uso de la biblioteca con el servicio Tabla</span><span class="sxs-lookup"><span data-stu-id="c11aa-126">Using the library with the Table service</span></span>
<span data-ttu-id="c11aa-127">Los tipos usados para comunicarse con el servicio Tabla de Azure dependen de la biblioteca de servicios de datos WCF para la aplicación de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="c11aa-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="c11aa-128">A continuación, agregue una referencia a las bibliotecas WCF necesarias mediante la consola del administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="c11aa-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="c11aa-130">Use el siguiente comando para que el administrador de paquetes apunte a la ubicación de la máquina:</span><span class="sxs-lookup"><span data-stu-id="c11aa-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="c11aa-131">Este comando agregará automáticamente todas las referencias necesarias a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="c11aa-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="c11aa-132">Si no desea usar la consola del administrador de paquetes, puede agregar la carpeta NuGet de servicios de datos WCF en su máquina local a la lista de orígenes de paquetes y, a continuación, agregar la referencia a través de la interfaz de usuario como se describe en [Administración de paquetes NuGet mediante el cuadro de diálogo](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="c11aa-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="c11aa-133">Cuando haya hecho referencia al paquete NuGet de servicios de datos WCF, cambie el código en el evento **Click** del botón:</span><span class="sxs-lookup"><span data-stu-id="c11aa-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="c11aa-134">Este código comprueba si la tabla con el nombre *table1* existe en su cuenta y, a continuación, se crea si no existiera.</span><span class="sxs-lookup"><span data-stu-id="c11aa-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="c11aa-135">También puede agregar una referencia a Microsoft.WindowsAzure.Storage.Table.dll que está disponible en el mismo paquete que descargó.</span><span class="sxs-lookup"><span data-stu-id="c11aa-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="c11aa-136">Esta biblioteca contiene una funcionalidad adicional como consultas genéricas y de serialización basadas en reflejo.</span><span class="sxs-lookup"><span data-stu-id="c11aa-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="c11aa-137">Tenga en cuenta que esta biblioteca no es compatible con JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c11aa-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png

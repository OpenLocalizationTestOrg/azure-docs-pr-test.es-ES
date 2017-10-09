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
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>Cómo toouse el almacenamiento de Azure en aplicaciones de la tienda de Windows
## <a name="overview"></a>Información general
Esta guía muestra cómo tooget se inicia con el desarrollo de aplicaciones de la tienda de Windows que usa el almacenamiento de Azure.

## <a name="download-required-tools"></a>Descarga de las herramientas necesarias
* [Visual Studio](https://www.visualstudio.com/downloads/) resulta fácil toobuild, depurar, localizar, empaquetar e implementar aplicaciones de la tienda de Windows. Se requiere Visual Studio 2012 o posterior.
* Hola [biblioteca de cliente de almacenamiento de Azure](https://www.nuget.org/packages/WindowsAzure.Storage) proporciona una biblioteca de clases en tiempo de ejecución de Windows para trabajar con el almacenamiento de Azure.
* [WCF datos servicios herramientas para aplicaciones tienda Windows](http://www.microsoft.com/download/details.aspx?id=30714) amplía la experiencia de hello Agregar referencia de servicio con el soporte técnico de OData del lado cliente para aplicaciones de la tienda de Windows en Visual Studio.

## <a name="develop-apps"></a>Desarrollo de aplicaciones
### <a name="getting-ready"></a>Preparación
Cree un nuevo proyecto de aplicaciones de la Tienda Windows en Visual Studio 2012 o posterior:

![store-apps-storage-vs-project][store-apps-storage-vs-project]

A continuación, agregue una biblioteca de cliente de almacenamiento de Azure de referencia toohello haciendo clic en **referencias**, haga clic en **Agregar referencia**y, a continuación, examinar toohello biblioteca de cliente de almacenamiento de Windows Runtime que descargar:

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>Con biblioteca Hola con hello Blob y servicios de cola
En este punto, la aplicación es servicios de Azure Blob y cola de hello toocall listo. Agregue los siguiente hello **con** instrucciones para que se pueden hacer referencia directamente a los tipos de almacenamiento de Azure:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

A continuación, agregue una página de tooyour de botón. Agregar Hola después código tooits **haga clic en** eventos y modificar su método de controlador de eventos mediante hello [palabra clave async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Este código supone que hay dos variables de cadena, *accountName* y *accountKey*. Representan nombre Hola de su clave de cuenta de hello y cuenta de almacenamiento que está asociado a esa cuenta.

Compile y ejecute la aplicación hello. Haga clic en botón Hola comprobará si un contenedor denominado *container1* existe en su cuenta y crearla si no es así.

### <a name="using-hello-library-with-hello-table-service"></a>Usar la biblioteca de hello con hello servicio tabla
Tipos que son toocommunicate usado con el servicio de la tabla de Azure de hello dependen de WCF Data Services para la biblioteca de aplicación de tienda Windows hello. A continuación, agregue que una referencia toohello requiere bibliotecas WCF mediante el uso de Hola Package Manager Console:

![store-apps-storage-package-manager][store-apps-storage-package-manager]

Usar hello después comando toopoint ubicación toohello del Administrador de paquetes en el equipo:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Este comando agregará automáticamente todas las referencias necesarias tooyour proyecto. Si no desea toouse Hola consola de administrador de paquetes, puede agregar carpeta de NuGet de servicios de datos de WCF de hello en la lista de toohello de equipo local de orígenes de paquetes y, a continuación, agregar referencia de Hola a través de hello interfaz de usuario, como se describe en [administración de uso de paquetes de NuGet Hola diálogo](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Cuando se hace referencia a paquetes de NuGet de servicios de datos de WCF de hello, cambie el código de hello en el botón **haga clic en** eventos:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Este código comprueba si la tabla con el nombre *table1* existe en su cuenta y, a continuación, se crea si no existiera.

También puede agregar una referencia tooMicrosoft.WindowsAzure.Storage.Table.dll, que está disponible en el mismo paquete que descargó de Hola. Esta biblioteca contiene una funcionalidad adicional como consultas genéricas y de serialización basadas en reflejo. Tenga en cuenta que esta biblioteca no es compatible con JavaScript.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png

---
title: aaaGet a trabajar con almacenamiento de tabla de Azure y servicios conectados de Visual Studio (ASP.NET) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de tabla de Azure en un proyecto de ASP.NET en Visual Studio después de conectar la cuenta de almacenamiento de tooa con servicios conectados de Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: e7ed17098c8742954972dc9e1b50eca77221e327
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="221ee-103">Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="221ee-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="221ee-104">Información general</span><span class="sxs-lookup"><span data-stu-id="221ee-104">Overview</span></span>

<span data-ttu-id="221ee-105">El almacenamiento de tabla permite toostore grandes cantidades de datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="221ee-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="221ee-106">servicio de Hello es un almacén de datos NoSQL que acepta llamadas autenticadas de dentro y fuera Hola nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="221ee-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="221ee-107">Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.</span><span class="sxs-lookup"><span data-stu-id="221ee-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="221ee-108">Este tutorial muestra cómo código toowrite ASP.NET en algunos escenarios comunes con las entidades de almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="221ee-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="221ee-109">Entre los escenarios descritos se incluyen crear, consultar y eliminar entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="221ee-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="221ee-110">Prerequisites</span></span>

* [<span data-ttu-id="221ee-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="221ee-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="221ee-112">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="221ee-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="221ee-113">Creación de un controlador MVC</span><span class="sxs-lookup"><span data-stu-id="221ee-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="221ee-114">Hola **el Explorador de soluciones**, haga clic en **controladores**y, en el menú contextual de hello, seleccione **Agregar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="221ee-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Agregar una aplicación de ASP.NET MVC tooan de controlador](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="221ee-116">En hello **agregar scaffolding** cuadro de diálogo, seleccione **controlador de MVC 5 - vacío**y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="221ee-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especifique el tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="221ee-118">En hello **Agregar controlador** cuadro de diálogo, nombre del controlador que hello *TablesController*y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="221ee-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Controlador de MVC Hola de nombre](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="221ee-120">Agregue los siguiente hello *con* toohello directivas `TablesController.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="221ee-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="221ee-121">Creación de una clase de modelo</span><span class="sxs-lookup"><span data-stu-id="221ee-121">Create a model class</span></span>

<span data-ttu-id="221ee-122">Muchos de los ejemplos de hello en este artículo utilizan un **TableEntity**-deriva la clase llamada **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="221ee-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="221ee-123">Hola pasos guiarle por declarar esta clase como una clase de modelo:</span><span class="sxs-lookup"><span data-stu-id="221ee-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="221ee-124">Hola **el Explorador de soluciones**, haga clic en **modelos**y, en el menú contextual de hello, seleccione **Agregar -> clase**.</span><span class="sxs-lookup"><span data-stu-id="221ee-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="221ee-125">En hello **Agregar nuevo elemento** cuadro de diálogo, clase de nombre hello, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="221ee-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="221ee-126">Hola abierto `CustomerEntity.cs` de archivos y agregue Hola siguiente **con** directiva:</span><span class="sxs-lookup"><span data-stu-id="221ee-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="221ee-127">Modificar clase hello para que, cuando termine, clase de Hola se declara como en el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="221ee-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="221ee-128">clase Hello declara una clase de entidad denominada **CustomerEntity** que usa Hola nombre del cliente como clave de fila de Hola y last name como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="221ee-129">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="221ee-129">Create a table</span></span>

<span data-ttu-id="221ee-130">Hello siguientes pasos muestran cómo toocreate una tabla:</span><span class="sxs-lookup"><span data-stu-id="221ee-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="221ee-131">En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="221ee-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="221ee-132">Abra hello `TablesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="221ee-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="221ee-133">Agregue un método llamado **CreateTable** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="221ee-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="221ee-134">Dentro de hello **CreateTable** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="221ee-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="221ee-135">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="221ee-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="221ee-136">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="221ee-137">Obtener un **CloudTable** objeto que representa un nombre de tabla que desee toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="221ee-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="221ee-138">Hola **CloudTableClient.GetTableReference** método no hace una solicitud en el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="221ee-139">referencia de Hola se devuelve si existe la tabla de Hola o no.</span><span class="sxs-lookup"><span data-stu-id="221ee-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="221ee-140">Llamar a hello **CloudTable.CreateIfNotExists** tabla de hello toocreate del método si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="221ee-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="221ee-141">Hola **CloudTable.CreateIfNotExists** método **true** si la tabla de hello no existe y se haya creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="221ee-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="221ee-142">En caso contrario, se devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="221ee-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="221ee-143">Hola de actualización **ViewBag** por nombre de Hola de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="221ee-144">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="221ee-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="221ee-145">En hello **agregar vista** cuadro de diálogo, escriba **CreateTable** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="221ee-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="221ee-146">Abra `CreateTable.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="221ee-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="221ee-147">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="221ee-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="221ee-148">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="221ee-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="221ee-149">Ejecute la aplicación hello y seleccione **crear una tabla** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="221ee-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Crear tabla](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="221ee-151">Tal y como se mencionó anteriormente, Hola **CloudTable.CreateIfNotExists** método **true** sólo cuando la tabla de hello no existe y se crea.</span><span class="sxs-lookup"><span data-stu-id="221ee-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="221ee-152">Por lo tanto, si ejecuta la aplicación hello cuando Hola tabla existe, método hello devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="221ee-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="221ee-153">aplicación de hello toorun varias veces, debe eliminar tabla Hola antes de ejecutar la aplicación hello nuevo.</span><span class="sxs-lookup"><span data-stu-id="221ee-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="221ee-154">Eliminar tabla de hello puede realizarse a través de hello **CloudTable.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="221ee-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="221ee-155">También puede eliminar tabla de hello mediante hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="221ee-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="221ee-156">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="221ee-156">Add an entity tooa table</span></span>

<span data-ttu-id="221ee-157">*Entidades* asignar tooC\# objetos mediante el uso de una clase personalizada derivan de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="221ee-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="221ee-158">tooadd una tabla de tooa de entidad, cree una clase que define las propiedades de saludo de la entidad.</span><span class="sxs-lookup"><span data-stu-id="221ee-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="221ee-159">En esta sección, podrá ver cómo toodefine una clase de entidad que utiliza Hola nombre del cliente como clave de fila de Hola y last name como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="221ee-160">Juntos, partición de una entidad y la clave de fila identifican entidad de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="221ee-161">Las entidades con la misma clave de partición pueden consultarse más rápidamente que aquellas con diferentes claves de partición, pero el uso de claves de partición diversas permite una mayor escalabilidad de las operaciones paralelas.</span><span class="sxs-lookup"><span data-stu-id="221ee-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="221ee-162">Para cualquier propiedad que se debe almacenar en el servicio de la tabla de hello, propiedad Hola debe ser una propiedad pública de un tipo admitido que expone tanto establecer y recuperar valores.</span><span class="sxs-lookup"><span data-stu-id="221ee-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="221ee-163">clase de entidad de Hola *debe* declarar un constructor sin parámetros público.</span><span class="sxs-lookup"><span data-stu-id="221ee-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="221ee-164">En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="221ee-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="221ee-165">Abra hello `TablesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="221ee-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="221ee-166">Agregar Hola después de la directiva para que Hola código de hello `TablesController.cs` archivo puede tener acceso a hello **CustomerEntity** clase:</span><span class="sxs-lookup"><span data-stu-id="221ee-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="221ee-167">Agregue un método llamado **AddEntity** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="221ee-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="221ee-168">Dentro de hello **AddEntity** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="221ee-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="221ee-169">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="221ee-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="221ee-170">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="221ee-171">Obtener un **CloudTable** objeto que representa un toowhich de tabla de referencia toohello va nueva entidad de tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="221ee-172">Crear instancias e inicializar hello **CustomerEntity** clase.</span><span class="sxs-lookup"><span data-stu-id="221ee-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="221ee-173">Crear un **TableOperation** objeto que inserta la entidad customer ya Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="221ee-174">Ejecutar la operación de inserción de Hola por Hola que realiza la llamada **CloudTable.Execute** método.</span><span class="sxs-lookup"><span data-stu-id="221ee-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="221ee-175">Puede comprobar el resultado de hello de operación de hello inspeccionando hello **TableResult.HttpStatusCode** propiedad.</span><span class="sxs-lookup"><span data-stu-id="221ee-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="221ee-176">Un código de estado de 2xx indica la acción de hello solicitada por el cliente de Hola se procesó correctamente.</span><span class="sxs-lookup"><span data-stu-id="221ee-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="221ee-177">Por ejemplo, correcta las inserciones de nuevas entidades da como resultado un código de estado HTTP 204, lo que significa que se procesó correctamente la operación de Hola y Hola servidor no devolvió ningún contenido.</span><span class="sxs-lookup"><span data-stu-id="221ee-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="221ee-178">Hola de actualización **ViewBag** con nombre de la tabla de Hola y Hola resultados de operación de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="221ee-179">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="221ee-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="221ee-180">En hello **agregar vista** cuadro de diálogo, escriba **AddEntity** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="221ee-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="221ee-181">Abra `AddEntity.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="221ee-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="221ee-182">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="221ee-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="221ee-183">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="221ee-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="221ee-184">Ejecute la aplicación hello y seleccione **Agregar entidad** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="221ee-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Agregar entidad](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="221ee-186">Puede comprobar que se ha agregado la entidad de hello siguiendo los pasos de hello en la sección de hello, [obtener una sola entidad](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="221ee-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="221ee-187">También puede usar hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview todos Hola entidades para las tablas.</span><span class="sxs-lookup"><span data-stu-id="221ee-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="221ee-188">Agregar un lote de la tabla de entidades tooa</span><span class="sxs-lookup"><span data-stu-id="221ee-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="221ee-189">En suma toobeing pueda demasiado[agregar una tabla de tooa de entidad uno a la vez](#add-an-entity-to-a-table), también puede agregar entidades en lote.</span><span class="sxs-lookup"><span data-stu-id="221ee-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="221ee-190">Agregar entidades en lotes reduce el número de Hola de ida y vuelta entre el código y Hola servicio tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="221ee-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="221ee-191">Hola pasos muestra cómo tooadd tooa de varias entidades de la tabla con una operación única instrucción insert:</span><span class="sxs-lookup"><span data-stu-id="221ee-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="221ee-192">En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="221ee-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="221ee-193">Abra hello `TablesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="221ee-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="221ee-194">Agregue un método llamado **AddEntities** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="221ee-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="221ee-195">Dentro de hello **AddEntities** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="221ee-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="221ee-196">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="221ee-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="221ee-197">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="221ee-198">Obtener un **CloudTable** objeto que representa un toowhich de tabla de referencia toohello son nuevas entidades de curso tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="221ee-199">Crear instancias de algunos objetos de cliente en función de hello **CustomerEntity** clase presentada en la sección de hello, modelo [agregar una tabla de tooa de entidad](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="221ee-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="221ee-200">Obtenga un objeto **TableBatchOperation**.</span><span class="sxs-lookup"><span data-stu-id="221ee-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="221ee-201">Agregue el objeto de lote de entidades toohello operación insert.</span><span class="sxs-lookup"><span data-stu-id="221ee-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="221ee-202">Ejecutar operación de inserción de lote de Hola Hola llamada **CloudTable.ExecuteBatch** método.</span><span class="sxs-lookup"><span data-stu-id="221ee-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="221ee-203">Hola **CloudTable.ExecuteBatch** método devuelve una lista de **TableResult** objetos donde cada **TableResult** objeto puede ser examinado toodetermine Hola éxito o error de cada operación individual.</span><span class="sxs-lookup"><span data-stu-id="221ee-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="221ee-204">En este ejemplo, pasar la vista de lista tooa de Hola y deje que vista Hola mostrar resultados de Hola de cada operación.</span><span class="sxs-lookup"><span data-stu-id="221ee-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="221ee-205">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="221ee-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="221ee-206">En hello **agregar vista** cuadro de diálogo, escriba **AddEntities** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="221ee-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="221ee-207">Abra `AddEntities.cshtml`y modifíquelo para que se asemeje como Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="221ee-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="221ee-208">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="221ee-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="221ee-209">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="221ee-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="221ee-210">Ejecute la aplicación hello y seleccione **agregar entidades** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="221ee-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![agregar entidades](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="221ee-212">Puede comprobar que se ha agregado la entidad de hello siguiendo los pasos de hello en la sección de hello, [obtener una sola entidad](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="221ee-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="221ee-213">También puede usar hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview todos Hola entidades para las tablas.</span><span class="sxs-lookup"><span data-stu-id="221ee-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="221ee-214">Obtención de una sola entidad</span><span class="sxs-lookup"><span data-stu-id="221ee-214">Get a single entity</span></span>

<span data-ttu-id="221ee-215">Esta sección muestra cómo tooget una entidad única desde una tabla mediante Hola clave de fila y la clave de partición de la entidad.</span><span class="sxs-lookup"><span data-stu-id="221ee-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="221ee-216">En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment)y utiliza los datos de [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="221ee-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="221ee-217">Abra hello `TablesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="221ee-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="221ee-218">Agregue un método llamado **GetSingle** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="221ee-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="221ee-219">Dentro de hello **GetSingle** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="221ee-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="221ee-220">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="221ee-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="221ee-221">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="221ee-222">Obtener un **CloudTable** objeto que representa una tabla de toohello de referencia desde el que va a recuperar la entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="221ee-223">Cree un objeto de operación de recuperación que tome un objeto de entidad derivado de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="221ee-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="221ee-224">Hola primer parámetro es hello *partitionKey*, y el segundo parámetro de hello es hello *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="221ee-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="221ee-225">Con hello **CustomerEntity** clase y los datos presentados en la sección de hello [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table), Hola después de la tabla de Hola de consultas de fragmento de código para un **CustomerEntity** entidad con un *partitionKey* valor de "Smith" y un *rowKey* valor de "Ben":</span><span class="sxs-lookup"><span data-stu-id="221ee-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="221ee-226">Ejecutar la operación de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="221ee-227">Pasar toohello vista de resultado de hello para su presentación.</span><span class="sxs-lookup"><span data-stu-id="221ee-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="221ee-228">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="221ee-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="221ee-229">En hello **agregar vista** cuadro de diálogo, escriba **GetSingle** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="221ee-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="221ee-230">Abra `GetSingle.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="221ee-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="221ee-231">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="221ee-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="221ee-232">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="221ee-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="221ee-233">Ejecute la aplicación hello y seleccione **obtener único** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="221ee-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![GetSingle](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="221ee-235">Obtención de todas las entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="221ee-235">Get all entities in a partition</span></span>

<span data-ttu-id="221ee-236">Como se mencionó en la sección de hello, [agregar una tabla de tooa de entidad](#add-an-entity-to-a-table), combinación de Hola de una partición y una clave de fila identifican de forma única una entidad en una tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="221ee-237">Puede realizarse una consulta en las entidades con la misma clave de partición de manera más rápida que en aquellas que tienen claves de partición distintas.</span><span class="sxs-lookup"><span data-stu-id="221ee-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="221ee-238">Esta sección se muestra cómo tooquery una tabla para todas las entidades de Hola de una partición especificada.</span><span class="sxs-lookup"><span data-stu-id="221ee-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="221ee-239">En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment)y utiliza los datos de [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="221ee-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="221ee-240">Abra hello `TablesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="221ee-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="221ee-241">Agregue un método llamado **GetPartition** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="221ee-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="221ee-242">Dentro de hello **GetPartition** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="221ee-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="221ee-243">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="221ee-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="221ee-244">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="221ee-245">Obtener un **CloudTable** objeto que representa una tabla de toohello de referencia desde el que va a recuperar entidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="221ee-246">Crear una instancia de un **TableQuery** objeto que especifica la consulta de Hola Hola **donde** cláusula.</span><span class="sxs-lookup"><span data-stu-id="221ee-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="221ee-247">Con hello **CustomerEntity** clase y los datos presentados en la sección de hello [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table), siguiente de hello tabla de Hola de consultas de fragmento de código para una todas las entidades de código donde hello  **PartitionKey** (apellido del cliente) tiene un valor de "Smith":</span><span class="sxs-lookup"><span data-stu-id="221ee-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="221ee-248">Dentro de un bucle, llame a hello **CloudTable.ExecuteQuerySegmented** método pasando el objeto de consulta de Hola crea una instancia en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="221ee-249">Hola **CloudTable.ExecuteQuerySegmented** método devuelve un **TableContinuationToken** objeto, cuando **null** -indica que no hay más entidades tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="221ee-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="221ee-250">En el bucle de hello, usar otro tooiterate de bucle sobre Hola devuelve entidades.</span><span class="sxs-lookup"><span data-stu-id="221ee-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="221ee-251">En el siguiente ejemplo de código de hello, cada entidad devuelta se agrega tooa lista.</span><span class="sxs-lookup"><span data-stu-id="221ee-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="221ee-252">Una vez Hola bucle finaliza, lista de Hola se pasa tooa vista para mostrar:</span><span class="sxs-lookup"><span data-stu-id="221ee-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="221ee-253">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="221ee-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="221ee-254">En hello **agregar vista** cuadro de diálogo, escriba **GetPartition** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="221ee-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="221ee-255">Abra `GetPartition.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="221ee-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="221ee-256">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="221ee-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="221ee-257">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="221ee-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="221ee-258">Ejecute la aplicación hello y seleccione **obtener partición** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="221ee-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![GetPartition](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="221ee-260">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="221ee-260">Delete an entity</span></span>

<span data-ttu-id="221ee-261">Esta sección se muestra cómo toodelete una entidad de una tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="221ee-262">En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment)y utiliza los datos de [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="221ee-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="221ee-263">Abra hello `TablesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="221ee-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="221ee-264">Agregue un método llamado **DeleteEntity** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="221ee-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="221ee-265">Dentro de hello **DeleteEntity** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="221ee-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="221ee-266">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="221ee-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="221ee-267">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="221ee-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="221ee-268">Obtener un **CloudTable** objeto que representa una tabla de toohello de referencia desde el que va a eliminar entidad Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="221ee-269">Cree un objeto de operación de eliminación que tome un objeto de entidad derivado de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="221ee-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="221ee-270">En este caso, usamos hello **CustomerEntity** clase y los datos presentados en la sección de hello [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="221ee-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="221ee-271">Hola la entidad **ETag** debe establecerse el valor válido de tooa.</span><span class="sxs-lookup"><span data-stu-id="221ee-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="221ee-272">Ejecutar la operación de eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="221ee-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="221ee-273">Pasar toohello vista de resultado de hello para su presentación.</span><span class="sxs-lookup"><span data-stu-id="221ee-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="221ee-274">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="221ee-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="221ee-275">En hello **agregar vista** cuadro de diálogo, escriba **DeleteEntity** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="221ee-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="221ee-276">Abra `DeleteEntity.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="221ee-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="221ee-277">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="221ee-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="221ee-278">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="221ee-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="221ee-279">Ejecute la aplicación hello y seleccione **eliminar entidad** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="221ee-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![GetSingle](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="221ee-281">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="221ee-281">Next steps</span></span>
<span data-ttu-id="221ee-282">Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="221ee-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="221ee-283">Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="221ee-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="221ee-284">Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="221ee-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)

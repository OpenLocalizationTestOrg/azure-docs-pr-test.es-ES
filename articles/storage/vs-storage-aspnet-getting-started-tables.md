---
title: "Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET) | Microsoft Docs"
description: "Introducción al uso de Azure Table Storage en un proyecto ASP.NET en Visual Studio después de conectarse a una cuenta de almacenamiento mediante Servicios conectados de Visual Studio"
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
ms.openlocfilehash: d9cb32483d3f582bbeb0ccc6a204a8b6d9ea5c96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="e3acb-103">Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e3acb-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="e3acb-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e3acb-104">Overview</span></span>

<span data-ttu-id="e3acb-105">El almacenamiento de tabla de Azure permite almacenar una gran cantidad de datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="e3acb-105">Azure Table storage enables you to store large amounts of structured data.</span></span> <span data-ttu-id="e3acb-106">El servicio es un almacén de datos NoSQL que acepta llamadas autenticadas desde dentro y fuera de la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3acb-106">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="e3acb-107">Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.</span><span class="sxs-lookup"><span data-stu-id="e3acb-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="e3acb-108">Este tutorial muestra cómo escribir código ASP.NET para algunos escenarios comunes mediante entidades de Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="e3acb-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="e3acb-109">Entre los escenarios descritos se incluyen crear, consultar y eliminar entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="e3acb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e3acb-110">Prerequisites</span></span>

* [<span data-ttu-id="e3acb-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e3acb-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="e3acb-112">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e3acb-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="e3acb-113">Creación de un controlador MVC</span><span class="sxs-lookup"><span data-stu-id="e3acb-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="e3acb-114">En el **Explorador de soluciones**, haga clic con el botón derecho en **Controladores** y, en el menú contextual, seleccione **Agregar > Controlador**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Incorporación de un controlador a una aplicación de ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="e3acb-116">En el cuadro de diálogo **Agregar scaffold**, seleccione **Controlador MVC 5 - Vacío** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especifique el tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="e3acb-118">En el cuadro de diálogo **Agregar controlador**, denomine *TablesController* al controlador y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-118">On the **Add Controller** dialog, name the controller *TablesController*, and select **Add**.</span></span>

    ![Asignación de nombre al controladorMVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="e3acb-120">Agregue las siguientes directivas *using* al archivo `TablesController.cs`:</span><span class="sxs-lookup"><span data-stu-id="e3acb-120">Add the following *using* directives to the `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="e3acb-121">Creación de una clase de modelo</span><span class="sxs-lookup"><span data-stu-id="e3acb-121">Create a model class</span></span>

<span data-ttu-id="e3acb-122">Muchos de los ejemplos de este artículo utilizan una clase derivada de **TableEntity** llamada **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-122">Many of the examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="e3acb-123">Los pasos siguientes lo guiarán por el proceso de declarar esta clase como una clase de modelo:</span><span class="sxs-lookup"><span data-stu-id="e3acb-123">The following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="e3acb-124">En el **Explorador de soluciones**, haga clic con el botón derecho en **Modelos** y, en el menú contextual, seleccione **Agregar > Clase**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-124">In the **Solution Explorer**, right-click **Models**, and, from the context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="e3acb-125">En el cuadro de diálogo **Agregar nuevo elemento**, denomine la clase **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-125">On the **Add New Item** dialog, name the class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="e3acb-126">Abra el archivo `CustomerEntity.cs` y agregue el siguiente la directiva **using**:</span><span class="sxs-lookup"><span data-stu-id="e3acb-126">Open the `CustomerEntity.cs` file, and add the following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="e3acb-127">Modifique la clase para que, cuando termine, se declare como en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="e3acb-127">Modify the class so that, when finished, the class is declared as in the following code.</span></span> <span data-ttu-id="e3acb-128">La clase declara una clase de entidad llamada **CustomerEntity** que usa el nombre del cliente como clave de fila y el apellido como clave de partición.</span><span class="sxs-lookup"><span data-stu-id="e3acb-128">The class declares an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

## <a name="create-a-table"></a><span data-ttu-id="e3acb-129">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="e3acb-129">Create a table</span></span>

<span data-ttu-id="e3acb-130">Los siguientes pasos muestran cómo crear una tabla:</span><span class="sxs-lookup"><span data-stu-id="e3acb-130">The following steps illustrate how to create a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="e3acb-131">En esta sección se da por supuesto que ha completado los pasos [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="e3acb-131">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="e3acb-132">Abra el archivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="e3acb-132">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="e3acb-133">Agregue un método llamado **CreateTable** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="e3acb-134">Dentro del método **CreateTable**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e3acb-134">Within the **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e3acb-135">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso).</span><span class="sxs-lookup"><span data-stu-id="e3acb-135">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="e3acb-136">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="e3acb-137">Obtenga un objeto **CloudTable** que representa una referencia al nombre de tabla que desea.</span><span class="sxs-lookup"><span data-stu-id="e3acb-137">Get a **CloudTable** object that represents a reference to the desired table name.</span></span> <span data-ttu-id="e3acb-138">El método **CloudTableClient.GetTableReference** no hace ninguna solicitud en Table Storage.</span><span class="sxs-lookup"><span data-stu-id="e3acb-138">The **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="e3acb-139">Se devuelve la referencia tanto si la tabla existe como si no.</span><span class="sxs-lookup"><span data-stu-id="e3acb-139">The reference is returned whether or not the table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="e3acb-140">Llame a la **CloudTable.CreateIfNotExists** método para crear la tabla si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="e3acb-140">Call the **CloudTable.CreateIfNotExists** method to create the table if it does not yet exist.</span></span> <span data-ttu-id="e3acb-141">El método **CloudTable.CreateIfNotExists** devuelve **True** si la tabla no existe y se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="e3acb-141">The **CloudTable.CreateIfNotExists** method returns **true** if the table does not exist, and is successfully created.</span></span> <span data-ttu-id="e3acb-142">En caso contrario, se devuelve **False**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="e3acb-143">Actualice **ViewBag** con el nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-143">Update the **ViewBag** with the name of the table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="e3acb-144">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Tables** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-144">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="e3acb-145">En el cuadro de diálogo **Agregar vista**, escriba **CreateTable** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-145">On the **Add View** dialog, enter **CreateTable** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="e3acb-146">Abra `CreateTable.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="e3acb-146">Open `CreateTable.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="e3acb-147">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="e3acb-147">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="e3acb-148">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="e3acb-148">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="e3acb-149">Ejecute la aplicación y seleccione **Crear tabla** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="e3acb-149">Run the application, and select **Create table** to see results similar to the following screen shot:</span></span>
  
    ![Crear tabla](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="e3acb-151">Como se dijo anteriormente, el método **CloudTable.CreateIfNotExists** devuelve **true** solo si la tabla no existía, pero se creó.</span><span class="sxs-lookup"><span data-stu-id="e3acb-151">As mentioned previously, the **CloudTable.CreateIfNotExists** method returns **true** only when the table doesn't exist and is created.</span></span> <span data-ttu-id="e3acb-152">Por lo tanto, si se ejecuta la aplicación cuando la tabla existe, el método devuelve **False**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-152">Therefore, if you run the app when the table exists, the method returns **false**.</span></span> <span data-ttu-id="e3acb-153">Para ejecutar la aplicación varias veces, debe eliminar la tabla antes de ejecutar la aplicación de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e3acb-153">To run the app multiple times, you must delete the table before running the app again.</span></span> <span data-ttu-id="e3acb-154">La eliminación de la tabla puede realizarse a través del método **CloudTable.Delete**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-154">Deleting the table can be done via the **CloudTable.Delete** method.</span></span> <span data-ttu-id="e3acb-155">También puede eliminar la tabla mediante [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) o [el Explorador de Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="e3acb-155">You can also delete the table using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="e3acb-156">Adición de una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="e3acb-156">Add an entity to a table</span></span>

<span data-ttu-id="e3acb-157">Las *entidades* se asignan a objetos C\# utilizando una clase personalizada derivada de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-157">*Entities* map to C\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="e3acb-158">Para agregar una entidad a una tabla, cree una clase que defina las propiedades de la entidad.</span><span class="sxs-lookup"><span data-stu-id="e3acb-158">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="e3acb-159">En esta sección, descubrirá cómo definir una clase de entidad que utiliza el nombre de pila del cliente como clave de fila y el apellido como clave de partición.</span><span class="sxs-lookup"><span data-stu-id="e3acb-159">In this section, you'll see how to define an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="e3acb-160">En conjunto, la clave de partición y la clave de fila de una entidad la identifican inequívocamente en la tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-160">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="e3acb-161">Las entidades con la misma clave de partición pueden consultarse más rápidamente que aquellas con diferentes claves de partición, pero el uso de claves de partición diversas permite una mayor escalabilidad de las operaciones paralelas.</span><span class="sxs-lookup"><span data-stu-id="e3acb-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="e3acb-162">Toda propiedad que deba almacenarse en Table service debe ser una propiedad pública de un tipo compatible que exponga tanto el establecimiento como la recuperación de valores.</span><span class="sxs-lookup"><span data-stu-id="e3acb-162">For any property that should be stored in the table service, the property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="e3acb-163">La clase de entidad *must* declara un constructor sin parámetros público.</span><span class="sxs-lookup"><span data-stu-id="e3acb-163">The entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="e3acb-164">En esta sección se da por supuesto que ha completado los pasos [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="e3acb-164">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="e3acb-165">Abra el archivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="e3acb-165">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="e3acb-166">Agregue la siguiente directiva para que el código del archivo `TablesController.cs` pueda tener acceso a la clase **CustomerEntity**:</span><span class="sxs-lookup"><span data-stu-id="e3acb-166">Add the following directive so that the code in the `TablesController.cs` file can access the **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="e3acb-167">Agregue un método llamado **AddEntity** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="e3acb-168">Dentro del método **AddEntity**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e3acb-168">Within the **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e3acb-169">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso).</span><span class="sxs-lookup"><span data-stu-id="e3acb-169">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="e3acb-170">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="e3acb-171">Obtenga un objeto **CloudTable** que represente una referencia a la tabla a la que va a agregar la nueva entidad.</span><span class="sxs-lookup"><span data-stu-id="e3acb-171">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="e3acb-172">Cree instancias e inicialice la clase **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-172">Instantiate and initialize the **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="e3acb-173">Cree el objeto **TableOperation** que inserta la entidad del cliente.</span><span class="sxs-lookup"><span data-stu-id="e3acb-173">Create a **TableOperation** object that inserts the customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="e3acb-174">Ejecute la operación de inserción mediante una llamada al método **CloudTable.Execute**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-174">Execute the insert operation by calling the **CloudTable.Execute** method.</span></span> <span data-ttu-id="e3acb-175">Puede comprobar el resultado de la operación inspeccionando la propiedad **TableResult.HttpStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-175">You can verify the result of the operation by inspecting the **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="e3acb-176">Un código de estado de 2xx indica que la acción solicitada por el cliente se procesó correctamente.</span><span class="sxs-lookup"><span data-stu-id="e3acb-176">A status code of 2xx indicates the action requested by the client was processed successfully.</span></span> <span data-ttu-id="e3acb-177">Por ejemplo, las inserciones correctas de las nuevas entidades dan lugar a un código de estado HTTP de 204, lo que significa que la operación se procesó correctamente y el servidor no devolvió ningún contenido.</span><span class="sxs-lookup"><span data-stu-id="e3acb-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that the operation was successfully processed and the server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="e3acb-178">Actualice **ViewBag** con el nombre de tabla y los resultados de la operación de inserción.</span><span class="sxs-lookup"><span data-stu-id="e3acb-178">Update the **ViewBag** with the table name, and the results of the insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="e3acb-179">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Tables** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-179">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="e3acb-180">En el cuadro de diálogo **Agregar vista**, escriba **AddEntity** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-180">On the **Add View** dialog, enter **AddEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="e3acb-181">Abra `AddEntity.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="e3acb-181">Open `AddEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="e3acb-182">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="e3acb-182">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="e3acb-183">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="e3acb-183">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="e3acb-184">Ejecute la aplicación y seleccione **Agregar entidad** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="e3acb-184">Run the application, and select **Add entity** to see results similar to the following screen shot:</span></span>
  
    ![Agregar entidad](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="e3acb-186">Puede comprobar que se ha agregado la entidad siguiendo los pasos descritos en la sección [Obtención de una sola entidad](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="e3acb-186">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="e3acb-187">También puede usar [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) para ver todas las entidades de las tablas.</span><span class="sxs-lookup"><span data-stu-id="e3acb-187">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-to-a-table"></a><span data-ttu-id="e3acb-188">Incorporación de un lote de entidades a una tabla</span><span class="sxs-lookup"><span data-stu-id="e3acb-188">Add a batch of entities to a table</span></span>

<span data-ttu-id="e3acb-189">Además de poder [agregar una entidad a una tabla de una en una](#add-an-entity-to-a-table), también puede agregar entidades por lotes.</span><span class="sxs-lookup"><span data-stu-id="e3acb-189">In addition to being able to [add an entity to a table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="e3acb-190">Esto reduce de forma masiva el número de idas y vueltas entre el código y Azure Table service.</span><span class="sxs-lookup"><span data-stu-id="e3acb-190">Adding entities in batch reduces the number of round-trips between your code and the Azure table service.</span></span> <span data-ttu-id="e3acb-191">Los siguientes pasos muestran cómo agregar varias entidades a una tabla con una sola operación de inserción:</span><span class="sxs-lookup"><span data-stu-id="e3acb-191">The following steps illustrate how to add multiple entities to a table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="e3acb-192">En esta sección se da por supuesto que ha completado los pasos [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="e3acb-192">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="e3acb-193">Abra el archivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="e3acb-193">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="e3acb-194">Agregue un método llamado **AddEntities** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="e3acb-195">Dentro del método **AddEntities**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e3acb-195">Within the **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e3acb-196">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso).</span><span class="sxs-lookup"><span data-stu-id="e3acb-196">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="e3acb-197">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="e3acb-198">Obtenga un objeto **CloudTable** que represente una referencia a la tabla a la que va a agregar las nuevas entidades.</span><span class="sxs-lookup"><span data-stu-id="e3acb-198">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="e3acb-199">Cree instancias de algunos objetos de cliente basados en la clase de modelo **CustomerEntity** de la sección [Adición de una entidad a una tabla](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="e3acb-199">Instantiate some customer objects based on the **CustomerEntity** model class presented in the section, [Add an entity to a table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="e3acb-200">Obtenga un objeto **TableBatchOperation**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="e3acb-201">Agregue entidades al objeto de operación de inserción de por lotes.</span><span class="sxs-lookup"><span data-stu-id="e3acb-201">Add entities to the batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="e3acb-202">Ejecute la operación de inserción por lotes mediante una llamada al método **CloudTable.ExecuteBatch**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-202">Execute the batch insert operation by calling the **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="e3acb-203">El método **CloudTable.ExecuteBatch** devuelve una lista de objetos **TableResult** donde cada **TableResult** se puede examinar para determinar el éxito o el fracaso de cada operación individual.</span><span class="sxs-lookup"><span data-stu-id="e3acb-203">The **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined to determine the success or failure of each individual operation.</span></span> <span data-ttu-id="e3acb-204">En este ejemplo, pase la lista a una vista y permita que se muestren los resultados de cada operación.</span><span class="sxs-lookup"><span data-stu-id="e3acb-204">For this example, pass the list to a view and let the view display the results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="e3acb-205">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Tables** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="e3acb-206">En el cuadro de diálogo **Agregar vista**, escriba **AddEntities** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-206">On the **Add View** dialog, enter **AddEntities** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="e3acb-207">Abra `AddEntities.cshtml` y modifíquelo de modo que se parezca a lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e3acb-207">Open `AddEntities.cshtml`, and modify it so that it looks like the following.</span></span>

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

1. <span data-ttu-id="e3acb-208">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="e3acb-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="e3acb-209">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="e3acb-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="e3acb-210">Ejecute la aplicación y seleccione **Agregar entidades** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="e3acb-210">Run the application, and select **Add entities** to see results similar to the following screen shot:</span></span>
  
    ![agregar entidades](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="e3acb-212">Puede comprobar que se ha agregado la entidad siguiendo los pasos descritos en la sección [Obtención de una sola entidad](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="e3acb-212">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="e3acb-213">También puede usar [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) para ver todas las entidades de las tablas.</span><span class="sxs-lookup"><span data-stu-id="e3acb-213">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="e3acb-214">Obtención de una sola entidad</span><span class="sxs-lookup"><span data-stu-id="e3acb-214">Get a single entity</span></span>

<span data-ttu-id="e3acb-215">En esta sección se muestra cómo obtener una sola entidad de una tabla mediante la clave de fila y la clave de partición de la entidad.</span><span class="sxs-lookup"><span data-stu-id="e3acb-215">This section illustrates how to get a single entity from a table using the entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="e3acb-216">En esta sección se da por supuesto que ha completado los pasos descritos en [Configuración del entorno de desarrollo](#set-up-the-development-environment) y utiliza los datos de [Incorporación de un lote de entidades a una tabla](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="e3acb-216">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="e3acb-217">Abra el archivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="e3acb-217">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="e3acb-218">Agregue un método llamado **GetSingle** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="e3acb-219">Dentro del método **GetSingle**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e3acb-219">Within the **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e3acb-220">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso).</span><span class="sxs-lookup"><span data-stu-id="e3acb-220">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="e3acb-221">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="e3acb-222">Obtenga un objeto **CloudTable** que represente una referencia a la tabla de la que va a recuperar la entidad.</span><span class="sxs-lookup"><span data-stu-id="e3acb-222">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="e3acb-223">Cree un objeto de operación de recuperación que tome un objeto de entidad derivado de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="e3acb-224">El primer parámetro es *partitionKey* y el segundo parámetro es *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="e3acb-224">The first parameter is the *partitionKey*, and the second parameter is the *rowKey*.</span></span> <span data-ttu-id="e3acb-225">Mediante la clase **CustomerEntity** y los datos presentados en la sección [Incorporación de un lote de entidades a una tabla](#add-a-batch-of-entities-to-a-table), el fragmento de código siguiente consulta la tabla para una entidad **CustomerEntity** con un valor *partitionKey* de "Smith" y un valor *rowKey* de "Ben":</span><span class="sxs-lookup"><span data-stu-id="e3acb-225">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="e3acb-226">Ejecute la operación de recuperación.</span><span class="sxs-lookup"><span data-stu-id="e3acb-226">Execute the retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="e3acb-227">Pase el resultado a la vista para que se muestre.</span><span class="sxs-lookup"><span data-stu-id="e3acb-227">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="e3acb-228">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Tables** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-228">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="e3acb-229">En el cuadro de diálogo **Agregar vista**, escriba **GetSingle** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-229">On the **Add View** dialog, enter **GetSingle** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="e3acb-230">Abra `GetSingle.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="e3acb-230">Open `GetSingle.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="e3acb-231">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="e3acb-231">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="e3acb-232">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="e3acb-232">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="e3acb-233">Ejecute la aplicación y seleccione **GetSingle** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="e3acb-233">Run the application, and select **Get Single** to see results similar to the following screen shot:</span></span>
  
    ![GetSingle](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="e3acb-235">Obtención de todas las entidades de una partición</span><span class="sxs-lookup"><span data-stu-id="e3acb-235">Get all entities in a partition</span></span>

<span data-ttu-id="e3acb-236">Como se mencionó en la sección [Adición de una entidad a una tabla](#add-an-entity-to-a-table), la combinación de una partición y una clave de fila identifican de forma única una entidad de una tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-236">As mentioned in the section, [Add an entity to a table](#add-an-entity-to-a-table), the combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="e3acb-237">Puede realizarse una consulta en las entidades con la misma clave de partición de manera más rápida que en aquellas que tienen claves de partición distintas.</span><span class="sxs-lookup"><span data-stu-id="e3acb-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="e3acb-238">Esta sección muestra cómo consultar una tabla en todas las entidades de una partición especificada.</span><span class="sxs-lookup"><span data-stu-id="e3acb-238">This section illustrates how to query a table for all the entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="e3acb-239">En esta sección se da por supuesto que ha completado los pasos descritos en [Configuración del entorno de desarrollo](#set-up-the-development-environment) y utiliza los datos de [Incorporación de un lote de entidades a una tabla](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="e3acb-239">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="e3acb-240">Abra el archivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="e3acb-240">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="e3acb-241">Agregue un método llamado **GetPartition** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="e3acb-242">Dentro del método **GetPartition**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e3acb-242">Within the **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e3acb-243">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso).</span><span class="sxs-lookup"><span data-stu-id="e3acb-243">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="e3acb-244">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="e3acb-245">Obtenga un objeto **CloudTable** que represente una referencia a la tabla de la que va a recuperar las entidades.</span><span class="sxs-lookup"><span data-stu-id="e3acb-245">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="e3acb-246">Cree una instancia de un objeto **TableQuery** especificando la consulta en la cláusula **Where**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-246">Instantiate a **TableQuery** object specifying the query in the **Where** clause.</span></span> <span data-ttu-id="e3acb-247">Mediante la clase **CustomerEntity** y los datos presentados en la sección [Incorporación de un lote de entidades a una tabla](#add-a-batch-of-entities-to-a-table), el fragmento de código siguiente consulta la tabla para todas las entidades donde **PartitionKey** (apellidos del cliente) tiene un valor de "Smith":</span><span class="sxs-lookup"><span data-stu-id="e3acb-247">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a all entities where the **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="e3acb-248">Dentro de un bucle, llame al método **CloudTable.ExecuteQuerySegmented** pasando el objeto de consulta del que creó una instancia en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="e3acb-248">Within a loop, call the **CloudTable.ExecuteQuerySegmented** method passing the query object you instantiated in the previous step.</span></span>  <span data-ttu-id="e3acb-249">El método **CloudTable.ExecuteQuerySegmented** devuelve un objeto **TableContinuationToken** que, cuando es **null**, indica que no hay más entidades para recuperar.</span><span class="sxs-lookup"><span data-stu-id="e3acb-249">The **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities to retrieve.</span></span> <span data-ttu-id="e3acb-250">Dentro del bucle, use otro bucle para iterar las entidades devueltas.</span><span class="sxs-lookup"><span data-stu-id="e3acb-250">Within the loop, use another loop to iterate over the returned entities.</span></span> <span data-ttu-id="e3acb-251">En el ejemplo de código siguiente, cada entidad devuelta se agrega a una lista.</span><span class="sxs-lookup"><span data-stu-id="e3acb-251">In the following code example, each returned entity is added to a list.</span></span> <span data-ttu-id="e3acb-252">Una vez que finaliza el bucle, la lista se pasa a una vista para mostrar los resultados:</span><span class="sxs-lookup"><span data-stu-id="e3acb-252">Once the loop ends, the list is passed to a view for display:</span></span> 

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

1. <span data-ttu-id="e3acb-253">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Tables** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-253">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="e3acb-254">En el cuadro de diálogo **Agregar vista**, escriba **GetPartition** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-254">On the **Add View** dialog, enter **GetPartition** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="e3acb-255">Abra `GetPartition.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="e3acb-255">Open `GetPartition.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="e3acb-256">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="e3acb-256">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="e3acb-257">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="e3acb-257">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="e3acb-258">Ejecute la aplicación y seleccione **GetPartition** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="e3acb-258">Run the application, and select **Get Partition** to see results similar to the following screen shot:</span></span>
  
    ![GetPartition](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="e3acb-260">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="e3acb-260">Delete an entity</span></span>

<span data-ttu-id="e3acb-261">Esta sección muestra cómo eliminar una entidad de una tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-261">This section illustrates how to delete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="e3acb-262">En esta sección se da por supuesto que ha completado los pasos descritos en [Configuración del entorno de desarrollo](#set-up-the-development-environment) y utiliza los datos de [Incorporación de un lote de entidades a una tabla](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="e3acb-262">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="e3acb-263">Abra el archivo `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="e3acb-263">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="e3acb-264">Agregue un método llamado **DeleteEntity** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="e3acb-265">Dentro del método **DeleteEntity**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e3acb-265">Within the **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e3acb-266">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso).</span><span class="sxs-lookup"><span data-stu-id="e3acb-266">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="e3acb-267">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.</span><span class="sxs-lookup"><span data-stu-id="e3acb-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="e3acb-268">Obtenga un objeto **CloudTable** que represente una referencia a la tabla de la que va a eliminar la entidad.</span><span class="sxs-lookup"><span data-stu-id="e3acb-268">Get a **CloudTable** object that represents a reference to the table from which you are deleting the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="e3acb-269">Cree un objeto de operación de eliminación que tome un objeto de entidad derivado de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="e3acb-270">En este caso, usamos la clase **CustomerEntity** y a los datos presentados en la sección [Incorporación de un lote de entidades a una tabla](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="e3acb-270">In this case, we use the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="e3acb-271">La **ETag** de la entidad debe establecerse en un valor válido.</span><span class="sxs-lookup"><span data-stu-id="e3acb-271">The entity's **ETag** must be set to a valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="e3acb-272">Ejecute la operación de eliminación.</span><span class="sxs-lookup"><span data-stu-id="e3acb-272">Execute the delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="e3acb-273">Pase el resultado a la vista para que se muestre.</span><span class="sxs-lookup"><span data-stu-id="e3acb-273">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="e3acb-274">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Tables** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-274">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="e3acb-275">En el cuadro de diálogo **Agregar vista**, escriba **DeleteEntity** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3acb-275">On the **Add View** dialog, enter **DeleteEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="e3acb-276">Abra `DeleteEntity.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="e3acb-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="e3acb-277">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="e3acb-277">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="e3acb-278">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="e3acb-278">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="e3acb-279">Ejecute la aplicación y seleccione **Eliminar entidad** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="e3acb-279">Run the application, and select **Delete entity** to see results similar to the following screen shot:</span></span>
  
    ![GetSingle](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="e3acb-281">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e3acb-281">Next steps</span></span>
<span data-ttu-id="e3acb-282">Consulte más guías de características para obtener información acerca de otras opciones del almacenamiento de datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="e3acb-282">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="e3acb-283">Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e3acb-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="e3acb-284">Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e3acb-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)

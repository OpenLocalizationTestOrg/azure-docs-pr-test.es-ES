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
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Información general

El almacenamiento de tabla permite toostore grandes cantidades de datos estructurados. servicio de Hello es un almacén de datos NoSQL que acepta llamadas autenticadas de dentro y fuera Hola nube de Azure. Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.

Este tutorial muestra cómo código toowrite ASP.NET en algunos escenarios comunes con las entidades de almacenamiento de tabla de Azure. Entre los escenarios descritos se incluyen crear, consultar y eliminar entidades de tabla. 

##<a name="prerequisites"></a>Requisitos previos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Cuenta de Azure Storage](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Creación de un controlador MVC 

1. Hola **el Explorador de soluciones**, haga clic en **controladores**y, en el menú contextual de hello, seleccione **Agregar -> controlador**.

    ![Agregar una aplicación de ASP.NET MVC tooan de controlador](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. En hello **agregar scaffolding** cuadro de diálogo, seleccione **controlador de MVC 5 - vacío**y seleccione **agregar**.

    ![Especifique el tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. En hello **Agregar controlador** cuadro de diálogo, nombre del controlador que hello *TablesController*y seleccione **agregar**.

    ![Controlador de MVC Hola de nombre](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Agregue los siguiente hello *con* toohello directivas `TablesController.cs` archivo:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Creación de una clase de modelo

Muchos de los ejemplos de hello en este artículo utilizan un **TableEntity**-deriva la clase llamada **CustomerEntity**. Hola pasos guiarle por declarar esta clase como una clase de modelo:

1. Hola **el Explorador de soluciones**, haga clic en **modelos**y, en el menú contextual de hello, seleccione **Agregar -> clase**.

1. En hello **Agregar nuevo elemento** cuadro de diálogo, clase de nombre hello, **CustomerEntity**.

1. Hola abierto `CustomerEntity.cs` de archivos y agregue Hola siguiente **con** directiva:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Modificar clase hello para que, cuando termine, clase de Hola se declara como en el siguiente código de hello. clase Hello declara una clase de entidad denominada **CustomerEntity** que usa Hola nombre del cliente como clave de fila de Hola y last name como clave de partición de Hola.

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

## <a name="create-a-table"></a>Creación de una tabla

Hello siguientes pasos muestran cómo toocreate una tabla:

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `TablesController.cs` archivo.

1. Agregue un método llamado **CreateTable** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de hello **CreateTable** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtener un **CloudTable** objeto que representa un nombre de tabla que desee toohello de referencia. Hola **CloudTableClient.GetTableReference** método no hace una solicitud en el almacenamiento de tabla. referencia de Hola se devuelve si existe la tabla de Hola o no. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Llamar a hello **CloudTable.CreateIfNotExists** tabla de hello toocreate del método si aún no existe. Hola **CloudTable.CreateIfNotExists** método **true** si la tabla de hello no existe y se haya creado correctamente. En caso contrario, se devuelve **false**.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Hola de actualización **ViewBag** por nombre de Hola de tabla de Hola.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **CreateTable** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `CreateTable.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Ejecute la aplicación hello y seleccione **crear una tabla** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Crear tabla](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Tal y como se mencionó anteriormente, Hola **CloudTable.CreateIfNotExists** método **true** sólo cuando la tabla de hello no existe y se crea. Por lo tanto, si ejecuta la aplicación hello cuando Hola tabla existe, método hello devuelve **false**. aplicación de hello toorun varias veces, debe eliminar tabla Hola antes de ejecutar la aplicación hello nuevo. Eliminar tabla de hello puede realizarse a través de hello **CloudTable.Delete** método. También puede eliminar tabla de hello mediante hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad

*Entidades* asignar tooC\# objetos mediante el uso de una clase personalizada derivan de **TableEntity**. tooadd una tabla de tooa de entidad, cree una clase que define las propiedades de saludo de la entidad. En esta sección, podrá ver cómo toodefine una clase de entidad que utiliza Hola nombre del cliente como clave de fila de Hola y last name como clave de partición de Hola. Juntos, partición de una entidad y la clave de fila identifican entidad de hello en la tabla de Hola. Las entidades con la misma clave de partición pueden consultarse más rápidamente que aquellas con diferentes claves de partición, pero el uso de claves de partición diversas permite una mayor escalabilidad de las operaciones paralelas. Para cualquier propiedad que se debe almacenar en el servicio de la tabla de hello, propiedad Hola debe ser una propiedad pública de un tipo admitido que expone tanto establecer y recuperar valores.
clase de entidad de Hola *debe* declarar un constructor sin parámetros público.

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).

1. Abra hello `TablesController.cs` archivo.

1. Agregar Hola después de la directiva para que Hola código de hello `TablesController.cs` archivo puede tener acceso a hello **CustomerEntity** clase:

    ```csharp
    using StorageAspnet.Models;
    ```

1. Agregue un método llamado **AddEntity** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de hello **AddEntity** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtener un **CloudTable** objeto que representa un toowhich de tabla de referencia toohello va nueva entidad de tooadd Hola. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Crear instancias e inicializar hello **CustomerEntity** clase.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Crear un **TableOperation** objeto que inserta la entidad customer ya Hola.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Ejecutar la operación de inserción de Hola por Hola que realiza la llamada **CloudTable.Execute** método. Puede comprobar el resultado de hello de operación de hello inspeccionando hello **TableResult.HttpStatusCode** propiedad. Un código de estado de 2xx indica la acción de hello solicitada por el cliente de Hola se procesó correctamente. Por ejemplo, correcta las inserciones de nuevas entidades da como resultado un código de estado HTTP 204, lo que significa que se procesó correctamente la operación de Hola y Hola servidor no devolvió ningún contenido.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Hola de actualización **ViewBag** con nombre de la tabla de Hola y Hola resultados de operación de inserción de Hola.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **AddEntity** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `AddEntity.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Ejecute la aplicación hello y seleccione **Agregar entidad** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Agregar entidad](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    Puede comprobar que se ha agregado la entidad de hello siguiendo los pasos de hello en la sección de hello, [obtener una sola entidad](#get-a-single-entity). También puede usar hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview todos Hola entidades para las tablas.

## <a name="add-a-batch-of-entities-tooa-table"></a>Agregar un lote de la tabla de entidades tooa

En suma toobeing pueda demasiado[agregar una tabla de tooa de entidad uno a la vez](#add-an-entity-to-a-table), también puede agregar entidades en lote. Agregar entidades en lotes reduce el número de Hola de ida y vuelta entre el código y Hola servicio tabla de Azure. Hola pasos muestra cómo tooadd tooa de varias entidades de la tabla con una operación única instrucción insert:

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).

1. Abra hello `TablesController.cs` archivo.

1. Agregue un método llamado **AddEntities** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de hello **AddEntities** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtener un **CloudTable** objeto que representa un toowhich de tabla de referencia toohello son nuevas entidades de curso tooadd Hola. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Crear instancias de algunos objetos de cliente en función de hello **CustomerEntity** clase presentada en la sección de hello, modelo [agregar una tabla de tooa de entidad](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Obtenga un objeto **TableBatchOperation**.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Agregue el objeto de lote de entidades toohello operación insert.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Ejecutar operación de inserción de lote de Hola Hola llamada **CloudTable.ExecuteBatch** método.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Hola **CloudTable.ExecuteBatch** método devuelve una lista de **TableResult** objetos donde cada **TableResult** objeto puede ser examinado toodetermine Hola éxito o error de cada operación individual. En este ejemplo, pasar la vista de lista tooa de Hola y deje que vista Hola mostrar resultados de Hola de cada operación. 
 
    ```csharp
    return View(results);
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **AddEntities** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `AddEntities.cshtml`y modifíquelo para que se asemeje como Hola siguiente.

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

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Ejecute la aplicación hello y seleccione **agregar entidades** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![agregar entidades](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    Puede comprobar que se ha agregado la entidad de hello siguiendo los pasos de hello en la sección de hello, [obtener una sola entidad](#get-a-single-entity). También puede usar hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview todos Hola entidades para las tablas.

## <a name="get-a-single-entity"></a>Obtención de una sola entidad

Esta sección muestra cómo tooget una entidad única desde una tabla mediante Hola clave de fila y la clave de partición de la entidad. 

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment)y utiliza los datos de [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table). 

1. Abra hello `TablesController.cs` archivo.

1. Agregue un método llamado **GetSingle** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de hello **GetSingle** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtener un **CloudTable** objeto que representa una tabla de toohello de referencia desde el que va a recuperar la entidad de Hola. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Cree un objeto de operación de recuperación que tome un objeto de entidad derivado de **TableEntity**. Hola primer parámetro es hello *partitionKey*, y el segundo parámetro de hello es hello *rowKey*. Con hello **CustomerEntity** clase y los datos presentados en la sección de hello [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table), Hola después de la tabla de Hola de consultas de fragmento de código para un **CustomerEntity** entidad con un *partitionKey* valor de "Smith" y un *rowKey* valor de "Ben":

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Ejecutar la operación de recuperación de Hola.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Pasar toohello vista de resultado de hello para su presentación.

    ```csharp
    return View(result);
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **GetSingle** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `GetSingle.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

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

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Ejecute la aplicación hello y seleccione **obtener único** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![GetSingle](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Obtención de todas las entidades de una partición

Como se mencionó en la sección de hello, [agregar una tabla de tooa de entidad](#add-an-entity-to-a-table), combinación de Hola de una partición y una clave de fila identifican de forma única una entidad en una tabla. Puede realizarse una consulta en las entidades con la misma clave de partición de manera más rápida que en aquellas que tienen claves de partición distintas. Esta sección se muestra cómo tooquery una tabla para todas las entidades de Hola de una partición especificada.  

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment)y utiliza los datos de [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table). 

1. Abra hello `TablesController.cs` archivo.

1. Agregue un método llamado **GetPartition** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de hello **GetPartition** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtener un **CloudTable** objeto que representa una tabla de toohello de referencia desde el que va a recuperar entidades de Hola. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Crear una instancia de un **TableQuery** objeto que especifica la consulta de Hola Hola **donde** cláusula. Con hello **CustomerEntity** clase y los datos presentados en la sección de hello [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table), siguiente de hello tabla de Hola de consultas de fragmento de código para una todas las entidades de código donde hello  **PartitionKey** (apellido del cliente) tiene un valor de "Smith":

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. Dentro de un bucle, llame a hello **CloudTable.ExecuteQuerySegmented** método pasando el objeto de consulta de Hola crea una instancia en el paso anterior de Hola.  Hola **CloudTable.ExecuteQuerySegmented** método devuelve un **TableContinuationToken** objeto, cuando **null** -indica que no hay más entidades tooretrieve. En el bucle de hello, usar otro tooiterate de bucle sobre Hola devuelve entidades. En el siguiente ejemplo de código de hello, cada entidad devuelta se agrega tooa lista. Una vez Hola bucle finaliza, lista de Hola se pasa tooa vista para mostrar: 

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

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **GetPartition** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `GetPartition.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

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

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Ejecute la aplicación hello y seleccione **obtener partición** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![GetPartition](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Eliminación de una entidad

Esta sección se muestra cómo toodelete una entidad de una tabla.

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello en [configurar el entorno de desarrollo de hello](#set-up-the-development-environment)y utiliza los datos de [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table). 

1. Abra hello `TablesController.cs` archivo.

1. Agregue un método llamado **DeleteEntity** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de hello **DeleteEntity** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de tabla.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Obtener un **CloudTable** objeto que representa una tabla de toohello de referencia desde el que va a eliminar entidad Hola. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Cree un objeto de operación de eliminación que tome un objeto de entidad derivado de **TableEntity**. En este caso, usamos hello **CustomerEntity** clase y los datos presentados en la sección de hello [agregar un lote de la tabla de entidades tooa](#add-a-batch-of-entities-to-a-table). Hola la entidad **ETag** debe establecerse el valor válido de tooa.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Ejecutar la operación de eliminación de Hola.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Pasar toohello vista de resultado de hello para su presentación.

    ```csharp
    return View(result);
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **tablas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **DeleteEntity** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `DeleteEntity.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

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

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Ejecute la aplicación hello y seleccione **eliminar entidad** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![GetSingle](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Pasos siguientes
Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.

  * [Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-queues.md)

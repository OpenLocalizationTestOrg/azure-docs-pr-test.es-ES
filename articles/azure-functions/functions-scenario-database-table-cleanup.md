---
title: Uso de Azure Functions para realizar una tarea de limpieza de base de datos | Microsoft Docs
description: "Use Azure Functions para programar una tarea que se conecte a Azure SQL Database a fin de limpiar filas de forma periódica."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="0bbe6-103">Uso de Azure Functions para conectarse a una base de datos de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0bbe6-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="0bbe6-104">En este tema se indica cómo usar Azure Functions para crear un trabajo programado que limpie hileras de una tabla en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="0bbe6-105">La nueva función C# se crea a partir de una plantilla de desencadenador de temporizador predefinida de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="0bbe6-106">Para que este escenario sea posible, también debe establecer una cadena de conexión de base de datos como un valor de configuración en la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="0bbe6-107">En este escenario se utiliza una operación masiva en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="0bbe6-108">Para que la función procese ciertas operaciones CRUD en una tabla de Mobile Apps, debería usar enlaces de [Mobile Apps](functions-bindings-mobile-apps.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bbe6-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0bbe6-109">Prerequisites</span></span>

+ <span data-ttu-id="0bbe6-110">En este tema se usa una función desencadenada por un temporizador.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="0bbe6-111">Efectúe los pasos del tema [Cree una función en Azure que se desencadena mediante un temporizador](functions-create-scheduled-function.md) para crear una versión en C# de esta función.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="0bbe6-112">En este tema se realiza una demostración de un comando de Transact-SQL que ejecuta una operación de limpieza masiva en la tabla **SalesOrderHeader** de la base de datos AdventureWorksLT de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="0bbe6-113">Para crear la base de datos de ejemplo AdventureWorksLT, efectúe los pasos indicados en el tema [Creación de una instancia de Azure SQL Database en Azure Portal](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0bbe6-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="0bbe6-114">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="0bbe6-114">Get connection information</span></span>

<span data-ttu-id="0bbe6-115">Deberá obtener la cadena de conexión de la base de datos que creó una vez concluidos los pasos de [Creación de una instancia de Azure SQL Database en Azure Portal](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0bbe6-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="0bbe6-116">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0bbe6-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="0bbe6-117">Seleccione **Bases de datos SQL** en el menú de la izquierda y seleccione la base de datos en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="0bbe6-118">Seleccione **Mostrar las cadenas de conexión de la base de datos** y copie la cadena de conexión de **ADO.NET** completa.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![Copie la cadena de conexión de ADO.NET.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="0bbe6-120">Establecimiento de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="0bbe6-120">Set the connection string</span></span> 

<span data-ttu-id="0bbe6-121">Una aplicación de función hospeda la ejecución de sus funciones en Azure.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="0bbe6-122">Se recomienda almacenar las cadenas de conexión y otros secretos en la configuración de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="0bbe6-123">El uso de la configuración de la aplicación impide divulgaciones accidentales de la cadena de conexión con el código.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="0bbe6-124">Vaya a la aplicación de función que creó en [Cree una función en Azure que se desencadena mediante un temporizador](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="0bbe6-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="0bbe6-125">Seleccione **Características de la plataforma** > **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Configuración de la aplicación para la aplicación de función.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="0bbe6-127">Desplácese hacia abajo hasta **Cadenas de conexión** y agregue una cadena de conexión con los valores de configuración especificados en la tabla.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Agregue una cadena de conexión a la configuración de la aplicación de función.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="0bbe6-129">Configuración</span><span class="sxs-lookup"><span data-stu-id="0bbe6-129">Setting</span></span>       | <span data-ttu-id="0bbe6-130">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="0bbe6-130">Suggested value</span></span> | <span data-ttu-id="0bbe6-131">Descripción</span><span class="sxs-lookup"><span data-stu-id="0bbe6-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="0bbe6-132">**Name**</span><span class="sxs-lookup"><span data-stu-id="0bbe6-132">**Name**</span></span>  |  <span data-ttu-id="0bbe6-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="0bbe6-133">sqldb_connection</span></span>  | <span data-ttu-id="0bbe6-134">Se usa para acceder a la cadena de conexión almacenada en el código de función.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="0bbe6-135">**Valor**</span><span class="sxs-lookup"><span data-stu-id="0bbe6-135">**Value**</span></span> | <span data-ttu-id="0bbe6-136">Cadena copiada</span><span class="sxs-lookup"><span data-stu-id="0bbe6-136">Copied string</span></span>  | <span data-ttu-id="0bbe6-137">Pegue la cadena de conexión que copió en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="0bbe6-138">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="0bbe6-138">**Type**</span></span> | <span data-ttu-id="0bbe6-139">Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="0bbe6-139">SQL Database</span></span> | <span data-ttu-id="0bbe6-140">Use la conexión predeterminada de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="0bbe6-141">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-141">Click **Save**.</span></span>

<span data-ttu-id="0bbe6-142">Ahora, puede agregar el código de función de C# que conecta con la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="0bbe6-143">Actualización del código de función</span><span class="sxs-lookup"><span data-stu-id="0bbe6-143">Update your function code</span></span>

1. <span data-ttu-id="0bbe6-144">En la aplicación de función, seleccione la función desencadenada por temporizador.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="0bbe6-145">Agregue las siguientes referencias de ensamblado en la parte superior del código de función existente:</span><span class="sxs-lookup"><span data-stu-id="0bbe6-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="0bbe6-146">Agregue las siguientes instrucciones `using` a la función:</span><span class="sxs-lookup"><span data-stu-id="0bbe6-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="0bbe6-147">Reemplace la función **Run** existente por el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="0bbe6-147">Replace the existing **Run** function with the following code:</span></span>
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="0bbe6-148">Con este comando se actualiza la columna **Estado** según la fecha de envío.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="0bbe6-149">Debería actualizar 32 filas de datos.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="0bbe6-150">Haga clic en **Guardar**, inspeccione la ventana **Registros** durante la ejecución de la siguiente función y, a continuación, anote el número de filas actualizadas en la tabla **SalesOrderHeader**.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![Vista de los registros de función.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="0bbe6-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0bbe6-152">Next steps</span></span>

<span data-ttu-id="0bbe6-153">A continuación, obtenga información sobre cómo usar Functions con Logic Apps para la integración con otros servicios.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="0bbe6-154">Creación de una función que se integre con Logic Apps</span><span class="sxs-lookup"><span data-stu-id="0bbe6-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="0bbe6-155">Para obtener más función sobre Functions, consulte los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="0bbe6-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="0bbe6-156">Referencia para desarrolladores de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="0bbe6-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="0bbe6-157">contiene las referencias del programador para codificar funciones y definir desencadenadores y enlaces.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="0bbe6-158">Prueba de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0bbe6-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="0bbe6-159">describe las diversas herramientas y técnicas para probar sus funciones.</span><span class="sxs-lookup"><span data-stu-id="0bbe6-159">Describes various tools and techniques for testing your functions.</span></span>  

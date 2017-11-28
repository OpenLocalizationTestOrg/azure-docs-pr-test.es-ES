---
title: aaaUse funciones de Azure tooperform una base de datos limpiar tarea | Documentos de Microsoft
description: Use las funciones de Azure tooschedule una tarea que se conecta tooAzure tooperiodically de base de datos SQL limpiar filas.
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
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="3fa2a-103">Usar funciones de Azure tooconnect tooan base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="3fa2a-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="3fa2a-104">Este tema muestra cómo toouse funciones de Azure toocreate programada del trabajo que limpia filas de una tabla en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="3fa2a-105">función de Hello nuevo C# se crea en función de una plantilla de desencadenador de temporizador predefinidos en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="3fa2a-106">toosupport este escenario, también debe establecer una cadena de conexión de base de datos como una configuración de aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="3fa2a-107">Este escenario usa una operación masiva con la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="3fa2a-108">toohave las función proceso CRUD de las operaciones individuales en una tabla de aplicaciones móviles, debe usar en su lugar [enlaces de aplicaciones móviles](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3fa2a-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fa2a-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3fa2a-109">Prerequisites</span></span>

+ <span data-ttu-id="3fa2a-110">En este tema se usa una función desencadenada por un temporizador.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="3fa2a-111">Hola completa los pasos en el tema de hello [crear una función de Azure que se desencadena por un temporizador](functions-create-scheduled-function.md) versión toocreate C# de esta función.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="3fa2a-112">Este tema muestra un comando de Transact-SQL que ejecuta una operación de limpieza de forma masiva en hello **SalesOrderHeader** tabla de base de datos de ejemplo de Hola AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="3fa2a-113">datos de ejemplo AdventureWorksLT de toocreate Hola Hola completa los pasos de tema de hello [crear una base de datos de SQL Azure en el portal de Azure hello](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3fa2a-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="3fa2a-114">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="3fa2a-114">Get connection information</span></span>

<span data-ttu-id="3fa2a-115">Se necesita la cadena de conexión de Hola de tooget de base de datos de Hola que creó al completar [crear una base de datos de SQL Azure en el portal de Azure hello](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3fa2a-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="3fa2a-116">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3fa2a-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="3fa2a-117">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y seleccione la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="3fa2a-118">Seleccione **mostrar cadenas de conexión de base de datos** hello copia completa y **ADO.NET** cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Copie la cadena de conexión de ADO.NET Hola.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="3fa2a-120">Establece la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="3fa2a-120">Set hello connection string</span></span> 

<span data-ttu-id="3fa2a-121">Una aplicación de la función hospeda ejecución Hola de las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="3fa2a-122">Es una mejor las cadenas de conexión de toostore de práctica y otros secretos en la configuración de aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="3fa2a-123">Con la configuración de aplicación impide la divulgación accidental de la cadena de conexión de hello con el código.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="3fa2a-124">Navegar por la aplicación de la función de tooyour que creó [crear una función de Azure que se desencadena por un temporizador](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="3fa2a-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="3fa2a-125">Seleccione **Características de la plataforma** > **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Configuración de la aplicación para la aplicación de la función de hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="3fa2a-127">Desplácese hacia abajo demasiado**las cadenas de conexión** y agregar una cadena de conexión mediante configuración de hello como se especifica en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![Agregar una configuración de la aplicación de la cadena toohello conexión función.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="3fa2a-129">Configuración</span><span class="sxs-lookup"><span data-stu-id="3fa2a-129">Setting</span></span>       | <span data-ttu-id="3fa2a-130">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="3fa2a-130">Suggested value</span></span> | <span data-ttu-id="3fa2a-131">Descripción</span><span class="sxs-lookup"><span data-stu-id="3fa2a-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="3fa2a-132">**Name**</span><span class="sxs-lookup"><span data-stu-id="3fa2a-132">**Name**</span></span>  |  <span data-ttu-id="3fa2a-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="3fa2a-133">sqldb_connection</span></span>  | <span data-ttu-id="3fa2a-134">Hola tooaccess usado almacena cadena de conexión en el código de función.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="3fa2a-135">**Valor**</span><span class="sxs-lookup"><span data-stu-id="3fa2a-135">**Value**</span></span> | <span data-ttu-id="3fa2a-136">Cadena copiada</span><span class="sxs-lookup"><span data-stu-id="3fa2a-136">Copied string</span></span>  | <span data-ttu-id="3fa2a-137">Más allá de la cadena de conexión de Hola que copió en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="3fa2a-138">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="3fa2a-138">**Type**</span></span> | <span data-ttu-id="3fa2a-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="3fa2a-139">SQL Database</span></span> | <span data-ttu-id="3fa2a-140">Usar conexión de base de datos SQL de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="3fa2a-141">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-141">Click **Save**.</span></span>

<span data-ttu-id="3fa2a-142">Ahora, puede agregar Hola función código de C# que se conecta tooyour base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="3fa2a-143">Actualización del código de función</span><span class="sxs-lookup"><span data-stu-id="3fa2a-143">Update your function code</span></span>

1. <span data-ttu-id="3fa2a-144">En la aplicación de la función, seleccione función de hello desencadenada por el temporizador.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="3fa2a-145">Agregue Hola siguiendo las referencias de ensamblado en parte superior de Hola Hola existente del código de función:</span><span class="sxs-lookup"><span data-stu-id="3fa2a-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="3fa2a-146">Agregue los siguiente hello `using` función toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="3fa2a-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="3fa2a-147">Reemplazar existente hello **ejecutar** función con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="3fa2a-147">Replace hello existing **Run** function with hello following code:</span></span>
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
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="3fa2a-148">Este comando de ejemplo actualiza hello **estado** columna según la fecha de envío de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="3fa2a-149">Debería actualizar 32 filas de datos.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="3fa2a-150">Haga clic en **guardar**, Hola inspección **registros** windows para hello función ejecución, a continuación, anote Hola número de filas actualizadas en hello **SalesOrderHeader** tabla.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Ver registros de funciones de Hola.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="3fa2a-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3fa2a-152">Next steps</span></span>

<span data-ttu-id="3fa2a-153">A continuación, obtenga información acerca de cómo las funciones de toouse a toointegrate Logic Apps con otros servicios.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="3fa2a-154">Creación de una función que se integre con Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3fa2a-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="3fa2a-155">Para obtener más información acerca de las funciones, vea Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="3fa2a-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="3fa2a-156">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="3fa2a-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="3fa2a-157">contiene las referencias del programador para codificar funciones y definir desencadenadores y enlaces.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="3fa2a-158">Prueba de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3fa2a-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="3fa2a-159">describe las diversas herramientas y técnicas para probar sus funciones.</span><span class="sxs-lookup"><span data-stu-id="3fa2a-159">Describes various tools and techniques for testing your functions.</span></span>  

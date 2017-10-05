---
title: "Creación de una función que conecte con los servicios de Azure | Microsoft Docs"
description: "Use Azure Functions para crear una aplicación sin servidor que se conecta a otros servicios de Azure."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="3bbe9-104">Use Azure Functions para crear una aplicación sin servidor que se conecta a otros servicios de Azure</span><span class="sxs-lookup"><span data-stu-id="3bbe9-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="3bbe9-105">En este tema se muestra cómo crear una función en Azure Functions que escucha los mensajes en una cola de Azure Storage y copia los mensajes en las filas de una tabla de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="3bbe9-106">Se utiliza una función desencadenada del temporizador para cargar mensajes en la cola.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="3bbe9-107">Una segunda función lee en la cola y escribe mensajes en la tabla.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="3bbe9-108">Tanto la cola como la tabla las crea automáticamente Azure Functions según las definiciones de enlace.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="3bbe9-109">Para hacer todo más interesante, se escribe una función en JavaScript y la otra en script de C#.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="3bbe9-110">Esto demuestra cómo una aplicación de la función puede tener funciones en distintos lenguajes.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="3bbe9-111">En un [vídeo de Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player) se puede ver una demostración de este escenario.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="3bbe9-112">Creación de una función que escribe en la cola</span><span class="sxs-lookup"><span data-stu-id="3bbe9-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="3bbe9-113">Para poder conectarse a una cola de almacenamiento, debe crear una función que carga la cola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="3bbe9-114">Esta función de JavaScript usa un desencadenador de temporizador que escribe un mensaje en la cola cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="3bbe9-115">Si ya no tiene una cuenta de Azure, consulte la experiencia [Probar Azure Functions](https://functions.azure.com/try) o [cree su cuenta gratis de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3bbe9-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="3bbe9-116">Vaya a Azure Portal y busque la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="3bbe9-117">Haga clic en **Nueva función** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="3bbe9-118">Llame a la función **FunctionsBindingsDemo1**, escriba el valor de la expresión cron de `0/10 * * * * *` para **Programación** y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Adición de una función desencadenada por el temporizador](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="3bbe9-120">Ahora ha creado una función desencadenada por el temporizador que se ejecuta cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="3bbe9-121">En la pestaña **Desarrollar** haga clic en **Registros** y consulte la actividad en el registro.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="3bbe9-122">Verá una entrada de registro escrita cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Compruebe el registro para comprobar que la función funciona.](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="3bbe9-124">Adición de un enlace de salida de la cola de mensajes</span><span class="sxs-lookup"><span data-stu-id="3bbe9-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="3bbe9-125">En la pestaña **Integrar**, elija **Nueva salida** > **Azure Queue Storage** > **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Adición de una función de temporizador de desencadenador](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="3bbe9-127">Escriba `myQueueItem` para **el nombre del parámetro de mensaje** y `functions-bindings` para el **nombre de la cola**, seleccione una **conexión de la cuenta de almacenamiento** existente o haga clic en **Nueva** para crear una y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![Creación del enlace de salida en la cola de almacenamiento](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="3bbe9-129">En la pestaña **Desarrollar**, anexe el código siguiente a la función:</span><span class="sxs-lookup"><span data-stu-id="3bbe9-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="3bbe9-130">Localice la instrucción *if* alrededor de la línea 9 de la función e introduzca el código siguiente después de la instrucción.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="3bbe9-131">Este código crea un elemento **myQueueItem** y establece su propiedad **time** en la marca de tiempo actual.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="3bbe9-132">A continuación, agrega el nuevo elemento de cola al enlace de **myQueueItem** del contexto.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="3bbe9-133">Haga clic en **Guardar y ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="3bbe9-134">Ver actualizaciones de almacenamiento mediante el Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="3bbe9-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="3bbe9-135">Puede comprobar que la función funciona consultando los mensajes en la cola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="3bbe9-136">Puede conectarse a la cola de almacenamiento mediante el Explorador de nube en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="3bbe9-137">Sin embargo, el portal facilita la conexión a su cuenta de almacenamiento mediante el Explorador de Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="3bbe9-138">En la pestaña **Integrar**, haga clic en el enlace de salida de la cola > **Documentación**, después muestre la cadena de conexión para la cuenta de almacenamiento y copie el valor.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="3bbe9-139">Use este valor para conectarse a su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-139">You use this value to connect to your storage account.</span></span>

    ![Descarga del explorador de Azure Storage](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="3bbe9-141">Si no lo ha hecho ya, descargue e instale el [Explorador de Microsoft Azure Storage](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="3bbe9-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="3bbe9-142">En el Explorador de Storage, haga clic en el icono de Azure Storage, pegue la cadena de conexión en el campo y complete el asistente.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Explorador de Storage agrega una conexión](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="3bbe9-144">En **Local y conectado**, expanda **Cuentas de almacenamiento** > su cuenta de almacenamiento > **Colas** > **Enlaces de funciones** y compruebe que los mensajes se escriben en la cola.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![Vista de mensajes en la cola](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="3bbe9-146">Si la cola no existe o está vacía, lo más probable es que haya un problema con el enlace o código de la función.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="3bbe9-147">Creación de una función que lee en la cola</span><span class="sxs-lookup"><span data-stu-id="3bbe9-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="3bbe9-148">Ahora que tiene mensajes que se van a agregar a la cola, puede crear otra función que lee de la cola y escribe los mensajes de forma permanente a una tabla de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="3bbe9-149">Haga clic en **Nueva función** > **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="3bbe9-150">Llame a la función `FunctionsBindingsDemo2`, escriba **functions-bindings** en el campo **Nombre de la cola**, seleccione una cuenta de almacenamiento existente o cree una y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Adición de una función de temporizador de cola de salida](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="3bbe9-152">(Opcional) Puede comprobar que la nueva función funciona mediante la visualización de la nueva cola en el Explorador de Storage como antes.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="3bbe9-153">También puede utilizar el Explorador de nube en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="3bbe9-154">(Opcional) Actualice la cola **functions-bindings** y observe que los elementos se han quitado de la cola.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="3bbe9-155">La eliminación se produce porque la función está enlazada a la cola **functions-bindings** como un desencadenador de entrada y la función lee la cola.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="3bbe9-156">Adición de un enlace de salida de tabla</span><span class="sxs-lookup"><span data-stu-id="3bbe9-156">Add a table output binding</span></span>

1. <span data-ttu-id="3bbe9-157">En FunctionsBindingsDemo2, haga clic en **Integrar** > **Nueva salida** > **Azure Table Storage** > **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Adición de un enlace a una tabla de Azure Storage](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="3bbe9-159">Escriba `functionbindings` para el **nombre de la tabla** y `myTable` para el **nombre de parámetro de la tabla**, elija un **conexión de la cuenta de almacenamiento** o cree una nueva y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configuración del enlace de la tabla de almacenamiento](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="3bbe9-161">En la pestaña **Desarrollar**, sustituya el código de función existente por el siguiente:</span><span class="sxs-lookup"><span data-stu-id="3bbe9-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add the item to the table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="3bbe9-162">La clase **TableItem** representa una fila en la tabla de almacenamiento y hay que agregar el elemento a la colección `myTable` de objetos **TableItem**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="3bbe9-163">Debe establecer las propiedades **PartitionKey** y **RowKey** para poder insertarlas en la tabla.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="3bbe9-164">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-164">Click **Save**.</span></span>  <span data-ttu-id="3bbe9-165">Por último, puede comprobar que la función funciona contemplando la tabla en el Explorador de Storage o el Explorador de nube de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="3bbe9-166">(Opcional) En la cuenta de almacenamiento del Explorador de Storage, expanda **Tablas** > **functionsbindings** y compruebe que se agregan filas a la tabla.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="3bbe9-167">También puede hacer lo mismo en el Explorador de nube en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![Visualización de las filas de la tabla](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="3bbe9-169">Si la tabla no existe o está vacía, lo más probable es que haya un problema con el enlace o código de la función.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="3bbe9-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3bbe9-170">Next steps</span></span>
<span data-ttu-id="3bbe9-171">Consulte los siguientes temas para más información sobre Azure Functions:</span><span class="sxs-lookup"><span data-stu-id="3bbe9-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="3bbe9-172">Referencia para desarrolladores de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="3bbe9-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="3bbe9-173">contiene las referencias del programador para codificar funciones y definir desencadenadores y enlaces.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="3bbe9-174">Prueba de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3bbe9-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="3bbe9-175">describe las diversas herramientas y técnicas para probar sus funciones.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="3bbe9-176">How to scale Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3bbe9-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="3bbe9-177">Trata los planes de servicio disponibles con Azure Functions, incluido el plan de hospedaje de Consumo, y cómo elegir el plan adecuado.</span><span class="sxs-lookup"><span data-stu-id="3bbe9-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]


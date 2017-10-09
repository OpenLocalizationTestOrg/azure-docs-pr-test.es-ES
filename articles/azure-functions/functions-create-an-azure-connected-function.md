---
title: "una función que se conecta a servicios de tooAzure aaaCreate | Documentos de Microsoft"
description: "Usar funciones de Azure toocreate una aplicación sin servidor que se conecta tooother Azure servicios."
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
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="bc319-104">Usar funciones de Azure toocreate una función que se conecta tooother Azure Servicios</span><span class="sxs-lookup"><span data-stu-id="bc319-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="bc319-105">Este tema muestra cómo una función en funciones de Azure que escucha toomessages en un Hola de cola y las copias de almacenamiento de Azure toocreate mensajes toorows en una tabla de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="bc319-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="bc319-106">Una función de temporizador desencadenada es tooload usa mensajes en cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc319-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="bc319-107">Una segunda función lee de la cola de Hola y escribe la tabla de toohello de mensajes.</span><span class="sxs-lookup"><span data-stu-id="bc319-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="bc319-108">Cola de Hola y tabla de Hola se crean automáticamente por funciones de Azure que se basan en definiciones de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc319-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="bc319-109">toomake cosas más interesantes, se escribe una función de JavaScript y Hola otro se escribe en la secuencia de comandos de C#.</span><span class="sxs-lookup"><span data-stu-id="bc319-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="bc319-110">Esto demuestra cómo una aplicación de la función puede tener funciones en distintos lenguajes.</span><span class="sxs-lookup"><span data-stu-id="bc319-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="bc319-111">En un [vídeo de Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player) se puede ver una demostración de este escenario.</span><span class="sxs-lookup"><span data-stu-id="bc319-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="bc319-112">Crear una función que escribe toohello cola</span><span class="sxs-lookup"><span data-stu-id="bc319-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="bc319-113">Para poder conectarse tooa cola de almacenamiento, deberá toocreate una función que carga la cola de mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc319-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="bc319-114">Esta función de JavaScript usa un desencadenador de temporizador que escribe una cola de mensajes toohello cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="bc319-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="bc319-115">Si ya no tiene una cuenta de Azure, visite hello [funciones de Azure intente](https://functions.azure.com/try) experiencia, o [crear su cuenta de Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="bc319-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="bc319-116">Vaya toohello portal de Azure y busque la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="bc319-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="bc319-117">Haga clic en **Nueva función** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="bc319-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="bc319-118">Nombre de función hello **FunctionsBindingsDemo1**, escriba el valor de la expresión cron `0/10 * * * * *` para **programación**y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="bc319-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Adición de una función desencadenada por el temporizador](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="bc319-120">Ahora ha creado una función desencadenada por el temporizador que se ejecuta cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="bc319-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="bc319-121">En hello **desarrollar** , haga clic en **registros** y ver la actividad de hello en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="bc319-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="bc319-122">Verá una entrada de registro escrita cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="bc319-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Ver Hola registro tooverify Hola función funciona](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="bc319-124">Adición de un enlace de salida de la cola de mensajes</span><span class="sxs-lookup"><span data-stu-id="bc319-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="bc319-125">En hello **integrar** ficha, elija **nueva salida** > **almacenamiento de cola de Azure** > **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="bc319-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Adición de una función de temporizador de desencadenador](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="bc319-127">Escriba `myQueueItem` para **nombre de parámetro de mensaje** y `functions-bindings` para **nombre de la cola**, seleccione una existente **conexión de la cuenta de almacenamiento** o haga clic en **nueva** toocreate un almacenamiento de conexión de la cuenta y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="bc319-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Crear cola de almacenamiento de toohello de enlace de salida de hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="bc319-129">Nuevo en hello **desarrollar** ficha, anexar Hola después de la función de toohello de código:</span><span class="sxs-lookup"><span data-stu-id="bc319-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="bc319-130">Busque hello *si* instrucción aproximadamente 9 de función de Hola y de línea siguiente de Hola de inserción de código después de esa instrucción.</span><span class="sxs-lookup"><span data-stu-id="bc319-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="bc319-131">Este código crea un **myQueueItem** y establece su **tiempo** marca de tiempo actual toohello de propiedad.</span><span class="sxs-lookup"><span data-stu-id="bc319-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="bc319-132">A continuación, agrega Hola nueva cola elemento toohello del contexto **myQueueItem** enlace.</span><span class="sxs-lookup"><span data-stu-id="bc319-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="bc319-133">Haga clic en **Guardar y ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="bc319-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="bc319-134">Ver actualizaciones de almacenamiento mediante el Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="bc319-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="bc319-135">Puede comprobar que funciona la función ver los mensajes en cola de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="bc319-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="bc319-136">Cola de almacenamiento de tooyour puede conectarse mediante el Explorador de nube en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc319-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="bc319-137">Sin embargo, portal de Hola resulta fácil tooconnect cuenta de almacenamiento de tooyour mediante el Explorador de almacenamiento de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bc319-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="bc319-138">Hola **integrar** , haga clic en la cola de salida enlace > **documentación**, a continuación, mostrar hello cadena de conexión para la cuenta de almacenamiento y copie el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc319-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="bc319-139">Utilice esta cuenta de almacenamiento de valor tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="bc319-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Descarga del explorador de Azure Storage](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="bc319-141">Si no lo ha hecho ya, descargue e instale el [Explorador de Microsoft Azure Storage](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="bc319-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="bc319-142">En el Explorador de almacenamiento, haga clic en hello tooAzure almacenamiento icono Conectar, pegue la cadena de conexión de hello en el campo de Hola y complete el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc319-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Explorador de Storage agrega una conexión](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="bc319-144">En **Local y conectado**, expanda **cuentas de almacenamiento** > su cuenta de almacenamiento > **colas** > **deenlacesdefunciones**y compruebe que los mensajes se escriben toohello cola.</span><span class="sxs-lookup"><span data-stu-id="bc319-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Vista de mensajes en cola de Hola](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="bc319-146">Si la cola de hello no existe o está vacío, más probable es que hay un problema con el enlace de función o el código.</span><span class="sxs-lookup"><span data-stu-id="bc319-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="bc319-147">Crear una función que se lee de la cola de Hola</span><span class="sxs-lookup"><span data-stu-id="bc319-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="bc319-148">Ahora que tiene añadidos toohello cola de mensajes, puede crear otra función que se lee de la cola de Hola y Hola escrituras permanentemente mensajes tooan tabla de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="bc319-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="bc319-149">Haga clic en **Nueva función** > **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="bc319-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="bc319-150">Nombre de función hello `FunctionsBindingsDemo2`, escriba **enlaces de funciones** en hello **nombre de la cola** campo, seleccione una cuenta de almacenamiento existente o crear uno y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="bc319-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Adición de una función de temporizador de cola de salida](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="bc319-152">(Opcional) Puede comprobar que la nueva función de hello funciona viendo la nueva cola de hello en el Explorador de almacenamiento como antes.</span><span class="sxs-lookup"><span data-stu-id="bc319-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="bc319-153">También puede utilizar el Explorador de nube en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc319-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="bc319-154">(Opcional) Actualizar hello **enlaces de funciones** poner en cola y observe que los elementos se han quitado de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc319-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="bc319-155">Hello eliminación se produce porque la función hello es toohello enlazado **enlaces de funciones** como una función de hello y desencadenador de entrada lee cola Hola de cola.</span><span class="sxs-lookup"><span data-stu-id="bc319-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="bc319-156">Adición de un enlace de salida de tabla</span><span class="sxs-lookup"><span data-stu-id="bc319-156">Add a table output binding</span></span>

1. <span data-ttu-id="bc319-157">En FunctionsBindingsDemo2, haga clic en **Integrar** > **Nueva salida** > **Azure Table Storage** > **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="bc319-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Agregar una tabla de almacenamiento de Azure de enlace tooan](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="bc319-159">Escriba `functionbindings` para el **nombre de la tabla** y `myTable` para el **nombre de parámetro de la tabla**, elija un **conexión de la cuenta de almacenamiento** o cree una nueva y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bc319-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configurar el enlace de tablas de almacenamiento de Hola](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="bc319-161">Hola **desarrollar** ficha, reemplace el código existente de la función de hello con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="bc319-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
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
        
        // Add hello item toohello table binding collection.
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
    <span data-ttu-id="bc319-162">Hola **TableItem** clase representa una fila de tabla de almacenamiento de Hola y agregar Hola elemento toohello `myTable` colección de **TableItem** objetos.</span><span class="sxs-lookup"><span data-stu-id="bc319-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="bc319-163">Debe establecer hello **PartitionKey** y **RowKey** propiedades toobe puede tooinsert en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc319-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="bc319-164">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bc319-164">Click **Save**.</span></span>  <span data-ttu-id="bc319-165">Por último, puede comprobar Hola función funciona mediante la visualización de tabla de hello en el Explorador de almacenamiento o el Explorador de Visual Studio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bc319-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="bc319-166">(Opcional) En la cuenta de almacenamiento en el Explorador de almacenamiento, expanda **tablas** > **functionsbindings** y compruebe que se han agregado filas de tabla toohello.</span><span class="sxs-lookup"><span data-stu-id="bc319-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="bc319-167">Puede hacer igual hello en el Explorador de nube en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc319-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Vista de filas de tabla de Hola](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="bc319-169">Si la tabla de hello no existe o está vacío, más probable es que hay un problema con el enlace de función o el código.</span><span class="sxs-lookup"><span data-stu-id="bc319-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="bc319-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bc319-170">Next steps</span></span>
<span data-ttu-id="bc319-171">Para obtener más información acerca de las funciones de Azure, vea Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="bc319-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="bc319-172">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="bc319-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="bc319-173">contiene las referencias del programador para codificar funciones y definir desencadenadores y enlaces.</span><span class="sxs-lookup"><span data-stu-id="bc319-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="bc319-174">Prueba de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="bc319-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="bc319-175">describe las diversas herramientas y técnicas para probar sus funciones.</span><span class="sxs-lookup"><span data-stu-id="bc319-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="bc319-176">¿Cómo tooscale las funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="bc319-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="bc319-177">Se tratan los planes de servicio disponibles con las funciones de Azure, incluido el plan de hospedaje de consumo de Hola y cómo toochoose Hola plan adecuado.</span><span class="sxs-lookup"><span data-stu-id="bc319-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]


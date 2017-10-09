---
title: "una función en Azure desencadenado por la cola de mensajes aaaCreate | Documentos de Microsoft"
description: "Usar funciones de Azure toocreate una función sin servidor que se invoca con un mensaje había enviado tooan cola de almacenamiento de Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a><span data-ttu-id="42bb5-103">Agregar la cola de mensajes tooan almacenamiento de Azure mediante funciones</span><span class="sxs-lookup"><span data-stu-id="42bb5-103">Add messages tooan Azure Storage queue using Functions</span></span>

<span data-ttu-id="42bb5-104">En las funciones de Azure, los enlaces de entrada y salidos proporcionan una manera declarativa tooconnect tooexternal servicio de datos de la función.</span><span class="sxs-lookup"><span data-stu-id="42bb5-104">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="42bb5-105">En este tema, aprenderá cómo tooupdate una función existente mediante la adición de una salida de enlace que envía mensajes tooAzure almacenamiento en la cola.</span><span class="sxs-lookup"><span data-stu-id="42bb5-105">In this topic, learn how tooupdate an existing function by adding an output binding that sends messages tooAzure Queue storage.</span></span>  

![Ver el mensaje en los registros de Hola.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a><span data-ttu-id="42bb5-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="42bb5-107">Prerequisites</span></span> 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* <span data-ttu-id="42bb5-108">Instalar hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="42bb5-108">Install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <span data-ttu-id="42bb5-109"><a name="add-binding"></a>Agregar un enlace de salida</span><span class="sxs-lookup"><span data-stu-id="42bb5-109"><a name="add-binding"></a>Add an output binding</span></span>
 
1. <span data-ttu-id="42bb5-110">Expanda su Function App y su función.</span><span class="sxs-lookup"><span data-stu-id="42bb5-110">Expand both your function app and your function.</span></span>

2. <span data-ttu-id="42bb5-111">Seleccione sucesivamente **Integrar**, **+ Nueva salida**, **Azure Queue Storage** y **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="42bb5-111">Select **Integrate** and **+ New output**, then choose **Azure Queue storage** and choose **Select**.</span></span>
    
    ![Agregar una función de tooa de enlace de salida de cola almacenamiento Hola portal de Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="42bb5-113">Usar la configuración de hello como se especifica en la tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="42bb5-113">Use hello settings as specified in hello table:</span></span> 

    ![Agregar una función de tooa de enlace de salida de cola almacenamiento Hola portal de Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="42bb5-115">Configuración</span><span class="sxs-lookup"><span data-stu-id="42bb5-115">Setting</span></span>      |  <span data-ttu-id="42bb5-116">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="42bb5-116">Suggested value</span></span>   | <span data-ttu-id="42bb5-117">Descripción</span><span class="sxs-lookup"><span data-stu-id="42bb5-117">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="42bb5-118">**Nombre de la cola**</span><span class="sxs-lookup"><span data-stu-id="42bb5-118">**Queue name**</span></span>   | <span data-ttu-id="42bb5-119">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="42bb5-119">myqueue-items</span></span>    | <span data-ttu-id="42bb5-120">nombre de Hola de hello en cola tooconnect tooin su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="42bb5-120">hello name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="42bb5-121">**Conexión de la cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="42bb5-121">**Storage account connection**</span></span> | <span data-ttu-id="42bb5-122">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="42bb5-122">AzureWebJobStorage</span></span> | <span data-ttu-id="42bb5-123">Puede usar la conexión de la cuenta de almacenamiento Hola ya está en uso por la aplicación de la función o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="42bb5-123">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="42bb5-124">**Nombre del parámetro de mensaje**</span><span class="sxs-lookup"><span data-stu-id="42bb5-124">**Message parameter name**</span></span> | <span data-ttu-id="42bb5-125">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="42bb5-125">outputQueueItem</span></span> | <span data-ttu-id="42bb5-126">nombre de Hola Hola enlace de parámetros de salida.</span><span class="sxs-lookup"><span data-stu-id="42bb5-126">hello name of hello output binding parameter.</span></span> | 

4. <span data-ttu-id="42bb5-127">Haga clic en **guardar** enlace de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="42bb5-127">Click **Save** tooadd hello binding.</span></span>
 
<span data-ttu-id="42bb5-128">Ahora que tiene un enlace de salida definido, debe tooupdate Hola código toouse Hola enlace tooadd tooa cola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="42bb5-128">Now that you have an output binding defined, you need tooupdate hello code toouse hello binding tooadd messages tooa queue.</span></span>  

## <a name="update-hello-function-code"></a><span data-ttu-id="42bb5-129">Actualizar código de función de Hola</span><span class="sxs-lookup"><span data-stu-id="42bb5-129">Update hello function code</span></span>

1. <span data-ttu-id="42bb5-130">Seleccione el código de la función de la función toodisplay hello en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="42bb5-130">Select your function toodisplay hello function code in hello editor.</span></span> 

2. <span data-ttu-id="42bb5-131">Para una función de C#, actualice la definición de función manera hello tooadd **outputQueueItem** parámetros de enlace de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="42bb5-131">For a C# function, update your function definition as follows tooadd hello **outputQueueItem** storage binding parameter.</span></span> <span data-ttu-id="42bb5-132">Omita este paso para una función de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="42bb5-132">Skip this step for a JavaScript function.</span></span>

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. <span data-ttu-id="42bb5-133">Agregar Hola siguiendo la función de toohello de código justo antes de que devuelve el método hello.</span><span class="sxs-lookup"><span data-stu-id="42bb5-133">Add hello following code toohello function just before hello method returns.</span></span> <span data-ttu-id="42bb5-134">Use Hola fragmento de código adecuado para el idioma de saludo de la función.</span><span class="sxs-lookup"><span data-stu-id="42bb5-134">Use hello appropriate snippet for hello language of your function.</span></span>

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. <span data-ttu-id="42bb5-135">Seleccione **guardar** toosave cambios.</span><span class="sxs-lookup"><span data-stu-id="42bb5-135">Select **Save** toosave changes.</span></span>

<span data-ttu-id="42bb5-136">valor de Hello pasado toohello desencadenador HTTP está incluido en una cola de mensajes toohello agregada.</span><span class="sxs-lookup"><span data-stu-id="42bb5-136">hello value passed toohello HTTP trigger is included in a message added toohello queue.</span></span>
 
## <a name="test-hello-function"></a><span data-ttu-id="42bb5-137">Probar función hello</span><span class="sxs-lookup"><span data-stu-id="42bb5-137">Test hello function</span></span> 

1. <span data-ttu-id="42bb5-138">Una vez guardados los cambios de código de hello, seleccione **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="42bb5-138">After hello code changes are saved, select **Run**.</span></span> 

    ![Agregar una función de tooa de enlace de salida de cola almacenamiento Hola portal de Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. <span data-ttu-id="42bb5-140">Compruebe Hola registros toomake seguro de que la función hello se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="42bb5-140">Check hello logs toomake sure that hello function succeeded.</span></span> <span data-ttu-id="42bb5-141">Una cola nueva denominada **outqueue** hello en primer lugar se utiliza en tiempo de ejecución de funciones al enlace de salida de hello creada en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="42bb5-141">A new queue named **outqueue** is created in your Storage account by hello Functions runtime when hello output binding is first used.</span></span>

<span data-ttu-id="42bb5-142">A continuación, puede conectarse tooyour almacenamiento cuenta tooverify Hola nuevo de colas y mensajes de bienvenida del agregado tooit.</span><span class="sxs-lookup"><span data-stu-id="42bb5-142">Next, you can connect tooyour storage account tooverify hello new queue and hello message you added tooit.</span></span> 

## <a name="connect-toohello-queue"></a><span data-ttu-id="42bb5-143">Conectar toohello cola</span><span class="sxs-lookup"><span data-stu-id="42bb5-143">Connect toohello queue</span></span>

<span data-ttu-id="42bb5-144">Omitir Hola tres primeros pasos si ya ha instalado el Explorador de almacenamiento y conectado tooyour cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="42bb5-144">Skip hello first three steps if you have already installed Storage Explorer and connected it tooyour storage account.</span></span>    

1. <span data-ttu-id="42bb5-145">En la función, elija **integrar** hello nueva y **almacenamiento de cola de Azure** el enlace de salida, a continuación, expanda **documentación**.</span><span class="sxs-lookup"><span data-stu-id="42bb5-145">In your function, choose **Integrate** and hello new **Azure Queue storage** output binding, then expand **Documentation**.</span></span> <span data-ttu-id="42bb5-146">Copie el **Nombre de cuenta** y la **Clave de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="42bb5-146">Copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="42bb5-147">Use estas cuentas de almacenamiento de credenciales tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="42bb5-147">You use these credentials tooconnect toohello storage account.</span></span>
 
    ![Obtener las credenciales de conexión de cuenta de almacenamiento de Hola.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. <span data-ttu-id="42bb5-149">Ejecute hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) herramienta, seleccione Hola conectarse icono de hello izquierda, elija **utilizar un nombre de la cuenta de almacenamiento y la clave**y seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="42bb5-149">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select hello connect icon on hello left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![Ejecutar la herramienta de explorador de la cuenta de almacenamiento de Hola.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. <span data-ttu-id="42bb5-151">Hola pegar **nombre de la cuenta** y **clave de cuenta** del paso 1 en sus campos correspondientes y haga clic en **siguiente**, y **conectar**.</span><span class="sxs-lookup"><span data-stu-id="42bb5-151">Paste hello **Account name** and **Account key** from step 1 into their corresponding fields, then select **Next**, and **Connect**.</span></span> 
  
    ![Pegue las credenciales de almacenamiento de Hola y conectarse.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. <span data-ttu-id="42bb5-153">Expanda la cuenta de almacenamiento de hello adjunta, **colas** y compruebe que una cola con el nombre **myqueue elementos** existe.</span><span class="sxs-lookup"><span data-stu-id="42bb5-153">Expand hello attached storage account, expand **Queues** and verify that a queue named **myqueue-items** exists.</span></span> <span data-ttu-id="42bb5-154">También debería ver un mensaje ya se encuentran en la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="42bb5-154">You should also see a message already in hello queue.</span></span>  
 
    ![Cree una cola de almacenamiento.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="42bb5-156">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="42bb5-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="42bb5-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42bb5-157">Next steps</span></span>

<span data-ttu-id="42bb5-158">Ha agregado una función de salida enlace tooan existente.</span><span class="sxs-lookup"><span data-stu-id="42bb5-158">You have added an output binding tooan existing function.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="42bb5-159">Para obtener más información sobre el almacenamiento de tooQueue de enlace, vea [enlaces de la cola de almacenamiento de las funciones de Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="42bb5-159">For more information about binding tooQueue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 




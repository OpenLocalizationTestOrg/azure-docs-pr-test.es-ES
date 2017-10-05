---
title: "Crear una función en Azure desencadenada por mensajes en cola | Microsoft Docs"
description: "Use Azure Functions para crear una función sin servidor que se invoca mediante mensajes enviados a una cola de Azure Storage."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="ffb89-103">Crear una función desencadenada por Azure Queue Storage</span><span class="sxs-lookup"><span data-stu-id="ffb89-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="ffb89-104">Obtenga información sobre cómo crear una función que se desencadena cuando se envían mensajes a una cola de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ffb89-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![Vea el mensaje en los registros.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="ffb89-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ffb89-106">Prerequisites</span></span>

- <span data-ttu-id="ffb89-107">Descargue e instale el [Explorador de Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ffb89-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="ffb89-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb89-108">An Azure subscription.</span></span> <span data-ttu-id="ffb89-109">Si no tiene una, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="ffb89-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="ffb89-110">Creación de una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="ffb89-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="ffb89-112">Después, cree una función en la nueva Function App.</span><span class="sxs-lookup"><span data-stu-id="ffb89-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="ffb89-113">Creación de una función desencadenada por el servicio Queue</span><span class="sxs-lookup"><span data-stu-id="ffb89-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="ffb89-114">Expanda su instancia de Function App y haga clic en el botón **+**, que se encuentra junto a **Functions**.</span><span class="sxs-lookup"><span data-stu-id="ffb89-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="ffb89-115">Si se trata de la primera función de Function App, seleccione **Función personalizada**.</span><span class="sxs-lookup"><span data-stu-id="ffb89-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="ffb89-116">Se muestra el conjunto completo de plantillas de funciones.</span><span class="sxs-lookup"><span data-stu-id="ffb89-116">This displays the complete set of function templates.</span></span>

    ![Página de inicio rápido de Functions en Azure Portal](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="ffb89-118">Seleccione la plantilla **QueueTrigger** de idioma que desee y use la configuración que se especifica en la tabla.</span><span class="sxs-lookup"><span data-stu-id="ffb89-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![Cree la función desencadenada por la cola de almacenamiento.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="ffb89-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="ffb89-120">Setting</span></span> | <span data-ttu-id="ffb89-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="ffb89-121">Suggested value</span></span> | <span data-ttu-id="ffb89-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="ffb89-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="ffb89-123">**Nombre de la cola**</span><span class="sxs-lookup"><span data-stu-id="ffb89-123">**Queue name**</span></span>   | <span data-ttu-id="ffb89-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="ffb89-124">myqueue-items</span></span>    | <span data-ttu-id="ffb89-125">Nombre de la cola a la que se va a conectar en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ffb89-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="ffb89-126">**Conexión de cuenta de Storage**</span><span class="sxs-lookup"><span data-stu-id="ffb89-126">**Storage account connection**</span></span> | <span data-ttu-id="ffb89-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="ffb89-127">AzureWebJobStorage</span></span> | <span data-ttu-id="ffb89-128">Puede usar la conexión de cuenta de almacenamiento que ya usa la Function App o crear una.</span><span class="sxs-lookup"><span data-stu-id="ffb89-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="ffb89-129">**Asigne un nombre a la función**</span><span class="sxs-lookup"><span data-stu-id="ffb89-129">**Name your function**</span></span> | <span data-ttu-id="ffb89-130">Único en la Function App</span><span class="sxs-lookup"><span data-stu-id="ffb89-130">Unique in your function app</span></span> | <span data-ttu-id="ffb89-131">Nombre de la función desencadenada por la cola.</span><span class="sxs-lookup"><span data-stu-id="ffb89-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="ffb89-132">Haga clic en **Crear** para crear la función.</span><span class="sxs-lookup"><span data-stu-id="ffb89-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="ffb89-133">Después, conéctese a su cuenta de Azure Storage y cree la cola de almacenamiento **myqueue-items**.</span><span class="sxs-lookup"><span data-stu-id="ffb89-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="ffb89-134">Creación de la cola</span><span class="sxs-lookup"><span data-stu-id="ffb89-134">Create the queue</span></span>

1. <span data-ttu-id="ffb89-135">En la función, haga clic en **Integrar**, expanda **Documentación** y copie los dos valores de **Nombre de cuenta** y **Clave de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="ffb89-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="ffb89-136">Use estas credenciales para conectarse a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ffb89-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="ffb89-137">Si ya se ha conectado a la cuenta de almacenamiento, vaya al paso 4.</span><span class="sxs-lookup"><span data-stu-id="ffb89-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![Obtenga las credenciales de conexión de la cuenta de almacenamiento.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="ffb89-139">v</span><span class="sxs-lookup"><span data-stu-id="ffb89-139">v</span></span>

1. <span data-ttu-id="ffb89-140">Ejecute la herramienta [Explorador de Microsoft Azure Storage](http://storageexplorer.com/), haga clic en el icono de conexión situado a la izquierda, seleccione **Use a storage account name and key** (Usar el nombre y la clave de una cuenta de almacenamiento) y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ffb89-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Ejecute la herramienta Explorador de la cuenta de almacenamiento.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="ffb89-142">Escriba los valores de **Nombre de cuenta** y **Clave de cuenta** del paso 1, haga clic en **Siguiente** y, después, en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="ffb89-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Escriba las credenciales de almacenamiento y conéctese.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="ffb89-144">Expanda la cuenta de almacenamiento asociada, haga clic con el botón derecho en **Colas**, haga clic en **Crear cola**, escriba `myqueue-items` y, después, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="ffb89-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Cree una cola de almacenamiento.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="ffb89-146">Ahora que tiene una cola de almacenamiento, puede probar la función. Para ello, agregue un mensaje a la cola.</span><span class="sxs-lookup"><span data-stu-id="ffb89-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="ffb89-147">Prueba de la función</span><span class="sxs-lookup"><span data-stu-id="ffb89-147">Test the function</span></span>

1. <span data-ttu-id="ffb89-148">De nuevo en Azure Portal, vaya a la función. Expanda **Registros** en la parte inferior de la página y asegúrese de que el streaming de registros no está en pausa.</span><span class="sxs-lookup"><span data-stu-id="ffb89-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="ffb89-149">En el Explorador de almacenamiento, expanda la cuenta de almacenamiento, **Colas** y **myqueue-items** y, después, haga clic en **Agregar mensaje**.</span><span class="sxs-lookup"><span data-stu-id="ffb89-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Agregue un mensaje a la cola.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="ffb89-151">Escriba su mensaje "Hola mundo"</span><span class="sxs-lookup"><span data-stu-id="ffb89-151">Type your "Hello World!"</span></span> <span data-ttu-id="ffb89-152">en **Texto del mensaje** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ffb89-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="ffb89-153">Espere unos segundos y, después, vuelva a los registros de función para comprobar que se ha leído el mensaje nuevo de la cola.</span><span class="sxs-lookup"><span data-stu-id="ffb89-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![Vea el mensaje en los registros.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="ffb89-155">En el Explorador de almacenamiento, haga clic en **Actualizar** y compruebe que el mensaje se ha procesado y ya no está en la cola.</span><span class="sxs-lookup"><span data-stu-id="ffb89-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ffb89-156">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="ffb89-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="ffb89-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ffb89-157">Next steps</span></span>

<span data-ttu-id="ffb89-158">Ha creado una función que se ejecuta cuando se agrega un mensaje a una cola de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ffb89-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="ffb89-159">Para obtener más información sobre los desencadenadores de Queue Storage, vea [Enlaces de colas de Storage en Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="ffb89-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>
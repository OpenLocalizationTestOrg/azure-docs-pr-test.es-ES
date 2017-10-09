---
title: "una función en Azure desencadenado por la cola de mensajes aaaCreate | Documentos de Microsoft"
description: "Usar funciones de Azure toocreate una función sin servidor que se invoca con un mensaje había enviado tooan cola de almacenamiento de Azure."
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
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="5ff28-103">Crear una función desencadenada por Azure Queue Storage</span><span class="sxs-lookup"><span data-stu-id="5ff28-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="5ff28-104">Obtenga información acerca de cómo toocreate una función que se desencadena cuando hay mensajes enviado tooan cola de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff28-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Ver el mensaje en los registros de Hola.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="5ff28-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5ff28-106">Prerequisites</span></span>

- <span data-ttu-id="5ff28-107">Descargue e instale hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5ff28-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="5ff28-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff28-108">An Azure subscription.</span></span> <span data-ttu-id="5ff28-109">Si no tiene una, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="5ff28-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="5ff28-110">Creación de una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="5ff28-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="5ff28-112">A continuación, cree una función en la aplicación de hello nueva función.</span><span class="sxs-lookup"><span data-stu-id="5ff28-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="5ff28-113">Creación de una función desencadenada por el servicio Queue</span><span class="sxs-lookup"><span data-stu-id="5ff28-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="5ff28-114">Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**.</span><span class="sxs-lookup"><span data-stu-id="5ff28-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="5ff28-115">Si se trata de la primera función en la aplicación de la función de hello, seleccione **función personalizada**.</span><span class="sxs-lookup"><span data-stu-id="5ff28-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="5ff28-116">Esto muestra el conjunto completo de Hola de plantillas de función.</span><span class="sxs-lookup"><span data-stu-id="5ff28-116">This displays hello complete set of function templates.</span></span>

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="5ff28-118">Seleccione hello **QueueTrigger** plantilla de idioma que desee y usar la configuración como se especifica en la tabla de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="5ff28-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Crear función de cola activada de almacenamiento de Hola.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="5ff28-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="5ff28-120">Setting</span></span> | <span data-ttu-id="5ff28-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5ff28-121">Suggested value</span></span> | <span data-ttu-id="5ff28-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="5ff28-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="5ff28-123">**Nombre de la cola**</span><span class="sxs-lookup"><span data-stu-id="5ff28-123">**Queue name**</span></span>   | <span data-ttu-id="5ff28-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="5ff28-124">myqueue-items</span></span>    | <span data-ttu-id="5ff28-125">Nombre del programa Hola a la cola tooconnect tooin su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5ff28-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="5ff28-126">**Conexión de la cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="5ff28-126">**Storage account connection**</span></span> | <span data-ttu-id="5ff28-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="5ff28-127">AzureWebJobStorage</span></span> | <span data-ttu-id="5ff28-128">Puede usar la conexión de la cuenta de almacenamiento Hola ya está en uso por la aplicación de la función o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="5ff28-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="5ff28-129">**Asigne un nombre a la función**</span><span class="sxs-lookup"><span data-stu-id="5ff28-129">**Name your function**</span></span> | <span data-ttu-id="5ff28-130">Único en la Function App</span><span class="sxs-lookup"><span data-stu-id="5ff28-130">Unique in your function app</span></span> | <span data-ttu-id="5ff28-131">Nombre de la función desencadenada por la cola.</span><span class="sxs-lookup"><span data-stu-id="5ff28-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="5ff28-132">Haga clic en **crear** toocreate la función.</span><span class="sxs-lookup"><span data-stu-id="5ff28-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="5ff28-133">A continuación, conectarse a tooyour cuenta de almacenamiento de Azure y crear hello **myqueue elementos** cola de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5ff28-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="5ff28-134">Crear cola Hola</span><span class="sxs-lookup"><span data-stu-id="5ff28-134">Create hello queue</span></span>

1. <span data-ttu-id="5ff28-135">En la función, haga clic en **Integrar**, expanda **Documentación** y copie los dos valores de **Nombre de cuenta** y **Clave de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="5ff28-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="5ff28-136">Use estas cuentas de almacenamiento de credenciales tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="5ff28-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="5ff28-137">Si ya se ha conectado la cuenta de almacenamiento, omitir toostep 4.</span><span class="sxs-lookup"><span data-stu-id="5ff28-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Obtener las credenciales de conexión de cuenta de almacenamiento de Hola.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="5ff28-139">v</span><span class="sxs-lookup"><span data-stu-id="5ff28-139">v</span></span>

1. <span data-ttu-id="5ff28-140">Ejecute hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) de herramientas, haga clic en hello conectarse icono de hello izquierda, elija **utilizar un nombre de la cuenta de almacenamiento y la clave**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="5ff28-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Ejecutar la herramienta de explorador de la cuenta de almacenamiento de Hola.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="5ff28-142">Escriba Hola **nombre-cuenta** y **clave de cuenta** del paso 1, haga clic en **siguiente** y, a continuación, **conectar**.</span><span class="sxs-lookup"><span data-stu-id="5ff28-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Escriba las credenciales de almacenamiento de Hola y conectarse.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="5ff28-144">Expanda Hola adjunta cuenta de almacenamiento, haga clic en **colas**, haga clic en **Crear cola**, tipo `myqueue-items`, y, a continuación, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="5ff28-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Cree una cola de almacenamiento.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="5ff28-146">Ahora que tiene una cola de almacenamiento, puede probar función hello mediante la adición de una cola de toohello de mensajes.</span><span class="sxs-lookup"><span data-stu-id="5ff28-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="5ff28-147">Probar función hello</span><span class="sxs-lookup"><span data-stu-id="5ff28-147">Test hello function</span></span>

1. <span data-ttu-id="5ff28-148">Nuevo en hello portal de Azure, examinar tooyour función expanda hello **registros** final Hola de página de Hola y asegúrese de que dicho registro de transmisión por secuencias no está en pausa.</span><span class="sxs-lookup"><span data-stu-id="5ff28-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="5ff28-149">En el Explorador de almacenamiento, expanda la cuenta de almacenamiento, **Colas** y **myqueue-items** y, después, haga clic en **Agregar mensaje**.</span><span class="sxs-lookup"><span data-stu-id="5ff28-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Agregue una cola de toohello de mensajes.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="5ff28-151">Escriba su mensaje "Hola mundo"</span><span class="sxs-lookup"><span data-stu-id="5ff28-151">Type your "Hello World!"</span></span> <span data-ttu-id="5ff28-152">en **Texto del mensaje** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5ff28-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="5ff28-153">Espere unos segundos, a continuación, volver atrás tooyour registros de funciones y compruebe que ese nuevo mensaje Hola se ha leído desde la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="5ff28-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Ver el mensaje en los registros de Hola.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="5ff28-155">En el Explorador de almacenamiento, haga clic en **actualizar** y compruebe ese mensaje Hola se ha procesado y ya no está en cola Hola.</span><span class="sxs-lookup"><span data-stu-id="5ff28-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="5ff28-156">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="5ff28-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="5ff28-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5ff28-157">Next steps</span></span>

<span data-ttu-id="5ff28-158">Ha creado una función que se ejecuta cuando se agrega un mensaje tooa cola de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5ff28-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="5ff28-159">Para obtener más información sobre los desencadenadores de Queue Storage, vea [Enlaces de colas de Storage en Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="5ff28-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>
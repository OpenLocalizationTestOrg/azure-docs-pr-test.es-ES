---
title: "Creación de su primera función desde Azure Portal | Microsoft Docs"
description: "Obtenga información sobre cómo crear su primera función de Azure para su ejecución sin servidor mediante Azure Portal."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="12028-103">Creación de su primera función en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="12028-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="12028-104">Azure Functions permite ejecutar el código en un entorno sin servidor sin necesidad de crear una máquina virtual o publicar una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="12028-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="12028-105">En este tema, aprenderá a usar Functions para crear una función "Hola mundo" en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="12028-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Creación de una aplicación de función en Azure Portal](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="12028-107">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="12028-107">Log in to Azure</span></span>

<span data-ttu-id="12028-108">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="12028-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="12028-109">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="12028-109">Create a function app</span></span>

<span data-ttu-id="12028-110">Debe tener una Function App para hospedar la ejecución de las funciones.</span><span class="sxs-lookup"><span data-stu-id="12028-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="12028-111">Una Function App permite agrupar funciones como una unidad lógica para facilitar la administración, la implementación y el uso compartido de recursos.</span><span class="sxs-lookup"><span data-stu-id="12028-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="12028-112">Después, cree una función en la nueva Function App.</span><span class="sxs-lookup"><span data-stu-id="12028-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="12028-113"><a name="create-function"></a>Crear una función desencadenada por HTTP</span><span class="sxs-lookup"><span data-stu-id="12028-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="12028-114">Expanda la nueva Function App y haga clic en el botón **+** situado junto a **Funciones**.</span><span class="sxs-lookup"><span data-stu-id="12028-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="12028-115">En la página **Get started quickly** (Empiece a trabajar rápidamente), seleccione **Webhook y API**, **Elija un lenguaje** para la función y haga clic en **Crear esta función**.</span><span class="sxs-lookup"><span data-stu-id="12028-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Inicio rápido de funciones en Azure Portal.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="12028-117">Se crea una función en el lenguaje elegido mediante la plantilla para una función desencadenada por HTTP.</span><span class="sxs-lookup"><span data-stu-id="12028-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="12028-118">Puede ejecutar la función nueva mediante el envío de una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="12028-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="12028-119">Prueba de la función</span><span class="sxs-lookup"><span data-stu-id="12028-119">Test the function</span></span>

1. <span data-ttu-id="12028-120">En la nueva función, haga clic en **</> Get función URL** (</> Obtener URL de función), seleccione **default (Function key)** [predeterminada (tecla de función)] y, después, haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="12028-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Copiar la dirección URL de la función desde Azure Portal](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="12028-122">Pegue la dirección URL de la función en la barra de direcciones de su explorador.</span><span class="sxs-lookup"><span data-stu-id="12028-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="12028-123">Anexe la cadena de consulta `&name=<yourname>` a esta dirección URL y presione la tecla `Enter` en el teclado para ejecutar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="12028-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="12028-124">A continuación, se muestra un ejemplo de la respuesta devuelta por la función en el navegador Edge:</span><span class="sxs-lookup"><span data-stu-id="12028-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![Respuesta de la función en el explorador.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="12028-126">La dirección URL de la solicitud incluye una clave que, de forma predeterminada, es necesaria para tener acceso a la función a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="12028-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="12028-127">Cuando se ejecuta la función, se escribe información de seguimiento en los registros.</span><span class="sxs-lookup"><span data-stu-id="12028-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="12028-128">Para ver el resultado del seguimiento de la ejecución anterior, vuelva a la función en el portal y haga clic en la flecha hacia arriba que encontrará en la parte inferior de la pantalla para expandir **Registros**.</span><span class="sxs-lookup"><span data-stu-id="12028-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![Visor de registros de las funciones en Azure Portal.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="12028-130">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="12028-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="12028-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12028-131">Next steps</span></span>

<span data-ttu-id="12028-132">Ha creado una Function App con una función simple desencadenada por HTTP.</span><span class="sxs-lookup"><span data-stu-id="12028-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="12028-133">Para obtener más información, vea [Enlaces HTTP y webhook en Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="12028-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>




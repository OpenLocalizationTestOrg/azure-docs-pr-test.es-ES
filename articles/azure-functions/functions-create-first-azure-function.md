---
title: "aaaCreate la primera función de hello Portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate su primera Azure funcionar para la ejecución sin servidor con Hola portal de Azure."
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
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="f2772-103">Crear la primera función en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f2772-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="f2772-104">Las funciones de Azure permite ejecutar el código en un entorno sin servidor sin necesidad de toofirst crear una máquina virtual o publicar una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f2772-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="f2772-105">En este tema, aprenderá cómo toouse funciona toocreate una función de "Hola a todos" Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2772-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Crear aplicación de función en hello portal de Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="f2772-107">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="f2772-107">Log in tooAzure</span></span>

<span data-ttu-id="f2772-108">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f2772-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="f2772-109">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="f2772-109">Create a function app</span></span>

<span data-ttu-id="f2772-110">Debe tener una ejecución de la función aplicación toohost Hola de las funciones.</span><span class="sxs-lookup"><span data-stu-id="f2772-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="f2772-111">Una Function App permite agrupar funciones como una unidad lógica para facilitar la administración, la implementación y el uso compartido de recursos.</span><span class="sxs-lookup"><span data-stu-id="f2772-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="f2772-112">A continuación, cree una función en la aplicación de hello nueva función.</span><span class="sxs-lookup"><span data-stu-id="f2772-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="f2772-113"><a name="create-function"></a>Crear una función desencadenada por HTTP</span><span class="sxs-lookup"><span data-stu-id="f2772-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="f2772-114">Expanda la aplicación de función nueva, haga clic en hello  **+**  aparece al lado demasiado**funciones**.</span><span class="sxs-lookup"><span data-stu-id="f2772-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="f2772-115">Hola **empezar a trabajar rápidamente** página, seleccione **WebHook + API**, **elegir un idioma** de función y haga clic en **crear esta función** .</span><span class="sxs-lookup"><span data-stu-id="f2772-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Inicio rápido de funciones en hello portal de Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="f2772-117">Se crea una función en el lenguaje elegido con plantilla de Hola para una función HTTP que se desencadena.</span><span class="sxs-lookup"><span data-stu-id="f2772-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="f2772-118">Puede ejecutar la nueva función de hello enviando una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2772-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="f2772-119">Probar función hello</span><span class="sxs-lookup"><span data-stu-id="f2772-119">Test hello function</span></span>

1. <span data-ttu-id="f2772-120">En la nueva función, haga clic en **</> Get función URL** (</> Obtener URL de función), seleccione **default (Function key)** [predeterminada (tecla de función)] y, después, haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="f2772-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Copiar dirección URL de función hello de hello portal de Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="f2772-122">Pegue la dirección URL de función de hello en la barra de direcciones de su explorador.</span><span class="sxs-lookup"><span data-stu-id="f2772-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="f2772-123">Anexar la cadena de consulta de hello `&name=<yourname>` toothis dirección URL y presione hello `Enter` clave en la solicitud de hello tooexecute de teclado.</span><span class="sxs-lookup"><span data-stu-id="f2772-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="f2772-124">Hola te mostramos un ejemplo de respuesta de hello devuelto por la función hello en el Explorador de Edge hello:</span><span class="sxs-lookup"><span data-stu-id="f2772-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![Respuesta de la función en el Explorador de Hola.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="f2772-126">solicitud de Hello URL incluye una clave que es necesario, de forma predeterminada, tooaccess la función a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2772-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="f2772-127">Cuando se ejecuta la función, la información de seguimiento se escribe toohello registros.</span><span class="sxs-lookup"><span data-stu-id="f2772-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="f2772-128">resultado del seguimiento de hello toosee desde la ejecución anterior de hello, devolver tooyour función en el portal de Hola y haga clic en hello arriba final Hola de hello pantalla tooexpand **registros**.</span><span class="sxs-lookup"><span data-stu-id="f2772-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![Visor de registros de funciones de hello portal de Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="f2772-130">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="f2772-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="f2772-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2772-131">Next steps</span></span>

<span data-ttu-id="f2772-132">Ha creado una Function App con una función simple desencadenada por HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2772-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="f2772-133">Para obtener más información, vea [Enlaces HTTP y webhook en Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="f2772-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>




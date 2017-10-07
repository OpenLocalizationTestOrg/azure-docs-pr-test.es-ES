---
title: "una función en Azure desencadenado por un webhook de GitHub aaaCreate | Documentos de Microsoft"
description: "Utilice las funciones de Azure toocreate una función sin servidor que invoca un webhook de GitHub."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="72ab8-103">Creación de una función desencadenada por Webhook de GitHub</span><span class="sxs-lookup"><span data-stu-id="72ab8-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="72ab8-104">Obtenga información acerca de cómo toocreate una función que se desencadena por una solicitud de webhook HTTP con una carga específica de GitHub.</span><span class="sxs-lookup"><span data-stu-id="72ab8-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Github Webhook desencadenó función Hola portal de Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="72ab8-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="72ab8-106">Prerequisites</span></span>

+ <span data-ttu-id="72ab8-107">Una cuenta de GitHub con un proyecto como mínimo.</span><span class="sxs-lookup"><span data-stu-id="72ab8-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="72ab8-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="72ab8-108">An Azure subscription.</span></span> <span data-ttu-id="72ab8-109">Si no tiene una, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="72ab8-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="72ab8-110">Creación de una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="72ab8-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="72ab8-112">A continuación, cree una función en la aplicación de hello nueva función.</span><span class="sxs-lookup"><span data-stu-id="72ab8-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="72ab8-113">Crear una función desencadenada de webhook de GitHub</span><span class="sxs-lookup"><span data-stu-id="72ab8-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="72ab8-114">Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="72ab8-115">Si se trata de la primera función en la aplicación de la función de hello, seleccione **función personalizada**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="72ab8-116">Esto muestra el conjunto completo de Hola de plantillas de función.</span><span class="sxs-lookup"><span data-stu-id="72ab8-116">This displays hello complete set of function templates.</span></span>

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="72ab8-118">Seleccione hello **GitHub WebHook** plantilla para el idioma que desee.</span><span class="sxs-lookup"><span data-stu-id="72ab8-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="72ab8-119">Asigne un **nombre a la función** y seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-119">**Name your function**, then select **Create**.</span></span>

     ![Crear una función de webhook desencadenada GitHub Hola portal de Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="72ab8-121">En la nueva función, haga clic en **<> / Get función URL**, a continuación, copiar y guardar los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="72ab8-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="72ab8-122">Hola lo mismo para **<> / GitHub obtener secreto**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="72ab8-123">Use estos webhook de hello valores tooconfigure en GitHub.</span><span class="sxs-lookup"><span data-stu-id="72ab8-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Revise el código de la función hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="72ab8-125">A continuación, va a crear un webhook en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="72ab8-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="72ab8-126">Configurar hello webhook</span><span class="sxs-lookup"><span data-stu-id="72ab8-126">Configure hello webhook</span></span>

1. <span data-ttu-id="72ab8-127">En GitHub, vaya repositorio tooa perteneciente al usuario.</span><span class="sxs-lookup"><span data-stu-id="72ab8-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="72ab8-128">También puede utilizar los repositorios bifurcados.</span><span class="sxs-lookup"><span data-stu-id="72ab8-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="72ab8-129">Si necesita toofork un repositorio, use <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="72ab8-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="72ab8-130">Haga clic en **Configuración**, después en **Webhooks** y, finalmente, en **Agregar Webhook**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Agregar un webhook de GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="72ab8-132">Usar la configuración de acuerdo con lo especificado en la tabla de Hola, a continuación, haga clic en **agregar webhook**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Establecer la dirección URL del webhook Hola y el secreto](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="72ab8-134">Configuración</span><span class="sxs-lookup"><span data-stu-id="72ab8-134">Setting</span></span> | <span data-ttu-id="72ab8-135">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="72ab8-135">Suggested value</span></span> | <span data-ttu-id="72ab8-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="72ab8-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="72ab8-137">**Dirección URL de carga**</span><span class="sxs-lookup"><span data-stu-id="72ab8-137">**Payload URL**</span></span> | <span data-ttu-id="72ab8-138">Valor copiado</span><span class="sxs-lookup"><span data-stu-id="72ab8-138">Copied value</span></span> | <span data-ttu-id="72ab8-139">Usar valor Hola devuelto por **<> / Get función URL**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="72ab8-140">**Secreto**</span><span class="sxs-lookup"><span data-stu-id="72ab8-140">**Secret**</span></span>   | <span data-ttu-id="72ab8-141">Valor copiado</span><span class="sxs-lookup"><span data-stu-id="72ab8-141">Copied value</span></span> | <span data-ttu-id="72ab8-142">Usar valor Hola devuelto por **<> / GitHub obtener secreto**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="72ab8-143">**Tipo de contenido**</span><span class="sxs-lookup"><span data-stu-id="72ab8-143">**Content type**</span></span> | <span data-ttu-id="72ab8-144">application/json</span><span class="sxs-lookup"><span data-stu-id="72ab8-144">application/json</span></span> | <span data-ttu-id="72ab8-145">función Hello espera una carga JSON.</span><span class="sxs-lookup"><span data-stu-id="72ab8-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="72ab8-146">Desencadenadores de eventos</span><span class="sxs-lookup"><span data-stu-id="72ab8-146">Event triggers</span></span> | <span data-ttu-id="72ab8-147">Dejarme seleccionar eventos individuales</span><span class="sxs-lookup"><span data-stu-id="72ab8-147">Let me select individual events</span></span> | <span data-ttu-id="72ab8-148">Sólo queremos tootrigger en los eventos de comentario del problema.</span><span class="sxs-lookup"><span data-stu-id="72ab8-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="72ab8-149">Comentario de problema</span><span class="sxs-lookup"><span data-stu-id="72ab8-149">Issue comment</span></span> |  |

<span data-ttu-id="72ab8-150">Ahora, Hola webhook es tootrigger configurado la función cuando se agrega un nuevo comentario de problema.</span><span class="sxs-lookup"><span data-stu-id="72ab8-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="72ab8-151">Probar función hello</span><span class="sxs-lookup"><span data-stu-id="72ab8-151">Test hello function</span></span>

1. <span data-ttu-id="72ab8-152">En el repositorio de GitHub, abra hello **problemas** ficha en una nueva ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="72ab8-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="72ab8-153">En la ventana nueva hello, haga clic en **problema nuevo**, escriba un título y, a continuación, haga clic en **Enviar nuevo problema**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="72ab8-154">Problema de hello, escriba un comentario y haga clic en **comentario**.</span><span class="sxs-lookup"><span data-stu-id="72ab8-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![Agregue un comentario de problema de GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="72ab8-156">Retroceda toohello portal y ver los registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="72ab8-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="72ab8-157">Debería ver una entrada de seguimiento con el texto del comentario nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="72ab8-157">You should see a trace entry with hello new comment text.</span></span>

     ![Ver el texto del comentario de hello en los registros de Hola.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="72ab8-159">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="72ab8-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="72ab8-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72ab8-160">Next steps</span></span>

<span data-ttu-id="72ab8-161">Ha creado una función que se ejecuta cuando se recibe una solicitud de un webhook de GitHub.</span><span class="sxs-lookup"><span data-stu-id="72ab8-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="72ab8-162">Para más información sobre los desencadenadores de webhook, consulte [Enlaces HTTP y webhook en Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="72ab8-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>

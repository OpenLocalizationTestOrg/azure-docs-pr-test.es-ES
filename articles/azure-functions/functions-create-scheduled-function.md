---
title: "aaaCreate una función que se ejecuta según una programación en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una función de Azure que se ejecuta según una programación que usted defina."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="1a2cf-103">Cree una función en Azure que se desencadena mediante un temporizador</span><span class="sxs-lookup"><span data-stu-id="1a2cf-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="1a2cf-104">Obtenga información acerca de cómo toouse funciones de Azure toocreate una función que se ejecuta según una programación que usted defina.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Crear aplicación de función en hello portal de Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="1a2cf-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1a2cf-106">Prerequisites</span></span>

<span data-ttu-id="1a2cf-107">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="1a2cf-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="1a2cf-108">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="1a2cf-109">Creación de una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="1a2cf-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="1a2cf-111">A continuación, cree una función en la aplicación de hello nueva función.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="1a2cf-112">Creación de una función desencadenada por un temporizador</span><span class="sxs-lookup"><span data-stu-id="1a2cf-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="1a2cf-113">Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="1a2cf-114">Si se trata de la primera función en la aplicación de la función de hello, seleccione **función personalizada**.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="1a2cf-115">Esto muestra el conjunto completo de Hola de plantillas de función.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-115">This displays hello complete set of function templates.</span></span>

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="1a2cf-117">Seleccione hello **TimerTrigger** plantilla para el idioma que desee.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="1a2cf-118">A continuación, use configuración de hello como se especifica en la tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="1a2cf-118">Then use hello settings as specified in hello table:</span></span>

    ![Crear una función de temporizador desencadenada Hola portal de Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="1a2cf-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="1a2cf-120">Setting</span></span> | <span data-ttu-id="1a2cf-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="1a2cf-121">Suggested value</span></span> | <span data-ttu-id="1a2cf-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a2cf-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="1a2cf-123">**Asigne un nombre a la función**</span><span class="sxs-lookup"><span data-stu-id="1a2cf-123">**Name your function**</span></span> | <span data-ttu-id="1a2cf-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="1a2cf-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="1a2cf-125">Define el nombre de saludo de la función de temporizador desencadenada.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="1a2cf-126">**[Programación](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="1a2cf-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="1a2cf-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="1a2cf-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="1a2cf-128">Un campo de seis [expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que programa la función toorun cada minuto.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="1a2cf-129">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-129">Click **Create**.</span></span> <span data-ttu-id="1a2cf-130">Se crea una función en el lenguaje elegido que se ejecuta cada minuto.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="1a2cf-131">Ver la información de seguimiento escrito registros toohello para comprobar la ejecución.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![Visor de registros de funciones de hello portal de Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="1a2cf-133">Ahora, puede cambiar la programación de la función de Hola para que se ejecute con menos frecuencia, por ejemplo, una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="1a2cf-134">Programación de temporizador de actualización Hola</span><span class="sxs-lookup"><span data-stu-id="1a2cf-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="1a2cf-135">Expanda la función y haga clic en **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="1a2cf-136">Esto es donde definir la entrada y salida enlaces para la función y establecer programación Hola.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="1a2cf-137">Escriba el nuevo valor de **Programación** `0 0 */1 * * *` y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Funciones de actualización de programación de temporizador en hello portal de Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="1a2cf-139">Ahora tiene una función que se ejecuta una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="1a2cf-140">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="1a2cf-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="1a2cf-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a2cf-141">Next steps</span></span>

<span data-ttu-id="1a2cf-142">Ha creado una función que se ejecuta según una programación.</span><span class="sxs-lookup"><span data-stu-id="1a2cf-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="1a2cf-143">Para obtener más información sobre los desencadenadores de temporizador, vea [Programación de la ejecución de código con Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="1a2cf-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>
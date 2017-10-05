---
title: "Crear una función que se ejecuta según una programación en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo crear una función de Azure que se ejecuta según la programación que usted defina."
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
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="096d8-103">Cree una función en Azure que se desencadena mediante un temporizador</span><span class="sxs-lookup"><span data-stu-id="096d8-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="096d8-104">Obtenga información sobre cómo usar Azure Functions para crear una función que se ejecuta según la programación que usted defina.</span><span class="sxs-lookup"><span data-stu-id="096d8-104">Learn how to use Azure Functions to create a function that runs based a schedule that you define.</span></span>

![Creación de una aplicación de función en Azure Portal](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="096d8-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="096d8-106">Prerequisites</span></span>

<span data-ttu-id="096d8-107">Para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="096d8-107">To complete this tutorial:</span></span>

+ <span data-ttu-id="096d8-108">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="096d8-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="096d8-109">Creación de una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="096d8-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="096d8-111">Después, cree una función en la nueva Function App.</span><span class="sxs-lookup"><span data-stu-id="096d8-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="096d8-112">Creación de una función desencadenada por un temporizador</span><span class="sxs-lookup"><span data-stu-id="096d8-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="096d8-113">Expanda su instancia de Function App y haga clic en el botón **+**, que se encuentra junto a **Functions**.</span><span class="sxs-lookup"><span data-stu-id="096d8-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="096d8-114">Si se trata de la primera función de Function App, seleccione **Función personalizada**.</span><span class="sxs-lookup"><span data-stu-id="096d8-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="096d8-115">Se muestra el conjunto completo de plantillas de funciones.</span><span class="sxs-lookup"><span data-stu-id="096d8-115">This displays the complete set of function templates.</span></span>

    ![Página de inicio rápido de Functions en Azure Portal](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="096d8-117">Seleccione la plantilla **TimerTrigger** del idioma que desee.</span><span class="sxs-lookup"><span data-stu-id="096d8-117">Select the **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="096d8-118">Luego, use la configuración que se especifica en la tabla:</span><span class="sxs-lookup"><span data-stu-id="096d8-118">Then use the settings as specified in the table:</span></span>

    ![Creación de una función desencadenada mediante un temporizador en Azure Portal.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="096d8-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="096d8-120">Setting</span></span> | <span data-ttu-id="096d8-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="096d8-121">Suggested value</span></span> | <span data-ttu-id="096d8-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="096d8-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="096d8-123">**Asigne un nombre a la función**</span><span class="sxs-lookup"><span data-stu-id="096d8-123">**Name your function**</span></span> | <span data-ttu-id="096d8-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="096d8-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="096d8-125">Define el nombre de la función desencadenada por el temporizador.</span><span class="sxs-lookup"><span data-stu-id="096d8-125">Defines the name of your timer triggered function.</span></span> |
    | <span data-ttu-id="096d8-126">**[Programación](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="096d8-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="096d8-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="096d8-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="096d8-128">[Expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) de seis campos que programa la función para que se ejecute cada minuto.</span><span class="sxs-lookup"><span data-stu-id="096d8-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function to run every minute.</span></span> |

2. <span data-ttu-id="096d8-129">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="096d8-129">Click **Create**.</span></span> <span data-ttu-id="096d8-130">Se crea una función en el lenguaje elegido que se ejecuta cada minuto.</span><span class="sxs-lookup"><span data-stu-id="096d8-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="096d8-131">Vea la información de seguimiento que se escribe en los registros para comprobar la ejecución.</span><span class="sxs-lookup"><span data-stu-id="096d8-131">Verify execution by viewing trace information written to the logs.</span></span>

    ![Visor de registros de las funciones en Azure Portal.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="096d8-133">Ahora puede cambiar la programación de la función para que se ejecute con menos frecuencia, por ejemplo, una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="096d8-133">Now, you can change the function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-the-timer-schedule"></a><span data-ttu-id="096d8-134">Actualizar la programación del temporizador</span><span class="sxs-lookup"><span data-stu-id="096d8-134">Update the timer schedule</span></span>

1. <span data-ttu-id="096d8-135">Expanda la función y haga clic en **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="096d8-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="096d8-136">Aquí es donde se definen los enlaces de entrada y salida de la función y se establece la programación.</span><span class="sxs-lookup"><span data-stu-id="096d8-136">This is where you define input and output bindings for your function and also set the schedule.</span></span> 

2. <span data-ttu-id="096d8-137">Escriba el nuevo valor de **Programación** `0 0 */1 * * *` y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="096d8-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Programación del temporizador de actualización de funciones en Azure Portal.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="096d8-139">Ahora tiene una función que se ejecuta una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="096d8-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="096d8-140">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="096d8-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="096d8-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="096d8-141">Next steps</span></span>

<span data-ttu-id="096d8-142">Ha creado una función que se ejecuta según una programación.</span><span class="sxs-lookup"><span data-stu-id="096d8-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="096d8-143">Para obtener más información sobre los desencadenadores de temporizador, vea [Programación de la ejecución de código con Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="096d8-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>
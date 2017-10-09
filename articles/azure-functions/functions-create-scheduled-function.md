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
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Cree una función en Azure que se desencadena mediante un temporizador

Obtenga información acerca de cómo toouse funciones de Azure toocreate una función que se ejecuta según una programación que usted defina.

![Crear aplicación de función en hello portal de Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

+ Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creación de una Function App de Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

A continuación, cree una función en la aplicación de hello nueva función.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Creación de una función desencadenada por un temporizador

1. Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**. Si se trata de la primera función en la aplicación de la función de hello, seleccione **función personalizada**. Esto muestra el conjunto completo de Hola de plantillas de función.

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. Seleccione hello **TimerTrigger** plantilla para el idioma que desee. A continuación, use configuración de hello como se especifica en la tabla de hello:

    ![Crear una función de temporizador desencadenada Hola portal de Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Configuración | Valor sugerido | Descripción |
    |---|---|---|
    | **Asigne un nombre a la función** | TimerTriggerCSharp1 | Define el nombre de saludo de la función de temporizador desencadenada. |
    | **[Programación](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Un campo de seis [expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que programa la función toorun cada minuto. |

2. Haga clic en **Crear**. Se crea una función en el lenguaje elegido que se ejecuta cada minuto.

3. Ver la información de seguimiento escrito registros toohello para comprobar la ejecución.

    ![Visor de registros de funciones de hello portal de Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Ahora, puede cambiar la programación de la función de Hola para que se ejecute con menos frecuencia, por ejemplo, una vez cada hora. 

## <a name="update-hello-timer-schedule"></a>Programación de temporizador de actualización Hola

1. Expanda la función y haga clic en **Integrar**. Esto es donde definir la entrada y salida enlaces para la función y establecer programación Hola. 

2. Escriba el nuevo valor de **Programación** `0 0 */1 * * *` y, después, haga clic en **Guardar**.  

![Funciones de actualización de programación de temporizador en hello portal de Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

Ahora tiene una función que se ejecuta una vez cada hora. 

## <a name="clean-up-resources"></a>Limpieza de recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Pasos siguientes

Ha creado una función que se ejecuta según una programación.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obtener más información sobre los desencadenadores de temporizador, vea [Programación de la ejecución de código con Azure Functions](functions-bindings-timer.md).
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
# <a name="create-your-first-function-in-hello-azure-portal"></a>Crear la primera función en hello portal de Azure

Las funciones de Azure permite ejecutar el código en un entorno sin servidor sin necesidad de toofirst crear una máquina virtual o publicar una aplicación web. En este tema, aprenderá cómo toouse funciona toocreate una función de "Hola a todos" Hola portal de Azure.

![Crear aplicación de función en hello portal de Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Creación de una aplicación de función

Debe tener una ejecución de la función aplicación toohost Hola de las funciones. Una Function App permite agrupar funciones como una unidad lógica para facilitar la administración, la implementación y el uso compartido de recursos. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

A continuación, cree una función en la aplicación de hello nueva función.

## <a name="create-function"></a>Crear una función desencadenada por HTTP

1. Expanda la aplicación de función nueva, haga clic en hello  **+**  aparece al lado demasiado**funciones**.

2.  Hola **empezar a trabajar rápidamente** página, seleccione **WebHook + API**, **elegir un idioma** de función y haga clic en **crear esta función** . 
   
    ![Inicio rápido de funciones en hello portal de Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Se crea una función en el lenguaje elegido con plantilla de Hola para una función HTTP que se desencadena. Puede ejecutar la nueva función de hello enviando una solicitud HTTP.

## <a name="test-hello-function"></a>Probar función hello

1. En la nueva función, haga clic en **</> Get función URL** (</> Obtener URL de función), seleccione **default (Function key)** [predeterminada (tecla de función)] y, después, haga clic en **Copiar**. 

    ![Copiar dirección URL de función hello de hello portal de Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Pegue la dirección URL de función de hello en la barra de direcciones de su explorador. Anexar la cadena de consulta de hello `&name=<yourname>` toothis dirección URL y presione hello `Enter` clave en la solicitud de hello tooexecute de teclado. Hola te mostramos un ejemplo de respuesta de hello devuelto por la función hello en el Explorador de Edge hello:

    ![Respuesta de la función en el Explorador de Hola.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    solicitud de Hello URL incluye una clave que es necesario, de forma predeterminada, tooaccess la función a través de HTTP.   

3. Cuando se ejecuta la función, la información de seguimiento se escribe toohello registros. resultado del seguimiento de hello toosee desde la ejecución anterior de hello, devolver tooyour función en el portal de Hola y haga clic en hello arriba final Hola de hello pantalla tooexpand **registros**. 

   ![Visor de registros de funciones de hello portal de Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Limpieza de recursos

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Pasos siguientes

Ha creado una Function App con una función simple desencadenada por HTTP.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obtener más información, vea [Enlaces HTTP y webhook en Azure Functions](functions-bindings-http-webhook.md).




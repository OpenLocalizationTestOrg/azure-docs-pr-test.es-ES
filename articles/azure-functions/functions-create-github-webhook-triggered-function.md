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
# <a name="create-a-function-triggered-by-a-github-webhook"></a>Creación de una función desencadenada por Webhook de GitHub

Obtenga información acerca de cómo toocreate una función que se desencadena por una solicitud de webhook HTTP con una carga específica de GitHub.

![Github Webhook desencadenó función Hola portal de Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Requisitos previos

+ Una cuenta de GitHub con un proyecto como mínimo.
+ Una suscripción de Azure. Si no tiene una, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creación de una Function App de Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

A continuación, cree una función en la aplicación de hello nueva función.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>Crear una función desencadenada de webhook de GitHub

1. Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**. Si se trata de la primera función en la aplicación de la función de hello, seleccione **función personalizada**. Esto muestra el conjunto completo de Hola de plantillas de función.

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Seleccione hello **GitHub WebHook** plantilla para el idioma que desee. Asigne un **nombre a la función** y seleccione **Crear**.

     ![Crear una función de webhook desencadenada GitHub Hola portal de Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. En la nueva función, haga clic en **<> / Get función URL**, a continuación, copiar y guardar los valores de hello. Hola lo mismo para **<> / GitHub obtener secreto**. Use estos webhook de hello valores tooconfigure en GitHub.

    ![Revise el código de la función hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

A continuación, va a crear un webhook en el repositorio de GitHub.

## <a name="configure-hello-webhook"></a>Configurar hello webhook

1. En GitHub, vaya repositorio tooa perteneciente al usuario. También puede utilizar los repositorios bifurcados. Si necesita toofork un repositorio, use <https://github.com/Azure-Samples/functions-quickstart>.

1. Haga clic en **Configuración**, después en **Webhooks** y, finalmente, en **Agregar Webhook**.

    ![Agregar un webhook de GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Usar la configuración de acuerdo con lo especificado en la tabla de Hola, a continuación, haga clic en **agregar webhook**.

    ![Establecer la dirección URL del webhook Hola y el secreto](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Configuración | Valor sugerido | Descripción |
|---|---|---|
| **Dirección URL de carga** | Valor copiado | Usar valor Hola devuelto por **<> / Get función URL**. |
| **Secreto**   | Valor copiado | Usar valor Hola devuelto por **<> / GitHub obtener secreto**. |
| **Tipo de contenido** | application/json | función Hello espera una carga JSON. |
| Desencadenadores de eventos | Dejarme seleccionar eventos individuales | Sólo queremos tootrigger en los eventos de comentario del problema.  |
| | Comentario de problema |  |

Ahora, Hola webhook es tootrigger configurado la función cuando se agrega un nuevo comentario de problema.

## <a name="test-hello-function"></a>Probar función hello

1. En el repositorio de GitHub, abra hello **problemas** ficha en una nueva ventana del explorador.

1. En la ventana nueva hello, haga clic en **problema nuevo**, escriba un título y, a continuación, haga clic en **Enviar nuevo problema**.

1. Problema de hello, escriba un comentario y haga clic en **comentario**.

    ![Agregue un comentario de problema de GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Retroceda toohello portal y ver los registros de Hola. Debería ver una entrada de seguimiento con el texto del comentario nuevo Hola.

     ![Ver el texto del comentario de hello en los registros de Hola.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Limpieza de recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Pasos siguientes

Ha creado una función que se ejecuta cuando se recibe una solicitud de un webhook de GitHub.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para más información sobre los desencadenadores de webhook, consulte [Enlaces HTTP y webhook en Azure Functions](functions-bindings-http-webhook.md).

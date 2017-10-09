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
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>Crear una función desencadenada por Azure Queue Storage

Obtenga información acerca de cómo toocreate una función que se desencadena cuando hay mensajes enviado tooan cola de almacenamiento de Azure.

![Ver el mensaje en los registros de Hola.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Requisitos previos

- Descargue e instale hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

- Una suscripción de Azure. Si no tiene una, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creación de una Function App de Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

A continuación, cree una función en la aplicación de hello nueva función.

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>Creación de una función desencadenada por el servicio Queue

1. Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**. Si se trata de la primera función en la aplicación de la función de hello, seleccione **función personalizada**. Esto muestra el conjunto completo de Hola de plantillas de función.

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. Seleccione hello **QueueTrigger** plantilla de idioma que desee y usar la configuración como se especifica en la tabla de Hola Hola.

    ![Crear función de cola activada de almacenamiento de Hola.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | Configuración | Valor sugerido | Descripción |
    |---|---|---|
    | **Nombre de la cola**   | myqueue-items    | Nombre del programa Hola a la cola tooconnect tooin su cuenta de almacenamiento. |
    | **Conexión de la cuenta de almacenamiento** | AzureWebJobStorage | Puede usar la conexión de la cuenta de almacenamiento Hola ya está en uso por la aplicación de la función o cree uno nuevo.  |
    | **Asigne un nombre a la función** | Único en la Function App | Nombre de la función desencadenada por la cola. |

3. Haga clic en **crear** toocreate la función.

A continuación, conectarse a tooyour cuenta de almacenamiento de Azure y crear hello **myqueue elementos** cola de almacenamiento.

## <a name="create-hello-queue"></a>Crear cola Hola

1. En la función, haga clic en **Integrar**, expanda **Documentación** y copie los dos valores de **Nombre de cuenta** y **Clave de cuenta**. Use estas cuentas de almacenamiento de credenciales tooconnect toohello. Si ya se ha conectado la cuenta de almacenamiento, omitir toostep 4.

    ![Obtener las credenciales de conexión de cuenta de almacenamiento de Hola.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. Ejecute hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) de herramientas, haga clic en hello conectarse icono de hello izquierda, elija **utilizar un nombre de la cuenta de almacenamiento y la clave**y haga clic en **siguiente**.

    ![Ejecutar la herramienta de explorador de la cuenta de almacenamiento de Hola.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. Escriba Hola **nombre-cuenta** y **clave de cuenta** del paso 1, haga clic en **siguiente** y, a continuación, **conectar**.

    ![Escriba las credenciales de almacenamiento de Hola y conectarse.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. Expanda Hola adjunta cuenta de almacenamiento, haga clic en **colas**, haga clic en **Crear cola**, tipo `myqueue-items`, y, a continuación, presione ENTRAR.

    ![Cree una cola de almacenamiento.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

Ahora que tiene una cola de almacenamiento, puede probar función hello mediante la adición de una cola de toohello de mensajes.

## <a name="test-hello-function"></a>Probar función hello

1. Nuevo en hello portal de Azure, examinar tooyour función expanda hello **registros** final Hola de página de Hola y asegúrese de que dicho registro de transmisión por secuencias no está en pausa.

1. En el Explorador de almacenamiento, expanda la cuenta de almacenamiento, **Colas** y **myqueue-items** y, después, haga clic en **Agregar mensaje**.

    ![Agregue una cola de toohello de mensajes.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. Escriba su mensaje "Hola mundo" en **Texto del mensaje** y haga clic en **Aceptar**.

1. Espere unos segundos, a continuación, volver atrás tooyour registros de funciones y compruebe que ese nuevo mensaje Hola se ha leído desde la cola de Hola.

    ![Ver el mensaje en los registros de Hola.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. En el Explorador de almacenamiento, haga clic en **actualizar** y compruebe ese mensaje Hola se ha procesado y ya no está en cola Hola.

## <a name="clean-up-resources"></a>Limpieza de recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Pasos siguientes

Ha creado una función que se ejecuta cuando se agrega un mensaje tooa cola de almacenamiento.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obtener más información sobre los desencadenadores de Queue Storage, vea [Enlaces de colas de Storage en Azure Functions](functions-bindings-storage-queue.md).
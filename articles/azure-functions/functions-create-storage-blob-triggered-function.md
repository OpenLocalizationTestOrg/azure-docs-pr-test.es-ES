---
title: "aaaCreate una función en desencadenado por almacenamiento de blobs de Azure | Documentos de Microsoft"
description: "Usar funciones de Azure toocreate una función sin servidor invocada por elementos había agregado tooAzure el almacenamiento de blobs."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Crear una función desencadenada por Azure Blob Storage

Obtenga información acerca de cómo toocreate una función que se desencadena cuando los archivos están cargados tooor actualizado en el almacenamiento de blobs de Azure.

![Ver el mensaje en los registros de Hola.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Requisitos previos

+ Descargue e instale hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).
+ Una suscripción de Azure. Si no tiene una, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creación de una Function App de Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App creada correctamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

A continuación, cree una función en la aplicación de hello nueva función.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Creación de una función desencadenada por Blob Storage

1. Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**. Si se trata de la primera función en la aplicación de la función de hello, seleccione **función personalizada**. Esto muestra el conjunto completo de Hola de plantillas de función.

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. Seleccione hello **BlobTrigger** plantilla de idioma que desee y usar la configuración como se especifica en la tabla de Hola Hola.

    ![Crear función de almacenamiento desencadenada Blob Hola.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | Configuración | Valor sugerido | Descripción |
    |---|---|---|
    | **Ruta de acceso**   | mycontainer/{name}    | Ubicación de Blob Storage que se está supervisando. nombre de archivo de Hola de blob de Hola se pasa en el enlace de hello como hello _nombre_ parámetro.  |
    | **Conexión de la cuenta de almacenamiento** | AzureWebJobStorage | Puede usar la conexión de la cuenta de almacenamiento Hola ya está en uso por la aplicación de la función o cree uno nuevo.  |
    | **Asigne un nombre a la función** | Único en la Function App | Nombre de la función desencadenada por este blob. |

3. Haga clic en **crear** toocreate la función.

A continuación, conectarse a tooyour cuenta de almacenamiento de Azure y crear hello **mycontainer** contenedor.

## <a name="create-hello-container"></a>Crear contenedor de Hola

1. En la función, haga clic en **Integrar**, expanda **Documentación** y copie los dos valores de **Nombre de cuenta** y **Clave de cuenta**. Use estas cuentas de almacenamiento de credenciales tooconnect toohello. Si ya se ha conectado la cuenta de almacenamiento, omitir toostep 4.

    ![Obtener las credenciales de conexión de cuenta de almacenamiento de Hola.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Ejecute hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) de herramientas, haga clic en hello conectarse icono de hello izquierda, elija **utilizar un nombre de la cuenta de almacenamiento y la clave**y haga clic en **siguiente**.

    ![Ejecutar la herramienta de explorador de la cuenta de almacenamiento de Hola.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Escriba Hola **nombre-cuenta** y **clave de cuenta** del paso 1, haga clic en **siguiente** y, a continuación, **conectar**. 

    ![Escriba las credenciales de almacenamiento de Hola y conectarse.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Expanda Hola adjunta cuenta de almacenamiento, haga clic en **contenedores de blobs**, haga clic en **crear contenedor de blob**, tipo `mycontainer`, y, a continuación, presione ENTRAR.

    ![Cree una cola de almacenamiento.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Ahora que tiene un contenedor de blobs, puede probar función hello mediante la carga de un contenedor de toohello de archivo.

## <a name="test-hello-function"></a>Probar función hello

1. Nuevo en hello portal de Azure, examinar tooyour función expanda hello **registros** final Hola de página de Hola y asegúrese de que dicho registro de transmisión por secuencias no está en pausa.

1. En el Explorador de almacenamiento, expanda la cuenta de almacenamiento, **Contenedores de blobs** y **mycontainer**. Haga clic en **Cargar** y en **Cargar archivos…**

    ![Cargar un contenedor de blobs de toohello de archivo.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. Hola **cargar archivos** diálogo cuadro, haga clic en hello **archivos** campo. Examinar el archivo tooa en el equipo local, como un archivo de imagen, selecciónelo y haga clic en **abiertos** y, a continuación, **cargar**.

1. Volver atrás tooyour función registros y compruebe que se ha leído el blob Hola.

   ![Ver el mensaje en los registros de Hola.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > Cuando se ejecuta la aplicación de la función en el plan de consumo de hello predeterminado, puede haber un retraso de seguridad tooseveral minutos entre blob que se agregaron o actualizaron de Hola y Hola función va a desencadenar. Si necesita una latencia baja en las funciones desencadenadas por el blob, considere la posibilidad de ejecutar la Function App en un plan de App Service.

## <a name="clean-up-resources"></a>Limpieza de recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Pasos siguientes

Ha creado una función que se ejecuta cuando un blob se agrega tooor actualizado en el almacenamiento de blobs. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obtener más información sobre los desencadenadores de Blob Storage, vea [Enlaces de Blob Storage en Azure Functions](functions-bindings-storage-blob.md).

---
title: "una función en Azure desencadenado por la cola de mensajes aaaCreate | Documentos de Microsoft"
description: "Usar funciones de Azure toocreate una función sin servidor que se invoca con un mensaje había enviado tooan cola de almacenamiento de Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a>Agregar la cola de mensajes tooan almacenamiento de Azure mediante funciones

En las funciones de Azure, los enlaces de entrada y salidos proporcionan una manera declarativa tooconnect tooexternal servicio de datos de la función. En este tema, aprenderá cómo tooupdate una función existente mediante la adición de una salida de enlace que envía mensajes tooAzure almacenamiento en la cola.  

![Ver el mensaje en los registros de Hola.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>Requisitos previos 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* Instalar hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="add-binding"></a>Agregar un enlace de salida
 
1. Expanda su Function App y su función.

2. Seleccione sucesivamente **Integrar**, **+ Nueva salida**, **Azure Queue Storage** y **Seleccionar**.
    
    ![Agregar una función de tooa de enlace de salida de cola almacenamiento Hola portal de Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. Usar la configuración de hello como se especifica en la tabla de hello: 

    ![Agregar una función de tooa de enlace de salida de cola almacenamiento Hola portal de Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | Configuración      |  Valor sugerido   | Descripción                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nombre de la cola**   | myqueue-items    | nombre de Hola de hello en cola tooconnect tooin su cuenta de almacenamiento. |
    | **Conexión de la cuenta de almacenamiento** | AzureWebJobStorage | Puede usar la conexión de la cuenta de almacenamiento Hola ya está en uso por la aplicación de la función o cree uno nuevo.  |
    | **Nombre del parámetro de mensaje** | outputQueueItem | nombre de Hola Hola enlace de parámetros de salida. | 

4. Haga clic en **guardar** enlace de hello tooadd.
 
Ahora que tiene un enlace de salida definido, debe tooupdate Hola código toouse Hola enlace tooadd tooa cola de mensajes.  

## <a name="update-hello-function-code"></a>Actualizar código de función de Hola

1. Seleccione el código de la función de la función toodisplay hello en el editor de Hola. 

2. Para una función de C#, actualice la definición de función manera hello tooadd **outputQueueItem** parámetros de enlace de almacenamiento. Omita este paso para una función de JavaScript.

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. Agregar Hola siguiendo la función de toohello de código justo antes de que devuelve el método hello. Use Hola fragmento de código adecuado para el idioma de saludo de la función.

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. Seleccione **guardar** toosave cambios.

valor de Hello pasado toohello desencadenador HTTP está incluido en una cola de mensajes toohello agregada.
 
## <a name="test-hello-function"></a>Probar función hello 

1. Una vez guardados los cambios de código de hello, seleccione **ejecutar**. 

    ![Agregar una función de tooa de enlace de salida de cola almacenamiento Hola portal de Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. Compruebe Hola registros toomake seguro de que la función hello se realizó correctamente. Una cola nueva denominada **outqueue** hello en primer lugar se utiliza en tiempo de ejecución de funciones al enlace de salida de hello creada en la cuenta de almacenamiento.

A continuación, puede conectarse tooyour almacenamiento cuenta tooverify Hola nuevo de colas y mensajes de bienvenida del agregado tooit. 

## <a name="connect-toohello-queue"></a>Conectar toohello cola

Omitir Hola tres primeros pasos si ya ha instalado el Explorador de almacenamiento y conectado tooyour cuenta de almacenamiento.    

1. En la función, elija **integrar** hello nueva y **almacenamiento de cola de Azure** el enlace de salida, a continuación, expanda **documentación**. Copie el **Nombre de cuenta** y la **Clave de cuenta**. Use estas cuentas de almacenamiento de credenciales tooconnect toohello.
 
    ![Obtener las credenciales de conexión de cuenta de almacenamiento de Hola.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. Ejecute hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) herramienta, seleccione Hola conectarse icono de hello izquierda, elija **utilizar un nombre de la cuenta de almacenamiento y la clave**y seleccione **siguiente**.

    ![Ejecutar la herramienta de explorador de la cuenta de almacenamiento de Hola.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. Hola pegar **nombre de la cuenta** y **clave de cuenta** del paso 1 en sus campos correspondientes y haga clic en **siguiente**, y **conectar**. 
  
    ![Pegue las credenciales de almacenamiento de Hola y conectarse.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. Expanda la cuenta de almacenamiento de hello adjunta, **colas** y compruebe que una cola con el nombre **myqueue elementos** existe. También debería ver un mensaje ya se encuentran en la cola de Hola.  
 
    ![Cree una cola de almacenamiento.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>Limpieza de recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Pasos siguientes

Ha agregado una función de salida enlace tooan existente. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obtener más información sobre el almacenamiento de tooQueue de enlace, vea [enlaces de la cola de almacenamiento de las funciones de Azure](functions-bindings-storage-queue.md). 




---
title: "una función en Azure desencadenado por un webhook genérico aaaCreate | Documentos de Microsoft"
description: "Utilice las funciones de Azure toocreate una función sin servidor que invoca un webhook de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a>Creación de una función desencadenada por un webhook genérico

Las funciones de Azure permite ejecutar el código en un entorno sin servidor sin necesidad de toofirst crear una máquina virtual o publicar una aplicación web. Por ejemplo, puede configurar un toobe función desencadenada una alerta generada por el Monitor de Azure. Este tema muestra cómo el código C# tooexecute cuando un grupo de recursos está agregado tooyour suscripción.   

![Webhook genérico desencadenó función Hola portal de Azure](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a>Requisitos previos 

toocomplete este tutorial:

+ Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creación de una Function App de Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

A continuación, cree una función en la aplicación de hello nueva función.

## <a name="create-function"></a>Creación de una función desencadenada mediante un webhook genérico

1. Expanda la aplicación de la función y haga clic en hello  **+**  aparece al lado demasiado**funciones**. Si esta función es hello primera de ellas en la aplicación de la función, seleccione **función personalizada**. Esto muestra el conjunto completo de Hola de plantillas de función.

    ![Página de inicio rápido de funciones en hello portal de Azure](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. Seleccione hello **WebHook genérico - C#** plantilla. Escriba un nombre para la función de C# y, después, seleccione **Crear**.

     ![Cree una función genérica webhook desencadenada en hello portal de Azure](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. En la nueva función, haga clic en **<> / Get función URL**, a continuación, copiar y guardar el valor de Hola. Utilice este webhook de hello tooconfigure de valor. 

    ![Revise el código de la función hello](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
Después, cree un punto de conexión de webhook en una alerta de registro de actividad en Azure Monitor. 

## <a name="create-an-activity-log-alert"></a>Creación de una alerta de registro de actividad

1. En el portal de Azure de Hola, vaya toohello **Monitor** servicio, seleccione **alertas**y haga clic en **Agregar alerta de registro de actividad**.   

    ![Supervisión](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. Usar la configuración de hello como se especifica en la tabla de hello:

    ![Creación de una alerta de registro de actividad](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | Configuración      |  Valor sugerido   | Descripción                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nombre de alerta de registro de actividad** | resource-group-create-alert | Nombre de alerta de registro de actividad de Hola. |
    | **Suscripción** | Su suscripción | suscripción de Hola que estás usando para este tutorial. | 
    |  **Grupo de recursos** | myResourceGroup | grupo de recursos de Hello alertar a los recursos Hola se implementa en. Usar Hola mismo grupo de recursos a medida que la aplicación de la función hace tooclean más fácil de después de completar el tutorial de Hola. |
    | **Categoría de eventos** | Administrativo | Esta categoría incluye los cambios realizados tooAzure recursos.  |
    | **Tipo de recurso** | Grupos de recursos | Filtra las actividades de grupo de tooresource alertas. |
    | **Grupo de recursos**<br/>y **recurso** | Todo | Supervisa todos los recursos. |
    | **Nombre de la operación** | Crear grupo de recursos | Filtra las operaciones de toocreate de alertas. |
    | **Level** | Informativo | Incluye las alertas de nivel informativo. | 
    | **Estado** | Correcto | Tooactions de alertas de filtros que se han completado correctamente. |
    | **Grupo de acción** | Nuevo | Crear un nuevo grupo de acción, que define la toma de la acción de hello cuando se genera una alerta. |
    | **Nombre del grupo de acción** | function-webhook | Un grupo de acciones de nombre tooidentify Hola.  | 
    | **Nombre corto** | funcwebhook | Un nombre corto para el grupo de acciones de Hola. |  

3. En **acciones**, agregar una acción mediante la configuración de hello como se especifica en la tabla de hello: 

    ![Agregar un grupo de acciones](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | Configuración      |  Valor sugerido   | Descripción                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Name** | CallFunctionWebhook | Un nombre para la acción de Hola. |
    | **Tipo de acción** | webhook | alerta de toohello de respuesta de Hello es que se llama a una dirección URL del Webhook. |
    | **Detalles** | Dirección URL de la función | Pegue en la dirección URL del webhook Hola de función hello que copió anteriormente. |v

4. Haga clic en **Aceptar** grupo de alerta y la acción de hello toocreate.  

Hola webhook ahora se llama cuando se crea un grupo de recursos en su suscripción. A continuación, actualizar código de hello en su Hola de toohandle datos de registro JSON en el cuerpo de saludo de solicitud de Hola de función.   

## <a name="update-hello-function-code"></a>Actualizar código de función de Hola

1. Navegar por la aplicación de función tooyour atrás en el portal de Hola y expanda la función. 

2. Reemplace el código de script de Hola C# en función de hello en el portal de hello con hello siguiente código:

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

Ahora puede probar la función hello mediante la creación de un nuevo grupo de recursos en su suscripción.

## <a name="test-hello-function"></a>Probar función hello

1. Haga clic en el icono de grupo de recursos de hello en izquierda Hola de hello portal de Azure, seleccione **+ agregar**, escriba un **nombre del grupo de recursos**y seleccione **crear** toocreate un grupo de recursos vacío.
    
    ![Cree un grupo de recursos.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. Función tooyour volver y expanda hello **registros** ventana. Una vez creado el grupo de recursos de hello, desencadenadores de alerta de registro de actividad Hola Hola webhook y se ejecuta la función hello. Verá que el nombre de Hola de nuevo grupo de recursos Hola escrito toohello registros.  

    ![Agregue una configuración de la aplicación de prueba.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. (Opcional) Volver atrás y eliminar el grupo de recursos de Hola que ha creado. Tenga en cuenta que esta actividad no desencadenará la función hello. Esto es porque delete operaciones se filtran por alerta de Hola. 

## <a name="clean-up-resources"></a>Limpieza de recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Pasos siguientes

Ha creado una función que se ejecuta cuando se recibe una solicitud de un webhook genérico. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para más información sobre los desencadenadores de webhook, consulte [Enlaces HTTP y webhook en Azure Functions](functions-bindings-http-webhook.md). toolearn más sobre el desarrollo de las funciones de C#, vea [referencia del programador de C# de funciones de Azure script](functions-reference-csharp.md).


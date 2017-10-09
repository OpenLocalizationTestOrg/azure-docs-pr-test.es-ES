---
title: "una función que se integra con aplicaciones de Azure lógica aaaCreate | Documentos de Microsoft"
description: "Crear una función que se integra con las aplicaciones lógicas de Azure y Azure cognitivos servicios opiniones de tweet toocategorize y enviar notificaciones cuando opinión es deficiente."
services: functions, logic-apps, cognitive-services
keywords: "flujo de trabajo, aplicaciones de nube, servicios en la nube, procesos empresariales, integración de sistemas, integración de aplicaciones empresariales, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Creación de una función que se integre con Azure Logic Apps

Funciones de Azure se integra con aplicaciones de Azure lógica de Hola Diseñador de aplicaciones de la lógica. Esta integración permite usar hello capacidad de ejecución de funciones en las orquestaciones con otros servicios de terceros y Azure. 

Este tutorial muestra cómo las funciones toouse con lógica de aplicaciones y servicios de Azure cognitivos opiniones tooanalyze de entradas de Twitter. Una función HTTP desencadenada clasifica tweets como verde, amarillo o rojo en función de puntuación de opiniones Hola. Se envía un correo electrónico cuando se detecta una opinión deficiente. 

![imagen de los dos primeros pasos de una aplicación en el diseñador de Logic Apps](media/functions-twitter-email/designer1.png)

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Cree una cuenta de Cognitive Services.
> * Crear una función que clasifica las opiniones de tweet.
> * Crear una aplicación de lógica que se conecta tooTwitter.
> * Agregar aplicación de lógica de toohello de detección de opinión. 
> * Se conectan Hola lógica aplicación toohello funcionan.
> * Enviar un correo electrónico en función de la respuesta de Hola de función hello.

## <a name="prerequisites"></a>Requisitos previos

+ Una cuenta de [Twitter](https://twitter.com/) activa. 
+ Una cuenta de [Outlook.com](https://outlook.com/) (para enviar las notificaciones).
+ Este tema se utiliza como sus recursos de Hola de punto de partida creados en [crear la primera función de hello portal de Azure](functions-create-first-azure-function.md).  
Si aún no lo ha hecho, complete estos toocreate ahora de pasos de la aplicación de la función.

## <a name="create-a-cognitive-services-account"></a>Creación de una cuenta de Cognitive Services

Una cuenta de servicios cognitivos es necesario toodetect Hola opiniones de tweets de que se está supervisando.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

2. Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.

3. Haga clic en **Datos y análisis** > **Cognitive Services**. A continuación, usar la configuración de hello como especificado en la tabla de hello, acepte los términos de Hola y compruebe **toodashboard Pin**.

    ![Hoja para crear cuenta de Cognitive Services](media/functions-twitter-email/cog_svcs_account.png)

    | Configuración      |  Valor sugerido   | Descripción                                        |
    | --- | --- | --- |
    | **Name** | MyCognitiveServicesAccnt | Elija un nombre de cuenta único. |
    | **Tipo de API** | Text Analytics API | API usar texto tooanalyze.  |
    | **Ubicación** | Oeste de EE. UU. | Actualmente, solo está disponible **Oeste de EE. UU.** para análisis de texto. |
    | **Plan de tarifa** | F0 | Comience con el nivel más bajo de Hola. Si se queda sin llamadas, escalar tooa de nivel superior.|
    | **Grupos de recursos** | myResourceGroup | Use Hola mismo grupo de recursos para todos los servicios en este tutorial.|

4. Haga clic en **crear** toocreate su cuenta. Una vez creada la cuenta de hello, haga clic en el nuevo panel de toohello anclados de cuenta de servicios cognitivos. 

5. En la cuenta de hello, haga clic en **claves**y a continuación, copie el valor de Hola de **clave 1** y guárdelo. Utilice este tooyour de aplicación de lógica de hello tooconnect clave cuenta Services cognitivos. 
 
    ![simétricas](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>Crear función hello

Funciones proporciona un toooffload excelente manera tareas de procesamiento en un flujo de trabajo de aplicaciones de la lógica. Este tutorial usa un HTTP desencadena función tooprocess tweet opiniones las puntuaciones de servicios cognitivos y devolver un valor de categoría.  

1. Expanda la aplicación de la función, haga clic en hello  **+**  aparece al lado demasiado**funciones**, haga clic en hello **HTTPTrigger** plantilla. Tipo de `CategorizeSentiment` para la función hello **nombre** y haga clic en **crear**.

    ![Hoja Instancias de Function App, Functions +](media/functions-twitter-email/add_fun.png)

2. Reemplace el contenido de Hola de archivo de hello run.csx con el siguiente código de hello, a continuación, haga clic en **guardar**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    Este código de la función devuelve una categoría de color en función de puntuación de opiniones Hola recibidos en la solicitud de saludo. 

3. función de hello tootest, haga clic en **prueba** en la ficha de prueba de Hola Hola tooexpand más a la derecha. Escriba un valor de `0.2` para hello **cuerpo de la solicitud**y, a continuación, haga clic en **ejecutar**. Un valor de **rojo** se devuelve en hello cuerpo de respuesta de Hola. 

    ![Probar función hello en hello portal de Azure](./media/functions-twitter-email/test.png)

Ahora, tiene una función que clasifica las puntuaciones de opinión. A continuación, cree una aplicación lógica que integre la función con las cuentas de Twitter y Cognitive Services. 

## <a name="create-a-logic-app"></a>Creación de una aplicación lógica   

1. En el Hola portal de Azure, haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.

2. Haga clic en **Integración empresarial** > **Aplicación lógica**. A continuación, usar la configuración de hello como especificado en la tabla de hello, compruebe **Pin toodashboard**y haga clic en **crear**.
 
4. A continuación, escriba un **nombre** como `TweetSentiment`, usar la configuración de hello como se especifica en la tabla de hello, acepte los términos de Hola y comprobar **toodashboard Pin**.

    ![Crear aplicación lógica en hello portal de Azure](./media/functions-twitter-email/new_logicApp.png)

    | Configuración      |  Valor sugerido   | Descripción                                        |
    | ----------------- | ------------ | ------------- |
    | **Name** | TweetSentiment | Elija un nombre adecuado para la aplicación. |
    | **Grupos de recursos** | myResourceGroup | API usar texto tooanalyze.  |
    | **Ubicación** | Este de EE. UU. | Elija un tooyou de cierre de ubicación. |
    | **Grupos de recursos** | myResourceGroup | Elija Hola el mismo grupo de recursos existente como antes.|

4. Haga clic en **crear** toocreate la aplicación lógica. Después de crea la aplicación hello, haga clic en el nuevo panel de toohello anclados de aplicación lógica. A continuación, en hello lógica el Diseñador de aplicaciones, desplácese hacia abajo y haga clic en hello **en blanco de lógica de aplicación** plantilla. 

    ![Plantilla Aplicación lógica en blanco](media/functions-twitter-email/blank.png)

Ahora puede usar el Diseñador de aplicaciones de la lógica tooadd servicios y desencadenadores tooyour aplicación hello.

## <a name="connect-tootwitter"></a>Conectar tooTwitter

En primer lugar, cree una cuenta de Twitter tooyour de conexión. aplicación de la lógica de Hello sondea tweets, que desencadenen hello toorun de aplicación.

1. En el Diseñador de hello, haga clic en hello **Twitter** de servicio y haga clic en hello **cuando se registra un nuevo tweet** desencadenador. Inicie sesión en tooyour cuenta de Twitter y autorizar aplicaciones lógicas toouse tu cuenta.

2. Use la configuración de desencadenador de Twitter de hello como se especifica en la tabla de Hola. 

    ![Configuración del conector de Twitter](media/functions-twitter-email/azure_tweet.png)

    | Configuración      |  Valor sugerido   | Descripción                                        |
    | ----------------- | ------------ | ------------- |
    | **Texto de búsqueda** | #Azure | Use una hashtag que sea lo suficientemente popular para toogenerate nueva tweets en intervalo de saludo elegido. Al utilizar el nivel gratuito de Hola y su hashtag es demasiado popular, puede usar rápidamente las transacciones de hello en su cuenta de servicios cognitivos. |
    | **Frecuencia** | Minuto | unidad de frecuencia de Hello utilizada para el sondeo de Twitter.  |
    | **Intervalo** | 15 | tiempo de Hello transcurrido entre las solicitudes de Twitter, en unidades de frecuencia. |

3.  Haga clic en **guardar** tooconnect tooyour cuenta de Twitter. 

Ahora, la aplicación es tooTwitter conectado. A continuación, conectar opiniones de tootext análisis toodetect Hola de tweets recopilados.

## <a name="add-sentiment-detection"></a>Agregar la detección de opiniones

1. Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.

    ![Nuevo paso y Agregar una acción](media/functions-twitter-email/new_step.png)

2. En **elegir una acción**, haga clic en **análisis de texto**y, a continuación, haga clic en hello **detectar opiniones** acción.

    ![Detectar sentimiento](media/functions-twitter-email/detect_sent.png)

3. Escriba un nombre de conexión como `MyCognitiveServicesConnection`, pegue la clave de Hola para los servicios cognitivos cuenta que ha guardado y haga clic en **crear**.  

4. Haga clic en **tooanalyze de texto** > **Tweet texto**y, a continuación, haga clic en **guardar**.  

    ![Detectar sentimiento](media/functions-twitter-email/ds_tta.png)

Ahora que se configura la detección de opinión, puede agregar una función de tooyour de conexión que usa Hola opiniones puntuación resultado.

## <a name="connect-sentiment-output-tooyour-function"></a>Conectar opiniones salida tooyour función

1. Hola lógica el Diseñador de aplicaciones, haga clic en **nuevo paso** > **agregar una acción**y, a continuación, haga clic en **funciones de Azure**. 

2. Haga clic en **elegir una función de Azure**, seleccione hello **CategorizeSentiment** función que ha creado anteriormente.  

    ![Cuadro de función de Azure que muestra Elegir una función de Azure](media/functions-twitter-email/choose_fun.png)

3. En **Cuerpo de la solicitud**, haga clic en **Puntuación** y, a continuación, en **Guardar**.

    ![Score](media/functions-twitter-email/trigger_score.png)

Ahora, la función se desencadena cuando se envía una puntuación de opinión de aplicación lógica de hello. Una categoría codificado por colores devuelto toohello lógica aplicación por función hello. A continuación, agregue una notificación de correo electrónico que se envía cuando el valor de una opinión de **rojo** devuelta por la función de Hola. 

## <a name="add-email-notifications"></a>Agregar notificaciones por correo electrónico

Hola última parte del flujo de trabajo de hello es tootrigger un correo electrónico cuando se usa para puntuar opiniones hello como _rojo_. Este tema utiliza un conector de Outlook.com. Puede realizar similar pasos toouse un conector Gmail o Outlook de Office 365.   

1. Hola lógica el Diseñador de aplicaciones, haga clic en **nuevo paso** > **agregar una condición**. 

2. Haga clic en **Elegir un valor** y, a continuación, haga clic en **Cuerpo**. Seleccione **Es igual a**, haga clic en **Elegir un valor**, escriba `RED` y haga clic en **Guardar**. 

    ![Agregar una aplicación de lógica de toohello de condición.](media/functions-twitter-email/condition.png)

3. En **si es así, no hacen nada**, haga clic en **agregar una acción**, busque `outlook.com`, haga clic en **enviar un correo electrónico**e inicie sesión en tooyour cuenta de Outlook.com.
    
    ![Elegir una acción para la condición de Hola.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Si no tiene una cuenta de Outlook.com, puede elegir otro conector, como Gmail u Office 365 Outlook

4. Hola **enviar un correo electrónico** acción, usar la configuración de correo electrónico de hello como especificada en la tabla de Hola. 

    ![Configurar el correo electrónico de hello para el envío de hello una acción de correo electrónico.](media/functions-twitter-email/sendemail.png)

    | Configuración      |  Valor sugerido   | Descripción  |
    | ----------------- | ------------ | ------------- |
    | **To** | Escriba su dirección de correo electrónico | dirección de correo electrónico de Hola que recibe la notificación de Hola. |
    | **Asunto** | Detectada opinión de tweet negativa  | línea de asunto Hola de notificación de correo electrónico de Hola.  |
    | **Cuerpo** | Texto de tweet, ubicación | Haga clic en hello **Tweet texto** y **ubicación** parámetros. |

5.  Haga clic en **Guardar**.

Ahora que ha finalizado el flujo de trabajo de hello, puede habilitar la aplicación de la lógica de hello y vea función hello en el trabajo.

## <a name="test-hello-workflow"></a>Flujo de trabajo de prueba Hola

1. Hola diseñador la lógica de aplicación, haga clic en **ejecutar** toostart Hola aplicación.

2. En la columna izquierda de hello, haga clic en **Introducción** toosee estado de Hola de aplicación lógica de hello. 
 
    ![Estado de ejecución de la aplicación lógica](media/functions-twitter-email/over1.png)

3. (Opcional) Haga clic en uno de hello ejecuciones toosee detalles de ejecución de Hola.

4. Paso tooyour función, ver los registros de Hola y compruebe que los valores de opinión se recibe y procesa.
 
    ![Ver los registros de función](media/functions-twitter-email/sent.png)

5. Cuando se detecta una opinión potencialmente negativa, recibirá un correo electrónico. Si no ha recibido un correo electrónico, puede cambiar tooreturn de código de función de hello rojo cada vez:

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    Después de comprobar las notificaciones de correo electrónico, cambiar código original de toohello inversa:

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Después de completar este tutorial, debe deshabilitar la aplicación de la lógica de hello. Al deshabilitar la aplicación hello, no está cargada para las ejecuciones y utilizar las transacciones de hello en su cuenta de servicios cognitivos.

Ahora, ha visto lo fácil que es toointegrate funciones en un flujo de trabajo de las aplicaciones lógicas.

## <a name="disable-hello-logic-app"></a>Deshabilitar la aplicación de la lógica de hello

aplicación de lógica de hello toodisable, haga clic en **Introducción** y, a continuación, haga clic en **deshabilitar** en la parte superior de Hola de pantalla de bienvenida. Esto detiene Hola aplicación de lógica de ejecución y gastos sin eliminar la aplicación hello. 

![Registros de la función](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Cree una cuenta de Cognitive Services.
> * Crear una función que clasifica las opiniones de tweet.
> * Crear una aplicación de lógica que se conecta tooTwitter.
> * Agregar aplicación de lógica de toohello de detección de opinión. 
> * Se conectan Hola lógica aplicación toohello funcionan.
> * Enviar un correo electrónico en función de la respuesta de Hola de función hello.

Avanzar toohello siguiente tutorial toolearn cómo toocreate una API sin servidor para la función.

> [!div class="nextstepaction"] 
> [Creación de una API sin servidor mediante Azure Functions](functions-create-serverless-api.md)

toolearn más información acerca de las aplicaciones lógicas, consulte [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).


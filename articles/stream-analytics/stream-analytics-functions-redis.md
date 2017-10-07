---
title: "procesamiento en tiempo real de aaaStream análisis para las funciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse una función de Azure había conectada una cola de Bus de servicio, toopopulate una caché en Redis de Azure desde la salida de hello de un trabajo de análisis de transmisiones."
keywords: "flujo de datos, caché en redis, cola del bus de servicio"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>¿Cómo toostore datos de análisis de transmisiones de Azure en una caché en Redis de Azure mediante las funciones de Azure
Análisis de transmisiones de Azure le permite desarrollar e implementar soluciones de bajo coste toogain en tiempo real conocimientos dispositivos, sensores, infraestructura y las aplicaciones o cualquier flujo de datos rápidamente. Permite varios casos de uso, como la administración y supervisión en tiempo real, comando y control, detección de fraudes, automóviles conectados y mucho más. En muchos de estos escenarios, puede que desee datos toostore arroja análisis de transmisiones de Azure en un almacén de datos distribuidos como una caché en Redis de Azure.

Imaginemos que forma parte de una empresa de telecomunicaciones. Está tratando de fraude SIM toodetect donde varias llamadas procedentes de Hola misma identidad, en Hola mismo tiempo, pero en diferentes geográficamente ubicaciones. Tiene que almacenar todos los Hola posibles fraudulentas llamadas en una caché en Redis de Azure. En este blog, le brindamos la orientación que necesita para poder completar fácilmente la tarea. 

## <a name="prerequisites"></a>Requisitos previos
Hola completa [detección de fraudes en tiempo real] [ fraud-detection] ejemplo paso a paso para ASA

## <a name="architecture-overview"></a>Introducción a la arquitectura
![Captura de pantalla de arquitectura](./media/stream-analytics-functions-redis/architecture-overview.png)

Como se muestra en hello anterior figura, análisis de transmisiones permite toobe de datos de entrada de transmisión por secuencias, consulta y envíe el resultado de tooan. En función de la salida de hello, funciones de Azure puede desencadenar algún tipo de evento. 

En este blog, céntrese en parte de las funciones de Azure Hola de esta canalización o más concretamente Hola desencadenamiento de un evento que almacena datos fraudulentas en la memoria caché de Hola.
Después de completar hello [detección de fraudes en tiempo real] [ fraud-detection] tutorial, tendrá una entrada (un concentrador de eventos), una consulta y una salida (almacenamiento de blobs) ya configurado y en ejecución. En este blog, cambiamos Hola salida toouse una cola de Bus de servicio en su lugar. A continuación, nos conectamos a una cola de toothis de función de Azure. 

## <a name="create-and-connect-a-service-bus-queue-output"></a>Creación y conexión de una salida de cola del Bus de servicio
toocreate una cola de Bus de servicio, siga los pasos 1 y 2 de la sección de .NET de hello en [empezar a trabajar con colas de Service Bus][servicebus-getstarted].
Ahora vamos a conectar hello toohello análisis de transmisiones trabajo en cola que se creó en hello anterior tutorial de detección de fraudes.

1. Hola portal de Azure, vaya toohello **salidas** hoja de su trabajo y seleccione **agregar** al principio de Hola de página de Hola.
   
    ![Agregar salidas](./media/stream-analytics-functions-redis/adding-outputs.png)
2. Elija **cola de Service Bus** como hello **receptor** y siga las instrucciones de hello en pantalla de bienvenida. Seguro de espacio de nombres de hello toochoose de hello cola de Bus de servicio creará en [empezar a trabajar con colas de Service Bus][servicebus-getstarted]. Cuando haya terminado, haga clic en el botón "secundario" Hola.
3. Especifique Hola siguientes valores:
   
   * **Formato del serializador de eventos**: JSON
   * **Codificación**: UTF8
   * **FORMATO**: separado por líneas
4. Haga clic en hello **crear** botón tooadd este origen y tooverify que análisis de transmisiones puede conectarse correctamente toohello cuenta de almacenamiento.
5. Hola **consulta** ficha, reemplace la consulta actual Hola por siguiente Hola. Reemplazar * [su nombre de BUS de servicio] * con el nombre de la salida de hello que creó en el paso 3. 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a>Creación de una instancia de Caché en Redis de Azure
Crear una caché en Redis de Azure siguiendo la sección de .NET de hello en [cómo tooUse Azure Redis Cache] [ use-rediscache] hasta que llama a sección hello ***configurar clientes de caché de hello***.
Una vez que finalice, tendrá una nueva instancia de Caché en Redis. En **toda la configuración de**, seleccione **las claves de acceso** y tome nota de hello ***cadena de conexión principal***.

![Captura de pantalla de arquitectura](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>Creación de una Función de Azure
Siga [crear su primera función Azure] [ functions-getstarted] tooget tutorial a trabajar con funciones de Azure. Si ya tiene una función de Azure que debería como toouse y luego pase demasiado[tooRedis memoria caché de escritura](#Writing-to-Redis-Cache)

1. En el portal de hello, seleccione Servicios de aplicaciones de navegación izquierdo de hello, a continuación, haga clic en el sitio Web de aplicación de la función Azure aplicación nombre tooget toohello la función.
    ![Captura de pantalla de lista de funciones de App Services](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. Haga clic en **Nueva función > ServiceBusQueueTrigger – C#**. Para hello campos siguientes, siga estas instrucciones:
   
   * **Nombre de la cola**: Hola mismo nombre como nombre de Hola que especificó al crear cola de hello en [empezar a trabajar con colas de Service Bus] [ servicebus-getstarted] (no el nombre de Hola Hola del bus de servicio). Asegúrese de que usar cola de Hola que está conectado toohello análisis de transmisiones de salida.
   * **Conexión de Service Bus**: seleccione **Agregar una cadena de conexión**. cadena de conexión de hello toofind, vaya toohello portal clásico, seleccione **Service Bus**, Hola bus de servicio que creó, y **información de conexión** final Hola de pantalla de bienvenida. Asegúrese de que se encuentra en la pantalla principal de bienvenida en esta página. Copie y pegue la cadena de conexión de Hola. Sentirse tooenter libre cualquier nombre de la conexión.
     
       ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **AccessRights**: elija **Administrar**.
3. Haga clic en **Crear**

## <a name="writing-tooredis-cache"></a>TooRedis caché de escritura
Creamos una función de Azure que lee desde una cola del Bus de servicio. Lo único que queda toodo es usar nuestro toowrite función este toohello datos caché en Redis. 

1. Seleccione el recién creado **ServiceBusQueueTrigger**y haga clic en **función de la configuración de la aplicación** en hello esquina superior derecha. Seleccione **ir tooApp servicio Configuración > Configuración > configuración de la aplicación**
2. Hola sección cadenas de conexión, cree un nombre en hello **nombre** sección. Pegue la cadena de conexión principal de Hola que encontró en hello **crear una caché en Redis** recorra hello **valor** sección. Seleccione **Personalizado** donde aparece **SQL Database**.
3. Haga clic en **guardar** en la parte superior de Hola.
   
    ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/function-connection-string.png)
4. Ahora vuelva toohello configuración de servicio de la aplicación y seleccione **Herramientas > Editor de aplicación de servicio (vista previa) > en > vaya**.
   
    ![Captura de pantalla de conexión del Bus de servicio](./media/stream-analytics-functions-redis/app-service-editor.png)
5. En un editor de su elección, cree un archivo JSON denominado **project.json** con Hola siguiente y guárdelo en disco local tooyour.
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. Cargar este archivo en el directorio raíz de saludo de la función (no WWWROOT). Debería ver un archivo denominado **project.lock.json** aparecen automáticamente, confirmando que Hola Nuget paquetes "StackExchange.Redis" y "Newtonsoft.Json" se han importado.
7. Hola **run.csx** archivo, reemplace el código generados previamente Hola con el siguiente código de hello. En función de lazyConnection hello, reemplace "CONN NAME" con el nombre de Hola que creó en el paso 2 de **almacenar datos en caché en Redis hello**.

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a>Iniciar el trabajo de análisis de transmisiones de Hola
1. Inicie la aplicación de hello telcodatagen.exe. uso de Hello es como sigue:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. En la hoja de trabajo de análisis de transmisiones de hello en el portal de hello, haga clic en **iniciar** al principio de Hola de página de Hola.
   
    ![Captura de pantalla de Iniciar trabajo](./media/stream-analytics-functions-redis/starting-job.png)
3. Hola **Start job** hoja que aparece, seleccione **ahora** y, a continuación, haga clic en hello **iniciar** situado en la parte inferior de Hola de pantalla de bienvenida. estado del trabajo Hola cambia tooStarting y tarde tooRunning de cambios.
   
    ![Captura de pantalla de selección de tiempo de Iniciar trabajo](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>Ejecución de la solución y comprobación de los resultados
Volviendo a tooyour **ServiceBusQueueTrigger** página, ahora debería ver las instrucciones de registro. Estos registros se muestran que se obtuvo algo Hola cola de Bus de servicio, póngalo en la base de datos de hello y captura usando tiempo hello como clave de Hola!

tooverify que los datos están en la memoria caché de Redis, ir a página de caché de Redis tooyour en el nuevo portal de hello (como se muestra en hello anterior [crear una caché en Redis de Azure](#Create-an-Azure-Redis-Cache) paso) y seleccione consola.

Ahora puede escribir Redis comandos tooconfirm que los datos se están en realidad en caché de Hola.

![Captura de pantalla de Consola de Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>Pasos siguientes
Nos complace sobre cosas de hello nuevas funciones de Azure y análisis de transmisiones pueden hacer conjuntamente y esperamos que esto desbloquea nuevas posibilidades para usted. Si tiene comentarios sobre la acción que realizará a continuación, cree Hola libre toouse [UserVoice de Azure sitio](https://feedback.azure.com/forums/270577-stream-analytics).

Si es nuevo Microsoft Azure, le invitamos tootry alejar por registrarse para una [libre de la cuenta de prueba de Azure](https://azure.microsoft.com/pricing/free-trial/). Si está tooStream nuevo análisis, le invitamos demasiado[crear su primer trabajo de análisis de transmisiones](stream-analytics-create-a-job.md).

Si necesita ayuda o tiene alguna pregunta, publíquela en [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) o en los foros de [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics). 

También puede ver Hola recursos siguientes:

* [Azure Functions developer reference](../azure-functions/functions-reference.md)
* [Referencia para desarrolladores de C# de Funciones de Azure](../azure-functions/functions-reference-csharp.md)
* [Referencia para desarrolladores de F# de Azure Functions](../azure-functions/functions-reference-fsharp.md)
* [Referencia para desarrolladores de NodeJS de Funciones de Azure](../azure-functions/functions-reference.md)
* [Enlaces y desencadenadores de las Funciones de azure](../azure-functions/functions-triggers-bindings.md)
* [Cómo toomonitor Redis de Azure almacenan en caché](../redis-cache/cache-how-to-monitor.md)

Siga toostay actualizada sobre todas las últimas noticias de Hola y otras características, [ @AzureStreaming ](https://twitter.com/AzureStreaming) en Twitter.

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md

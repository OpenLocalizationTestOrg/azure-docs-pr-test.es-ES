---
title: "desencadenadores de aplicación de API del servicio de aaaApp | Documentos de Microsoft"
description: "¿Cómo tooimplement desencadena en un App de API de servicio de aplicaciones de Azure"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a>Desencadenadores de aplicación de API del Servicio de aplicaciones de Azure
> [!NOTE]
> Esta versión de artículo de Hola aplica la versión del esquema de tooAPI aplicaciones 2014-12-01-versión preliminar.
>
>

## <a name="overview"></a>Información general
Este artículo explica cómo tooimplement API aplicación desencadena y consumirlos desde una aplicación de lógica.

Todos los fragmentos de código de hello en este tema se copian de hello [ejemplo de código de aplicación de API de FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).

Tenga en cuenta que necesitará Hola de toodownload siguiente paquete de nuget para el código de hello en este artículo toobuild y ejecute: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>¿Qué son los desencadenadores de aplicación de API?
Es un escenario común para una toofire de aplicación de API un evento para que los clientes de aplicación de API de hello pueden tomar medidas apropiadas de hello en el evento de respuesta toohello. Hola mecanismo en función de API de REST que admite este escenario se llama a un desencadenador de aplicaciones de API.

Por ejemplo, supongamos que el código de cliente está usando hello [aplicación de API del conector de Twitter](../connectors/connectors-create-api-twitter.md) y el código necesita tooperform acción basándose en el nuevo tweets que contienen determinadas palabras. En este caso, podría configurar una toofacilitate de desencadenador de inserción o de sondeo esta necesidad.

## <a name="poll-trigger-versus-push-trigger"></a>Desencadenador de sondeo frente a desencadenador de inserción
Actualmente, se admiten dos tipos de desencadenadores:

* Desencadenador de sondeo: cliente sondea la aplicación de API de hello para la notificación de un evento que ha activado
* Desencadenador de inserción: cliente recibe una notificación por aplicación hello API cuando se activa un evento

### <a name="poll-trigger"></a>Desencadenador de sondeo
Un desencadenador de sondeo se implementa como una API de REST regular y espera su toopoll de los clientes (por ejemplo, una aplicación lógica) en pedido tooget notificación. Mientras el cliente de hello puede mantener el estado, no tiene estado propio desencadenador de sondeo Hola.

Hola después de obtener información sobre los paquetes de solicitud y respuesta de saludo muestra algunos aspectos claves del contrato de desencadenador de sondeo de hello:

* Solicitud
  * Método HTTP: GET
  * parameters
    * triggerState: este parámetro opcional permite a los clientes toospecify su estado para que el desencadenador de sondeo de Hola correctamente puede decidir si tooreturn notificación o hello no según el estado especificado.
    * Parámetros específicos de la API
* Response
  * Código de estado **200** : la solicitud es válida y no hay una notificación de desencadenador de Hola. contenido de Hola de notificación de hello será el cuerpo de respuesta de Hola. Un encabezado "Retry-After" en la respuesta de hello indica que se deben recuperar datos de notificación adicionales con una llamada de solicitud posterior.
  * Código de estado **202** : la solicitud es válida, pero no hay ninguna nueva notificación de desencadenador de Hola.
  * Código de estado **4xx** : la solicitud no es válida. cliente de Hello no debe reintentar la solicitud de saludo.
  * Código de estado **5xx** : la solicitud ha producido un error interno en el servidor o un problema temporal. cliente de Hello debe reintentar la solicitud de saludo.

Hola siguiente fragmento de código es un ejemplo de cómo desencadenar tooimplement un sondeo.

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

tootest este sondeo activa, siga estos pasos:

1. Implementar Hola API aplicación con una configuración de autenticación de **público anónimo**.
2. Llamar a hello **táctil** operación tootouch un archivo. Hola siguiente imagen muestra una solicitud de ejemplo a través de Postman.
   ![Llamada a la operación Touch mediante Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Llamar al desencadenador de sondeo de hello con hello **triggerState** parámetro establece tooStep anterior de una marca de tiempo tooa #2. Hello siguiente imagen muestra solicitud de ejemplo de Hola a través de Postman.
   ![Llamada al desencadenador de sondeo mediante Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Desencadenador de inserción
Un desencadenador de inserción se implementa como una API de REST regular que inserta tooclients de notificaciones que se hayan registrado toobe una notificación cuando se activan eventos específicos.

Hola después de obtener información sobre los paquetes de solicitud y respuesta de saludo ilustran algunos aspectos claves del contrato de desencadenador de inserción de Hola.

* Solicitud
  * Método HTTP: PUT
  * parameters
    * Id. de lanzamiento: requerida: opaco de cadena (por ejemplo, un GUID) que representa Hola registro de un desencadenador de inserción.
    * callbackUrl: requerida: dirección URL de hello tooinvoke de devolución de llamada cuando se desencadene el evento de Hola. invocación de Hello es una simple llamada HTTP POST.
    * Parámetros específicos de la API
* Response
  * Código de estado **200** -solicitud tooregister cliente correctamente.
  * Código de estado **4xx** : la solicitud no es válida. cliente de Hello no debe reintentar la solicitud de saludo.
  * Código de estado **5xx** : la solicitud ha producido un error interno en el servidor o un problema temporal. cliente de Hello debe reintentar la solicitud de saludo.
* Devolución de llamada
  * Método HTTP: POST
  * Cuerpo de la solicitud: contenido de la notificación.

Hola siguiente fragmento de código es un ejemplo de cómo desencadenar tooimplement una inserción:

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

tootest este sondeo activa, siga estos pasos:

1. Implementar Hola API aplicación con una configuración de autenticación de **público anónimo**.
2. Examinar demasiado[http://requestb.in/](http://requestb.in/) toocreate un RequestBin que servirá como la dirección URL de devolución de llamada.
3. Llamar al desencadenador de inserción de hello con un GUID como **triggerId** y Hola RequestBin URL como **callbackUrl**.
   ![Llamada al desencadenador de inserción mediante Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Llamar a hello **táctil** operación tootouch un archivo. Hola siguiente imagen muestra una solicitud de ejemplo a través de Postman.
   ![Llamada a la operación Touch mediante Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Comprobación de hello RequestBin tooconfirm que Hola de devolución de llamada de desencadenador de inserción se invoca con el resultado de la propiedad.
   ![Llamada al desencadenador de sondeo mediante Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Descripción de los desencadenadores en la definición de la API
Después de implementar desencadenadores de Hola y distribuir su tooAzure de aplicación de API, navegue toohello **definición de la API** hoja en el portal de vista previa de Hola y verá que los desencadenadores se reconocen automáticamente en hello interfaz de usuario, que se controla mediante Hola definición de Swagger 2.0 API de la aplicación hello API.

![Hoja de definición de la API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Si hace clic en hello **descargar Swagger** botón y archivo JSON de hello abierto, verá resultados toohello similar siguientes:

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

propiedad de extensión de Hola **x-ms-del programador-desencadenador** es cómo se describe en la definición de la API en desencadenadores y se agrega automáticamente a puerta de enlace de aplicación Hola API cuando solicitan definición Hola API a través de puerta de enlace de hello si Hola solicitar tooone de Hola siguiendo criterios. (También puede agregar esta propiedad manualmente).

* Desencadenador de sondeo
  * Si es el método HTTP de hello **obtener**.
  * Si hello **operationId** propiedad contiene la cadena hello **desencadenador**.
  * Si hello **parámetros** propiedad incluye un parámetro con un **nombre** propiedad establecida demasiado**triggerState**.
* Desencadenador de inserción
  * Si es el método HTTP de hello **colocar**.
  * Si hello **operationId** propiedad contiene la cadena hello **desencadenador**.
  * Si hello **parámetros** propiedad incluye un parámetro con un **nombre** propiedad establecida demasiado**triggerId**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Uso de desencadenadores de la aplicación de API en aplicaciones lógicas
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Mostrar y configurar desencadenadores de la aplicación de API en el Diseñador de aplicaciones de la lógica de Hola
Si crea una aplicación de la lógica de Hola Hola de mismo grupo de recursos como aplicación de API, será capaz de tooadd lo lienzo del diseñador toohello simplemente haciendo clic en él. Hola después de imágenes muestra cómo hacerlo:

![Desencadenadores en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configuración del desencadenador de sondeo en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configuración del desencadenador de inserción en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>Optimización de los desencadenadores de la aplicación de API para aplicaciones de lógicas
Después de agregar desencadenadores tooan API de aplicación, hay algunas cosas que puede hacer experiencia de hello tooimprove cuando se utiliza la aplicación hello API en una aplicación de lógica.

Por ejemplo, hello **triggerState** parámetro para los desencadenadores de sondeo debe establecerse toohello siguiente expresión en la aplicación de la lógica de hello. Esta expresión debe evaluar la última invocación del desencadenador de Hola de aplicación lógica de hello de Hola y devuelve ese valor.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Nota: Para obtener una explicación de las funciones de hello utilizadas en expresión Hola anterior, consulte toohello documentación sobre [lenguaje de definición de flujo de trabajo de aplicación lógica](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Los usuarios de aplicación lógica necesitaría la expresión de hello tooprovide anteriormente para hello **triggerState** parámetro al usar Hola desencadenador. Es posible toohave este valor preestablecido por el Diseñador de la aplicación hello lógica a través de la propiedad de extensión de hello **x-ms-programador-recomendación**.  Hola **x-ms-visibilidad** propiedad de extensión se puede establecer valor de tooa de *interno* para que el propio parámetro hello no se muestra en el Diseñador de Hola.  Hola siguiente fragmento de código muestra que.

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

Para los desencadenadores de inserción, Hola **triggerId** parámetro debe identificar inequívocamente la aplicación de la lógica de hello. Una práctica recomendada es tooset este nombre de propiedad toohello de flujo de trabajo de hello mediante el uso de Hola la siguiente expresión:

    @workflow().name

Con hello **x-ms-programador-recomendación** y **x-ms-visibilidad** propiedades de extensión en su definición de API, Hola aplicación de API pueden transmitir establezca esta propiedad toohello lógica aplicación diseñador tooautomatically expresión para el usuario de Hola.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>Adición de propiedades de extensión en la definición de la API
Información de metadatos adicionales - como propiedades de extensión de hello **x-ms-programador-recomendación** y **x-ms-visibilidad** -pueden agregarse en la definición de hello API en uno de dos maneras de: estática o dinámica.

Para obtener metadatos estáticos, puede editar directamente hello */metadata/apiDefinition.swagger.json* un archivo en el proyecto y agregar propiedades de hello manualmente.

Para las aplicaciones de API con metadatos dinámicos, puede editar hello SwaggerConfig.cs archivo tooadd un filtro de operación que puede agregar estas extensiones.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Hola aquí te mostramos un ejemplo de cómo esta clase puede ser el escenario de implementada toofacilitate Hola metadatos dinámicos.

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }

## <a name="typical-output"></a>Salida típica

Hello en el ejemplo siguiente se muestra resultado de hello escrito toohello archivo de registro de ejemplo de Hola Hola a todos. el formato de salida de Hello es por legibilidad:

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a>Fragmentos de código

Esta sección describen algunas secciones claves de código de Hola Hola Hola\_ejemplo del mundo.

### <a name="iot-edge-gateway-creation"></a>Creación de puerta de enlace de IoT Edge

Debe implementar un *proceso de puerta de enlace*. Este programa crea la infraestructura interna de hello (broker hello), carga hello borde IoT módulos y configura el proceso de puerta de enlace de Hola. Borde de IoT proporciona hello **puerta de enlace\_crear\_de\_JSON** función tooenable toobootstrap una puerta de enlace desde un archivo JSON. Hola toouse **puerta de enlace\_crear\_de\_JSON** funcione, asígnele el archivo JSON de tooa de ruta de acceso de hello que especifica hello tooload de módulos de borde de IoT.

Puede encontrar código de hello de proceso de puerta de enlace de Hola Hola *Hello World* ejemplo Hola [main.c] [ lnk-main-c] archivo. Para mayor legibilidad, hello fragmento de código siguiente muestra una versión abreviada de código de proceso de puerta de enlace de Hola. Este programa de ejemplo crea una puerta de enlace y, a continuación, espera Hola de hello usuario toopress **ENTRAR** clave antes de que se destruye puerta de enlace de Hola.

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

archivo de configuración de JSON de Hello contiene una lista de tooload de módulos de borde de IoT y vínculos de hello entre módulos Hola. Cada módulo de IoT Edge debe especificar:

* **nombre**: un nombre único para el módulo de Hola.
* **cargador**: un cargador que sabe cómo hello tooload deseado módulo. Los cargadores son un punto de extensión para cargar diferentes tipos de módulos. IoT Edge proporciona cargadores para usarlos con módulos escritos en C nativo, Node.js, Java y .NET. ejemplo de Hola mundo Hola solo utiliza cargador C nativo de hello porque todos los módulos de hello en este ejemplo son bibliotecas dinámicas escritas en C. Para obtener más información acerca de cómo toouse módulos de borde IoT escritos en lenguajes diferentes, vea hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), o [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) ejemplos.
    * **nombre**: nombre de Hola del cargador de Hola usa el módulo de hello tooload.
    * **punto de entrada**: biblioteca de toohello de ruta de acceso de Hola que contiene el módulo de Hola. En Linux esta biblioteca es un archivo .so y en Windows un archivo .dll. punto de entrada de Hello es tipo toohello específico del cargador que se va a usar. Hola punto de entrada del cargador de Node.js es un archivo .js. Hola punto de entrada del cargador de Java es una ruta de clase y un nombre de clase. Hola punto de entrada del cargador de .NET es un nombre de ensamblado y un nombre de clase.

* **args**: cualquier módulo de Hola de información de configuración es necesario.

Hola después de código se muestra hello JSON usa toodeclare todos los Hola módulos IoT borde de ejemplo de Hola mundo Hola en Linux. Si un módulo requiere que los argumentos depende de diseño de hello del módulo de Hola. En este ejemplo, el módulo de registrador de hello toma un argumento que es el archivo de salida de toohello de ruta de acceso de Hola y Hola Hola\_módulo world no tiene ningún argumento.

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

archivo JSON de Hello contiene también vínculos de hello entre módulos de Hola que se pasan a toohello broker. Los vínculos tienen dos propiedades:

* **origen**: el nombre de un módulo de hello `modules` sección, o `\*`.
* **receptor**: el nombre de un módulo de hello `modules` sección.

Cada vínculo define la ruta y dirección de un mensaje. Mensajes de Hola **origen** módulo se entregan toohello **receptor** módulo. Puede establecer hello **origen** módulo demasiado`\*`, lo que indica que hello **receptor** módulo recibe mensajes desde cualquier módulo.

Hello siguiente muestra hello JSON utiliza tooconfigure vínculos entre los módulos de hello usados en Hola Hola\_ejemplo world en Linux. Todos los mensajes generan por hello `hello_world` módulo consume hello `logger` módulo.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Publicación de mensajes del módulo hola\_mundo

Puede encontrar código de hello usa Hola Hola\_toopublish mensajes de módulo de mundo Hola ['hello_world.c'] [ lnk-helloworld-c] archivo. Hello fragmento de código siguiente muestra una versión modificada del código de hello con comentarios agregados y algunos quitado para mayor legibilidad del código de control de errores:

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a>Procesamiento de mensajes del módulo Hola\_mundo

Hola Hola\_módulo world nunca procesa los mensajes que otros módulos de borde IoT publican toohello broker. Hola por lo tanto, la implementación de devolución de llamada de mensaje de Hola Hola Hola\_módulo world es una función de operación inefectiva.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Publicación y procesamiento de mensajes del módulo logger

módulo de registrador Hola recibe mensajes desde el agente de Hola y los escribe tooa archivo. Nunca publica ningún mensaje. Por lo tanto, código de hello del módulo de registrador Hola nunca llama hello **Broker_Publish** (función).

Hola **Logger_Receive** función Hola [logger.c] [ lnk-logger-c] archivo es broker de Hola de devolución de llamada de hello invoca el módulo de toodeliver mensajes toohello registrador. Hello fragmento de código siguiente muestra una versión modificada con comentarios agregados y algunos quitado para mayor legibilidad del código de control de errores:

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a>Pasos siguientes

En este artículo, se ejecutaba una puerta de enlace de IoT borde simple que escribe el archivo de registro de mensajes tooa. toorun un ejemplo que envía mensajes tooIoT concentrador, consulte [IoT borde, enviar mensajes del dispositivo a la nube con un dispositivo simulado con Linux] [ lnk-gateway-simulated-linux] o [IoT borde, enviar mensajes de dispositivo a la nube con una dispositivo simulado mediante Windows][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md
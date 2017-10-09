## <a name="typical-output"></a><span data-ttu-id="76706-101">Salida típica</span><span class="sxs-lookup"><span data-stu-id="76706-101">Typical output</span></span>

<span data-ttu-id="76706-102">Hello en el ejemplo siguiente se muestra resultado de hello escrito toohello archivo de registro de ejemplo de Hola Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="76706-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="76706-103">el formato de salida de Hello es por legibilidad:</span><span class="sxs-lookup"><span data-stu-id="76706-103">hello output is formatted for legibility:</span></span>

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

## <a name="code-snippets"></a><span data-ttu-id="76706-104">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="76706-104">Code snippets</span></span>

<span data-ttu-id="76706-105">Esta sección describen algunas secciones claves de código de Hola Hola Hola\_ejemplo del mundo.</span><span class="sxs-lookup"><span data-stu-id="76706-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="76706-106">Creación de puerta de enlace de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="76706-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="76706-107">Debe implementar un *proceso de puerta de enlace*.</span><span class="sxs-lookup"><span data-stu-id="76706-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="76706-108">Este programa crea la infraestructura interna de hello (broker hello), carga hello borde IoT módulos y configura el proceso de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="76706-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="76706-109">Borde de IoT proporciona hello **puerta de enlace\_crear\_de\_JSON** función tooenable toobootstrap una puerta de enlace desde un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="76706-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="76706-110">Hola toouse **puerta de enlace\_crear\_de\_JSON** funcione, asígnele el archivo JSON de tooa de ruta de acceso de hello que especifica hello tooload de módulos de borde de IoT.</span><span class="sxs-lookup"><span data-stu-id="76706-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="76706-111">Puede encontrar código de hello de proceso de puerta de enlace de Hola Hola *Hello World* ejemplo Hola [main.c] [ lnk-main-c] archivo.</span><span class="sxs-lookup"><span data-stu-id="76706-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="76706-112">Para mayor legibilidad, hello fragmento de código siguiente muestra una versión abreviada de código de proceso de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="76706-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="76706-113">Este programa de ejemplo crea una puerta de enlace y, a continuación, espera Hola de hello usuario toopress **ENTRAR** clave antes de que se destruye puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="76706-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

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

<span data-ttu-id="76706-114">archivo de configuración de JSON de Hello contiene una lista de tooload de módulos de borde de IoT y vínculos de hello entre módulos Hola.</span><span class="sxs-lookup"><span data-stu-id="76706-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="76706-115">Cada módulo de IoT Edge debe especificar:</span><span class="sxs-lookup"><span data-stu-id="76706-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="76706-116">**nombre**: un nombre único para el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="76706-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="76706-117">**cargador**: un cargador que sabe cómo hello tooload deseado módulo.</span><span class="sxs-lookup"><span data-stu-id="76706-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="76706-118">Los cargadores son un punto de extensión para cargar diferentes tipos de módulos.</span><span class="sxs-lookup"><span data-stu-id="76706-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="76706-119">IoT Edge proporciona cargadores para usarlos con módulos escritos en C nativo, Node.js, Java y .NET.</span><span class="sxs-lookup"><span data-stu-id="76706-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="76706-120">ejemplo de Hola mundo Hola solo utiliza cargador C nativo de hello porque todos los módulos de hello en este ejemplo son bibliotecas dinámicas escritas en C. Para obtener más información acerca de cómo toouse módulos de borde IoT escritos en lenguajes diferentes, vea hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), o [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) ejemplos.</span><span class="sxs-lookup"><span data-stu-id="76706-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="76706-121">**nombre**: nombre de Hola del cargador de Hola usa el módulo de hello tooload.</span><span class="sxs-lookup"><span data-stu-id="76706-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="76706-122">**punto de entrada**: biblioteca de toohello de ruta de acceso de Hola que contiene el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="76706-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="76706-123">En Linux esta biblioteca es un archivo .so y en Windows un archivo .dll.</span><span class="sxs-lookup"><span data-stu-id="76706-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="76706-124">punto de entrada de Hello es tipo toohello específico del cargador que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="76706-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="76706-125">Hola punto de entrada del cargador de Node.js es un archivo .js.</span><span class="sxs-lookup"><span data-stu-id="76706-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="76706-126">Hola punto de entrada del cargador de Java es una ruta de clase y un nombre de clase.</span><span class="sxs-lookup"><span data-stu-id="76706-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="76706-127">Hola punto de entrada del cargador de .NET es un nombre de ensamblado y un nombre de clase.</span><span class="sxs-lookup"><span data-stu-id="76706-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="76706-128">**args**: cualquier módulo de Hola de información de configuración es necesario.</span><span class="sxs-lookup"><span data-stu-id="76706-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="76706-129">Hola después de código se muestra hello JSON usa toodeclare todos los Hola módulos IoT borde de ejemplo de Hola mundo Hola en Linux.</span><span class="sxs-lookup"><span data-stu-id="76706-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="76706-130">Si un módulo requiere que los argumentos depende de diseño de hello del módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="76706-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="76706-131">En este ejemplo, el módulo de registrador de hello toma un argumento que es el archivo de salida de toohello de ruta de acceso de Hola y Hola Hola\_módulo world no tiene ningún argumento.</span><span class="sxs-lookup"><span data-stu-id="76706-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

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

<span data-ttu-id="76706-132">archivo JSON de Hello contiene también vínculos de hello entre módulos de Hola que se pasan a toohello broker.</span><span class="sxs-lookup"><span data-stu-id="76706-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="76706-133">Los vínculos tienen dos propiedades:</span><span class="sxs-lookup"><span data-stu-id="76706-133">A link has two properties:</span></span>

* <span data-ttu-id="76706-134">**origen**: el nombre de un módulo de hello `modules` sección, o `\*`.</span><span class="sxs-lookup"><span data-stu-id="76706-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="76706-135">**receptor**: el nombre de un módulo de hello `modules` sección.</span><span class="sxs-lookup"><span data-stu-id="76706-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="76706-136">Cada vínculo define la ruta y dirección de un mensaje.</span><span class="sxs-lookup"><span data-stu-id="76706-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="76706-137">Mensajes de Hola **origen** módulo se entregan toohello **receptor** módulo.</span><span class="sxs-lookup"><span data-stu-id="76706-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="76706-138">Puede establecer hello **origen** módulo demasiado`\*`, lo que indica que hello **receptor** módulo recibe mensajes desde cualquier módulo.</span><span class="sxs-lookup"><span data-stu-id="76706-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="76706-139">Hello siguiente muestra hello JSON utiliza tooconfigure vínculos entre los módulos de hello usados en Hola Hola\_ejemplo world en Linux.</span><span class="sxs-lookup"><span data-stu-id="76706-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="76706-140">Todos los mensajes generan por hello `hello_world` módulo consume hello `logger` módulo.</span><span class="sxs-lookup"><span data-stu-id="76706-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="76706-141">Publicación de mensajes del módulo hola\_mundo</span><span class="sxs-lookup"><span data-stu-id="76706-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="76706-142">Puede encontrar código de hello usa Hola Hola\_toopublish mensajes de módulo de mundo Hola ['hello_world.c'] [ lnk-helloworld-c] archivo.</span><span class="sxs-lookup"><span data-stu-id="76706-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="76706-143">Hello fragmento de código siguiente muestra una versión modificada del código de hello con comentarios agregados y algunos quitado para mayor legibilidad del código de control de errores:</span><span class="sxs-lookup"><span data-stu-id="76706-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

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

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="76706-144">Procesamiento de mensajes del módulo Hola\_mundo</span><span class="sxs-lookup"><span data-stu-id="76706-144">Hello\_world module message processing</span></span>

<span data-ttu-id="76706-145">Hola Hola\_módulo world nunca procesa los mensajes que otros módulos de borde IoT publican toohello broker.</span><span class="sxs-lookup"><span data-stu-id="76706-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="76706-146">Hola por lo tanto, la implementación de devolución de llamada de mensaje de Hola Hola Hola\_módulo world es una función de operación inefectiva.</span><span class="sxs-lookup"><span data-stu-id="76706-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="76706-147">Publicación y procesamiento de mensajes del módulo logger</span><span class="sxs-lookup"><span data-stu-id="76706-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="76706-148">módulo de registrador Hola recibe mensajes desde el agente de Hola y los escribe tooa archivo.</span><span class="sxs-lookup"><span data-stu-id="76706-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="76706-149">Nunca publica ningún mensaje.</span><span class="sxs-lookup"><span data-stu-id="76706-149">It never publishes any messages.</span></span> <span data-ttu-id="76706-150">Por lo tanto, código de hello del módulo de registrador Hola nunca llama hello **Broker_Publish** (función).</span><span class="sxs-lookup"><span data-stu-id="76706-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="76706-151">Hola **Logger_Receive** función Hola [logger.c] [ lnk-logger-c] archivo es broker de Hola de devolución de llamada de hello invoca el módulo de toodeliver mensajes toohello registrador.</span><span class="sxs-lookup"><span data-stu-id="76706-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="76706-152">Hello fragmento de código siguiente muestra una versión modificada con comentarios agregados y algunos quitado para mayor legibilidad del código de control de errores:</span><span class="sxs-lookup"><span data-stu-id="76706-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="76706-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76706-153">Next steps</span></span>

<span data-ttu-id="76706-154">En este artículo, se ejecutaba una puerta de enlace de IoT borde simple que escribe el archivo de registro de mensajes tooa.</span><span class="sxs-lookup"><span data-stu-id="76706-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="76706-155">toorun un ejemplo que envía mensajes tooIoT concentrador, consulte [IoT borde, enviar mensajes del dispositivo a la nube con un dispositivo simulado con Linux] [ lnk-gateway-simulated-linux] o [IoT borde, enviar mensajes de dispositivo a la nube con una dispositivo simulado mediante Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="76706-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md
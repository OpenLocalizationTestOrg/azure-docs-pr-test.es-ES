> [!div class="op_single_selector"]
> * [<span data-ttu-id="35967-101">Linux</span><span class="sxs-lookup"><span data-stu-id="35967-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="35967-102">Windows</span><span class="sxs-lookup"><span data-stu-id="35967-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="35967-103">Este artículo ofrece un tutorial detallado de hello [código de ejemplo de Hola a todos] [ lnk-helloworld-sample] componentes fundamentales de hello tooillustrate de hello [Azure IoT borde] [ lnk-iot-edge] arquitectura.</span><span class="sxs-lookup"><span data-stu-id="35967-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="35967-104">Hello ejemplo utiliza hello borde de IoT de Azure toobuild una puerta de enlace simple que registra cada cinco segundos de un archivo de tooa de mensaje "¡hello world".</span><span class="sxs-lookup"><span data-stu-id="35967-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="35967-105">En este tutorial, se describen los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="35967-105">This walkthrough covers:</span></span>

* <span data-ttu-id="35967-106">**Hola arquitectura de ejemplo del mundo**: describe cómo [conceptos arquitectónicos de borde de IoT de Azure] [ lnk-edge-concepts] toohello ejemplo de Hola a todos y cómo encajan los componentes de Hola se aplican.</span><span class="sxs-lookup"><span data-stu-id="35967-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="35967-107">**¿Cómo toobuild Hola ejemplo**: ejemplo de Hola Hola a toobuild necesarios pasos.</span><span class="sxs-lookup"><span data-stu-id="35967-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="35967-108">**¿Cómo toorun Hola ejemplo**: ejemplo de Hola Hola a toorun necesarios pasos.</span><span class="sxs-lookup"><span data-stu-id="35967-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="35967-109">**La salida típica**: muestra un ejemplo de Hola tooexpect de salida al ejecutar el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="35967-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="35967-110">**Fragmentos de código**: una colección de tooshow de fragmentos de código cómo implementa el ejemplo hello World Hola principales componentes de puerta de enlace de IoT borde.</span><span class="sxs-lookup"><span data-stu-id="35967-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="35967-111">Arquitectura de ejemplo Hello World</span><span class="sxs-lookup"><span data-stu-id="35967-111">Hello World sample architecture</span></span>
<span data-ttu-id="35967-112">ejemplo de Hola mundo Hola ilustra los conceptos de Hola que se describe en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="35967-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="35967-113">ejemplo de Hola mundo Hola implementa una puerta de enlace de IoT perimetral que tiene una canalización consta de dos módulos de IoT borde:</span><span class="sxs-lookup"><span data-stu-id="35967-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="35967-114">Hola *Hola a todos* módulo crea un mensaje cada cinco segundos y le pasa el módulo de registrador toohello.</span><span class="sxs-lookup"><span data-stu-id="35967-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="35967-115">Hola *registrador* mensajes de saludo de escrituras de módulo que recibe el archivo tooa.</span><span class="sxs-lookup"><span data-stu-id="35967-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Arquitectura del ejemplo Hola mundo creada con Azure IoT Edge][4]

<span data-ttu-id="35967-117">Como se describe en la sección anterior de hello, Hola mundo Hola módulo no pasa los mensajes directamente módulo de registrador toohello cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="35967-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="35967-118">En su lugar, publica a un agente de toohello mensajes cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="35967-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="35967-119">módulo de registrador Hola recibe el mensaje de bienvenida desde el agente de Hola y actúa sobre ella, escribir el contenido de hello del archivo de tooa de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="35967-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="35967-120">módulo de registrador Hola sólo consume mensajes desde el agente de hello, nunca publica nuevo agente de toohello de mensajes.</span><span class="sxs-lookup"><span data-stu-id="35967-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Cómo Hola broker enruta los mensajes entre los módulos en el borde de IoT de Azure][5]

<span data-ttu-id="35967-122">Hello ilustración anterior muestra hello arquitectura de ejemplo de Hola mundo Hola y rutas de acceso relativas de hello toohello archivos de código fuente que implementan diferentes partes de ejemplo de Hola Hola [repositorio][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="35967-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="35967-123">Explorar el código de hello por su cuenta o usar fragmentos de código de hello siguiente como guía.</span><span class="sxs-lookup"><span data-stu-id="35967-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md
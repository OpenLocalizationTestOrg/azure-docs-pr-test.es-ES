> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ad89-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="7ad89-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="7ad89-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="7ad89-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="7ad89-103">C#</span><span class="sxs-lookup"><span data-stu-id="7ad89-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="7ad89-104">Java</span><span class="sxs-lookup"><span data-stu-id="7ad89-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="7ad89-105">Los dispositivos gemelos son documentos JSON que almacenan información sobre el estado de los dispositivos (metadatos, configuraciones y condiciones).</span><span class="sxs-lookup"><span data-stu-id="7ad89-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="7ad89-106">Centro de IoT conserva a un gemelas de dispositivo para cada dispositivo que se conecta tooit.</span><span class="sxs-lookup"><span data-stu-id="7ad89-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="7ad89-107">Use los dispositivos gemelos para:</span><span class="sxs-lookup"><span data-stu-id="7ad89-107">Use device twins to:</span></span>

* <span data-ttu-id="7ad89-108">Almacenar metadatos del dispositivo desde el back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="7ad89-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="7ad89-109">Notificar la información de estado actual, como capacidades disponibles y las condiciones (por ejemplo, hello conectividad método usado) desde la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7ad89-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="7ad89-110">Sincronizar el estado de Hola de flujos de trabajo de larga duración (por ejemplo, las actualizaciones de firmware y configuración) entre una aplicación de dispositivo y una aplicación de back-end.</span><span class="sxs-lookup"><span data-stu-id="7ad89-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="7ad89-111">Consultar los metadatos, la configuración o el estado del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7ad89-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="7ad89-112">Los dispositivos gemelos están diseñados para la sincronización y para consultar las condiciones y configuraciones del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7ad89-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="7ad89-113">Obtener más información acerca de cuándo: los gemelos de toouse dispositivo se encuentra en [comprender: los gemelos de dispositivo][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="7ad89-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="7ad89-114">Los dispositivos gemelos se almacenan en un IoT Hub y contienen:</span><span class="sxs-lookup"><span data-stu-id="7ad89-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="7ad89-115">*etiquetas*, metadatos del dispositivo solo puedan acceder aquellos Hola solución back-end;</span><span class="sxs-lookup"><span data-stu-id="7ad89-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="7ad89-116">*las propiedades adecuadas*, objetos JSON modificables por solución Hola realizar copia de final y observable Hola del dispositivo; y</span><span class="sxs-lookup"><span data-stu-id="7ad89-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="7ad89-117">*notifica las propiedades*, los objetos JSON modificables por aplicación de dispositivo de hello y legibles por hello solución back-end.</span><span class="sxs-lookup"><span data-stu-id="7ad89-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="7ad89-118">Las etiquetas y propiedades no pueden contener matrices, pero se pueden anidar objetos.</span><span class="sxs-lookup"><span data-stu-id="7ad89-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="7ad89-119">Además, Hola solución back-end puede consultar en función de todos los Hola por encima de los datos: los gemelos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7ad89-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="7ad89-120">Consulte demasiado[comprender: los gemelos de dispositivo] [ lnk-twins] para obtener más información acerca de: los gemelos de dispositivo y toohello [lenguaje de consultas del centro de IoT] [ lnk-query] referencia Para consultar.</span><span class="sxs-lookup"><span data-stu-id="7ad89-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="7ad89-121">En este momento, son accesibles únicamente desde dispositivos que se conectan tooIoT concentrador: los gemelos de dispositivo mediante el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="7ad89-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="7ad89-122">Consulte toohello [compatibilidad MQTT] [ lnk-devguide-mqtt] artículo para obtener instrucciones sobre cómo toouse de aplicación de dispositivo existente de tooconvert MQTT.</span><span class="sxs-lookup"><span data-stu-id="7ad89-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="7ad89-123">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="7ad89-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="7ad89-124">Crear una aplicación de back-end que agrega *etiquetas* tooa gemelas de dispositivo y una aplicación de dispositivo simulado que informa de su conectividad de canal como un *notificado propiedad* en gemelas de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ad89-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="7ad89-125">Consultar dispositivos desde la aplicación de back-end se utilizan filtros en etiquetas de Hola y propiedades que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7ad89-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md
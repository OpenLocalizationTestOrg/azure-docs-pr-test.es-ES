> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca789-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="ca789-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="ca789-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="ca789-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="ca789-103">C#</span><span class="sxs-lookup"><span data-stu-id="ca789-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="ca789-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="ca789-104">Introduction</span></span>

<span data-ttu-id="ca789-105">En [empezar a trabajar con: los gemelos de centro de IoT dispositivo][lnk-twin-tutorial], ha aprendido cómo tooset metadatos del dispositivo de nuevo la solución final utilizar *etiquetas*, informe de las condiciones del dispositivo desde una aplicación de dispositivo usar *notificado propiedades*y consultar esta información utilizando un lenguaje similar a SQL.</span><span class="sxs-lookup"><span data-stu-id="ca789-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="ca789-106">En este tutorial, obtendrá información sobre cómo toouse Hola del doble del dispositivo de hello *deseado propiedades* junto con *notificado propiedades*, tooremotely configurar aplicaciones para dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ca789-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="ca789-107">Más concretamente, este tutorial muestra cómo se notifican un gemelas de dispositivo y propiedades que desee habilitar una configuración de varios pasos de una aplicación de dispositivo y proporcionan Hola visibilidad toohello solución back-end de estado de Hola de esta operación a través de todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ca789-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="ca789-108">Puede encontrar más información sobre el rol de Hola de configuraciones de dispositivos en [información general de administración de dispositivos con el centro de IoT][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="ca789-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="ca789-109">En un nivel superior, utilizando: los gemelos de dispositivo permite Hola solución back-end toospecify Hola configuración deseada para los dispositivos de hello administrado, en lugar de enviar comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="ca789-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="ca789-110">Esto coloca el dispositivo de hello responsable de configurar Hola mejor manera tooupdate su configuración (muy importante en escenarios de IoT cuyas condiciones de dispositivo específico afecten a Hola capacidad tooimmediately ejecutar comandos específicos), al notificar continuamente toohello solución volver finalice el estado actual de Hola y posibles condiciones de error del proceso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca789-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="ca789-111">Este patrón es toohello instrumental de administración de grandes conjuntos de dispositivos, puesto que permite Hola solución back-end toohave visibilidad completa del estado de Hola Hola del proceso de configuración en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ca789-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="ca789-112">En aquellos escenarios en los que los dispositivos se controlen de forma más interactiva (activar un ventilador desde una aplicación controlada por el usuario), considere la posibilidad de usar [métodos directos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="ca789-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="ca789-113">En este tutorial, cambios de back-end de soluciones de Hola Hola la configuración de telemetría de un dispositivo de destino y, como resultado de que, aplicación de dispositivo de hello sigue un tooapply de proceso en varias fases una configuración de actualización (por ejemplo, que requieren un reinicio del módulo de software, que este tutorial simula con un retraso simple).</span><span class="sxs-lookup"><span data-stu-id="ca789-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="ca789-114">Hola solución back-end almacena la configuración de hello en propiedades deseado del doble del dispositivo de Hola Hola siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="ca789-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="ca789-115">Puesto que las configuraciones pueden ser objetos complejos, normalmente se asignan identificadores únicos (hashes o [GUID][lnk-guid]) toosimplify sus comparaciones.</span><span class="sxs-lookup"><span data-stu-id="ca789-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="ca789-116">aplicación de dispositivo Hello notifica su configuración actual propiedad Hola deseado de la creación de reflejo **telemetryConfig** Hola notificado propiedades:</span><span class="sxs-lookup"><span data-stu-id="ca789-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="ca789-117">Tenga en cuenta cómo se notifica hello **telemetryConfig** tiene una propiedad adicional **estado**, usa el estado de hello tooreport Hola configuración del proceso de actualización.</span><span class="sxs-lookup"><span data-stu-id="ca789-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="ca789-118">Cuando se recibe una nueva configuración deseada, aplicación de dispositivo de hello notifica una configuración pendiente cambiando Hola información:</span><span class="sxs-lookup"><span data-stu-id="ca789-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="ca789-119">A continuación, en algún momento posterior, aplicación de dispositivo de hello notificará Hola éxito o error de esta operación actualizando Hola por encima de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="ca789-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="ca789-120">Tenga en cuenta cómo Hola solución back-end es capaz, en cualquier momento, el estado de hello tooquery Hola del proceso de configuración en todos los dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca789-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="ca789-121">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="ca789-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ca789-122">Crear una aplicación de dispositivo simulado que recibe las actualizaciones de configuración de back-end de hello soluciones e informes de varias actualizaciones como *notificado propiedades* en configuración de hello el proceso de actualización.</span><span class="sxs-lookup"><span data-stu-id="ca789-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="ca789-123">Cree una aplicación de back-end que las actualizaciones de Hola configuración deseada de un dispositivo y, a continuación, las consultas Hola proceso de actualización de configuración.</span><span class="sxs-lookup"><span data-stu-id="ca789-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

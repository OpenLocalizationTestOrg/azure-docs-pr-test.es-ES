> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d526-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="4d526-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="4d526-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="4d526-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="4d526-103">C#</span><span class="sxs-lookup"><span data-stu-id="4d526-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="4d526-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="4d526-104">Introduction</span></span>

<span data-ttu-id="4d526-105">En [Introducción a los dispositivos gemelos de IoT Hub][lnk-twin-tutorial], ha aprendido a establecer metadatos del dispositivo desde el back-end de la solución mediante *etiquetas*, a informar de las condiciones del dispositivo desde una aplicación de dispositivo mediante *propiedades notificadas* y a consultar esta información con un lenguaje similar a SQL.</span><span class="sxs-lookup"><span data-stu-id="4d526-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how to set device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="4d526-106">En este tutorial, aprenderá a usar las *propiedades deseadas* del dispositivo gemelo, además de las *propiedades notificadas*, para configurar aplicaciones de dispositivo de forma remota.</span><span class="sxs-lookup"><span data-stu-id="4d526-106">In this tutorial, you will learn how to use the the device twin's *desired properties* along with *reported properties*, to remotely configure device apps.</span></span> <span data-ttu-id="4d526-107">Más concretamente, este tutorial muestra la forma en que las propiedades notificadas y deseadas de un dispositivo gemelo permiten configurar una aplicación de dispositivo en varios pasos, y proporcionan al back-end de la solución visibilidad sobre el estado de esta operación en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4d526-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide the visibility to the solution back end of the status of this operation across all devices.</span></span> <span data-ttu-id="4d526-108">Puede encontrar más información sobre el rol de las configuraciones de dispositivo en [Información general sobre la administración de dispositivos con IoT Hub][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="4d526-108">You can find more information regarding the role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="4d526-109">De forma general, el uso de dispositivos gemelos permite que el back-end de la solución especifique la configuración deseada para los dispositivos administrados, en lugar de enviar comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="4d526-109">At a high level, using device twins enables the solution back end to specify the desired configuration for the managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="4d526-110">De esta forma, se encarga al dispositivo que establezca la mejor manera de actualizar su configuración (algo muy importante en los escenarios de IoT en los que las condiciones específicas del dispositivo afectan a la capacidad de ejecutar comandos específicos de manera inmediata), al mismo tiempo que envía de forma continua al back-end de la solución notificaciones sobre el estado actual y las posibles condiciones de error del proceso de actualización.</span><span class="sxs-lookup"><span data-stu-id="4d526-110">This puts the device in charge of setting up the best way to update its configuration (very important in IoT scenarios where specific device conditions affect the ability to immediately carry out specific commands), while continually reporting to the solution back end the current state and potential error conditions of the update process.</span></span> <span data-ttu-id="4d526-111">Este patrón es fundamental para la administración de grandes conjuntos de dispositivos, ya que permite que el back-end de la solución tenga una visibilidad completa del estado del proceso de configuración en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4d526-111">This pattern is instrumental to the management of large sets of devices, as it enables the solution back end to have full visibility of the state of the configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="4d526-112">En aquellos escenarios en los que los dispositivos se controlen de forma más interactiva (activar un ventilador desde una aplicación controlada por el usuario), considere la posibilidad de usar [métodos directos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="4d526-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="4d526-113">En este tutorial, el back-end de la solución cambia la configuración de la telemetría de un dispositivo de destino y, como consecuencia, la aplicación del dispositivo sigue un proceso con varios pasos para aplicar una actualización de la configuración (por ejemplo, que requiera que se reinicie un módulo de software), algo que en este tutorial se simula con un simple retraso.</span><span class="sxs-lookup"><span data-stu-id="4d526-113">In this tutorial, the solution back end changes the telemetry configuration of a target device and, as a result of that, the device app follows a multi-step process to apply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="4d526-114">El back-end de la solución almacena la configuración en las propiedades deseadas del dispositivo gemelo como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="4d526-114">The solution back end stores the configuration in the device twin's desired properties in the following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of the configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="4d526-115">Dado que las configuraciones pueden ser objetos complejos, normalmente se les asignan identificadores únicos (hashes o [GUID][lnk-guid]) para simplificar las comparaciones.</span><span class="sxs-lookup"><span data-stu-id="4d526-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) to simplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="4d526-116">La aplicación del dispositivo notifica su configuración actual, para lo que crea un reflejo de la propiedad deseada **telemetryConfig** en las propiedades notificadas:</span><span class="sxs-lookup"><span data-stu-id="4d526-116">The device app reports its current configuration mirroring the desired property **telemetryConfig** in the reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="4d526-117">Tenga en cuenta que la propiedad **telemetryConfig** notificada tiene un **estado** de propiedad adicional, que se usa para notificar el estado del proceso de actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="4d526-117">Note how the reported **telemetryConfig** has an additional property **status**, used to report the state of the configuration update process.</span></span>

<span data-ttu-id="4d526-118">Cuando se recibe una nueva configuración deseada, la aplicación del dispositivo notifica que hay una configuración pendiente, para lo que cambia la información:</span><span class="sxs-lookup"><span data-stu-id="4d526-118">When a new desired configuration is received, the device app reports a pending configuration by changing the information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of the pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="4d526-119">Posteriormente, la aplicación del dispositivo le indicará el acierto o error de esta operación mediante la actualización de la propiedad anterior.</span><span class="sxs-lookup"><span data-stu-id="4d526-119">Then, at some later time, the device app will report the success or failure of this operation by updating the above property.</span></span>
<span data-ttu-id="4d526-120">Tenga en cuenta que el back-end de la solución puede, en cualquier momento, consultar el estado del proceso de configuración de todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4d526-120">Note how the solution back end is able, at any time, to query the status of the configuration process across all the devices.</span></span>

<span data-ttu-id="4d526-121">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="4d526-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="4d526-122">Crear una aplicación de dispositivo simulado que reciba las actualizaciones de configuración del back-end de la solución y notifique varias actualizaciones como *propiedades notificadas* en el proceso de actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="4d526-122">Create a simulated device app that receives configuration updates from the solution back end, and reports multiple updates as *reported properties* on the configuration update process.</span></span>
* <span data-ttu-id="4d526-123">Crear una aplicación de back-end que actualice la configuración deseada de un dispositivo y, a continuación, consulte el proceso de actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="4d526-123">Create a back-end app that updates the desired configuration of a device, and then queries the configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

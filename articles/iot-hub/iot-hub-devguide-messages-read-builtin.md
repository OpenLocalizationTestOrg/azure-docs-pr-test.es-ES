---
title: "punto de conexión integrado de aaaUnderstand Hola centro de IoT de Azure | Documentos de Microsoft"
description: "Guía del desarrollador: describe cómo toouse Hola integrados, mensajes de dispositivo a la nube de leer de punto de conexión compatible de concentrador de eventos."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="bccf2-103">Leer los mensajes de dispositivo para la nube de extremo predefinido Hola</span><span class="sxs-lookup"><span data-stu-id="bccf2-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="bccf2-104">De forma predeterminada, los mensajes son el punto de conexión de toohello enrutado integrados a nivel de servicio (**mensajes de eventos**), que es compatible con [centros de eventos][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="bccf2-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="bccf2-105">Este punto de conexión está actualmente solo exponen mediante hello [AMQP] [ lnk-amqp] protocolo en el puerto 5671.</span><span class="sxs-lookup"><span data-stu-id="bccf2-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="bccf2-106">Un centro de IoT expone Hola tras propiedades tooenable se toocontrol Hola extremo de mensajería compatible de concentrador de eventos predefinido **mensajes de eventos**.</span><span class="sxs-lookup"><span data-stu-id="bccf2-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="bccf2-107">Propiedad</span><span class="sxs-lookup"><span data-stu-id="bccf2-107">Property</span></span>            | <span data-ttu-id="bccf2-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="bccf2-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="bccf2-109">**Número de particiones**</span><span class="sxs-lookup"><span data-stu-id="bccf2-109">**Partition count**</span></span> | <span data-ttu-id="bccf2-110">Establezca esta propiedad en el número de hello toodefine de creación de [particiones] [ lnk-event-hub-partitions] para la recopilación de eventos de dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="bccf2-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="bccf2-111">**Tiempo de retención**</span><span class="sxs-lookup"><span data-stu-id="bccf2-111">**Retention time**</span></span>  | <span data-ttu-id="bccf2-112">Esta propiedad especifica cuánto tiempo, en días, IoT Hub conserva los mensajes.</span><span class="sxs-lookup"><span data-stu-id="bccf2-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="bccf2-113">valor predeterminado de Hello es un día, pero puede ser mayor tooseven días.</span><span class="sxs-lookup"><span data-stu-id="bccf2-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="bccf2-114">Centro de IoT también permite toomanage grupos de consumidores en hello integrada dispositivo a la nube extremo de recepción.</span><span class="sxs-lookup"><span data-stu-id="bccf2-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="bccf2-115">De forma predeterminada, todos los mensajes que no coinciden de forma explícita una regla de enrutamiento de mensajes se escriben toohello punto de conexión integrados.</span><span class="sxs-lookup"><span data-stu-id="bccf2-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="bccf2-116">Si deshabilita esta ruta de reserva, los mensajes que no cumplen explícitamente ninguna reglas de enrutamiento de mensajes se quitan.</span><span class="sxs-lookup"><span data-stu-id="bccf2-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="bccf2-117">Puede modificar el tiempo de retención de hello, ya sea mediante programación a través de hello [API de REST de proveedor de recursos de centro de IoT][lnk-resource-provider-apis], o mediante el uso de hello [portal de Azure] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="bccf2-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="bccf2-118">Centro de IoT expone hello **mensajes de eventos** mensajes de dispositivo a la nube de hello tooread recibidos por el centro de servicios de extremo predefinido para el back-end.</span><span class="sxs-lookup"><span data-stu-id="bccf2-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="bccf2-119">Se trata de eventos concentrador compatible, lo que le permite toouse cualquier servicio de centros de eventos de hello mecanismos hello es compatible con para leer los mensajes.</span><span class="sxs-lookup"><span data-stu-id="bccf2-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="bccf2-120">Leer desde el punto de conexión integrados de Hola</span><span class="sxs-lookup"><span data-stu-id="bccf2-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="bccf2-121">Cuando usas hello [SDK del Bus de servicio de Azure para .NET] [ lnk-servicebus-sdk] o hello [centros de eventos - Host procesador de eventos][lnk-eventprocessorhost], puede usar cualquier conexión de centro de IoT cadenas con los permisos correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bccf2-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="bccf2-122">A continuación, utilice **mensajes de eventos** como nombre de concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bccf2-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="bccf2-123">Cuando usas SDK (o integraciones de producto) que no son conscientes de centro de IoT, debe recuperar un punto de conexión compatible de concentrador de eventos y un nombre de concentrador de eventos-compatible con opciones de configuración de centro de IoT de hello en hello [portal de Azure] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="bccf2-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="bccf2-124">En la hoja de centro de IoT de hello, haga clic en **extremos**.</span><span class="sxs-lookup"><span data-stu-id="bccf2-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="bccf2-125">Hola **extremos integrados** sección, haga clic en **eventos**.</span><span class="sxs-lookup"><span data-stu-id="bccf2-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="bccf2-126">Hello hoja contiene Hola siguientes valores: **punto de conexión de concentrador de eventos-compatible con**, **nombre de concentrador de eventos-compatible con**, **particiones**, **detiempoderetención**, y **grupos de consumidores**.</span><span class="sxs-lookup"><span data-stu-id="bccf2-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Configuración de dispositivo a nube][img-eventhubcompatible]

<span data-ttu-id="bccf2-128">Hola IoT Hub SDK requiere Hola nombre de punto de conexión de centro de IoT, que es **mensajes de eventos** tal y como se muestra en hello **extremos** hoja.</span><span class="sxs-lookup"><span data-stu-id="bccf2-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="bccf2-129">Si requiere Hola SDK que usa un **Hostname** o **Namespace** valor, quite el esquema de Hola Hola **punto de conexión de concentrador de eventos-compatible con**.</span><span class="sxs-lookup"><span data-stu-id="bccf2-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="bccf2-130">Por ejemplo, si el punto de conexión compatible de concentrador de eventos es **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** sería  **el centro de IOT-ns-myiothub-1234.servicebus.windows.net**, hello y **Namespace** sería **el centro de IOT-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="bccf2-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="bccf2-131">A continuación, puede usar cualquier directiva de acceso compartido que tiene hello **ServiceConnect** toohello tooconnect de permisos especificado concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="bccf2-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="bccf2-132">Si necesita toobuild una cadena de conexión de concentrador de eventos mediante el uso de la información anterior de hello, use Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="bccf2-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="bccf2-133">SDK de Hello e integraciones que pueden usar con los puntos de conexión compatible de concentrador de eventos que expone el centro de IoT incluye elementos de Hola Hola lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="bccf2-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="bccf2-134">[Cliente de Event Hubs de Java](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="bccf2-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="bccf2-135">[Spout de Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bccf2-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="bccf2-136">Puede ver hello [apetezca charlar un origen](https://github.com/apache/storm/tree/master/external/storm-eventhubs) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="bccf2-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="bccf2-137">[Integración de Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="bccf2-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bccf2-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bccf2-138">Next steps</span></span>

<span data-ttu-id="bccf2-139">Para obtener más información sobre los puntos de conexión de IoT Hub, vea [Puntos de conexión de IoT Hub][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="bccf2-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="bccf2-140">Hola [Introducción] [ lnk-get-started] los tutoriales muestra cómo toosend mensajes de dispositivo para la nube de simulación dispositivos y leen los mensajes de Hola de extremo predefinido Hola.</span><span class="sxs-lookup"><span data-stu-id="bccf2-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="bccf2-141">Para obtener información más detallada, vea hello [mensajes de dispositivo a la nube del centro de IoT de proceso mediante las rutas de] [ lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="bccf2-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="bccf2-142">Si desea que tooroute su dispositivo a la nube mensajes toocustom extremos, vea [utilizar las rutas de mensajes y los extremos personalizados para los mensajes de dispositivo para la nube][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="bccf2-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/

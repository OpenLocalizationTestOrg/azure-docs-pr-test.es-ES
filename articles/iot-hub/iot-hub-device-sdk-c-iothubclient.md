---
title: SDK de dispositivo IoT de Azure para C - IoTHubClient | Microsoft Docs
description: "Describe cómo usar la biblioteca IoTHubClient del SDK de dispositivo Azure IoT para C con el fin de crear aplicaciones para dispositivos que se comunican con un centro de IoT Hub."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: 422d89014511f0d08ba57a893570ff7b253b7bc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="b4fec-103">SDK de dispositivo IoT de Microsoft Azure para C: más información sobre IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="b4fec-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="b4fec-104">En el [primer el artículo](iot-hub-device-sdk-c-intro.md) de esta serie se presentaba el **SDK de dispositivo IoT de Azure**. En este artículo se explicaba que hay dos capas de arquitectura en el SDK.</span><span class="sxs-lookup"><span data-stu-id="b4fec-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="b4fec-105">En la base está la biblioteca de **IoTHubClient** que administra directamente la comunicación con Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b4fec-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="b4fec-106">Y está también la biblioteca del **serializador** , que se basa en él para proporcionar servicios de serialización.</span><span class="sxs-lookup"><span data-stu-id="b4fec-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="b4fec-107">En este artículo le proporcionamos detalles adicionales sobre la biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="b4fec-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="b4fec-108">El artículo anterior describe cómo usar la biblioteca **IoTHubClient** para enviar eventos a Centro de IoT y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="b4fec-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="b4fec-109">En este artículo ampliamos esa discusión y explicamos cómo administrar con mayor exactitud *cuándo* enviar y recibir datos, con una introducción a la **API de nivel inferior**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="b4fec-110">También explicaremos cómo adjuntar propiedades a eventos (y recuperarlas de mensajes) mediante las características de control de propiedades en la biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="b4fec-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="b4fec-111">Por último, proporcionaremos una explicación adicional sobre las diferentes formas de controlar los mensajes recibidos desde el Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b4fec-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="b4fec-112">El artículo concluye con un par de temas variados, e incluye más información acerca de las credenciales de dispositivo y cómo cambiar el comportamiento de **IoTHubClient** mediante las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="b4fec-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="b4fec-113">Usaremos ejemplos del SDK de **IoTHubClient** para explicar estos temas.</span><span class="sxs-lookup"><span data-stu-id="b4fec-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="b4fec-114">Si quiere seguir el artículo, vea las aplicaciones **iothub\_client\_sample\_http** y **iothub\_client\_sample\_amqp** que se incluyen en el SDK de dispositivo IoT de Azure para C. Todo lo descrito a continuación se muestra en estos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="b4fec-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="b4fec-115">Puede encontrar el [**SDK de dispositivo IoT de Azure para C**](https://github.com/Azure/azure-iot-sdk-c) en el repositorio de GitHub y ver los detalles de la API en la [referencia de la API de C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="b4fec-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="b4fec-116">API de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="b4fec-116">The lower-level APIs</span></span>
<span data-ttu-id="b4fec-117">En el artículo anterior describimos el funcionamiento básico de **IotHubClient** en el contexto de la aplicación **iothub\_client\_sample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="b4fec-118">Por ejemplo, se explicó cómo inicializar la biblioteca mediante este código.</span><span class="sxs-lookup"><span data-stu-id="b4fec-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="b4fec-119">Se describió también cómo enviar eventos mediante la llamada a esta función.</span><span class="sxs-lookup"><span data-stu-id="b4fec-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="b4fec-120">En el artículo también se describió cómo recibir mensajes mediante el registro de una función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="b4fec-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="b4fec-121">El artículo también mostró cómo liberar recursos mediante código como el siguiente.</span><span class="sxs-lookup"><span data-stu-id="b4fec-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="b4fec-122">Sin embargo, hay funciones complementarias de cada una de estas API:</span><span class="sxs-lookup"><span data-stu-id="b4fec-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="b4fec-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="b4fec-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="b4fec-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="b4fec-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="b4fec-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="b4fec-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="b4fec-126">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="b4fec-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="b4fec-127">Estas funciones incluyen "LL" en el nombre de la API.</span><span class="sxs-lookup"><span data-stu-id="b4fec-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="b4fec-128">Aparte de eso, los parámetros de cada una de estas funciones son idénticos a sus correspondiente no LL.</span><span class="sxs-lookup"><span data-stu-id="b4fec-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="b4fec-129">Sin embargo, el comportamiento de estas funciones es diferente en un aspecto importante.</span><span class="sxs-lookup"><span data-stu-id="b4fec-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="b4fec-130">Cuando se llama a **IoTHubClient\_CreateFromConnectionString**, las bibliotecas subyacentes crean un nuevo subproceso que se ejecuta en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b4fec-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="b4fec-131">Este subproceso envía eventos al Centro de IoT y recibe mensajes del mismo.</span><span class="sxs-lookup"><span data-stu-id="b4fec-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="b4fec-132">No se crea ningún subproceso de este tipo cuando se trabaja con las API "LL".</span><span class="sxs-lookup"><span data-stu-id="b4fec-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="b4fec-133">La creación de subproceso en segundo plano es muy práctico para el desarrollador.</span><span class="sxs-lookup"><span data-stu-id="b4fec-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="b4fec-134">No tiene que preocuparse por enviar eventos y recibir mensajes del Centro de IoT de forma explícita porque esto se produce automáticamente en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b4fec-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="b4fec-135">Por el contrario, las API "LL" proporcionan un control explícito sobre la comunicación con IoT Hub, si lo necesita.</span><span class="sxs-lookup"><span data-stu-id="b4fec-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="b4fec-136">Para comprenderlo mejor, veamos un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b4fec-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="b4fec-137">Cuando se llama a **IoTHubClient\_SendEventAsync**, lo que realmente se está haciendo es colocar el evento en un búfer.</span><span class="sxs-lookup"><span data-stu-id="b4fec-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="b4fec-138">El subproceso en segundo plano creado cuando se llama a **IoTHubClient\_CreateFromConnectionString** supervisa continuamente este búfer y envía los datos que contiene a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b4fec-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="b4fec-139">Esto sucede en segundo plano al mismo tiempo que el subproceso principal está realizando otro trabajo.</span><span class="sxs-lookup"><span data-stu-id="b4fec-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="b4fec-140">De forma similar, cuando se registra una función de devolución de llamada para mensajes mediante **IoTHubClient\_SetMessageCallback**, está indicando al SDK que el subproceso en segundo plano debe invocar la función de devolución de llamada cuando se recibe un mensaje, independientemente del subproceso principal.</span><span class="sxs-lookup"><span data-stu-id="b4fec-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="b4fec-141">Las API "LL" no crean un subproceso en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b4fec-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="b4fec-142">En su lugar, debe llamarse una nueva API para enviar y recibir datos a y desde Centro de IoT de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="b4fec-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="b4fec-143">Esto se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="b4fec-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="b4fec-144">La aplicación **iothub\_client\_sample\_http** que se incluye en el SDK muestra las API de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="b4fec-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="b4fec-145">En este ejemplo, enviamos eventos a IoT Hub con un código como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="b4fec-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="b4fec-146">Las tres primeras líneas crean el mensaje y la última línea envía el evento.</span><span class="sxs-lookup"><span data-stu-id="b4fec-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="b4fec-147">Sin embargo, tal y como se mencionó anteriormente, "enviar" el evento significa solamente que los datos se colocan en un búfer.</span><span class="sxs-lookup"><span data-stu-id="b4fec-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="b4fec-148">Nada se transmite en la red cuando llamamos a **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="b4fec-149">Para poder insertar realmente los datos en el IoT Hub, tiene que llamar a **IoTHubClient\_LL\_DoWork** como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b4fec-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="b4fec-150">Este código (de la aplicación **iothub\_client\_sample\_http**) llama repetidamente a **IoTHubClient\_LL\_DoWork**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="b4fec-151">Cada vez que se llama a **IoTHubClient\_LL\_DoWork**, envía algunos eventos del búfer al IoT Hub y recupera un mensaje en cola enviado al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4fec-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="b4fec-152">Esto último significa que si se registró una función de devolución de llamada para mensajes, se invoca la devolución de llamada (suponiendo que hay mensajes en cola).</span><span class="sxs-lookup"><span data-stu-id="b4fec-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="b4fec-153">Tendríamos registrado este tipo de función de devolución de llamada con un código como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="b4fec-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="b4fec-154">La razón por la que se llama a **IoTHubClient\_LL\_DoWork** a menudo en un bucle es porque cada vez que se llama, envía *algunos* eventos almacenados en el búfer al IoT Hub y recupera *el siguiente* mensaje en cola para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4fec-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="b4fec-155">No está garantizado que cada llamada envíe todos los eventos almacenados en búfer o recupere todos los mensajes en cola.</span><span class="sxs-lookup"><span data-stu-id="b4fec-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="b4fec-156">Si desea enviar todos los eventos en el búfer y luego continuar con otro procesamiento, puede reemplazar este bucle con un código como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="b4fec-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="b4fec-157">Este código llama a **IoTHubClient\_LL\_DoWork** hasta que todos los eventos del búfer se envíen al IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b4fec-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="b4fec-158">Tenga en cuenta que esto no significa que se recibieran todos los mensajes en cola.</span><span class="sxs-lookup"><span data-stu-id="b4fec-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="b4fec-159">El motivo en parte es que comprobar "todos" los mensajes no es una acción determinista.</span><span class="sxs-lookup"><span data-stu-id="b4fec-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="b4fec-160">¿Qué sucede si recupera "todos" los mensajes pero se envía otro al dispositivo inmediatamente después?</span><span class="sxs-lookup"><span data-stu-id="b4fec-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="b4fec-161">Una mejor manera de afrontar esto es con un tiempo de espera programado.</span><span class="sxs-lookup"><span data-stu-id="b4fec-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="b4fec-162">Por ejemplo, la función de devolución de llamada de mensaje puede restablecer un temporizador cada vez que se invoca.</span><span class="sxs-lookup"><span data-stu-id="b4fec-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="b4fec-163">Después puede escribir lógica para continuar el procesamiento si, por ejemplo, no se recibió ningún mensaje en los últimos *X* segundos.</span><span class="sxs-lookup"><span data-stu-id="b4fec-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="b4fec-164">Cuando termine de incorporar eventos y de recibir mensajes, asegúrese de llamar a la función correspondiente para limpiar los recursos.</span><span class="sxs-lookup"><span data-stu-id="b4fec-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="b4fec-165">Básicamente, hay solo un conjunto de API para enviar y recibir datos con un subproceso en segundo plano y otro conjunto de API que hace lo mismo sin el subproceso en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b4fec-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="b4fec-166">Muchos desarrolladores pueden preferir las API no LL, pero las API de nivel inferior son útiles cuando el desarrollador desea un control explícito sobre las transmisiones de red.</span><span class="sxs-lookup"><span data-stu-id="b4fec-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="b4fec-167">Por ejemplo, algunos dispositivos recopilan datos con el tiempo y solo incorporan eventos a intervalos especificados (por ejemplo, una vez cada hora o una vez al día).</span><span class="sxs-lookup"><span data-stu-id="b4fec-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="b4fec-168">Las API de nivel inferior permiten controlar de forma explícita cuándo se envían y reciben los datos desde el Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b4fec-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="b4fec-169">Otros preferirán la simplicidad que proporcionan las API de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="b4fec-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="b4fec-170">Todo ocurre en el subproceso principal en lugar de que parte del trabajo se realice en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b4fec-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="b4fec-171">Sea cual sea el modelo que elija, asegúrese de mantener la coherencia en las API que usa.</span><span class="sxs-lookup"><span data-stu-id="b4fec-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="b4fec-172">Si empieza con una llamada a **IoTHubClient\_LL\_CreateFromConnectionString**, asegúrese de usar solamente las API de nivel inferior correspondientes para cualquier trabajo que realice a continuación:</span><span class="sxs-lookup"><span data-stu-id="b4fec-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="b4fec-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="b4fec-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="b4fec-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="b4fec-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="b4fec-175">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="b4fec-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="b4fec-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="b4fec-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="b4fec-177">Y lo mismo sucede al revés.</span><span class="sxs-lookup"><span data-stu-id="b4fec-177">The opposite is true as well.</span></span> <span data-ttu-id="b4fec-178">Si empieza con **IoTHubClient\_CreateFromConnectionString** siga con las API no LL para cualquier procesamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="b4fec-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="b4fec-179">En el SDK de dispositivo IoT de Azure para C, vea la aplicación **iothub\_client\_sample\_http** para obtener un ejemplo completo de las API de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="b4fec-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="b4fec-180">Puede tomar como referencia la aplicación **iothub\_client\_sample\_amqp** para obtener un ejemplo completo de las API no LL.</span><span class="sxs-lookup"><span data-stu-id="b4fec-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="b4fec-181">Administración de propiedades</span><span class="sxs-lookup"><span data-stu-id="b4fec-181">Property handling</span></span>
<span data-ttu-id="b4fec-182">Hasta ahora cuando hemos descrito el envío de datos, nos hemos referido al cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="b4fec-183">Por ejemplo, considere este código:</span><span class="sxs-lookup"><span data-stu-id="b4fec-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="b4fec-184">Este ejemplo envía un mensaje al Centro de IoT con el texto "Hello World".</span><span class="sxs-lookup"><span data-stu-id="b4fec-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="b4fec-185">Pero el Centro de IoT también permite adjuntar propiedades a cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="b4fec-186">Las propiedades son pares de nombres y valores que se pueden adjuntar al mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="b4fec-187">Por ejemplo, podemos modificamos el código anterior para adjuntar una propiedad al mensaje:</span><span class="sxs-lookup"><span data-stu-id="b4fec-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="b4fec-188">Comenzamos llamando a **IoTHubMessage\_Properties** y pasándole el control del mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="b4fec-189">Lo que obtenemos es una referencia a **MAP\_HANDLE** que nos permite empezar a agregar propiedades.</span><span class="sxs-lookup"><span data-stu-id="b4fec-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="b4fec-190">Esto se logra mediante una llamada a **Map\_AddOrUpdate**, que toma una referencia a MAP\_HANDLE, el nombre de propiedad y el valor de propiedad.</span><span class="sxs-lookup"><span data-stu-id="b4fec-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="b4fec-191">Con esta API, podemos se pueden agregar todas la propiedades que se desee.</span><span class="sxs-lookup"><span data-stu-id="b4fec-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="b4fec-192">Cuando se lee el evento en **Event Hubs**, el receptor puede enumerar las propiedades y recuperar sus valores correspondientes.</span><span class="sxs-lookup"><span data-stu-id="b4fec-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="b4fec-193">Por ejemplo, en .NET esto se logra mediante el acceso a la [colección de propiedades en el objeto EventData](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4fec-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="b4fec-194">En el ejemplo anterior, adjuntamos propiedades a un evento que enviamos al Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b4fec-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="b4fec-195">Las propiedades también se pueden adjuntar a los mensajes recibidos desde el Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b4fec-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="b4fec-196">Si queremos recuperar las propiedades de un mensaje, podemos usar código similar al siguiente en la función de devolución de llamada del mensaje:</span><span class="sxs-lookup"><span data-stu-id="b4fec-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

<span data-ttu-id="b4fec-197">La llamada a **IoTHubMessage\_Properties** devuelve la referencia a **MAP\_HANDLE**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="b4fec-198">Después, pasamos esa referencia a **Map\_GetInternals** para obtener una referencia a una matriz de pares de nombres y valores (así como un recuento de las propiedades).</span><span class="sxs-lookup"><span data-stu-id="b4fec-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="b4fec-199">En ese momento solo hay que enumerar las propiedades para obtener los valores que queremos.</span><span class="sxs-lookup"><span data-stu-id="b4fec-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="b4fec-200">No es necesario usar propiedades en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4fec-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="b4fec-201">Pero si necesita establecerlas en eventos o recuperarlas de mensajes, la biblioteca **IoTHubClient** se lo pone fácil.</span><span class="sxs-lookup"><span data-stu-id="b4fec-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="b4fec-202">Administración de mensajes</span><span class="sxs-lookup"><span data-stu-id="b4fec-202">Message handling</span></span>
<span data-ttu-id="b4fec-203">Como se explicó anteriormente, cuando los mensajes llegan del Centro de IoT, la biblioteca **IoTHubClient** responde invocando una función de devolución de llamada registrada.</span><span class="sxs-lookup"><span data-stu-id="b4fec-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="b4fec-204">Hay un parámetro de valor devuelto de esta función que merece una explicación adicional.</span><span class="sxs-lookup"><span data-stu-id="b4fec-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="b4fec-205">Este es un extracto de la función de devolución de llamada en la aplicación de ejemplo **iothub\_client\_sample\_http**:</span><span class="sxs-lookup"><span data-stu-id="b4fec-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="b4fec-206">Observe que el tipo devuelto es **IOTHUBMESSAGE\_DISPOSITION\_RESULT** y, en este caso, devolvemos **IOTHUBMESSAGE\_ACCEPTED**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="b4fec-207">Hay otros valores que podemos obtener de esta función que cambian la forma en que la biblioteca **IoTHubClient** reacciona a la devolución de llamada del mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="b4fec-208">Estas son las opciones.</span><span class="sxs-lookup"><span data-stu-id="b4fec-208">Here are the options.</span></span>

* <span data-ttu-id="b4fec-209">**IOTHUBMESSAGE\_ACCEPTED**: el mensaje se procesó correctamente.</span><span class="sxs-lookup"><span data-stu-id="b4fec-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="b4fec-210">La biblioteca **IoTHubClient** no volverá a invocar la función de devolución de llamada con el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="b4fec-211">**IOTHUBMESSAGE\_REJECTED**: el mensaje no se procesó y no hay intención hacerlo en el futuro.</span><span class="sxs-lookup"><span data-stu-id="b4fec-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="b4fec-212">La biblioteca **IoTHubClient** no debe invocar la función de devolución de llamada con el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="b4fec-213">**IOTHUBMESSAGE\_ABANDONED**: el mensaje no se procesó correctamente, pero la biblioteca **IoTHubClient** debería invocar la función de devolución de llamada con el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="b4fec-214">Para los dos primeros códigos de retorno, la biblioteca **IoTHubClient** envía un mensaje al Centro de IoT que indica que el mensaje debe eliminarse de la cola del dispositivo y no volver a entregarse.</span><span class="sxs-lookup"><span data-stu-id="b4fec-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="b4fec-215">El efecto neto es el mismo (el mensaje se elimina de la cola del dispositivo), pero se registra si el mensaje se aceptó o se rechazó.</span><span class="sxs-lookup"><span data-stu-id="b4fec-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="b4fec-216">El registro de esta distinción es útil para los remitentes del mensaje que pueden escuchar los comentarios y saber así si un dispositivo aceptó o rechazó un mensaje determinado.</span><span class="sxs-lookup"><span data-stu-id="b4fec-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="b4fec-217">En este último caso, también se envía un mensaje al Centro de IoT que indica que el mensaje debe volver a entregarse.</span><span class="sxs-lookup"><span data-stu-id="b4fec-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="b4fec-218">Normalmente un mensaje se abandona si hay algún error, pero se desea volver a procesar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4fec-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="b4fec-219">Por el contrario, rechazar un mensaje es adecuado si se produce un error irrecuperable (o si simplemente decide que no quiere procesar el mensaje).</span><span class="sxs-lookup"><span data-stu-id="b4fec-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="b4fec-220">En cualquier caso simplemente debe tener en cuenta los diferentes códigos de retorno para poder obtener el comportamiento deseado de la biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="b4fec-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="b4fec-221">Credenciales de dispositivo alternativas</span><span class="sxs-lookup"><span data-stu-id="b4fec-221">Alternate device credentials</span></span>
<span data-ttu-id="b4fec-222">Como se explicó anteriormente, lo primero que hay que hacer cuando se trabaja con la biblioteca **IoTHubClient** es obtener un **IOTHUB\_CLIENT\_HANDLE** con una llamada como esta:</span><span class="sxs-lookup"><span data-stu-id="b4fec-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="b4fec-223">Los argumentos de **IoTHubClient\_CreateFromConnectionString** son la cadena de conexión de dispositivo y un parámetro que indica el protocolo que se usará para comunicarse con el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b4fec-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="b4fec-224">La cadena de conexión de dispositivo tiene un formato con el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="b4fec-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="b4fec-225">Hay cuatro grupos de información en esta cadena: nombre del Centro de IoT, sufijo del Centro de IoT, identificador de dispositivo y clave de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="b4fec-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="b4fec-226">Obtendrá el nombre de dominio completo (FQDN) de un centro de IoT cuando cree la instancia del centro de IoT en el portal de Azure. Así obtiene el nombre del centro de IoT (la primera parte del FQDN) y el sufijo del centro de IoT (el resto del FQDN).</span><span class="sxs-lookup"><span data-stu-id="b4fec-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="b4fec-227">Obtendrá el identificador de dispositivo y la clave de acceso compartido al registrar el dispositivo con IoT Hub (como se describe en el [artículo anterior](iot-hub-device-sdk-c-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="b4fec-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="b4fec-228">**IoTHubClient\_CreateFromConnectionString** le ofrece una manera de inicializar la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="b4fec-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="b4fec-229">Pero si lo prefiere, puede crear un nuevo **IOTHUB\_CLIENT\_HANDLE** usando estos parámetros individuales en lugar de la cadena de conexión de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4fec-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="b4fec-230">Esto se consigue con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="b4fec-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="b4fec-231">Esto consigue lo mismo que **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="b4fec-232">Puede parecer obvio que deseara usar **IoTHubClient\_CreateFromConnectionString** en lugar de este método de inicialización más detallado.</span><span class="sxs-lookup"><span data-stu-id="b4fec-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="b4fec-233">Sin embargo, tenga en cuenta que cuando se registra un dispositivo en el Centro de IoT, lo que obtenemos es un identificador de dispositivo y una clave de dispositivo (no una cadena de conexión).</span><span class="sxs-lookup"><span data-stu-id="b4fec-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="b4fec-234">La herramienta del SDK *Explorador de dispositivos* presentada en el [artículo anterior](iot-hub-device-sdk-c-intro.md) usa las bibliotecas del **SDK del servicio IoT de Azure** para crear la cadena de conexión de dispositivo a partir del identificador del dispositivo, la clave de dispositivo y el nombre de host del IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b4fec-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="b4fec-235">Por lo tanto, una llamada a **IoTHubClient\_LL\_Create** puede ser preferible porque ahorra el paso de generar una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="b4fec-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="b4fec-236">Use el método que le resulte conveniente.</span><span class="sxs-lookup"><span data-stu-id="b4fec-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="b4fec-237">Opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="b4fec-237">Configuration options</span></span>
<span data-ttu-id="b4fec-238">Hasta ahora todo lo descrito sobre forma en la que trabaja la biblioteca **IoTHubClient** refleja su comportamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="b4fec-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="b4fec-239">Sin embargo, hay algunas opciones que se pueden establecer para cambiar el funcionamiento de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="b4fec-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="b4fec-240">Esto se logra aprovechando la API **IoTHubClient\_LL\_SetOption**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="b4fec-241">En este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b4fec-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="b4fec-242">Hay un par de opciones que se usan con frecuencia:</span><span class="sxs-lookup"><span data-stu-id="b4fec-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="b4fec-243">**SetBatching** (bool): si es **true**, los datos enviados al IoT Hub se envían en lotes.</span><span class="sxs-lookup"><span data-stu-id="b4fec-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="b4fec-244">Si es **false**, los mensajes se envían individualmente.</span><span class="sxs-lookup"><span data-stu-id="b4fec-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="b4fec-245">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-245">The default is **false**.</span></span> <span data-ttu-id="b4fec-246">Tenga en cuenta que la opción **SetBatching** solo se aplica al protocolo HTTP y no a los protocolos MQTT o AMQP.</span><span class="sxs-lookup"><span data-stu-id="b4fec-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="b4fec-247">**Tiempo de espera** (entero sin sino): este valor se representa en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="b4fec-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="b4fec-248">Si el envío de una solicitud HTTP o la recepción de una respuesta supera este tiempo, la conexión agota el tiempo.</span><span class="sxs-lookup"><span data-stu-id="b4fec-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="b4fec-249">La opción de procesamiento por lotes es importante.</span><span class="sxs-lookup"><span data-stu-id="b4fec-249">The batching option is important.</span></span> <span data-ttu-id="b4fec-250">De forma predeterminada, la biblioteca incorpora los eventos individualmente (un evento único es lo que se pasa a **IoTHubClient\_LL\_SendEventAsync**).</span><span class="sxs-lookup"><span data-stu-id="b4fec-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="b4fec-251">Si la opción de procesamiento por lotes es **true**, la biblioteca recopilará tantos eventos como sea posible del búfer (hasta el tamaño máximo de mensaje que aceptará ese Centro de IoT).</span><span class="sxs-lookup"><span data-stu-id="b4fec-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="b4fec-252">El lote de eventos se envía a Centro de IoT en una sola llamada HTTP (los eventos individuales están agrupados en una matriz JSON).</span><span class="sxs-lookup"><span data-stu-id="b4fec-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="b4fec-253">Habilitar el procesamiento por lotes normalmente da como resultado un gran aumento del rendimiento ya que se reducen los recorridos de ida y vuelta de red.</span><span class="sxs-lookup"><span data-stu-id="b4fec-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="b4fec-254">Además, reduce considerablemente el ancho de banda porque se envía un conjunto de encabezados HTTP con un lote de eventos en lugar de un conjunto de encabezados para cada evento individual.</span><span class="sxs-lookup"><span data-stu-id="b4fec-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="b4fec-255">A menos que tenga una razón concreta para no hacerlo, normalmente es mejor habilitar el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="b4fec-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4fec-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4fec-256">Next steps</span></span>
<span data-ttu-id="b4fec-257">En este artículo se describe con detalle el comportamiento de la biblioteca **IoTHubClient** que se encuentra en el **SDK de dispositivo IoT de Azure para C**. Con esta información conocerá bien las capacidades de la biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="b4fec-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="b4fec-258">En el [siguiente artículo](iot-hub-device-sdk-c-serializer.md) se proporcionan detalles similares sobre la biblioteca del **serializador** .</span><span class="sxs-lookup"><span data-stu-id="b4fec-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="b4fec-259">Para más información acerca del desarrollo para IoT Hub, consulte los [SDK de IoT Hub][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="b4fec-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="b4fec-260">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="b4fec-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b4fec-261">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b4fec-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

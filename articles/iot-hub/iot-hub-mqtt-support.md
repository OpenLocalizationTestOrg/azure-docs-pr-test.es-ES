---
title: "Información sobre Azure MQTT con IoT Hub | Microsoft Docs"
description: "Guía del desarrollador: compatibilidad con dispositivos que se conectan a un punto de conexión orientado a dispositivos IoT Hub mediante el protocolo MQTT. Incluye información sobre la compatibilidad integrada de MQTT de los SDK de dispositivo IoT de Azure."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eab70c1aa9c49a137c2ac1012449d57915fb0d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a><span data-ttu-id="ecede-104">Comunicación con la instancia de IoT Hub mediante el protocolo MQTT</span><span class="sxs-lookup"><span data-stu-id="ecede-104">Communicate with your IoT hub using the MQTT protocol</span></span>

<span data-ttu-id="ecede-105">IoT Hub permite a los dispositivos comunicarse con los puntos de conexión de dispositivos de IoT Hub utilizando el protocolo [MQTT v3.1.1][lnk-mqtt-org] en el puerto 8883 o MQTT v3.1.1 sobre el protocolo WebSocket en el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="ecede-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="ecede-106">IoT Hub requiere que toda la comunicación del dispositivo se proteja mediante TLS/SSL (por lo tanto, IoT Hub no es compatible con conexiones no seguras en el puerto 1883).</span><span class="sxs-lookup"><span data-stu-id="ecede-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-to-iot-hub"></a><span data-ttu-id="ecede-107">Conexión al Centro de IoT</span><span class="sxs-lookup"><span data-stu-id="ecede-107">Connecting to IoT Hub</span></span>

<span data-ttu-id="ecede-108">Un dispositivo puede conectarse a un centro de IoT mediante el protocolo MQTT, ya sea mediante las bibliotecas de los [SDK de Azure IoT][lnk-device-sdks] o directamente mediante el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="ecede-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span></span>

## <a name="using-the-device-sdks"></a><span data-ttu-id="ecede-109">Uso de los SDK de dispositivo</span><span class="sxs-lookup"><span data-stu-id="ecede-109">Using the device SDKs</span></span>

<span data-ttu-id="ecede-110">Los [SDK de dispositivo][lnk-device-sdks] compatibles con el protocolo MQTT están disponibles para Java, Node.js, C, C# y Python.</span><span class="sxs-lookup"><span data-stu-id="ecede-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="ecede-111">Los SDK de dispositivo usan la cadena de conexión de IoT Hub estándar para establecer una conexión a un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ecede-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span></span> <span data-ttu-id="ecede-112">Para utilizar el protocolo MQTT, el parámetro de protocolo de cliente debe establecerse en **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="ecede-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span></span> <span data-ttu-id="ecede-113">De forma predeterminada, los SDK de dispositivo se conectan a un centro de IoT con la marca **CleanSession** establecida en **0** y usan **QoS 1** para el intercambio de mensajes con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ecede-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span></span>

<span data-ttu-id="ecede-114">Cuando un dispositivo se conecta a un centro de IoT, los SDK de dispositivo proporcionan métodos que permiten al dispositivo enviar y recibir mensajes desde un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ecede-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span></span>

<span data-ttu-id="ecede-115">La tabla siguiente contiene vínculos a ejemplos de código para cada idioma admitido y especifica el parámetro que se debe utilizar para establecer una conexión con el Centro de IoT mediante el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="ecede-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span></span>

| <span data-ttu-id="ecede-116">Idioma</span><span class="sxs-lookup"><span data-stu-id="ecede-116">Language</span></span> | <span data-ttu-id="ecede-117">Parámetro de protocolo</span><span class="sxs-lookup"><span data-stu-id="ecede-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="ecede-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="ecede-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="ecede-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="ecede-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="ecede-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="ecede-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="ecede-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="ecede-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="ecede-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="ecede-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="ecede-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="ecede-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="ecede-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="ecede-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="ecede-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="ecede-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="ecede-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="ecede-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="ecede-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="ecede-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a><span data-ttu-id="ecede-128">Migración de una aplicación de dispositivo de AMQP a MQTT</span><span class="sxs-lookup"><span data-stu-id="ecede-128">Migrating a device app from AMQP to MQTT</span></span>

<span data-ttu-id="ecede-129">Si usa los [SDK de dispositivo][lnk-device-sdks], el cambio de AMQP a MQTT requiere modificar el parámetro de protocolo en la inicialización del cliente como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ecede-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated previously.</span></span>

<span data-ttu-id="ecede-130">Al hacerlo, asegúrese de comprobar los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ecede-130">When doing so, make sure to check the following items:</span></span>

* <span data-ttu-id="ecede-131">AMQP devuelve errores para muchas condiciones, mientras que MQTT finaliza la conexión.</span><span class="sxs-lookup"><span data-stu-id="ecede-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span></span> <span data-ttu-id="ecede-132">Como resultado, la lógica de control de excepciones puede requerir algunos cambios.</span><span class="sxs-lookup"><span data-stu-id="ecede-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="ecede-133">MQTT no admite las operaciones *rechazar* al recibir [mensajes de la nube al dispositivo][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="ecede-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="ecede-134">Si su aplicación de back-end tiene que recibir una respuesta de la aplicación del dispositivo, considere los [métodos directos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="ecede-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-the-mqtt-protocol-directly"></a><span data-ttu-id="ecede-135">Uso del protocolo MQTT directamente</span><span class="sxs-lookup"><span data-stu-id="ecede-135">Using the MQTT protocol directly</span></span>
<span data-ttu-id="ecede-136">Si un dispositivo no puede usar los SDK de dispositivo, tendrá la posibilidad de conectarse a los puntos de conexión públicos del dispositivo mediante el protocolo MQTT en el puerto 8883.</span><span class="sxs-lookup"><span data-stu-id="ecede-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol on port 8883.</span></span> <span data-ttu-id="ecede-137">En el paquete **CONNECT** el dispositivo debe usar los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="ecede-137">In the **CONNECT** packet the device should use the following values:</span></span>

* <span data-ttu-id="ecede-138">Para el campo **ClientId**, use **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="ecede-138">For the **ClientId** field, use the **deviceId**.</span></span>
* <span data-ttu-id="ecede-139">Para el campo **Nombre de usuario** use `{iothubhostname}/{device_id}/api-version=2016-11-14`, donde {iothubhostname} es el CName completo de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ecede-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span></span>

    <span data-ttu-id="ecede-140">Por ejemplo, si el nombre de su centro IoT es **contoso.azure-devices.net** y si el nombre del dispositivo es **MyDevice01**, el campo **Nombre de usuario** completo debe contener `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="ecede-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="ecede-141">Para el campo **Contraseña** , use un token SAS.</span><span class="sxs-lookup"><span data-stu-id="ecede-141">For the **Password** field, use a SAS token.</span></span> <span data-ttu-id="ecede-142">El formato del token de SAS es el mismo que para los protocolos HTTP y AMQP:</span><span class="sxs-lookup"><span data-stu-id="ecede-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="ecede-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="ecede-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="ecede-144">Para más información sobre cómo generar tokens de SAS, consulte la sección sobre el [uso de tokens de seguridad de IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="ecede-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="ecede-145">Al realizar la prueba, también puede utilizar la herramienta [Explorador de dispositivos][lnk-device-explorer] para generar rápidamente un token SAS que puede copiar y pegar en su propio código:</span><span class="sxs-lookup"><span data-stu-id="ecede-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="ecede-146">Vaya a la pestaña **Administración** del **Explorador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="ecede-146">Go to the **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="ecede-147">Haga clic en **Token de SAS** (parte superior derecha).</span><span class="sxs-lookup"><span data-stu-id="ecede-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="ecede-148">En **SASTokenForm**, seleccione el dispositivo en el menú desplegable **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="ecede-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span></span> <span data-ttu-id="ecede-149">Establezca el valor para **TTL**.</span><span class="sxs-lookup"><span data-stu-id="ecede-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="ecede-150">Haga clic en **Generar** para crear el token.</span><span class="sxs-lookup"><span data-stu-id="ecede-150">Click **Generate** to create your token.</span></span>

     <span data-ttu-id="ecede-151">El token de SAS que ha generado tiene esta estructura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="ecede-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="ecede-152">La parte de este token que se debe usar como el campo **Password** para conectarse con MQTT es: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="ecede-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="ecede-153">Para paquetes de conexión y desconexión de MQTT, IoT Hub emite un evento sobre el canal **Supervisión de operaciones** con información adicional que puede ayudarle a solucionar problemas de conectividad.</span><span class="sxs-lookup"><span data-stu-id="ecede-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="ecede-154">Envío de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="ecede-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="ecede-155">Después de realizar con éxito una conexión, un dispositivo puede enviar mensajes a un centro IoT mediante `devices/{device_id}/messages/events/` o `devices/{device_id}/messages/events/{property_bag}` como un **Nombre del tema**.</span><span class="sxs-lookup"><span data-stu-id="ecede-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="ecede-156">El elemento `{property_bag}` permite al dispositivo enviar mensajes con propiedades adicionales en un formato con codificación URL.</span><span class="sxs-lookup"><span data-stu-id="ecede-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="ecede-157">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecede-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="ecede-158">Este elemento `{property_bag}` usa la misma codificación que se utiliza para las cadenas de consulta en el protocolo HTTP.</span><span class="sxs-lookup"><span data-stu-id="ecede-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span></span>
>
>

<span data-ttu-id="ecede-159">La aplicación del dispositivo también puede utilizar `devices/{device_id}/messages/events/{property_bag}` como el **nombre del tema Will** para definir los *mensajes Will* que se reenviarán como un mensaje de telemetría.</span><span class="sxs-lookup"><span data-stu-id="ecede-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span></span>

- <span data-ttu-id="ecede-160">IoT Hub no admite mensajes QoS 2.</span><span class="sxs-lookup"><span data-stu-id="ecede-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="ecede-161">Si una aplicación de dispositivo publica un mensaje con **QoS 2**, el IoT Hub cierra la conexión de red.</span><span class="sxs-lookup"><span data-stu-id="ecede-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span></span>
- <span data-ttu-id="ecede-162">IoT Hub no retiene los mensajes de conservación.</span><span class="sxs-lookup"><span data-stu-id="ecede-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="ecede-163">Si un dispositivo envía un mensaje con la marca **RETAIN** establecida en 1, el IoT Hub agrega la propiedad de aplicación **x-opt-retain** al mensaje.</span><span class="sxs-lookup"><span data-stu-id="ecede-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span></span> <span data-ttu-id="ecede-164">En este caso, en lugar de retener el mensaje de conservación, IoT Hub lo pasa a la aplicación de back-end.</span><span class="sxs-lookup"><span data-stu-id="ecede-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span></span>
- <span data-ttu-id="ecede-165">IoT Hub solo admite una conexión MQTT activa por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ecede-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="ecede-166">Todas las conexiones MQTT nuevas en nombre del mismo identificador de dispositivo provocarán que IoT Hub cierre la existente.</span><span class="sxs-lookup"><span data-stu-id="ecede-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span></span>

<span data-ttu-id="ecede-167">Para obtener más información, consulte la [guía del desarrollador de mensajería][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="ecede-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="ecede-168">Recepción de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="ecede-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="ecede-169">Para recibir mensajes de IoT Hub, un dispositivo debe suscribirse usando `devices/{device_id}/messages/devicebound/#` como un **filtro de tema**.</span><span class="sxs-lookup"><span data-stu-id="ecede-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="ecede-170">El comodín de varios niveles **#** en el filtro de tema solo se utiliza para permitir que el dispositivo reciba propiedades adicionales en el nombre del tema.</span><span class="sxs-lookup"><span data-stu-id="ecede-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span></span> <span data-ttu-id="ecede-171">¿IoT Hub no permite el uso de **#** o **?**</span><span class="sxs-lookup"><span data-stu-id="ecede-171">IoT Hub does not allow the usage of the **#** or **?**</span></span> <span data-ttu-id="ecede-172">caracteres comodín para el filtrado de subtemas.</span><span class="sxs-lookup"><span data-stu-id="ecede-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="ecede-173">Puesto que IoT Hub no es un agente de mensajería de publicación-suscripción de propósito general, solo admite los filtros de tema y los nombres de tema documentados.</span><span class="sxs-lookup"><span data-stu-id="ecede-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span></span>

<span data-ttu-id="ecede-174">El dispositivo no recibe ningún mensaje desde IoT Hub hasta que se suscribe correctamente al punto de conexión específico del dispositivo, representado por el filtro del tema `devices/{device_id}/messages/devicebound/#`.</span><span class="sxs-lookup"><span data-stu-id="ecede-174">The device does not receive any messages from IoT Hub, until it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="ecede-175">Después de que se establece una suscripción correcta, el dispositivo comienza a recibir solo los mensajes de la nube al dispositivo que se han enviado a él después de la hora de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ecede-175">After successful subscription has been established, the device starts receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span></span> <span data-ttu-id="ecede-176">Si el dispositivo se conecta con la marca **CleanSession** establecida en **0**, la suscripción se conserva entre distintas sesiones.</span><span class="sxs-lookup"><span data-stu-id="ecede-176">If the device connects with **CleanSession** flag set to **0**, the subscription is persisted across different sessions.</span></span> <span data-ttu-id="ecede-177">En este caso, la próxima vez que se conecta con **CleanSession 0**, el dispositivo recibe mensajes pendientes que se han enviado a él mientras estaba desconectado.</span><span class="sxs-lookup"><span data-stu-id="ecede-177">In this case, the next time it connects with **CleanSession 0** the device receives outstanding messages that have been sent to it while it was disconnected.</span></span> <span data-ttu-id="ecede-178">Si el dispositivo usa la marca **CleanSession** establecida en **1**, no recibe los mensajes de IoT Hub hasta que se suscribe al punto de conexión del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ecede-178">If the device uses **CleanSession** flag set to **1** though, it does not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span></span>

<span data-ttu-id="ecede-179">IoT Hub entrega los mensajes con el **Nombre del tema** `devices/{device_id}/messages/devicebound/`, o `devices/{device_id}/messages/devicebound/{property_bag}` si hay alguna propiedad de mensaje.</span><span class="sxs-lookup"><span data-stu-id="ecede-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="ecede-180">`{property_bag}` contiene pares clave-valor con codificación URL de propiedades del mensaje.</span><span class="sxs-lookup"><span data-stu-id="ecede-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="ecede-181">Las propiedades de la aplicación y del sistema configuradas por el usuario (como **messageId** o **correlationId**) son las únicas que se incluyen en el paquete de propiedades.</span><span class="sxs-lookup"><span data-stu-id="ecede-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span></span> <span data-ttu-id="ecede-182">Los nombres de propiedad del sistema tienen el prefijo **$**; las propiedades de aplicaciones utilizan el nombre de propiedad original sin prefijo.</span><span class="sxs-lookup"><span data-stu-id="ecede-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span></span>

<span data-ttu-id="ecede-183">Cuando una aplicación de dispositivo se suscribe a un tema con **QoS 2**, IoT Hub concede el QoS de nivel 1 (el máximo) en el paquete **SUBACK**.</span><span class="sxs-lookup"><span data-stu-id="ecede-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span></span> <span data-ttu-id="ecede-184">Después de eso, IoT Hub envía mensajes al dispositivo con QoS 1.</span><span class="sxs-lookup"><span data-stu-id="ecede-184">After that, IoT Hub delivers messages to the device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="ecede-185">Recuperación de propiedades del dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="ecede-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="ecede-186">En primer lugar, un dispositivo se suscribe a `$iothub/twin/res/#` para recibir las respuestas de la operación.</span><span class="sxs-lookup"><span data-stu-id="ecede-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span></span> <span data-ttu-id="ecede-187">A continuación, envía un mensaje en blanco al tema `$iothub/twin/GET/?$rid={request id}`, con un valor en **request id**.</span><span class="sxs-lookup"><span data-stu-id="ecede-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**.</span></span> <span data-ttu-id="ecede-188">El servicio envía entonces un mensaje de respuesta que contiene los datos del dispositivo gemelo del tema `$iothub/twin/res/{status}/?$rid={request id}`, usando el mismo **identificador de solicitud** que la solicitud.</span><span class="sxs-lookup"><span data-stu-id="ecede-188">The service then sends a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span></span>

<span data-ttu-id="ecede-189">El identificador de la solicitud puede ser cualquier valor válido de propiedad de mensaje, según la [guía del desarrollador de mensajería de IoT Hub][lnk-messaging], y el estado se valida como entero.</span><span class="sxs-lookup"><span data-stu-id="ecede-189">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="ecede-190">El cuerpo de la respuesta contiene la sección de propiedades del dispositivo gemelo:</span><span class="sxs-lookup"><span data-stu-id="ecede-190">The response body contains the properties section of the device twin:</span></span>

<span data-ttu-id="ecede-191">El cuerpo de la entrada del registro de identidad limitado al miembro "properties", p. ej.:</span><span class="sxs-lookup"><span data-stu-id="ecede-191">The body of the identity registry entry limited to the “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="ecede-192">Los códigos de estado posibles son:</span><span class="sxs-lookup"><span data-stu-id="ecede-192">The possible status codes are:</span></span>

|<span data-ttu-id="ecede-193">Estado</span><span class="sxs-lookup"><span data-stu-id="ecede-193">Status</span></span> | <span data-ttu-id="ecede-194">Descripción</span><span class="sxs-lookup"><span data-stu-id="ecede-194">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="ecede-195">200</span><span class="sxs-lookup"><span data-stu-id="ecede-195">200</span></span> | <span data-ttu-id="ecede-196">Correcto</span><span class="sxs-lookup"><span data-stu-id="ecede-196">Success</span></span> |
| <span data-ttu-id="ecede-197">429</span><span class="sxs-lookup"><span data-stu-id="ecede-197">429</span></span> | <span data-ttu-id="ecede-198">Demasiadas solicitudes (limitadas), según el artículo sobre [limitaciones de IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="ecede-198">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="ecede-199">5**</span><span class="sxs-lookup"><span data-stu-id="ecede-199">5**</span></span> | <span data-ttu-id="ecede-200">Errores del servidor</span><span class="sxs-lookup"><span data-stu-id="ecede-200">Server errors</span></span> |

<span data-ttu-id="ecede-201">Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ecede-201">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="ecede-202">Actualización de las propiedades notificadas del dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="ecede-202">Update device twin's reported properties</span></span>

<span data-ttu-id="ecede-203">La secuencia siguiente describe cómo un dispositivo actualiza las propiedades notificadas en el dispositivo gemelo de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="ecede-203">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span></span>

1. <span data-ttu-id="ecede-204">En primer lugar, un dispositivo debe suscribirse al tema `$iothub/twin/res/#` para recibir las respuestas de la operación de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ecede-204">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="ecede-205">Un dispositivo envía un mensaje que contiene la actualización del dispositivo gemelo al tema `$iothub/twin/PATCH/properties/reported/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="ecede-205">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="ecede-206">Este mensaje incluye un valor de **identificador de solicitud**.</span><span class="sxs-lookup"><span data-stu-id="ecede-206">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="ecede-207">Después, el servicio envía un mensaje de respuesta que contiene el nuevo valor de ETag de la colección de propiedades notificadas del tema `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="ecede-207">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="ecede-208">Este mensaje de respuesta usa el mismo **identificador de solicitud** que la solicitud.</span><span class="sxs-lookup"><span data-stu-id="ecede-208">This response message uses the same **request id** as the request.</span></span>

<span data-ttu-id="ecede-209">El cuerpo del mensaje de solicitud contiene un documento JSON que proporciona nuevos valores para propiedades notificadas (no se pueden modificar otras propiedad ni metadatos).</span><span class="sxs-lookup"><span data-stu-id="ecede-209">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="ecede-210">En el documento JSON, cada miembro actualiza o agrega al miembro correspondiente en el documento del dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="ecede-210">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span></span> <span data-ttu-id="ecede-211">La configuración de un miembro en `null`, elimina el miembro del objeto contenedor.</span><span class="sxs-lookup"><span data-stu-id="ecede-211">A member set to `null`, deletes the member from the containing object.</span></span> <span data-ttu-id="ecede-212">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecede-212">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="ecede-213">Los códigos de estado posibles son:</span><span class="sxs-lookup"><span data-stu-id="ecede-213">The possible status codes are:</span></span>

|<span data-ttu-id="ecede-214">Estado</span><span class="sxs-lookup"><span data-stu-id="ecede-214">Status</span></span> | <span data-ttu-id="ecede-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="ecede-215">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="ecede-216">200</span><span class="sxs-lookup"><span data-stu-id="ecede-216">200</span></span> | <span data-ttu-id="ecede-217">Correcto</span><span class="sxs-lookup"><span data-stu-id="ecede-217">Success</span></span> |
| <span data-ttu-id="ecede-218">400</span><span class="sxs-lookup"><span data-stu-id="ecede-218">400</span></span> | <span data-ttu-id="ecede-219">Solicitud incorrecta.</span><span class="sxs-lookup"><span data-stu-id="ecede-219">Bad Request.</span></span> <span data-ttu-id="ecede-220">JSON con formato incorrecto</span><span class="sxs-lookup"><span data-stu-id="ecede-220">Malformed JSON</span></span> |
| <span data-ttu-id="ecede-221">429</span><span class="sxs-lookup"><span data-stu-id="ecede-221">429</span></span> | <span data-ttu-id="ecede-222">Demasiadas solicitudes (limitadas), según el artículo sobre [limitaciones de IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="ecede-222">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="ecede-223">5**</span><span class="sxs-lookup"><span data-stu-id="ecede-223">5**</span></span> | <span data-ttu-id="ecede-224">Errores del servidor</span><span class="sxs-lookup"><span data-stu-id="ecede-224">Server errors</span></span> |

<span data-ttu-id="ecede-225">Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ecede-225">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="ecede-226">Recepción de notificaciones de actualización de las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="ecede-226">Receiving desired properties update notifications</span></span>

<span data-ttu-id="ecede-227">Cuando se conecta un dispositivo, IoT Hub envía notificaciones al tema `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que contiene la actualización realizada por la solución de back-end.</span><span class="sxs-lookup"><span data-stu-id="ecede-227">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span></span> <span data-ttu-id="ecede-228">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecede-228">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="ecede-229">Para las actualizaciones de propiedad, los valores `null` significan que se elimina el miembro del objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="ecede-229">As for property updates, `null` values means that the JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="ecede-230">IoT Hub genera notificaciones de cambio solo si los dispositivos están conectados.</span><span class="sxs-lookup"><span data-stu-id="ecede-230">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="ecede-231">Asegúrese de implementar el [flujo de reconexión de dispositivos][lnk-devguide-twin-reconnection] para mantener las propiedades que desee sincronizadas entre IoT Hub y la aplicación del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ecede-231">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span></span>

<span data-ttu-id="ecede-232">Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ecede-232">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-to-a-direct-method"></a><span data-ttu-id="ecede-233">Respuesta a un método directo</span><span class="sxs-lookup"><span data-stu-id="ecede-233">Respond to a direct method</span></span>

<span data-ttu-id="ecede-234">En primer lugar, tiene que suscribirse un dispositivo a `$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="ecede-234">First, a device has to subscribe to `$iothub/methods/POST/#`.</span></span> <span data-ttu-id="ecede-235">IoT Hub envía solicitudes de método al tema `$iothub/methods/POST/{method name}/?$rid={request id}`, con un valor JSON válido o un cuerpo vacío.</span><span class="sxs-lookup"><span data-stu-id="ecede-235">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="ecede-236">Para responder, el dispositivo envía un mensaje con un valor JSON válido o un cuerpo vacío al tema `$iothub/methods/res/{status}/?$rid={request id}`, donde **request id** tiene que coincidir con el mensaje de solicitud y **status** debe ser un entero.</span><span class="sxs-lookup"><span data-stu-id="ecede-236">To respond, the device sends a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span></span>

<span data-ttu-id="ecede-237">Para obtener más información, consulte la [guía para desarrolladores sobre el método directo][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="ecede-237">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="ecede-238">Consideraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="ecede-238">Additional considerations</span></span>

<span data-ttu-id="ecede-239">Como consideración final, si necesita personalizar el comportamiento del protocolo MQTT en el lado de la nube, debe revisar la [puerta de enlace de protocolos de IoT de Azure][lnk-azure-protocol-gateway] que le permite implementar una puerta de enlace de protocolo personalizado de alto rendimiento que interactúa directamente con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ecede-239">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="ecede-240">La puerta de enlace de protocolos de IoT de Azure le permite personalizar el protocolo del dispositivo para dar cabida a las implementaciones de MQTT de Brownfield u otros protocolos personalizados.</span><span class="sxs-lookup"><span data-stu-id="ecede-240">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="ecede-241">Sin embargo, este enfoque requiere que se ejecute y se ponga en funcionamiento una puerta de enlace de protocolo personalizado.</span><span class="sxs-lookup"><span data-stu-id="ecede-241">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecede-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ecede-242">Next steps</span></span>

<span data-ttu-id="ecede-243">Para más información sobre el protocolo MQTT, consulte la [documentación de MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="ecede-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="ecede-244">Para más información acerca de planificación de la implementación del Centro de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="ecede-244">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="ecede-245">[Catálogo de dispositivos de Azure Certified for IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="ecede-245">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="ecede-246">[Compatibilidad con protocolos adicionales][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="ecede-246">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="ecede-247">[Comparación con Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="ecede-247">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="ecede-248">[Escalado, alta disponibilidad y recuperación ante desastres][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="ecede-248">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="ecede-249">Para explorar aún más las funcionalidades de Centro de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="ecede-249">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ecede-250">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="ecede-250">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="ecede-251">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ecede-251">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md

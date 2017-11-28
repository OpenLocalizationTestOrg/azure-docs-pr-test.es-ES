---
title: "soporte técnico de Azure IoT Hub MQTT aaaUnderstand | Documentos de Microsoft"
description: "Desarrollador guía: compatibilidad para dispositivos que se conectan tooan centro de IoT dispositivo extremo mediante Hola protocolo MQTT. Incluye información sobre la compatibilidad integrada de MQTT en hello SDK de dispositivos de IoT de Azure."
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
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="ac1a2-104">Comunicarse con el centro de IoT mediante Protocolo de hello MQTT</span><span class="sxs-lookup"><span data-stu-id="ac1a2-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="ac1a2-105">Centro de IoT permite toocommunicate de dispositivos con extremos de dispositivo de centro de IoT hello mediante hello [MQTT v3.1.1] [ lnk-mqtt-org] protocolo en el puerto 8883 o v3.1.1 MQTT a través del protocolo WebSocket en el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="ac1a2-106">Centro de IoT requiere todos los toobe de comunicación de dispositivos segura mediante el uso de TLS/SSL (por lo tanto, centro de IoT no es compatible con conexiones no seguras a través del puerto 1883).</span><span class="sxs-lookup"><span data-stu-id="ac1a2-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="ac1a2-107">Concentrador de conexión tooIoT</span><span class="sxs-lookup"><span data-stu-id="ac1a2-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="ac1a2-108">Un dispositivo puede usar Centro de IoT de hello MQTT protocolo tooconnect tooan mediante bibliotecas de Hola Hola [SDK de Azure IoT] [ lnk-device-sdks] o directamente con el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="ac1a2-109">Uso de dispositivo de hello SDK</span><span class="sxs-lookup"><span data-stu-id="ac1a2-109">Using hello device SDKs</span></span>

<span data-ttu-id="ac1a2-110">[SDK de dispositivos] [ lnk-device-sdks] ese protocolo MQTT Hola de soporte técnico están disponibles para Java, Node.js, C, C# y Python.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="ac1a2-111">dispositivo de Hello SDK usar Hola estándar centro de IoT conexión cadena tooestablish un centro de IoT tooan de conexión.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="ac1a2-112">Protocolo MQTT de toouse hello, parámetro de protocolo de cliente de hello debe establecerse demasiado**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="ac1a2-113">De forma predeterminada, el dispositivo de hello SDK, conectar tooan centro de IoT con hello **CleanSession** marca se establece demasiado**0** y usar **QoS 1** de intercambio de mensajes con el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="ac1a2-114">Cuando un dispositivo está conectado tooan centro de IoT, dispositivo Hola SDK proporcionan métodos que permiten mensajes de Hola dispositivo toosend tooand recibir mensajes de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="ac1a2-115">Hello tabla siguiente contiene vínculos toocode ejemplos para cada idioma compatible y especifica Hola parámetro toouse tooestablish un concentrador de conexión tooIoT con hello MQTT protocolo.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="ac1a2-116">language</span><span class="sxs-lookup"><span data-stu-id="ac1a2-116">Language</span></span> | <span data-ttu-id="ac1a2-117">Parámetro de protocolo</span><span class="sxs-lookup"><span data-stu-id="ac1a2-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="ac1a2-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="ac1a2-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="ac1a2-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="ac1a2-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="ac1a2-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="ac1a2-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="ac1a2-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="ac1a2-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="ac1a2-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="ac1a2-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="ac1a2-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="ac1a2-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="ac1a2-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="ac1a2-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="ac1a2-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="ac1a2-128">Migrar una aplicación de dispositivo de AMQP tooMQTT</span><span class="sxs-lookup"><span data-stu-id="ac1a2-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="ac1a2-129">Si usas hello [dispositivo SDK][lnk-device-sdks], cambiar de usar AMQP tooMQTT requiere cambiar el parámetro de protocolo de hello en la inicialización del cliente hello como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="ac1a2-130">Al hacerlo, asegúrese de que hello toocheck siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="ac1a2-131">AMQP devuelve errores para muchas condiciones, mientras que MQTT finaliza la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="ac1a2-132">Como resultado, la lógica de control de excepciones puede requerir algunos cambios.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="ac1a2-133">MQTT no admite hello *rechazar* operaciones cuando se reciben [mensajes en la nube al dispositivo][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="ac1a2-134">Si la aplicación de back-end necesita tooreceive una respuesta de aplicación de dispositivo de hello, considere el uso de [dirigir métodos][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="ac1a2-135">Directamente con el protocolo de hello MQTT</span><span class="sxs-lookup"><span data-stu-id="ac1a2-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="ac1a2-136">Si un dispositivo no puede usar el dispositivo de hello SDK, todavía se pueden conectar los puntos de conexión de un dispositivo público toohello mediante el protocolo MQTT hello en el puerto 8883.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="ac1a2-137">Hola **conectar** dispositivo Hola de paquetes debe usar Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="ac1a2-138">Para hello **ClientId** campo, use hello **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="ac1a2-139">Para hello **nombre de usuario** campo, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, donde {iothubhostname} es Hola CName completa del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="ac1a2-140">Por ejemplo, si hello es el nombre de su centro de IoT **contoso.azure devices.net** y si Hola nombre del dispositivo es **MyDevice01**, Hola completa **nombre de usuario** campo debe contener `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="ac1a2-141">Para hello **contraseña** campo, use un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="ac1a2-142">formato de Hola de hello token SAS es igual Hola como para hello HTTP y protocolos AMQP:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="ac1a2-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="ac1a2-144">Para obtener más información acerca de cómo toogenerate tokens SAS, vea la sección de dispositivo de Hola de [tokens de seguridad usando el centro de IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="ac1a2-145">Al realizar pruebas, también puede utilizar hello [explorer dispositivo] [ lnk-device-explorer] tooquickly herramienta generar un token SAS que puede copiar y pegar en su propio código:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="ac1a2-146">Vaya toohello **administración** ficha **dispositivo explorador**.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="ac1a2-147">Haga clic en **Token de SAS** (parte superior derecha).</span><span class="sxs-lookup"><span data-stu-id="ac1a2-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="ac1a2-148">En **SASTokenForm**, seleccione el dispositivo en hello **DeviceID** de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="ac1a2-149">Establezca el valor para **TTL**.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="ac1a2-150">Haga clic en **generar** toocreate el token.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="ac1a2-151">token SAS que se genera Hello tiene esta estructura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="ac1a2-152">Hola parte de este token toouse como hello **contraseña** tooconnect de campo mediante MQTT es: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="ac1a2-153">Para MQTT conectar y desconectar paquetes, centro de IoT emite un evento en hello **supervisión de Operations** canal con información adicional que puede ayudar a problemas de conectividad de tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="ac1a2-154">Envío de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="ac1a2-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="ac1a2-155">Después de realizar una conexión correcta, un dispositivo puede enviar mensajes tooIoT concentrador mediante `devices/{device_id}/messages/events/` o `devices/{device_id}/messages/events/{property_bag}` como un **el nombre del tema**.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="ac1a2-156">Hola `{property_bag}` elemento permite mensajes de Hola dispositivo toosend con propiedades adicionales en un formato con codificación url.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="ac1a2-157">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="ac1a2-158">Esto `{property_bag}` elemento usa Hola misma codificación que para las cadenas de consulta de protocolo de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="ac1a2-159">También puede utilizar la aplicación de dispositivo de Hello `devices/{device_id}/messages/events/{property_bag}` como hello **será el nombre del tema** toodefine *mensajes* toobe reenviado como un mensaje de telemetría.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="ac1a2-160">IoT Hub no admite mensajes QoS 2.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="ac1a2-161">Si una aplicación de dispositivo publica un mensaje con **2 QoS**, centro de IoT se cierra la conexión de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="ac1a2-162">IoT Hub no retiene los mensajes de conservación.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="ac1a2-163">Si un dispositivo envía un mensaje con hello **conservar** marca establece too1, centro de IoT agrega hello **x-opt-conservar** toohello mensaje de la propiedad de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="ac1a2-164">En este caso, en lugar de conservar Hola Retener mensaje, centro de IoT pasa toohello aplicación de back-end.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="ac1a2-165">IoT Hub solo admite una conexión MQTT activa por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="ac1a2-166">Cualquier nueva conexión MQTT en nombre de hello mismo Id. de dispositivo hace centro de IoT conexión existente de toodrop Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="ac1a2-167">Para obtener más información, consulte la [guía del desarrollador de mensajería][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="ac1a2-168">Recepción de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="ac1a2-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="ac1a2-169">mensajes de tooreceive centro de IoT, un dispositivo debe suscribirse con `devices/{device_id}/messages/devicebound/#` como un **tema filtro**.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="ac1a2-170">Hola comodín multinivel  **#**  Hola tema filtro se utiliza únicamente tooallow Hola propiedades adicionales del dispositivo tooreceive en el nombre del tema Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="ac1a2-171">¿Centro de IoT no permitir el uso de Hola de hello  **#**  o **?**</span><span class="sxs-lookup"><span data-stu-id="ac1a2-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="ac1a2-172">caracteres comodín para el filtrado de subtemas.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="ac1a2-173">Como centro de IoT no es un agente de mensajería de publicación-suscripción de propósito general, solo admite nombres de temas de hello documentado y filtros de tema.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="ac1a2-174">Hello dispositivo no recibirá ningún mensaje del centro de IoT, hasta que se ha suscrito correctamente extremo específico del dispositivo de tooits, representado por hello `devices/{device_id}/messages/devicebound/#` filtro de tema.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="ac1a2-175">Una vez establecida la suscripción es correcta, dispositivo Hola comienza a recibir mensajes de solo nube al dispositivo que se han enviado tooit tarde Hola de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="ac1a2-176">Si se conecta el dispositivo de hello con **CleanSession** marca se establece demasiado**0**, suscripción Hola se conserva entre sesiones diferentes.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="ac1a2-177">Hola en este caso, la próxima vez que se conecta con **CleanSession 0** dispositivo Hola recibe mensajes pendientes que se han enviado tooit mientras estaba desconectado.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="ac1a2-178">Si utiliza el dispositivo de hello **CleanSession** marca se establece demasiado**1** sin embargo, no recibe ningún mensaje de centro de IoT hasta que se suscribe el punto de conexión tooits dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="ac1a2-179">Centro de IoT entrega mensajes con hello **el nombre del tema** `devices/{device_id}/messages/devicebound/`, o `devices/{device_id}/messages/devicebound/{property_bag}` si no hay ninguna propiedad de mensaje.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="ac1a2-180">`{property_bag}` contiene pares clave-valor con codificación URL de propiedades del mensaje.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="ac1a2-181">Solo propiedades de la aplicación y las propiedades establecidas por el usuario del sistema (como **messageId** o **correlationId**) se incluyen en la bolsa de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="ac1a2-182">Nombres de propiedad del sistema tienen el prefijo de hello  **$** , propiedades de la aplicación usan el nombre original de la propiedad de hello con ningún prefijo.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="ac1a2-183">Cuando una aplicación de dispositivo suscribe tema tooa con **QoS 2**, centro de IoT concede nivel máximo QoS 1 Hola **SUBACK** paquetes.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="ac1a2-184">Después de eso, centro de IoT entrega dispositivo toohello de mensajes con QoS 1.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="ac1a2-185">Recuperación de propiedades del dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="ac1a2-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="ac1a2-186">En primer lugar, un dispositivo se suscribe demasiado`$iothub/twin/res/#`, las respuestas de la operación de tooreceive Hola.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="ac1a2-187">A continuación, envía un mensaje vacío tootopic `$iothub/twin/GET/?$rid={request id}`, con un valor rellenado para **Id. de solicitud**. servicio de hello, a continuación, envía un mensaje de respuesta que contiene los datos de hello dispositivo gemelas en tema `$iothub/twin/res/{status}/?$rid={request id}`, utilizando Hola mismo  **Id. de solicitud** como solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="ac1a2-188">El identificador de la solicitud puede ser cualquier valor válido de propiedad de mensaje, según la [guía del desarrollador de mensajería de IoT Hub][lnk-messaging], y el estado se valida como entero.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="ac1a2-189">cuerpo de respuesta de Hello contiene la sección de propiedades de Hola de gemelas de dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="ac1a2-190">cuerpo de Hola de entrada del registro de hello identidad había limitado a toohello miembro de "propiedades", por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

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

<span data-ttu-id="ac1a2-191">Hola códigos de estado posibles son:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-191">hello possible status codes are:</span></span>

|<span data-ttu-id="ac1a2-192">Estado</span><span class="sxs-lookup"><span data-stu-id="ac1a2-192">Status</span></span> | <span data-ttu-id="ac1a2-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="ac1a2-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="ac1a2-194">200</span><span class="sxs-lookup"><span data-stu-id="ac1a2-194">200</span></span> | <span data-ttu-id="ac1a2-195">Correcto</span><span class="sxs-lookup"><span data-stu-id="ac1a2-195">Success</span></span> |
| <span data-ttu-id="ac1a2-196">429</span><span class="sxs-lookup"><span data-stu-id="ac1a2-196">429</span></span> | <span data-ttu-id="ac1a2-197">Demasiadas solicitudes (limitadas), según el artículo sobre [limitaciones de IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="ac1a2-198">5**</span><span class="sxs-lookup"><span data-stu-id="ac1a2-198">5**</span></span> | <span data-ttu-id="ac1a2-199">Errores del servidor</span><span class="sxs-lookup"><span data-stu-id="ac1a2-199">Server errors</span></span> |

<span data-ttu-id="ac1a2-200">Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="ac1a2-201">Actualización de las propiedades notificadas del dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="ac1a2-201">Update device twin's reported properties</span></span>

<span data-ttu-id="ac1a2-202">Hello secuencia siguiente describe cómo un dispositivo actualiza Hola notificado propiedades en gemelas de dispositivo de hello en el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="ac1a2-203">Un dispositivo en primer lugar debe suscribirse toohello `$iothub/twin/res/#` las respuestas de la operación de tema tooreceive Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="ac1a2-204">Un dispositivo envía un mensaje que contiene Hola dispositivo gemelas actualización toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` tema.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="ac1a2-205">Este mensaje incluye un valor de **identificador de solicitud**.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="ac1a2-206">Hola servicio, a continuación, envía un mensaje de respuesta que contiene Hola nuevo valor de ETag de Hola colección de propiedades incluido en el tema `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="ac1a2-207">Este mensaje de respuesta utiliza Hola mismo **Id. de solicitud** como solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="ac1a2-208">cuerpo del mensaje de solicitud de Hello contiene un documento JSON, que proporciona nuevos valores para propiedades incluidos (no se pueden modificar ninguna otra propiedad o metadatos).</span><span class="sxs-lookup"><span data-stu-id="ac1a2-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="ac1a2-209">Cada miembro en el documento JSON de hello actualiza o agrega a un miembro correspondiente Hola documento del doble del dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="ac1a2-210">Un conjunto de miembros demasiado`null`, eliminaciones Hola miembro de Hola que contiene el objeto.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="ac1a2-211">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="ac1a2-212">Hola códigos de estado posibles son:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-212">hello possible status codes are:</span></span>

|<span data-ttu-id="ac1a2-213">Estado</span><span class="sxs-lookup"><span data-stu-id="ac1a2-213">Status</span></span> | <span data-ttu-id="ac1a2-214">Descripción</span><span class="sxs-lookup"><span data-stu-id="ac1a2-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="ac1a2-215">200</span><span class="sxs-lookup"><span data-stu-id="ac1a2-215">200</span></span> | <span data-ttu-id="ac1a2-216">Correcto</span><span class="sxs-lookup"><span data-stu-id="ac1a2-216">Success</span></span> |
| <span data-ttu-id="ac1a2-217">400</span><span class="sxs-lookup"><span data-stu-id="ac1a2-217">400</span></span> | <span data-ttu-id="ac1a2-218">Solicitud incorrecta.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-218">Bad Request.</span></span> <span data-ttu-id="ac1a2-219">JSON con formato incorrecto</span><span class="sxs-lookup"><span data-stu-id="ac1a2-219">Malformed JSON</span></span> |
| <span data-ttu-id="ac1a2-220">429</span><span class="sxs-lookup"><span data-stu-id="ac1a2-220">429</span></span> | <span data-ttu-id="ac1a2-221">Demasiadas solicitudes (limitadas), según el artículo sobre [limitaciones de IoT Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="ac1a2-222">5**</span><span class="sxs-lookup"><span data-stu-id="ac1a2-222">5**</span></span> | <span data-ttu-id="ac1a2-223">Errores del servidor</span><span class="sxs-lookup"><span data-stu-id="ac1a2-223">Server errors</span></span> |

<span data-ttu-id="ac1a2-224">Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="ac1a2-225">Recepción de notificaciones de actualización de las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="ac1a2-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="ac1a2-226">Cuando se conecta un dispositivo, centro de IoT envía tema de las notificaciones toohello `$iothub/twin/PATCH/properties/desired/?$version={new version}`, que incluyen contenido de Hola de actualización de hello realizada Hola solución back-end.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="ac1a2-227">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="ac1a2-228">Para las actualizaciones de la propiedad, `null` valores decir Hola JSON del objeto miembro que se va a eliminar.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="ac1a2-229">IoT Hub genera notificaciones de cambio solo si los dispositivos están conectados.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="ac1a2-230">Realizar seguro hello tooimplement [flujo de reconexión de dispositivo] [ lnk-devguide-twin-reconnection] tookeep Hola deseado propiedades sincronizados entre el centro de IoT y aplicación de dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="ac1a2-231">Para obtener más información, consulte la [guía para desarrolladores sobre dispositivos gemelos][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="ac1a2-232">Método directo de responder tooa</span><span class="sxs-lookup"><span data-stu-id="ac1a2-232">Respond tooa direct method</span></span>

<span data-ttu-id="ac1a2-233">En primer lugar, un dispositivo tiene toosubscribe demasiado`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="ac1a2-234">Centro de IoT envía el tema del método solicitudes toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, con un valor JSON válido o con un cuerpo vacío.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="ac1a2-235">toorespond, dispositivo Hola envía un mensaje con un valor JSON válido o un tema de toohello de cuerpo vacío `$iothub/methods/res/{status}/?$rid={request id}`, donde **Id. de solicitud** tiene toomatch Hola uno en el mensaje de solicitud de Hola y **estado** tiene toobe un entero .</span><span class="sxs-lookup"><span data-stu-id="ac1a2-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="ac1a2-236">Para obtener más información, consulte la [guía para desarrolladores sobre el método directo][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="ac1a2-237">Consideraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="ac1a2-237">Additional considerations</span></span>

<span data-ttu-id="ac1a2-238">Como una última consideración, si necesita el comportamiento del protocolo MQTT toocustomize hello en lado de hello en la nube, debe revisar hello [puerta de enlace de IoT de Azure protocolo] [ lnk-azure-protocol-gateway] que le permite toodeploy un alto rendimiento puerta de enlace de protocolo personalizado que se comunica directamente con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="ac1a2-239">puerta de enlace de protocolo de Hello IoT de Azure permite toocustomize Hola dispositivo protocolo tooaccommodate brownfield MQTT implementaciones u otros protocolos personalizados.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="ac1a2-240">Sin embargo, este enfoque requiere que se ejecute y se ponga en funcionamiento una puerta de enlace de protocolo personalizado.</span><span class="sxs-lookup"><span data-stu-id="ac1a2-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac1a2-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac1a2-241">Next steps</span></span>

<span data-ttu-id="ac1a2-242">toolearn más información acerca del protocolo MQTT hello, vea hello [documentación MQTT][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="ac1a2-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="ac1a2-243">toolearn más información acerca de la planeación de la implementación del centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="ac1a2-244">[Catálogo de dispositivos de Azure Certified for IoT][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="ac1a2-245">[Compatibilidad con protocolos adicionales][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="ac1a2-246">[Comparación con Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="ac1a2-247">[Escalado, alta disponibilidad y recuperación ante desastres][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="ac1a2-248">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="ac1a2-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ac1a2-249">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="ac1a2-250">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ac1a2-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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

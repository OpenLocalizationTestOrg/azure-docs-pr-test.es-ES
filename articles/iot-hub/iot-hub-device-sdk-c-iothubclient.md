---
title: dispositivos de IoT aaaAzure SDK para C - IoTHubClient | Documentos de Microsoft
description: La biblioteca de IoTHubClient toouse hello en dispositivo de hello IoT de Azure SDK para aplicaciones de C toocreate dispositivos que se comunican con un centro de IoT.
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
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>SDK de dispositivo IoT de Microsoft Azure para C: más información sobre IoTHubClient
Hola [primero el artículo](iot-hub-device-sdk-c-intro.md) en este Hola serie introducida **dispositivos de IoT de Azure SDK para C**. En este artículo se explicaba que hay dos capas de arquitectura en el SDK. En la base de hello es hello **IoTHubClient** biblioteca que administra directamente la comunicación con el centro de IoT. También hay hello **serializador** biblioteca que se basa en dicha tooprovide servicios de serialización. En este artículo proporcionaremos información adicional sobre hello **IoTHubClient** biblioteca.

artículo anterior de Hola se describe cómo hello toouse **IoTHubClient** tooIoT de eventos de biblioteca toosend concentrador y recibir mensajes. En este artículo se extiende esa discusión mediante la explicación de cómo administrar precisamente toomore *cuando* enviar y recibir datos, se presenta toohello **API de nivel inferior**. También explicaremos cómo tooattach propiedades tooevents (y recuperarlos a partir de mensajes) mediante la propiedad Hola controlar características en hello **IoTHubClient** biblioteca. Por último, le presentaremos una explicación adicional de maneras diferentes toohandle mensajes recibidos desde el centro de IoT.

Hello artículo concluye al cubrir un par de varios temas, incluidos más información acerca de las credenciales del dispositivo y cómo toochange Hola comportamiento de hello **IoTHubClient** mediante opciones de configuración.

Vamos a usar hello **IoTHubClient** ejemplos de SDK de tooexplain estos temas. Si desea que toofollow a lo largo de, vea hello **el centro de IOT\_cliente\_ejemplo\_http** y **el centro de IOT\_cliente\_ejemplo\_amqp** las aplicaciones que se incluyen en el dispositivo de hello IoT de Azure SDK para C. todo lo descrito en hello las secciones siguientes se muestra en estos ejemplos.

Puede encontrar Hola [ **dispositivos de IoT de Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositorio y ver los detalles de la API de Hola Hola [referencia de la API de C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Hola las API de nivel inferior
artículo anterior de Hola describe la operación básica de Hola de hello **IotHubClient** en contexto de Hola de hello **el centro de IOT\_cliente\_ejemplo\_amqp** aplicación. Por ejemplo, explica cómo tooinitialize Hola biblioteca con este código.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

También se describe cómo los eventos toosend usando esta llamada de función.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

artículo de Hello también describe cómo los mensajes tooreceive registrando una función de devolución de llamada.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

artículo de Hello también se ha explicado cómo recursos toofree mediante código como el siguiente de saludo.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

Sin embargo, hay tooeach de funciones complementarias de estas API:

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Estas funciones incluyen "LL" en nombre de la API de Hola. Aparte de eso, los parámetros de Hola de cada una de estas funciones son equivalentes de no LL tootheir idénticos. Sin embargo, el comportamiento de Hola de estas funciones es diferente en un aspecto importante.

Cuando se llama a **IoTHubClient\_CreateFromConnectionString**, bibliotecas subyacente Hola crean un nuevo subproceso que se ejecuta en segundo plano de Hola. Este subproceso envía eventos al Centro de IoT y recibe mensajes del mismo. Ningún subproceso de este tipo se crea cuando se trabaja con hello "LL" API. creación de Hello de subproceso en segundo plano hello es un desarrollador de toohello comodidad. No es necesario tooworry sobre explícitamente eventos de enviar y recibir mensajes desde el centro de IoT--se produce automáticamente en segundo plano de Hola. En cambio, Hola "LL" API proporcionan un control explícito sobre la comunicación con el centro de IoT, si lo necesita.

toounderstand este mejor, echemos un vistazo a un ejemplo:

Cuando se llama a **IoTHubClient\_SendEventAsync**, lo que realmente está haciendo es sinónimo de poner eventos hello en un búfer. Hola subproceso en segundo plano creado cuando se llama a **IoTHubClient\_CreateFromConnectionString** continuamente supervisa este búfer y envíe cualquier dato que contiene tooIoT concentrador. Esto sucede en segundo plano de hello en hello mismo tiempo que Hola subproceso principal está realizando otro trabajo.

De forma similar, al registrar una función de devolución de llamada para mensajes con **IoTHubClient\_SetMessageCallback**, está dando a fondo de hello SDK toohave Hola subproceso invocar la función de devolución de llamada de hello cuando un mensaje recibido, independiente del subproceso principal de Hola.

Hola "LL" API no se crean un subproceso en segundo plano. En su lugar, una nueva API debe llamarse tooexplicitly enviar y recibir datos desde el centro de IoT. Esto se muestra en el siguiente ejemplo de Hola.

Hola **el centro de IOT\_cliente\_ejemplo\_http** aplicaciones que estén incluidas en la muestra de SDK de Hola Hola las API de nivel inferior. En ese ejemplo, enviamos tooIoT concentrador de eventos con código como Hola siguiente:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

tres primeras líneas Hello crean mensajes de bienvenida y última línea de hello envía eventos de Hola. Sin embargo, como se mencionó anteriormente, "Enviar" eventos de hello significa que los datos de hello simplemente se colocan en un búfer. Nada se transmite en la red de hello cuando se llama a **IoTHubClient\_LL\_SendEventAsync**. En orden tooactually entrada Hola datos tooIoT concentrador, se debe llamar a **IoTHubClient\_LL\_DoWork**, como en este ejemplo:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Este código (de hello **el centro de IOT\_cliente\_ejemplo\_http** aplicación) llama repetidamente **IoTHubClient\_LL\_DoWork** . Cada vez que **IoTHubClient\_LL\_DoWork** es llama, envía algunos eventos de hello búfer tooIoT concentrador y recupera un mensaje en cola que se envían toohello dispositivo. este último caso de Hello significa que si se registra una función de devolución de llamada para los mensajes, a continuación, se invoca la devolución de llamada de hello (suponiendo que se ponen en cola los mensajes de). Una función de devolución de llamada de este tipo se habría registrado con código como Hola siguiente:

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

Hola motivo que **IoTHubClient\_LL\_DoWork** se denomina a menudo en un bucle es que cada vez que se llama, envía *algunos* almacenado en búfer eventos tooIoT concentrador y recupera *Hola junto* mensaje en la cola para el dispositivo de Hola. Cada llamada no está garantizado toosend de almacenamiento en búfer todos los eventos o en cola tooretrieve todos los mensajes. Si desea que todos los eventos de hello almacene en búfer y, a continuación, continuar con el resto del procesamiento de toosend puede reemplazar este bucle con código como Hola siguiente:

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Este código llama **IoTHubClient\_LL\_DoWork** hasta que todos los eventos en el búfer de Hola se han enviado tooIoT concentrador. Tenga en cuenta que esto no significa que se recibieran todos los mensajes en cola. Parte del motivo hello es que comprobar si hay mensajes "all" no es determinista como una acción. ¿Qué ocurre si recuperar "todos" de los mensajes de Hola, pero, a continuación, otro se envía toohello dispositivo inmediatamente después? Un toodeal de manera mejor con la es con un tiempo de espera programado. Por ejemplo, función de devolución de llamada de mensajes de Hola pudo restablecer un temporizador cada vez que se invoca. A continuación, puede escribir procesamiento de toocontinue la lógica si, por ejemplo, se ha recibido ningún mensaje de Hola última *X* segundos.

Cuando está terminado ingressing eventos y recibir mensajes, para ser seguro toocall Hola correspondiente función tooclean los recursos.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Básicamente hay solo un conjunto de API toosend y recibir datos con un subproceso en segundo plano y otro conjunto de API que Hola lo mismo sin subproceso en segundo plano Hola. Muchos de los desarrolladores quizás prefiera Hola LL API no pero hello las API de nivel inferior son útiles cuando Hola programador desea un control explícito sobre las transmisiones de red. Por ejemplo, algunos dispositivos recopilan datos con el tiempo y solo incorporan eventos a intervalos especificados (por ejemplo, una vez cada hora o una vez al día). Hola Hola control tooexplicitly de capacidad al enviar y recibir datos desde el centro de IoT ofrecen a las API de nivel inferior. Otros simplemente preferirán simplicidad Hola ese Hola que proporcionan las API de nivel inferior. Todo lo que ocurre en el subproceso principal de hello en lugar de algunos ocurra de trabajo en segundo plano de Hola.

Cualquier modelo que elija, ser seguro toobe consistente en que las API que use. Si inicia mediante una llamada a **IoTHubClient\_LL\_CreateFromConnectionString**, asegúrese de usar solo Hola correspondiente a las API de nivel inferior para cualquier trabajo de seguimiento:

* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy
* IoTHubClient\_LL\_DoWork

Hola opuesto también es true. Si empieza con **IoTHubClient\_CreateFromConnectionString**, a continuación, use Hola LL API no para cualquier procesamiento adicional.

En dispositivos de IoT de Azure de hello SDK para C, vea hello **el centro de IOT\_cliente\_ejemplo\_http** inferior-nivel de aplicación para obtener un ejemplo completo de hello API. Hola **el centro de IOT\_cliente\_ejemplo\_amqp** puede hacer referencia a aplicación para obtener un ejemplo completo de Hola LL API no.

## <a name="property-handling"></a>Administración de propiedades
Hasta ahora cuando hemos descrito envío de datos, nos hemos ha hace referencia toohello cuerpo del mensaje de bienvenida. Por ejemplo, considere este código:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Este ejemplo envía un tooIoT mensaje concentrador con texto hello "Hola mundo". Sin embargo, centro de IoT también permite el mensaje de propiedades toobe tooeach adjunto. Propiedades son pares de nombre/valor que pueden ser mensajes toohello adjunto. Por ejemplo, se podrá modificar Hola anterior código tooattach un mensaje de toohello de propiedad:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Comenzamos llamando **IoTHubMessage\_propiedades** y pasándole el identificador hello de nuestro mensaje. Lo que obtenemos es un **mapa\_controlar** referencia que nos permite agregar propiedades de toostart. Hola este último se lleva a cabo mediante una llamada a **mapa\_AddOrUpdate**, que toma un mapa de referencia tooa\_identificador, el nombre de la propiedad de Hola y el valor de propiedad de Hola. Con esta API, podemos se pueden agregar todas la propiedades que se desee.

Cuando se leen los eventos de Hola de **centros de eventos**, receptor de hello puede mostrar propiedades de Hola y recuperar sus valores correspondientes. Por ejemplo, en .NET esto se lograría accediendo hello [colección de propiedades del objeto de hello EventData](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

En el ejemplo anterior de hello, vamos a adjuntar eventos de tooan de propiedades que enviamos tooIoT concentrador. Propiedades también pueden ser toomessages adjunto recibido desde el centro de IoT. Si lo deseamos tooretrieve propiedades de un mensaje, podemos utilizar código como Hola siguiente en la función de devolución de llamada de mensaje:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
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

Hola llamada demasiado**IoTHubMessage\_propiedades** devuelve hello **mapa\_controlar** referencia. , A continuación, pasar dicha referencia demasiado**mapa\_GetInternals** tooobtain una matriz de tooan de referencia de nombre/valor de hello pares (así como un recuento de propiedades de hello). En ese momento es cuestión de enumerar Hola propiedades tooget toohello valores que deseamos.

No tiene propiedades toouse en la aplicación. Sin embargo, si necesita tooset usarlas en eventos o recuperarlos desde mensajes, hello **IoTHubClient** biblioteca facilita el proceso.

## <a name="message-handling"></a>Administración de mensajes
Como se mencionó anteriormente, cuando llegan los mensajes de Hola de centro de IoT **IoTHubClient** biblioteca responde al invocar una función de devolución de llamada registrada. Hay un parámetro de valor devuelto de esta función que merece una explicación adicional. Este es un extracto de la función de devolución de llamada de hello en hello **el centro de IOT\_cliente\_ejemplo\_http** aplicación de ejemplo:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Tenga en cuenta que es el tipo de valor devuelto de hello **IOTHUBMESSAGE\_DISPOSITION\_resultado** y en este caso particular, devolvemos **IOTHUBMESSAGE\_aceptado**. Hay otros valores, podemos devolvemos desde esta función que cambiar cómo Hola **IoTHubClient** biblioteca reacciona devolución de llamada de toohello mensaje. Estas son opciones de Hola.

* **IOTHUBMESSAGE\_aceptado** : mensaje de bienvenida se ha procesado correctamente. Hola **IoTHubClient** biblioteca no invocará la función de devolución de llamada de hello nuevo con hello mismo mensaje.
* **IOTHUBMESSAGE\_rechazado** : no se procesó el mensaje de bienvenida y no hay ningún toodo deseo en Hola futuras. Hola **IoTHubClient** biblioteca no debe invocar la función de devolución de llamada de hello nuevo con hello mismo mensaje.
* **IOTHUBMESSAGE\_ABANDONED** : no se procesó correctamente el mensaje de bienvenida, pero Hola **IoTHubClient** biblioteca debe invocar la función de devolución de llamada de hello nuevo con hello mismo mensaje.

Para hello primero dos códigos de retorno, hello **IoTHubClient** biblioteca envía un tooIoT de mensaje que indica ese mensaje Hola de concentrador debe eliminarse de cola de dispositivo de hello y no entregado de nuevo. efecto neto de Hello es Hola igual (mensaje de bienvenida se elimina de la cola de dispositivo de hello), pero todavía se registra si los mensajes de bienvenida se ha aceptado o rechazado.  La grabación de esta distinción es útil toosenders de mensaje de bienvenida que pueden realizar escuchas de los comentarios y averiguar si un dispositivo ha aceptado o rechazado un mensaje determinado.

En caso último Hola se envía un mensaje también tooIoT concentrador, pero indica que ese mensaje Hola debería volverse a entregar. Normalmente podrá abandonar un mensaje si encuentra algún error, pero desea tootry tooprocess Hola mensaje nuevo. En cambio, rechazar un mensaje es adecuado cuando se produce un error irrecuperable (o si simplemente decide que no desea que el mensaje de bienvenida de tooprocess).

En cualquier caso, tener en cuenta distintos códigos de retorno Hola por lo que puede susciten comportamiento de Hola que desea en hello **IoTHubClient** biblioteca.

## <a name="alternate-device-credentials"></a>Credenciales de dispositivo alternativas
Como se explicó anteriormente, Hola toodo lo primero que cuando se trabaja con hello **IoTHubClient** biblioteca es tooobtain una **el centro de IOT\_cliente\_controlar** con una llamada como Hola Después de:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Hola argumentos demasiado**IoTHubClient\_CreateFromConnectionString** son de cadena de conexión de dispositivo de Hola y un parámetro que indica el protocolo de hello usamos toocommunicate con centro de IoT. cadena de conexión de dispositivo de Hello tiene un formato que aparece como sigue:

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

Hay cuatro grupos de información en esta cadena: nombre del Centro de IoT, sufijo del Centro de IoT, identificador de dispositivo y clave de acceso compartido. Obtener nombre de dominio completo (FQDN) de Hola de un centro de IoT cuando se crea la instancia del concentrador IoT en hello portal de Azure, esto da nombre (Hola primera parte del programa Hola FQDN) del centro de IoT de Hola y el sufijo de centro de IoT hello (resto de Hola de hello FQDN). Obtener Id. de dispositivo de Hola y la clave de acceso compartido de hello al registrar el dispositivo con el centro de IoT (como se describe en hello [artículo anterior](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** le ofrece la biblioteca de hello tooinitialize unidireccional. Si lo prefiere, puede crear un nuevo **el centro de IOT\_cliente\_controlar** mediante el uso de estos parámetros individuales en lugar de la cadena de conexión de dispositivo de Hola. Esto se logra con hello siguiente código:

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

Esto lleva a cabo Hola lo mismo que **IoTHubClient\_CreateFromConnectionString**.

Puede parecer obvio que desearía toouse **IoTHubClient\_CreateFromConnectionString** en lugar de este método de inicialización más detallado. Sin embargo, tenga en cuenta que cuando se registra un dispositivo en el Centro de IoT, lo que obtenemos es un identificador de dispositivo y una clave de dispositivo (no una cadena de conexión). Hola *explorador del dispositivo* herramienta SDK que se introduce en hello [artículo anterior](iot-hub-device-sdk-c-intro.md) usa las bibliotecas en hello **IoT de Azure SDK del servicio** cadena de conexión de dispositivo toocreate Hola desde Id. de dispositivo de Hello, clave de dispositivo y nombre de host del centro de IoT. Por lo que una llamada a **IoTHubClient\_LL\_crear** puede ser preferible porque ahorra paso Hola consiste en generar una cadena de conexión. Use el método que le resulte conveniente.

## <a name="configuration-options"></a>Opciones de configuración
Hasta ahora todo lo que se describe sobre Hola Hola de manera **IoTHubClient** biblioteca works refleja su comportamiento predeterminado. Sin embargo, hay algunas opciones que se puede establecer toochange cómo funciona la biblioteca de Hola. Esto se logra mediante el aprovechamiento de hello **IoTHubClient\_LL\_SetOption** API. En este ejemplo:

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Hay un par de opciones que se usan con frecuencia:

* **SetBatching** (bool): si **true**, entonces tooIoT centro de datos que se envían se envía en lotes. Si es **false**, los mensajes se envían individualmente. valor predeterminado de Hello es **false**. Tenga en cuenta que hello **SetBatching** opción solo aplica toohello HTTP y no toohello MQTT o AMQP protocolos.
* **Tiempo de espera** (entero sin sino): este valor se representa en milisegundos. Si envía una solicitud HTTP o recibir una respuesta tarda más tiempo, a continuación, Hola se agota.

opción de procesamiento por lotes de Hello es importante. De forma predeterminada, Hola eventos de biblioteca de ingresses individualmente (un único evento es lo que se pase demasiado**IoTHubClient\_LL\_SendEventAsync**). Si es la opción de procesamiento por lotes de Hola **true**, biblioteca de hello recopila todos los eventos como sea posible de búfer de hello (arriba toohello tamaño máximo del mensaje que aceptará centro de IoT).  Hello lote de eventos se envía tooIoT concentrador en una única llamada HTTP (eventos individuales de hello están agrupados en una matriz JSON). Habilitar el procesamiento por lotes normalmente da como resultado un gran aumento del rendimiento ya que se reducen los recorridos de ida y vuelta de red. Además, reduce considerablemente el ancho de banda porque se envía un conjunto de encabezados HTTP con un lote de eventos en lugar de un conjunto de encabezados para cada evento individual. A menos que tenga un motivo concreto toodo en caso contrario, normalmente querrá tooenable procesamiento por lotes.

## <a name="next-steps"></a>Pasos siguientes
Este artículo se describen en el comportamiento de Hola de detalle de hello **IoTHubClient** biblioteca se encuentra en hello **dispositivos de IoT de Azure SDK para C**. Con esta información, debe tener un buen conocimiento de las capacidades de Hola de hello **IoTHubClient** biblioteca. Hola [artículo siguiente](iot-hub-device-sdk-c-serializer.md) proporciona detalles similares en hello **serializador** biblioteca.

toolearn más sobre el desarrollo de centro de IoT, vea hello [SDK de Azure IoT][lnk-sdks].

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

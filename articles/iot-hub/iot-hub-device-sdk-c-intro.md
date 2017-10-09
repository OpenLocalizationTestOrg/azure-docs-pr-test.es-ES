---
title: dispositivo de aaaThe IoT de Azure SDK para C | Documentos de Microsoft
description: "Introducción al SDK de dispositivos de IoT de Azure de Hola para C y obtenga información acerca de cómo toocreate aplicaciones para dispositivos que se comunican con un centro de IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>SDK de dispositivo IoT de Azure para C

Hola **dispositivos de IoT de Azure SDK** es un conjunto de bibliotecas diseñado el proceso de hello toosimplify de enviar mensajes de tooand recibir los mensajes de Hola **centro de IoT de Azure** servicio. Hay distintas variaciones de hello SDK, como destino una plataforma concreta, pero este artículo describen hello **dispositivos de IoT de Azure SDK para C**.

dispositivo de Hello IoT de Azure SDK para C se escribe en ANSI C (C99) toomaximize portabilidad. Esta característica hace Hola bibliotecas adecuadas toooperate en varias plataformas y dispositivos, especialmente cuando se minimiza el disco y consumo de memoria es una prioridad.

Hay una amplia gama de plataformas en qué Hola SDK se ha probado (vea hello [Azure Certified para el catálogo de dispositivos de IoT](https://catalog.azureiotsuite.com/) para obtener más información). Aunque en este artículo incluye tutoriales de código de ejemplo que se ejecuta en la plataforma de Windows hello, código de hello descrito en este artículo es idéntico a lo largo intervalo de Hola de las plataformas compatibles.

Este artículo presenta toohello arquitectura de SDK de dispositivos de IoT de Azure Hola de C. Muestra cómo enviar datos tooIoT centro de biblioteca de dispositivos de tooinitialize hello y recibir los mensajes de. información de Hello en este artículo debería ser suficiente tooget iniciado mediante Hola SDK, pero también proporciona punteros tooadditional información acerca de las bibliotecas de Hola.

## <a name="sdk-architecture"></a>Arquitectura del SDK

Puede encontrar Hola [ **dispositivos de IoT de Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositorio y ver los detalles de la API de Hola Hola [referencia de la API de C](https://azure.github.io/azure-iot-sdk-c/index.html).

versión más reciente de Hola de bibliotecas de hello puede encontrarse en hello **maestro** rama del repositorio de hello:

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* Hola implementación básica de hello SDK es Hola **el centro de IOT\_cliente** carpeta que contiene la implementación de Hola de capa de API más bajo de Hola Hola SDK: Hola **IoTHubClient** biblioteca. Hola **IoTHubClient** biblioteca contiene las API de implementación de mensajería sin formato para enviar mensajes tooIoT concentrador y recibir mensajes desde el centro de IoT. Quien use esta biblioteca es responsable de la implementación de la serialización de mensajes, pero otros detalles de la comunicación con IoT Hub se controlan automáticamente.
* Hola **serializador** carpeta contiene funciones auxiliares y ejemplos que muestran cómo tooserialize datos antes de enviar el uso del centro de IoT de tooAzure Hola biblioteca de cliente. uso de Hola de serializador de hello no es obligatorio y se proporciona como una comodidad. Hola toouse **serializador** biblioteca, define un modelo que especifica datos toosend tooIoT hello y centro de mensajes de saludo espera tooreceive de él. Una vez definido el modelo de hello, Hola SDK proporciona una superficie de API que permite tooeasily trabajo con el dispositivo a la nube y mensajes en la nube a dispositivo sin preocuparse de Hola detalles de serialización. biblioteca de Hello depende de otras bibliotecas de código abierto que implementan el transporte mediante protocolos como MQTT y AMQP.
* Hola **IoTHubClient** biblioteca depende de otras bibliotecas de código abierto:
  * Hola [Azure C compartido utilidad](https://github.com/Azure/azure-c-shared-utility) biblioteca, que proporciona la funcionalidad común para realizar tareas básicas (como cadenas, manipulación de lista y E/S) necesaria a través de varios SDK de C relacionadas con Azure.
  * Hola [uAMQP Azure](https://github.com/Azure/azure-uamqp-c) biblioteca, que es una implementación de cliente de AMQP optimizada para dispositivos de limitación de recursos.
  * Hola [uMQTT Azure](https://github.com/Azure/azure-umqtt-c) biblioteca, que es una biblioteca de propósito general implementar hello MQTT protocolo y optimizado para dispositivos de limitación de recursos.

Uso de estas bibliotecas es más fácil toounderstand examinando el código de ejemplo. Hola las secciones siguientes le guiará por varias aplicaciones de ejemplo de Hola que se incluyen en hello SDK. En este tutorial debe proporcionarle un buen sentirse para hello varias funciones de niveles arquitectónicos de Hola de Hola SDK y un Hola de toohow de introducción las API de funcionar.

## <a name="before-you-run-hello-samples"></a>Antes de ejecutar los ejemplos de hello

Antes de poder ejecutar los ejemplos de hello en dispositivo de hello IoT de Azure SDK para C, debe [crear una instancia del servicio del centro de IoT hello](iot-hub-create-through-portal.md) en su suscripción de Azure. A continuación, complete Hola siguientes tareas:

* Preparación del entorno de desarrollo
* Obtención de las credenciales del dispositivo.

### <a name="prepare-your-development-environment"></a>Preparación del entorno de desarrollo

Los paquetes se proporcionan para plataformas comunes (por ejemplo, NuGet para Windows o apt_get para Debian y Ubuntu) y ejemplos de hello usan estos paquetes cuando esté disponible. En algunos casos, necesitará toocompile Hola SDK para o en el dispositivo. Si necesita toocompile Hola SDK, consulte [preparar el entorno de desarrollo](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) en el repositorio de GitHub de Hola.

código de aplicación de ejemplo de tooobtain hello, descarga una copia del programa Hola SDK desde GitHub. Obtenga una copia de origen Hola de hello **maestro** rama de hello [repositorio de GitHub](https://github.com/Azure/azure-iot-sdk-c).


### <a name="obtain-hello-device-credentials"></a>Obtener las credenciales del dispositivo Hola

Ahora que tiene código fuente de ejemplo de Hola, hello toodo de lo siguiente es tooget un conjunto de credenciales de dispositivo. Para un dispositivo toobe puede tooaccess un centro de IoT, primero debe agregar Hola dispositivo toohello del registro de identidad de centro de IoT. Al agregar un dispositivo, obtendrá un conjunto de credenciales de dispositivo que necesita para el centro de IoT de hello dispositivo toobe tooconnect capaz de toohello. aplicaciones de ejemplo de Hola se describe en la sección siguiente Hola espera que estas credenciales en forma de Hola de un **cadena de conexión de dispositivo**.

Hay varias toohelp de herramientas de código abierto que administra el centro de IoT.

* Una aplicación de Windows llamada [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).
* Una herramienta de la CLI de node.js multiplataforma llamada [iothub-explorer](https://github.com/azure/iothub-explorer).

Este tutorial usa Hola gráfica *explorer dispositivo* herramienta. También puede usar hello *el centro de IOT explorador* herramienta si lo prefiere toouse una herramienta CLI.

herramienta de explorador del dispositivo de Hello usa hello Azure IoT servicio bibliotecas tooperform distintas funciones en el centro de IoT, incluida la adición de dispositivos. Si usas tooadd un dispositivo de la herramienta de explorador del dispositivo hello, obtendrá una cadena de conexión para el dispositivo. Necesita esta aplicación de ejemplo de conexión cadena toorun Hola.

Si no está familiarizado con la herramienta de explorador del dispositivo de hello, Hola procedimiento describe cómo toouse tooadd un dispositivo y obtener una cadena de conexión de dispositivo.

herramienta de explorador de dispositivos de hello tooinstall, consulte [cómo toouse Hola explorador del dispositivo para los dispositivos del centro de IoT](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).

Al ejecutar el programa Hola, verá esta interfaz:

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

Escriba su **cadena de conexión del centro de IoT** Hola primero campo y haga clic en **actualización**. Este paso configura la herramienta de Hola para que puedan comunicarse con el centro de IoT.

Cuando se configura la cadena de conexión de centro de IoT hello, haga clic en hello **administración** ficha:

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

Esta ficha es donde se administran los dispositivos de hello registrados en el centro de IoT.

Crear un dispositivo, haga clic en hello **crear** botón. Se muestra un cuadro de diálogo con un conjunto de claves (principal y secundaria) previamente rellenadas. Escriba un valor en **Device ID** (Id. de dispositivo) y haga clic en **Create** (Crear).

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

Cuando se crea el dispositivo de hello, dispositivos de hello lista actualizaciones con todos los dispositivos de hello registrado, incluidos Hola que acaba de crear. Si hace clic con el botón derecho en el dispositivo nuevo, verá este menú:

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

Si elige **copiar la cadena de conexión del dispositivo seleccionado**, cadena de conexión de dispositivo de hello es copiada toohello Portapapeles. Mantener una copia de la cadena de conexión de dispositivo de Hola. Se necesita cuando se ejecutan aplicaciones de ejemplo de Hola descritas en hello las secciones siguientes.

Cuando haya completado los pasos de hello anteriores, está listo toostart ejecutar algún código. Ambos ejemplos tienen una constante al principio de hello del archivo de código fuente principal de Hola que permite tooenter una cadena de conexión. Por ejemplo, Hola línea correspondiente de hello **el centro de IOT\_cliente\_ejemplo\_mqtt** aplicación aparece como sigue.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Utilizar la biblioteca en IoTHubClient Hola

Dentro de hello **el centro de IOT\_cliente** carpeta Hola [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repositorio, hay un **ejemplos** carpeta que contenga una aplicación denominada **el centro de IOT\_cliente\_ejemplo\_mqtt**.

versión de Windows Hello de hello **el centro de IOT\_cliente\_ejemplo\_mqtt** aplicación incluye Hola después de solución de Visual Studio:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> Si abre este proyecto en Visual Studio de 2017, acepte mensajes hello toohello tooretarget Hola proyecto última versión.

Esta solución contiene un proyecto. En esta solución hay cuatro paquetes de NuGet instalados:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

Siempre debe hello **Microsoft.Azure.C.SharedUtility** cuando se trabaja con hello SDK del paquete. Este ejemplo usa el protocolo MQTT de hello, por lo tanto, debe incluir hello **Microsoft.Azure.umqtt** y **Microsoft.Azure.IoTHub.MqttTransport** (no hay equivalente paquetes para HTTP y AMQP de paquetes ). Dado que el ejemplo de Hola usa hello **IoTHubClient** biblioteca, también debe incluir hello **Microsoft.Azure.IoTHub.IoTHubClient** paquete de la solución.

Implementación de hello para la aplicación de ejemplo de Hola se puede encontrar en hello **el centro de IOT\_cliente\_ejemplo\_mqtt.c** archivo de código fuente.

pasos siguientes Hello utilizan este toowalk de aplicación de ejemplo le guían a través de los requisitos hello toouse **IoTHubClient** biblioteca.

### <a name="initialize-hello-library"></a>Inicializar la biblioteca de Hola

> [!NOTE]
> Antes de empezar a trabajar con bibliotecas de hello, puede que necesite tooperform algunas operaciones de inicialización específica de la plataforma. Por ejemplo, si tiene previsto toouse AMQP en Linux debe inicializar la biblioteca OpenSSL de Hola. Hola ejemplos de hello [repositorio de GitHub](https://github.com/Azure/azure-iot-sdk-c) llamar a la función de utilidad hello **plataforma\_init** cuando Hola cliente inicia y llamar a hello **plataforma\_deinit**  función antes de salir. Estas funciones se declaran en el archivo de encabezado de hello platform.h. Examine las definiciones de Hola de estas funciones para la plataforma de destino en hello [repositorio](https://github.com/Azure/azure-iot-sdk-c) toodetermine si es necesario tooinclude cualquier código de inicialización específica de la plataforma en el cliente.

en primer lugar, toostart trabajar con bibliotecas de hello, asignar un identificador de cliente de centro de IoT:

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

Pasar una copia de la cadena de conexión de dispositivo de Hola que obtuvo en función de hello dispositivo explorador herramienta toothis. También se designa toouse de protocolo de comunicaciones de Hola. En este ejemplo se utiliza MQTT, pero también se pueden usar AMQP y HTTP.

Cuando haya válido **el centro de IOT\_cliente\_controlar**, puede iniciar una llamada a toosend de las API de Hola y recibir mensajes tooand centro de IoT.

### <a name="send-messages"></a>Envío de mensajes

aplicación de ejemplo de Hola configura un centro de IoT de bucle toosend mensajes tooyour. Hola siguiente fragmento de código:

- Crea un mensaje.
- Agrega un mensaje de toohello de propiedad.
- Envía un mensaje.

Primero, cree un mensaje:

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

Cada vez que se envía un mensaje, especifique una función de devolución de llamada de tooa de referencia que se invoca cuando se envían datos de Hola. En este ejemplo, se llama la función de devolución de llamada de hello **SendConfirmationCallback**. Hola siguiente fragmento de código muestra esta función de devolución de llamada:

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Tenga en cuenta Hola llamada toohello **IoTHubMessage\_destruir** función cuando haya terminado con el mensaje de bienvenida. Esta función libera recursos de hello asignados cuando se creó el mensaje de bienvenida.

### <a name="receive-messages"></a>Recepción de mensajes

La recepción de mensajes es una operación asincrónica. En primer lugar, registrar hello tooinvoke de devolución de llamada cuando el dispositivo de hello recibe un mensaje:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

Hola último parámetro es un toowhatever de puntero void que desee. En el ejemplo hello, es un entero de tooan de puntero, pero podría ser un puntero tooa estructura de datos más compleja. Este parámetro permite toooperate de función de devolución de llamada de hello en estado compartido con un llamador de Hola de esta función.

Cuando el dispositivo de hello recibe un mensaje, hello función de devolución de llamada registrada se invoca. Dicha función de devolución de llamada recupera:

* Id. de mensaje de Hola y el Id. de correlación del mensaje de bienvenida.
* contenido del mensaje Hola.
* Las propiedades personalizadas de mensajes de bienvenida.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Hola de uso **IoTHubMessage\_GetByteArray** mensaje de saludo de función tooretrieve, que en este ejemplo es una cadena.

### <a name="uninitialize-hello-library"></a>Cancelar la inicialización Hola biblioteca

Cuando haya terminado de enviar eventos y recibir mensajes, se puede cancelar la inicialización Hola IoT biblioteca. toodo por lo tanto, emita Hola después de la llamada de función:

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Esta llamada se libere recursos Hola previamente asignados por hello **IoTHubClient\_CreateFromConnectionString** (función).

Como puede ver, es fácil toosend y recibir mensajes con hello **IoTHubClient** biblioteca. biblioteca de Hello controla los detalles de hello de la comunicación con el centro de IoT, incluidos lo toouse de protocolo (desde la perspectiva de Hola de desarrollador de hello, esta es una opción de configuración simple).

Hola **IoTHubClient** biblioteca también proporciona un control preciso sobre cómo datos de hello tooserialize el dispositivo envía tooIoT concentrador. En algunos casos, este nivel de control representa una ventaja, pero en otros es un detalle de implementación que no desea toobe preocupan. Si ese es el caso de hello, puede considerar el uso de hello **serializador** biblioteca, que se describe en la sección siguiente Hola.

## <a name="use-hello-serializer-library"></a>Utilizar la biblioteca de serializador de Hola

Hola conceptualmente **serializador** biblioteca se ubica en la parte superior hello **IoTHubClient** biblioteca Hola SDK. Usa hello **IoTHubClient** biblioteca para hello subyacente comunicación con el centro de IoT, pero agrega capacidades de modelado que eliminan la carga de Hola de trabajar con la serialización del mensaje del programador de Hola. Un ejemplo ilustra mejor el funcionamiento de esta biblioteca.

Hola interior **serializador** carpeta Hola [repositorio de azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), es un **ejemplos** carpeta que contenga una aplicación denominada **simplesample \_mqtt**. la versión de Windows Hello de este ejemplo incluye Hola después de solución de Visual Studio:

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> Si abre este proyecto en Visual Studio de 2017, acepte mensajes hello toohello tooretarget Hola proyecto última versión.

Al igual que con el ejemplo anterior de hello, éste incluye varios paquetes de NuGet:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

Ha visto la mayoría de estos paquetes en el ejemplo de Hola a anterior, pero **Microsoft.Azure.IoTHub.Serializer** es nuevo. Este paquete es necesario cuando se utiliza hello **serializador** biblioteca.

Implementación de Hola de aplicación de ejemplo de Hola se puede encontrar en hello **simplesample\_mqtt.c** archivo.

Hello secciones siguientes le guían por partes principales de Hola de este ejemplo.

### <a name="initialize-hello-library"></a>Inicializar la biblioteca de Hola

toostart trabajar con hello **serializador** biblioteca, llamada Hola inicialización API:

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

Hola llamada toohello **serializador\_init** función es una llamada de un solo uso e inicializa Hola biblioteca subyacente. A continuación, se llama a hello **IoTHubClient\_LL\_CreateFromConnectionString** función, que es Hola misma API como en hello **IoTHubClient** ejemplo. Esta llamada establece la cadena de conexión del dispositivo (esta llamada es también donde elegir protocolo Hola desea toouse). Este ejemplo utiliza MQTT como transporte de hello, pero podría utilizar AMQP o HTTP.

Por último, llame hello **crear\_modelo\_instancia** función. **WeatherStation** es Hola espacio de nombres del modelo de Hola y **ContosoAnemometer** es Hola nombre del modelo de Hola. Una vez creada la instancia de modelo de hello, puede usar toostart enviar y recibir mensajes. Sin embargo, es importante toounderstand qué es un modelo.

### <a name="define-hello-model"></a>Definir el modelo de Hola

Un modelo en hello **serializador** biblioteca define los mensajes de Hola que el dispositivo puede enviar tooIoT mensajes hello y concentrador, denominado *acciones* Hola modeling language, que se puede recibir. Definir un modelo con un conjunto de macros de C en hello **simplesample\_mqtt** aplicación de ejemplo:

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Hola **comenzar\_espacio de nombres** y **final\_espacio de nombres** macros ambos desconectar el espacio de nombres de Hola de modelo de hello como argumento. Se espera que haya nada entre estas macros es una definición de Hola de su modelo o modelos y estructuras de datos de Hola que usan modelos de Hola.

En este ejemplo, hay un único modelo denominado **ContosoAnemometer**. Este modelo define dos conjuntos de datos que el dispositivo puede enviar tooIoT concentrador: **DeviceId** y **WindSpeed**. También define tres acciones (mensajes) que el dispositivo puede recibir: **TurnFanOn**, **TurnFanOff** y **SetAirResistance**. Cada elemento de datos tiene un tipo y cada acción tiene un nombre (y, opcionalmente, un conjunto de parámetros).

datos de Hola y las acciones definidas en el modelo de hello definen una superficie de API que puede usar toosend mensajes tooIoT concentrador y responder toomessages enviado toohello dispositivo. El uso de este modelo se entiende mejor con un ejemplo.

### <a name="send-messages"></a>Envío de mensajes

modelo de Hello define los datos de hello puede enviar tooIoT concentrador. En este ejemplo, que significa que uno de hello dos elementos de datos definidos mediante hello **WITH_DATA** macro. Hay varios pasos a necesario toosend **DeviceId** y **WindSpeed** centro de IoT tooan de valores. Hola en primer lugar es datos de hello tooset desea toosend:

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

Hello modelo que se definió anteriormente le permite valores de hello tooset estableciendo los miembros de un **struct**. A continuación, serializar mensajes de bienvenida que desee toosend:

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

Este código serializa el búfer de dispositivo para la nube tooa hello (que se hace referencia por **destino**). código de Hello, a continuación, invoca hello **sendMessage** función toosend Hola mensaje tooIoT concentrador:

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


Hola segundo parámetro toolast de **IoTHubClient\_LL\_SendEventAsync** es una función de devolución de llamada de tooa de referencia que se llama cuando se envían correctamente datos de Hola. Aquí se muestra la función de devolución de llamada de hello en el ejemplo hello:

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

Hola segundo parámetro es un contexto de toouser puntero; Hola mismo puntero pasa demasiado**IoTHubClient\_LL\_SendEventAsync**. En este caso, el contexto de hello es un contador simple, pero puede ser que desee.

Eso es todo lo hay mensajes de dispositivo a la nube de toosending. Hello sólo lo dejado toocover es cómo tooreceive mensajes.

### <a name="receive-messages"></a>Recepción de mensajes

Recibir un mensaje funciona del mismo modo toohello funcionamiento de mensajes de Hola **IoTHubClient** biblioteca. En primer lugar, se registra una función de devolución de llamada de mensaje:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

A continuación, puede escribir la función de devolución de llamada de Hola que se invoca cuando se recibe un mensaje:

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

Este código es reutilizable, ha Hola mismo para cualquier solución. Esta función recibe mensajes de bienvenida y se encarga de enrutarlo toohello función adecuada a través de la llamada de hello demasiado**EXECUTE\_comando**. función Hello que se llama en este momento depende de definición de Hola de acciones de hello en el modelo.

Cuando se define una acción en el modelo, que se requiere tooimplement una función que se llama cuando el dispositivo recibe mensajes de bienvenida del correspondiente. Por ejemplo, si el modelo define esta acción:

```c
WITH_ACTION(SetAirResistance, int, Position)
```

Defina una función con esta firma:

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Tenga en cuenta cómo Hola nombre de función hello coincide con hello de acción de hello en el modelo de Hola y que Hola parámetros de función hello son Hola especificado para la acción de Hola. primer parámetro de Hello siempre es necesario y contiene una instancia de toohello del puntero del modelo.

Cuando el dispositivo de hello recibe un mensaje que coincide con esta firma, se llama función correspondiente Hola. Por lo tanto, además de tener tooinclude Hola reutilizable código de **IoTHubMessage**, recibir mensajes es cuestión de definir una función sencilla para cada acción definida en el modelo.

### <a name="uninitialize-hello-library"></a>Cancelar la inicialización Hola biblioteca

Cuando haya terminado de enviar los datos y recibir mensajes, se puede cancelar la inicialización Hola IoT biblioteca:

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

Cada una de estas tres funciones se alinea con hello tres funciones de inicialización que se ha descrito anteriormente. Llamar a estas API garantiza que se liberan los recursos asignados previamente.

## <a name="next-steps"></a>Pasos siguientes

En este artículo se trata aspectos básicos de hello del uso de bibliotecas de Hola Hola **dispositivos de IoT de Azure SDK para C**. Que proporcionaba con suficiente toounderstand información qué se incluye en el SDK de Hola, su arquitectura y cómo tooget a trabajar con hello ejemplos de Windows. artículo siguiente Hola continúa descripción Hola de hello SDK explicando [más información acerca de la biblioteca de hello IoTHubClient](iot-hub-device-sdk-c-iothubclient.md).

toolearn más sobre el desarrollo de centro de IoT, vea hello [SDK de Azure IoT][lnk-sdks].

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

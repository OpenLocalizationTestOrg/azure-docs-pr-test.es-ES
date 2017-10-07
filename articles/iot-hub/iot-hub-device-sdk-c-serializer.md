---
title: dispositivos de IoT aaaAzure SDK para C - serializador | Documentos de Microsoft
description: La biblioteca de serializador toouse hello en dispositivo de hello IoT de Azure SDK para aplicaciones de C toocreate dispositivos que se comunican con un centro de IoT.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>SDK de dispositivo IoT de Azure para C: más información sobre el serializador
Hola [primero el artículo](iot-hub-device-sdk-c-intro.md) en este Hola serie introducida **dispositivos de IoT de Azure SDK para C**. artículo siguiente Hola proporciona una descripción más detallada de hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). En este artículo se completa cobertura de hello SDK al proporcionar una descripción más detallada de hello restantes componente: Hola **serializador** biblioteca.

artículo introductorio Hola se describe cómo hello toouse **serializador** biblioteca toosend eventos tooand recibir mensajes desde el centro de IoT. En este artículo, se amplía esa discusión proporcionando una explicación más completa de cómo toomodel los datos con hello **serializador** lenguaje de macros. artículo Hello también incluye información más detallada sobre cómo biblioteca Hola serializa los mensajes (y en algunos casos cómo se puede controlar un comportamiento de serialización hello). Describiremos también puede modificar algunos parámetros que determinan el tamaño de Hola de modelos de Hola que haya creado.

Por último, artículo Hola repasa algunos temas que se tratan en los artículos anteriores como mensaje y control de la propiedad. Hola mismo utilizando hello como buscaremos el esas características, trabajar en **serializador** biblioteca como lo hacen con hello **IoTHubClient** biblioteca.

Todo lo descrito en este artículo se basa en hello **serializador** ejemplos del SDK. Si desea que toofollow a lo largo de, vea hello **simplesample\_amqp** y **simplesample\_http** aplicaciones incluidas en el SDK de dispositivos de IoT de Azure Hola de C.

Puede encontrar Hola [ **dispositivos de IoT de Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositorio y ver los detalles de la API de Hola Hola [referencia de la API de C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-modeling-language"></a>lenguaje de modelado de Hola
Hola [artículo introductorio](iot-hub-device-sdk-c-intro.md) en este Hola serie introducida **dispositivos de IoT de Azure SDK para C** modeling language a través de ejemplo de Hola incluido en hello **simplesample\_amqp**  aplicación:

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Como puede ver, Hola lenguaje de modelado se basa en las macros de C. La definición comienza siempre con **BEGIN\_NAMESPACE** y termina siempre con **END\_NAMESPACE**. Es tooname Hola espacio de nombres común para su empresa o, como en este ejemplo, el proyecto de Hola que estás trabajando en.

¿Qué va en el interior de espacio de nombres de hello son definiciones de modelo. En este caso, hay un único modelo para un anemómetro. Una vez más, el modelo de hello puede tener cualquier nombre, pero normalmente se denomina para el dispositivo de Hola o un tipo de datos que desee tooexchange con el centro de IoT.  

Los modelos contienen una definición de eventos de hello puede entrada tooIoT concentrador (hello *datos*), así como mensajes de saludo puede recibir de centro de IoT (hello *acciones*). Como puede ver en el ejemplo de Hola, los eventos tienen un tipo y un nombre; las acciones tienen un nombre y parámetros opcionales (cada uno con un tipo).

Lo que no se muestra en este ejemplo son tipos de datos adicionales que son compatibles con hello SDK. Los trataremos a continuación.

> [!NOTE]
> Centro de IoT hace referencia a un dispositivo envía tooit como de datos de toohello *eventos*, mientras que Hola lenguaje de modelado refiere tooit como *datos* (definido mediante **WITH_DATA**). Del mismo modo, centro de IoT hace referencia a datos toohello enviar toodevices como *mensajes*, mientras que Hola lenguaje de modelado refiere tooit como *acciones* (definido mediante **WITH_ACTION**). Tenga en cuenta que estos términos pueden usarse indistintamente en este artículo.
> 
> 

### <a name="supported-data-types"></a>Tipos de datos admitidos
Hola siguientes tipos de datos se admite en los modelos creados con hello **serializador** biblioteca:

| Tipo | Description |
| --- | --- |
| double |número de punto flotante de doble precisión |
| int |entero de 32 bits |
| float |número de punto flotante de precisión simple |
| long |entero largo |
| int8\_t |entero de 8 bits |
| int16\_t |entero de 16 bits |
| int32\_t |entero de 32 bits |
| int64\_t |entero de 64 bits |
| booleano |boolean |
| ascii\_char\_ptr |Cadena ASCII |
| EDM\_DATE\_TIME\_OFFSET |desplazamiento de fecha y hora |
| EDM\_GUID |GUID |
| EDM\_BINARY |binary |
| DECLARE\_STRUCT |tipo de dato complejo |

Comencemos con hello último tipo de datos. Hola **DECLARE\_STRUCT** permite tipos de datos complejos toodefine, que son agrupaciones de hello otros tipos primitivos. Estas agrupaciones nos permiten toodefine un modelo que el siguiente aspecto:

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

Nuestro modelo contiene un evento de datos único de tipo **TestType**. **TestType** es un tipo complejo que incluye varios miembros, que se muestran colectivamente tipos primitivos de hello admitidos por hello **serializador** lenguaje de modelado.

Con un modelo similar al siguiente, podemos escribir código toosend datos tooIoT concentrador que aparece como sigue:

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

Básicamente, asignamos un miembro de valor tooevery de hello **prueba** estructura y, a continuación, llamar a **SendAsync** toosend hello **prueba** datos evento toohello en la nube. **SendAsync** es una función auxiliar que envía un tooIoT de eventos de datos único concentrador:

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

Esta función serializa Hola determinado evento de datos y lo envía tooIoT concentrador mediante **IoTHubClient\_SendEventAsync**. Se trata de hello mismo código se describe en los artículos anteriores (**SendAsync** encapsula la lógica de hello en una función adecuada).

Es una otra función auxiliar que se utiliza en el código anterior hello **GetDateTimeOffset**. Esta función transforma Hola momento dado en un valor de tipo **EDM\_fecha\_tiempo\_desplazamiento**:

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

Si ejecuta este código, Hola siguiente mensaje se envía tooIoT concentrador:

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Tenga en cuenta que la serialización de hello es JSON, que es el formato de hello generado por hello **serializador** biblioteca. También tenga en cuenta que cada miembro de hello serializa el objeto JSON coincide con los miembros de Hola de hello **TestType** que hemos definido en nuestro modelo. valores de Hello también coinciden exactamente con los utiliza en el código de hello. Sin embargo, tenga en cuenta que los datos binarios de hello tiene una codificación base64: "AQID" es Hola codificación base64 de {0 x 01, 0 x 02, 0 x 03}.

Este ejemplo muestra la ventaja de Hola de usar hello **serializador** biblioteca--permite poner en la nube toosend JSON toohello, sin necesidad de tooexplicitly tratar con la serialización en nuestra aplicación. Todo lo que hay tooworry sobre es establecer valores de hello de hello eventos de datos en nuestro modelo y, a continuación, llamar a simple toosend API esos nube toohello de eventos.

Con esta información, podemos definir modelos, que incluyen el intervalo de Hola de tipos de datos compatibles, incluidos los tipos complejos (podríamos incluso incluimos tipos complejos dentro de otros tipos complejos). No obstante, serializa texto JSON generado por hello ejemplo anterior muestra un aspecto importante. *Cómo* enviamos datos con hello **serializador** biblioteca determina exactamente cómo se forma Hola JSON. Este punto en particular es de lo que hablaremos a continuación.

## <a name="more-about-serialization"></a>Más información sobre la serialización
sección anterior de Hello resalta un ejemplo de resultado de hello generado por hello **serializador** biblioteca. En esta sección, explicaremos cómo biblioteca Hola serializa los datos y cómo se puede controlar este comportamiento mediante la API de serialización de Hola.

En las conversaciones de Hola de orden tooadvance durante la serialización, trabajamos con un nuevo modelo basado en un termostato. En primer lugar, vamos a proporcionar cierta información general sobre el escenario de hello estamos intentando tooaddress.

Queremos toomodel un termostato que mide la temperatura y humedad. Cada elemento de datos va toobe enviado tooIoT concentrador de manera diferente. De forma predeterminada, Hola ingresses termostato un evento de temperatura una vez cada 2 minutos; un evento de humedad es ingressed una vez cada 15 minutos. Una vez ingressed cualquier evento, debe incluir una marca de tiempo que muestra el tiempo de hello esa temperatura correspondiente Hola o humedad medirla.

Con este escenario, podrá mostrar datos de dos maneras diferentes toomodel hello y explicaremos efecto Hola que modelado se en hello serializado salida.

### <a name="model-1"></a>Modelo 1
Aquí es Hola primera versión de un modelo que admite Hola escenario anterior:

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

Tenga en cuenta ese modelo Hola incluye dos eventos de datos: **temperatura** y **humedad**. A diferencia de los ejemplos anteriores, el tipo de Hola de cada evento es una estructura definida mediante **DECLARE\_STRUCT**. **TemperatureEvent** incluye una medida de la temperatura y una marca de tiempo; **HumidityEvent** contiene una medida de humedad y una marca de tiempo. Este modelo nos da una manera natural toomodel Hola de datos para el escenario de Hola que se ha descrito anteriormente. Cuando se envía una nube de toohello de eventos, ya sea te enviaremos una temperatura/marca de tiempo o un par de humedad/marca de tiempo.

Podemos enviarle una temperatura evento toohello en la nube mediante código como Hola siguiente:

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Se podrá utilizar valores codificados de forma rígida de temperatura y humedad en el código de ejemplo de Hola, pero suponga que estamos recuperando realmente estos valores mediante el muestreo de sensores correspondiente de hello en termostato Hola.

código de Hello anterior utiliza hello **GetDateTimeOffset** auxiliar que se introdujo previamente. Por motivos que se convertirá en claro posteriores, este código separa explícitamente tarea hello de serializar y enviar eventos de Hola. código de Hello anterior serializa el evento de temperatura de hello en un búfer. A continuación, **sendMessage** es una función auxiliar (incluido en **simplesample\_amqp**) que envía Hola tooIoT concentrador de eventos:

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

Este código es un subconjunto de hello **SendAsync** auxiliar que se describe en la sección anterior de hello, por lo que no entraremos sobre él nuevo aquí.

Al ejecutar el evento de temperatura para hello el anterior toosend código hello, este formulario serializado de evento Hola se envía tooIoT concentrador:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Vamos a enviar una temperatura que es de tipo **TemperatureEvent** y esa estructura contiene un miembro **Temperature** y **Time**. Esto se refleja directamente en datos Hola serializado.

Del mismo modo, podemos enviar un evento de humedad con este código:

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

formulario de Hello serializado que ha enviado tooIoT concentrador aparece como sigue:

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Nuevamente, es lo que se esperaba.

Con este modelo, puede imaginar lo fácil que se podrían agregar eventos adicionales. Definir estructuras más mediante **DECLARE\_STRUCT**e incluir el evento correspondiente de hello en hello modelo con **WITH\_datos**.

Ahora, vamos a modificar el modelo de Hola para que incluya Hola mismos datos, pero con una estructura diferente.

### <a name="model-2"></a>Modelo 2
Tenga en cuenta este toohello modelo alternativo uno anteriormente:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

En este caso hemos eliminado hello **DECLARE\_STRUCT** macros y simplemente está definiendo elementos de datos de Hola desde nuestro escenario utiliza tipos simples de hello lenguaje de modelado.

Solo para el momento de hello vamos a pasar por alto hello **tiempo** eventos. Con esa aside, mostramos Hola código tooingress **temperatura**:

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Este código, se envían siguiente Hola serializa tooIoT concentrador de eventos:

```
{"Temperature":75}
```

Y código de hello para el envío de eventos de humedad Hola aparezca como sigue:

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Este código envía este tooIoT concentrador:

```
{"Humidity":45}
```

Hasta ahora, no hay novedades. Ahora vamos a cambiar cómo utilizamos macro SERIALIZE de Hola.

Hola **SERIALIZE** macro puede tomar varios eventos de datos como argumentos. Esto nos permite hello tooserialize **temperatura** y **humedad** evento junto y enviar tooIoT concentrador en una llamada:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Se puede suponer que el resultado de hello de este código es que se envían eventos de datos de dos tooIoT concentrador:

[

{"Temperature":75},

{"Humidity":45}

]

En otras palabras, podría esperar que este código es Hola igual que enviar **temperatura** y **humedad** por separado. Es simplemente una toopass comodidad ambos eventos demasiado**SERIALIZE** Hola misma llamada. Sin embargo, no es el caso de hello. En su lugar, código de hello anterior envía este tooIoT de eventos de datos único concentrador:

{"Temperature":75, "Humidity":45}

Esto puede parecer extraño debido a que nuestro modelo define **Temperature** y **Humidity** como dos eventos *independientes*:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Punto de toohello más, se no modelar estos eventos donde **temperatura** y **humedad** están en hello misma estructura:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

Si se usa este modelo, sería más fácil toounderstand cómo **temperatura** y **humedad** se enviarían en hello mismo mensaje serializado. Sin embargo puede no estar claro por qué funciona de este modo al pasar ambos eventos de datos demasiado**SERIALIZE** con modelo 2.

Este comportamiento es más fácil toounderstand si sabe suposiciones Hola ese hello **serializador** biblioteca está realizando. sentido toomake de este volvamos atrás tooour modelo:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Considere este modelo en términos de orientación a objetos. En este caso, estamos modelando un dispositivo físico (un termostato) y ese dispositivo incluye atributos como **Temperature** y **Humidity**.

Podemos enviar un estado completo de Hola de nuestro modelo de código como Hola siguiente:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Suponiendo que se establecen valores de hello de temperatura y humedad, la hora, se vería un evento como este concentrador de tooIoT enviado:

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

En ocasiones, podría desear sólo toosend *algunos* propiedades de nube de hello modelo toohello (Esto es especialmente cierto si el modelo contiene un gran número de eventos de datos). Resulta útil toosend solo un subconjunto de eventos de datos, como en el ejemplo anterior:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Esto genera exactamente Hola mismo evento serializa como si hubiéramos definimos un **TemperatureEvent** con un **temperatura** y **tiempo** miembro, como se con 1 del modelo. En este caso hemos toogenerate pueda exactamente hello mismo eventos serializados mediante el uso de un modelo diferente (modelo 2) porque se llamó a **SERIALIZE** de forma diferente.

Hello importante es que si pasar varios eventos de datos demasiado**SERIALIZE,** , a continuación, se supone que cada evento es una propiedad en un único objeto JSON.

mejor método de Hello depende de y cómo pensar en el modelo. Si va a enviar "eventos" toohello en la nube y cada evento contiene un conjunto de propiedades definido, primer enfoque de hello hace mucho sentido. En ese caso utilizaría **DECLARE\_STRUCT** toodefine Hola estructura de cada evento y, a continuación, incluirlos en el modelo con hello **WITH\_datos** macro. A continuación, enviar cada evento como hicimos en hello primer ejemplo. En este enfoque solo pasaría un evento único datos demasiado**SERIALIZADOR**.

Si piensa sobre el modelo de una manera orientada a objetos, puede satisfacer segundo enfoque de Hola se. En este caso, Hola elementos definidos mediante **WITH\_datos** Hola "propiedades" del objeto. Pasar cualquier subconjunto de eventos demasiado**SERIALIZE** que le gusta, dependiendo de la cantidad de estado de "del objeto" desea toosend toohello en la nube.

Ningún enfoque es bueno ni malo. Solo debes tener en cuenta cómo hello **serializador** funciona de la biblioteca y un nuevo enfoque de modelado de Hola de selección que mejor se adapte a sus necesidades.

## <a name="message-handling"></a>Administración de mensajes
Hasta ahora en este artículo solo se han tratado el envío eventos tooIoT concentrador y no se ha resuelto recibir mensajes. Hola razón para que esto es lo que necesitamos tooknow acerca de la recepción de mensajes ha sido cubierto en gran medida en un [anteriormente artículo](iot-hub-device-sdk-c-intro.md). Como se explicaba en ese artículo, los mensajes se procesan mediante el registro de una función de devolución de llamada de mensaje:

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

A continuación, puede escribir la función de devolución de llamada de Hola que se invoca cuando se recibe un mensaje:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
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

Esta implementación de **IoTHubMessage** llamadas Hola función específica para cada acción en el modelo. Por ejemplo, si el modelo define esta acción:

```
WITH_ACTION(SetAirResistance, int, Position)
```

Debe definir una función con esta firma:

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** , a continuación, se llama cuando se envía ese mensaje tooyour dispositivo.

Aún se lo que no hemos explicado es qué versión de Hola serializado de aspecto del mensaje. ¿En otras palabras, si desea toosend una **SetAirResistance** dispositivo de tooyour de mensaje, lo que ese aspecto tiene?

Si va a enviar un dispositivo de tooa de mensaje, podría hacerlo a través de SDK del servicio Hola IoT de Azure. Todavía necesita tooknow qué cadena toosend tooinvoke una acción concreta. formato general de Hola para enviar un mensaje aparece como sigue:

```
{"Name" : "", "Parameters" : "" }
```

Va a enviar un objeto JSON serializado con dos propiedades: **nombre** es Hola nombre de acción de hello (mensaje) y **parámetros** contiene parámetros de Hola de esa acción.

Por ejemplo, tooinvoke **SetAirResistance** puede enviar este dispositivo de tooa mensaje:

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

nombre de la acción de Hello debe coincidir exactamente con una acción definida en el modelo. nombres de parámetro de Hello deben coincidir también. Tenga en cuenta que existe una distinción de mayúsculas y minúsculas. **Name** y **Parameters** van siempre en mayúsculas. Que el caso de hello toomatch seguro de su nombre de acción y los parámetros en el modelo. En este ejemplo, el nombre de la acción de hello es "SetAirResistance" y no "setairresistance".

Hola dos otras acciones **TurnFanOn** y **TurnFanOff** puede invocarse mediante el envío de estos dispositivos de tooa de mensajes:

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

En esta sección se describe todo lo que necesita tooknow cuando el envío de eventos y recibir mensajes con Hola **serializador** biblioteca. Antes de continuar, vamos a examinar algunos parámetros que puede configurar que controlan lo grande que es su modelo.

## <a name="macro-configuration"></a>Configuración de macros
Si usas hello **serializador** biblioteca una parte importante de hello SDK toobe en cuenta se encuentra en la biblioteca de azure-c-compartido-utilidad de Hola.
Si ha clonado repositorio hello Azure-iot-sdk-c desde GitHub con opción de hello--recursiva, encontrará esta biblioteca de utilidad compartida aquí:

```
.\\c-utility
```

Si no ha clonado biblioteca hello, lo encontrará [aquí](https://github.com/Azure/azure-c-shared-utility).

Biblioteca de utilidad compartida hello, encontrará Hola después de la carpeta:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Esta carpeta contiene una solución de Visual Studio denominada **macro\_utils\_h\_generator.sln**:

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

programa Hello en esta solución genera hello **macro\_utils.h** archivo. Hay una macro predeterminado\_archivo utils.h incluido con hello SDK. Esta solución permite toomodify algunos parámetros y, a continuación, vuelva a crear Hola basado en estos parámetros de archivo de encabezado.

Hola dos parámetros clave toobe preocupan son **nArithmetic** y **nMacroParameters** que se definen en estas dos líneas que se encuentra en la macro\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Estos valores son parámetros de hello predeterminados incluidos con hello SDK. Cada parámetro tiene Hola siguiente significado:

* nMacroParameters: controla el número de parámetros que puede tener en una definición de macro DECLARE\_MODEL.
* nArithmetic: número total de controles Hola de miembros permitidos en un modelo.

motivo de Hello que estos parámetros son importantes es porque controlan lo grande que puede ser el modelo. Por ejemplo, tenga en cuenta esta definición de modelo:

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Como se mencionó antes, **DECLARE\_MODEL** es simplemente una macro de C. Hola nombres de modelo de Hola y Hola **WITH\_datos** instrucción (todavía otra macro) es parámetros de **DECLARE\_modelo**. **nMacroParameters** define la cantidad de parámetros que puede incluirse en **DECLARE\_MODEL**. Esto permite definir de manera efectiva cuántas declaraciones de evento y acción puede tener. Por lo tanto, con el límite predeterminado de Hola de 124 Esto significa que puede definir un modelo con una combinación de aproximadamente 60 acciones y eventos de datos. Si intentas tooexceed este límite, recibirá errores de compilador que tengan un aspecto similar toothis:

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Hola **nArithmetic** parámetro es más sobre el funcionamiento interno de Hola de lenguaje de macros de hello de la aplicación.  Controla el número total de Hola de miembros que puede haber en el modelo, incluidos los **DECLARE_STRUCT** macros. Si comienza a ver errores del compilador como este, debería intentar aumentar el valor de **nArithmetic**:

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Si desea toochange estos parámetros, modifique los valores de hello en macro hello\_archivo utils.tt, recompile Hola macro\_utils\_h\_generator.sln solución y Hola ejecución el programa compilado. Al hacer esto, una macro nueva\_utils.h archivo generado y lo coloca en Hola.\\ Common\\directorio inc.

En la versión nuevo Hola de orden toouse de macro\_utils.h, remove hello **serializador** paquete de NuGet con la solución y, en su lugar incluir hello **serializador** proyecto de Visual Studio. Esto permite la toocompile código contra el código fuente de Hola de biblioteca de serializador de Hola. Esto incluye la macro Hola actualiza\_utils.h. Si desea toodo para **simplesample\_amqp**, iniciar mediante la eliminación de paquete de NuGet hello para la biblioteca de serializador de Hola de solución de hello:

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

A continuación, agregue esta solución de Visual Studio tooyour de proyecto:

> .\\c\\serializer\\build\\windows\\serializer.vcxproj
> 
> 

Cuando haya terminado, su solución debe tener este aspecto:

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Ahora cuando se compila la solución, hello actualizado macro\_utils.h se incluye en el archivo binario.

Tenga en cuenta que, si se aumentan estos valores mucho, se podrían exceder los límites del compilador. toothis punto, hello **nMacroParameters** es Hola parámetro principal con qué toobe que se trate. especificación de C99 Hola especifica que un mínimo de 127 parámetros se permiten en una definición de macro. Hello Microsoft compilador sigue la especificación de hello exactamente (y tiene un límite de 127), por lo que no será capaz de tooincrease **nMacroParameters** más allá del valor predeterminado de Hola. Otros compiladores le puede permitir toodo así (por ejemplo, compilador de GNU hello es compatible con un límite más alto).

Hasta ahora hemos cubierto casi todo lo que necesita tooknow acerca de cómo toowrite código con hello **serializador** biblioteca. Antes de concluir, vamos a revisar algunos temas de artículos anteriores sobre los que es posible que se esté preguntando.

## <a name="hello-lower-level-apis"></a>Hola las API de nivel inferior
aplicación de ejemplo de Hola en la que se centra en este artículo es **simplesample\_amqp**. Este ejemplo usa Hola eventos de nivel superior (hello no-"LL") las API toosend y recibir mensajes. Si usa estas API, se ejecuta un subproceso en segundo plano que se encarga de enviar eventos y recibir mensajes. Sin embargo, puede usar Hola nivel inferior (LL) API tooeliminate este subproceso en segundo plano y tener un control explícito al enviar eventos o recibir mensajes de la nube de Hola.

Como se describe en un [artículo anterior](iot-hub-device-sdk-c-iothubclient.md), hay un conjunto de funciones que consta de hello APIs de nivel superior:

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_Destroy

Estas API se muestran en **simplesample\_amqp**.

Hay un conjunto similar de API de nivel inferior.

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Tenga en cuenta que trabajo de las API de nivel inferior de Hola Hola exactamente como se describe en los artículos de hello anterior. Puede usar el primer conjunto de API de hello si desea que un toohandle de subproceso de fondo eventos de enviar y recibir mensajes. Use el segundo conjunto de API de hello si desea que un control explícito sobre al enviar y recibir datos desde el centro de IoT. Cualquier conjunto de trabajo de las API igualmente bien con hello **serializador** biblioteca.

Para obtener un ejemplo de cómo hello las API de nivel inferior se usan con hello **serializador** biblioteca, vea hello **simplesample\_http** aplicación.

## <a name="additional-topics"></a>Otros temas
Algunos otros temas que merece la pena mencionar de nuevo son el control de propiedades, el uso de credenciales de dispositivo alternativas y las opciones de configuración. Todos estos temas se trataron en un [artículo anterior](iot-hub-device-sdk-c-iothubclient.md). Hello punto más importante es que todas estas características funcionan en hello misma manera con hello **serializador** biblioteca como lo hacen con hello **IoTHubClient** biblioteca. Por ejemplo, si desea eventos tooan de tooattach propiedades del modelo, se utiliza **IoTHubMessage\_propiedades** y **mapa**\_**AddorUpdate**, Hola misma forma en que se ha descrito anteriormente:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Si generó un suceso Hola de hello **serializador** biblioteca o creados manualmente mediante hello **IoTHubClient** no importa la biblioteca.

Para hello alternar las credenciales del dispositivo, usando **IoTHubClient\_LL\_crear** funciona tan bien como **IoTHubClient\_CreateFromConnectionString** para asignar un **el centro de IOT\_cliente\_controlar**.

Por último, si usas hello **serializador** biblioteca, puede establecer opciones de configuración con **IoTHubClient\_LL\_SetOption** tal y como lo hizo cuando se usa hello **IoTHubClient** biblioteca.

Una característica que sea único toohello **serializador** library son inicialización Hola API. Para poder empezar a trabajar con la biblioteca de hello, debe llamar a **serializador\_init**:

```
serializer_init(NULL);
```

Esto se hace justo antes de llamar a **IoTHubClient\_CreateFromConnectionString**.

De forma similar, cuando haya acabado trabajar con la biblioteca de hello, última llamada de hello conseguirá que es demasiado**serializador\_deinit**:

```
serializer_deinit();
```

En caso contrario, Hola a todos los de otras funcionalidades enumeradas anteriormente trabajo mismo Hola Hola **serializador** biblioteca como lo hacen en hello **IoTHubClient** biblioteca. Para obtener más información acerca de cualquiera de estos temas, vea hello [artículo anterior](iot-hub-device-sdk-c-iothubclient.md) en esta serie.

## <a name="next-steps"></a>Pasos siguientes
Este artículo se describe en aspectos exclusivos de detalle Hola de hello **serializador** biblioteca contenido en hello **dispositivos de IoT de Azure SDK para C**. Con información de hello proporcionada debe tener una buena comprensión de cómo toouse modela toosend eventos y recibir mensajes desde centro de IoT.

Con esto concluye también serie de tres partes de hello en cómo las aplicaciones de toodevelop con Hola **dispositivos de IoT de Azure SDK para C**. Esto debe ser suficiente información toonot solo introducción pero ofrecerle una explicación exhaustiva sobre el funcionamiento de las API de Hola. Para obtener información adicional, hay algunos ejemplos en hello que SDK no se trata aquí. En caso contrario, Hola [documentación del SDK de](https://github.com/Azure/azure-iot-sdk-c) es un buen recurso para obtener información adicional.

toolearn más sobre el desarrollo de centro de IoT, vea hello [SDK de Azure IoT][lnk-sdks].

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

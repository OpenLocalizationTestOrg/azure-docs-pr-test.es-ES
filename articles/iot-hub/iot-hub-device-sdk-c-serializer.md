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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="36c86-103">SDK de dispositivo IoT de Azure para C: más información sobre el serializador</span><span class="sxs-lookup"><span data-stu-id="36c86-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="36c86-104">Hola [primero el artículo](iot-hub-device-sdk-c-intro.md) en este Hola serie introducida **dispositivos de IoT de Azure SDK para C**. artículo siguiente Hola proporciona una descripción más detallada de hello [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="36c86-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="36c86-105">En este artículo se completa cobertura de hello SDK al proporcionar una descripción más detallada de hello restantes componente: Hola **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="36c86-106">artículo introductorio Hola se describe cómo hello toouse **serializador** biblioteca toosend eventos tooand recibir mensajes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="36c86-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="36c86-107">En este artículo, se amplía esa discusión proporcionando una explicación más completa de cómo toomodel los datos con hello **serializador** lenguaje de macros.</span><span class="sxs-lookup"><span data-stu-id="36c86-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="36c86-108">artículo Hello también incluye información más detallada sobre cómo biblioteca Hola serializa los mensajes (y en algunos casos cómo se puede controlar un comportamiento de serialización hello).</span><span class="sxs-lookup"><span data-stu-id="36c86-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="36c86-109">Describiremos también puede modificar algunos parámetros que determinan el tamaño de Hola de modelos de Hola que haya creado.</span><span class="sxs-lookup"><span data-stu-id="36c86-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="36c86-110">Por último, artículo Hola repasa algunos temas que se tratan en los artículos anteriores como mensaje y control de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="36c86-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="36c86-111">Hola mismo utilizando hello como buscaremos el esas características, trabajar en **serializador** biblioteca como lo hacen con hello **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="36c86-112">Todo lo descrito en este artículo se basa en hello **serializador** ejemplos del SDK.</span><span class="sxs-lookup"><span data-stu-id="36c86-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="36c86-113">Si desea que toofollow a lo largo de, vea hello **simplesample\_amqp** y **simplesample\_http** aplicaciones incluidas en el SDK de dispositivos de IoT de Azure Hola de C.</span><span class="sxs-lookup"><span data-stu-id="36c86-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="36c86-114">Puede encontrar Hola [ **dispositivos de IoT de Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositorio y ver los detalles de la API de Hola Hola [referencia de la API de C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="36c86-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="36c86-115">lenguaje de modelado de Hola</span><span class="sxs-lookup"><span data-stu-id="36c86-115">hello modeling language</span></span>
<span data-ttu-id="36c86-116">Hola [artículo introductorio](iot-hub-device-sdk-c-intro.md) en este Hola serie introducida **dispositivos de IoT de Azure SDK para C** modeling language a través de ejemplo de Hola incluido en hello **simplesample\_amqp**  aplicación:</span><span class="sxs-lookup"><span data-stu-id="36c86-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="36c86-117">Como puede ver, Hola lenguaje de modelado se basa en las macros de C.</span><span class="sxs-lookup"><span data-stu-id="36c86-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="36c86-118">La definición comienza siempre con **BEGIN\_NAMESPACE** y termina siempre con **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="36c86-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="36c86-119">Es tooname Hola espacio de nombres común para su empresa o, como en este ejemplo, el proyecto de Hola que estás trabajando en.</span><span class="sxs-lookup"><span data-stu-id="36c86-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="36c86-120">¿Qué va en el interior de espacio de nombres de hello son definiciones de modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="36c86-121">En este caso, hay un único modelo para un anemómetro.</span><span class="sxs-lookup"><span data-stu-id="36c86-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="36c86-122">Una vez más, el modelo de hello puede tener cualquier nombre, pero normalmente se denomina para el dispositivo de Hola o un tipo de datos que desee tooexchange con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="36c86-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="36c86-123">Los modelos contienen una definición de eventos de hello puede entrada tooIoT concentrador (hello *datos*), así como mensajes de saludo puede recibir de centro de IoT (hello *acciones*).</span><span class="sxs-lookup"><span data-stu-id="36c86-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="36c86-124">Como puede ver en el ejemplo de Hola, los eventos tienen un tipo y un nombre; las acciones tienen un nombre y parámetros opcionales (cada uno con un tipo).</span><span class="sxs-lookup"><span data-stu-id="36c86-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="36c86-125">Lo que no se muestra en este ejemplo son tipos de datos adicionales que son compatibles con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="36c86-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="36c86-126">Los trataremos a continuación.</span><span class="sxs-lookup"><span data-stu-id="36c86-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="36c86-127">Centro de IoT hace referencia a un dispositivo envía tooit como de datos de toohello *eventos*, mientras que Hola lenguaje de modelado refiere tooit como *datos* (definido mediante **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="36c86-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="36c86-128">Del mismo modo, centro de IoT hace referencia a datos toohello enviar toodevices como *mensajes*, mientras que Hola lenguaje de modelado refiere tooit como *acciones* (definido mediante **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="36c86-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="36c86-129">Tenga en cuenta que estos términos pueden usarse indistintamente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="36c86-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="36c86-130">Tipos de datos admitidos</span><span class="sxs-lookup"><span data-stu-id="36c86-130">Supported data types</span></span>
<span data-ttu-id="36c86-131">Hola siguientes tipos de datos se admite en los modelos creados con hello **serializador** biblioteca:</span><span class="sxs-lookup"><span data-stu-id="36c86-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="36c86-132">Tipo</span><span class="sxs-lookup"><span data-stu-id="36c86-132">Type</span></span> | <span data-ttu-id="36c86-133">Description</span><span class="sxs-lookup"><span data-stu-id="36c86-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36c86-134">double</span><span class="sxs-lookup"><span data-stu-id="36c86-134">double</span></span> |<span data-ttu-id="36c86-135">número de punto flotante de doble precisión</span><span class="sxs-lookup"><span data-stu-id="36c86-135">double precision floating point number</span></span> |
| <span data-ttu-id="36c86-136">int</span><span class="sxs-lookup"><span data-stu-id="36c86-136">int</span></span> |<span data-ttu-id="36c86-137">entero de 32 bits</span><span class="sxs-lookup"><span data-stu-id="36c86-137">32 bit integer</span></span> |
| <span data-ttu-id="36c86-138">float</span><span class="sxs-lookup"><span data-stu-id="36c86-138">float</span></span> |<span data-ttu-id="36c86-139">número de punto flotante de precisión simple</span><span class="sxs-lookup"><span data-stu-id="36c86-139">single precision floating point number</span></span> |
| <span data-ttu-id="36c86-140">long</span><span class="sxs-lookup"><span data-stu-id="36c86-140">long</span></span> |<span data-ttu-id="36c86-141">entero largo</span><span class="sxs-lookup"><span data-stu-id="36c86-141">long integer</span></span> |
| <span data-ttu-id="36c86-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="36c86-142">int8\_t</span></span> |<span data-ttu-id="36c86-143">entero de 8 bits</span><span class="sxs-lookup"><span data-stu-id="36c86-143">8 bit integer</span></span> |
| <span data-ttu-id="36c86-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="36c86-144">int16\_t</span></span> |<span data-ttu-id="36c86-145">entero de 16 bits</span><span class="sxs-lookup"><span data-stu-id="36c86-145">16 bit integer</span></span> |
| <span data-ttu-id="36c86-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="36c86-146">int32\_t</span></span> |<span data-ttu-id="36c86-147">entero de 32 bits</span><span class="sxs-lookup"><span data-stu-id="36c86-147">32 bit integer</span></span> |
| <span data-ttu-id="36c86-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="36c86-148">int64\_t</span></span> |<span data-ttu-id="36c86-149">entero de 64 bits</span><span class="sxs-lookup"><span data-stu-id="36c86-149">64 bit integer</span></span> |
| <span data-ttu-id="36c86-150">booleano</span><span class="sxs-lookup"><span data-stu-id="36c86-150">bool</span></span> |<span data-ttu-id="36c86-151">boolean</span><span class="sxs-lookup"><span data-stu-id="36c86-151">boolean</span></span> |
| <span data-ttu-id="36c86-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="36c86-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="36c86-153">Cadena ASCII</span><span class="sxs-lookup"><span data-stu-id="36c86-153">ASCII string</span></span> |
| <span data-ttu-id="36c86-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="36c86-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="36c86-155">desplazamiento de fecha y hora</span><span class="sxs-lookup"><span data-stu-id="36c86-155">date time offset</span></span> |
| <span data-ttu-id="36c86-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="36c86-156">EDM\_GUID</span></span> |<span data-ttu-id="36c86-157">GUID</span><span class="sxs-lookup"><span data-stu-id="36c86-157">GUID</span></span> |
| <span data-ttu-id="36c86-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="36c86-158">EDM\_BINARY</span></span> |<span data-ttu-id="36c86-159">binary</span><span class="sxs-lookup"><span data-stu-id="36c86-159">binary</span></span> |
| <span data-ttu-id="36c86-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="36c86-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="36c86-161">tipo de dato complejo</span><span class="sxs-lookup"><span data-stu-id="36c86-161">complex data type</span></span> |

<span data-ttu-id="36c86-162">Comencemos con hello último tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="36c86-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="36c86-163">Hola **DECLARE\_STRUCT** permite tipos de datos complejos toodefine, que son agrupaciones de hello otros tipos primitivos.</span><span class="sxs-lookup"><span data-stu-id="36c86-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="36c86-164">Estas agrupaciones nos permiten toodefine un modelo que el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="36c86-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="36c86-165">Nuestro modelo contiene un evento de datos único de tipo **TestType**.</span><span class="sxs-lookup"><span data-stu-id="36c86-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="36c86-166">**TestType** es un tipo complejo que incluye varios miembros, que se muestran colectivamente tipos primitivos de hello admitidos por hello **serializador** lenguaje de modelado.</span><span class="sxs-lookup"><span data-stu-id="36c86-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="36c86-167">Con un modelo similar al siguiente, podemos escribir código toosend datos tooIoT concentrador que aparece como sigue:</span><span class="sxs-lookup"><span data-stu-id="36c86-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="36c86-168">Básicamente, asignamos un miembro de valor tooevery de hello **prueba** estructura y, a continuación, llamar a **SendAsync** toosend hello **prueba** datos evento toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="36c86-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="36c86-169">**SendAsync** es una función auxiliar que envía un tooIoT de eventos de datos único concentrador:</span><span class="sxs-lookup"><span data-stu-id="36c86-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

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

<span data-ttu-id="36c86-170">Esta función serializa Hola determinado evento de datos y lo envía tooIoT concentrador mediante **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="36c86-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="36c86-171">Se trata de hello mismo código se describe en los artículos anteriores (**SendAsync** encapsula la lógica de hello en una función adecuada).</span><span class="sxs-lookup"><span data-stu-id="36c86-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="36c86-172">Es una otra función auxiliar que se utiliza en el código anterior hello **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="36c86-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="36c86-173">Esta función transforma Hola momento dado en un valor de tipo **EDM\_fecha\_tiempo\_desplazamiento**:</span><span class="sxs-lookup"><span data-stu-id="36c86-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="36c86-174">Si ejecuta este código, Hola siguiente mensaje se envía tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="36c86-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="36c86-175">Tenga en cuenta que la serialización de hello es JSON, que es el formato de hello generado por hello **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="36c86-176">También tenga en cuenta que cada miembro de hello serializa el objeto JSON coincide con los miembros de Hola de hello **TestType** que hemos definido en nuestro modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="36c86-177">valores de Hello también coinciden exactamente con los utiliza en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="36c86-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="36c86-178">Sin embargo, tenga en cuenta que los datos binarios de hello tiene una codificación base64: "AQID" es Hola codificación base64 de {0 x 01, 0 x 02, 0 x 03}.</span><span class="sxs-lookup"><span data-stu-id="36c86-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="36c86-179">Este ejemplo muestra la ventaja de Hola de usar hello **serializador** biblioteca--permite poner en la nube toosend JSON toohello, sin necesidad de tooexplicitly tratar con la serialización en nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="36c86-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="36c86-180">Todo lo que hay tooworry sobre es establecer valores de hello de hello eventos de datos en nuestro modelo y, a continuación, llamar a simple toosend API esos nube toohello de eventos.</span><span class="sxs-lookup"><span data-stu-id="36c86-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="36c86-181">Con esta información, podemos definir modelos, que incluyen el intervalo de Hola de tipos de datos compatibles, incluidos los tipos complejos (podríamos incluso incluimos tipos complejos dentro de otros tipos complejos).</span><span class="sxs-lookup"><span data-stu-id="36c86-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="36c86-182">No obstante, serializa texto JSON generado por hello ejemplo anterior muestra un aspecto importante.</span><span class="sxs-lookup"><span data-stu-id="36c86-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="36c86-183">*Cómo* enviamos datos con hello **serializador** biblioteca determina exactamente cómo se forma Hola JSON.</span><span class="sxs-lookup"><span data-stu-id="36c86-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="36c86-184">Este punto en particular es de lo que hablaremos a continuación.</span><span class="sxs-lookup"><span data-stu-id="36c86-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="36c86-185">Más información sobre la serialización</span><span class="sxs-lookup"><span data-stu-id="36c86-185">More about serialization</span></span>
<span data-ttu-id="36c86-186">sección anterior de Hello resalta un ejemplo de resultado de hello generado por hello **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="36c86-187">En esta sección, explicaremos cómo biblioteca Hola serializa los datos y cómo se puede controlar este comportamiento mediante la API de serialización de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="36c86-188">En las conversaciones de Hola de orden tooadvance durante la serialización, trabajamos con un nuevo modelo basado en un termostato.</span><span class="sxs-lookup"><span data-stu-id="36c86-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="36c86-189">En primer lugar, vamos a proporcionar cierta información general sobre el escenario de hello estamos intentando tooaddress.</span><span class="sxs-lookup"><span data-stu-id="36c86-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="36c86-190">Queremos toomodel un termostato que mide la temperatura y humedad.</span><span class="sxs-lookup"><span data-stu-id="36c86-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="36c86-191">Cada elemento de datos va toobe enviado tooIoT concentrador de manera diferente.</span><span class="sxs-lookup"><span data-stu-id="36c86-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="36c86-192">De forma predeterminada, Hola ingresses termostato un evento de temperatura una vez cada 2 minutos; un evento de humedad es ingressed una vez cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="36c86-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="36c86-193">Una vez ingressed cualquier evento, debe incluir una marca de tiempo que muestra el tiempo de hello esa temperatura correspondiente Hola o humedad medirla.</span><span class="sxs-lookup"><span data-stu-id="36c86-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="36c86-194">Con este escenario, podrá mostrar datos de dos maneras diferentes toomodel hello y explicaremos efecto Hola que modelado se en hello serializado salida.</span><span class="sxs-lookup"><span data-stu-id="36c86-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="36c86-195">Modelo 1</span><span class="sxs-lookup"><span data-stu-id="36c86-195">Model 1</span></span>
<span data-ttu-id="36c86-196">Aquí es Hola primera versión de un modelo que admite Hola escenario anterior:</span><span class="sxs-lookup"><span data-stu-id="36c86-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="36c86-197">Tenga en cuenta ese modelo Hola incluye dos eventos de datos: **temperatura** y **humedad**.</span><span class="sxs-lookup"><span data-stu-id="36c86-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="36c86-198">A diferencia de los ejemplos anteriores, el tipo de Hola de cada evento es una estructura definida mediante **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="36c86-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="36c86-199">**TemperatureEvent** incluye una medida de la temperatura y una marca de tiempo; **HumidityEvent** contiene una medida de humedad y una marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="36c86-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="36c86-200">Este modelo nos da una manera natural toomodel Hola de datos para el escenario de Hola que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="36c86-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="36c86-201">Cuando se envía una nube de toohello de eventos, ya sea te enviaremos una temperatura/marca de tiempo o un par de humedad/marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="36c86-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="36c86-202">Podemos enviarle una temperatura evento toohello en la nube mediante código como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="36c86-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="36c86-203">Se podrá utilizar valores codificados de forma rígida de temperatura y humedad en el código de ejemplo de Hola, pero suponga que estamos recuperando realmente estos valores mediante el muestreo de sensores correspondiente de hello en termostato Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="36c86-204">código de Hello anterior utiliza hello **GetDateTimeOffset** auxiliar que se introdujo previamente.</span><span class="sxs-lookup"><span data-stu-id="36c86-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="36c86-205">Por motivos que se convertirá en claro posteriores, este código separa explícitamente tarea hello de serializar y enviar eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="36c86-206">código de Hello anterior serializa el evento de temperatura de hello en un búfer.</span><span class="sxs-lookup"><span data-stu-id="36c86-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="36c86-207">A continuación, **sendMessage** es una función auxiliar (incluido en **simplesample\_amqp**) que envía Hola tooIoT concentrador de eventos:</span><span class="sxs-lookup"><span data-stu-id="36c86-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="36c86-208">Este código es un subconjunto de hello **SendAsync** auxiliar que se describe en la sección anterior de hello, por lo que no entraremos sobre él nuevo aquí.</span><span class="sxs-lookup"><span data-stu-id="36c86-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="36c86-209">Al ejecutar el evento de temperatura para hello el anterior toosend código hello, este formulario serializado de evento Hola se envía tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="36c86-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="36c86-210">Vamos a enviar una temperatura que es de tipo **TemperatureEvent** y esa estructura contiene un miembro **Temperature** y **Time**.</span><span class="sxs-lookup"><span data-stu-id="36c86-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="36c86-211">Esto se refleja directamente en datos Hola serializado.</span><span class="sxs-lookup"><span data-stu-id="36c86-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="36c86-212">Del mismo modo, podemos enviar un evento de humedad con este código:</span><span class="sxs-lookup"><span data-stu-id="36c86-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="36c86-213">formulario de Hello serializado que ha enviado tooIoT concentrador aparece como sigue:</span><span class="sxs-lookup"><span data-stu-id="36c86-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="36c86-214">Nuevamente, es lo que se esperaba.</span><span class="sxs-lookup"><span data-stu-id="36c86-214">Again, this is as expected.</span></span>

<span data-ttu-id="36c86-215">Con este modelo, puede imaginar lo fácil que se podrían agregar eventos adicionales.</span><span class="sxs-lookup"><span data-stu-id="36c86-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="36c86-216">Definir estructuras más mediante **DECLARE\_STRUCT**e incluir el evento correspondiente de hello en hello modelo con **WITH\_datos**.</span><span class="sxs-lookup"><span data-stu-id="36c86-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="36c86-217">Ahora, vamos a modificar el modelo de Hola para que incluya Hola mismos datos, pero con una estructura diferente.</span><span class="sxs-lookup"><span data-stu-id="36c86-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="36c86-218">Modelo 2</span><span class="sxs-lookup"><span data-stu-id="36c86-218">Model 2</span></span>
<span data-ttu-id="36c86-219">Tenga en cuenta este toohello modelo alternativo uno anteriormente:</span><span class="sxs-lookup"><span data-stu-id="36c86-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="36c86-220">En este caso hemos eliminado hello **DECLARE\_STRUCT** macros y simplemente está definiendo elementos de datos de Hola desde nuestro escenario utiliza tipos simples de hello lenguaje de modelado.</span><span class="sxs-lookup"><span data-stu-id="36c86-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="36c86-221">Solo para el momento de hello vamos a pasar por alto hello **tiempo** eventos.</span><span class="sxs-lookup"><span data-stu-id="36c86-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="36c86-222">Con esa aside, mostramos Hola código tooingress **temperatura**:</span><span class="sxs-lookup"><span data-stu-id="36c86-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="36c86-223">Este código, se envían siguiente Hola serializa tooIoT concentrador de eventos:</span><span class="sxs-lookup"><span data-stu-id="36c86-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="36c86-224">Y código de hello para el envío de eventos de humedad Hola aparezca como sigue:</span><span class="sxs-lookup"><span data-stu-id="36c86-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="36c86-225">Este código envía este tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="36c86-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="36c86-226">Hasta ahora, no hay novedades.</span><span class="sxs-lookup"><span data-stu-id="36c86-226">So far there are still no surprises.</span></span> <span data-ttu-id="36c86-227">Ahora vamos a cambiar cómo utilizamos macro SERIALIZE de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="36c86-228">Hola **SERIALIZE** macro puede tomar varios eventos de datos como argumentos.</span><span class="sxs-lookup"><span data-stu-id="36c86-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="36c86-229">Esto nos permite hello tooserialize **temperatura** y **humedad** evento junto y enviar tooIoT concentrador en una llamada:</span><span class="sxs-lookup"><span data-stu-id="36c86-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="36c86-230">Se puede suponer que el resultado de hello de este código es que se envían eventos de datos de dos tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="36c86-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="36c86-231">[</span><span class="sxs-lookup"><span data-stu-id="36c86-231">[</span></span>

<span data-ttu-id="36c86-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="36c86-232">{"Temperature":75},</span></span>

<span data-ttu-id="36c86-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="36c86-233">{"Humidity":45}</span></span>

<span data-ttu-id="36c86-234">]</span><span class="sxs-lookup"><span data-stu-id="36c86-234">]</span></span>

<span data-ttu-id="36c86-235">En otras palabras, podría esperar que este código es Hola igual que enviar **temperatura** y **humedad** por separado.</span><span class="sxs-lookup"><span data-stu-id="36c86-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="36c86-236">Es simplemente una toopass comodidad ambos eventos demasiado**SERIALIZE** Hola misma llamada.</span><span class="sxs-lookup"><span data-stu-id="36c86-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="36c86-237">Sin embargo, no es el caso de hello.</span><span class="sxs-lookup"><span data-stu-id="36c86-237">However, that’s not hello case.</span></span> <span data-ttu-id="36c86-238">En su lugar, código de hello anterior envía este tooIoT de eventos de datos único concentrador:</span><span class="sxs-lookup"><span data-stu-id="36c86-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="36c86-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="36c86-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="36c86-240">Esto puede parecer extraño debido a que nuestro modelo define **Temperature** y **Humidity** como dos eventos *independientes*:</span><span class="sxs-lookup"><span data-stu-id="36c86-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="36c86-241">Punto de toohello más, se no modelar estos eventos donde **temperatura** y **humedad** están en hello misma estructura:</span><span class="sxs-lookup"><span data-stu-id="36c86-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="36c86-242">Si se usa este modelo, sería más fácil toounderstand cómo **temperatura** y **humedad** se enviarían en hello mismo mensaje serializado.</span><span class="sxs-lookup"><span data-stu-id="36c86-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="36c86-243">Sin embargo puede no estar claro por qué funciona de este modo al pasar ambos eventos de datos demasiado**SERIALIZE** con modelo 2.</span><span class="sxs-lookup"><span data-stu-id="36c86-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="36c86-244">Este comportamiento es más fácil toounderstand si sabe suposiciones Hola ese hello **serializador** biblioteca está realizando.</span><span class="sxs-lookup"><span data-stu-id="36c86-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="36c86-245">sentido toomake de este volvamos atrás tooour modelo:</span><span class="sxs-lookup"><span data-stu-id="36c86-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="36c86-246">Considere este modelo en términos de orientación a objetos.</span><span class="sxs-lookup"><span data-stu-id="36c86-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="36c86-247">En este caso, estamos modelando un dispositivo físico (un termostato) y ese dispositivo incluye atributos como **Temperature** y **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="36c86-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="36c86-248">Podemos enviar un estado completo de Hola de nuestro modelo de código como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="36c86-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="36c86-249">Suponiendo que se establecen valores de hello de temperatura y humedad, la hora, se vería un evento como este concentrador de tooIoT enviado:</span><span class="sxs-lookup"><span data-stu-id="36c86-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="36c86-250">En ocasiones, podría desear sólo toosend *algunos* propiedades de nube de hello modelo toohello (Esto es especialmente cierto si el modelo contiene un gran número de eventos de datos).</span><span class="sxs-lookup"><span data-stu-id="36c86-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="36c86-251">Resulta útil toosend solo un subconjunto de eventos de datos, como en el ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="36c86-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="36c86-252">Esto genera exactamente Hola mismo evento serializa como si hubiéramos definimos un **TemperatureEvent** con un **temperatura** y **tiempo** miembro, como se con 1 del modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="36c86-253">En este caso hemos toogenerate pueda exactamente hello mismo eventos serializados mediante el uso de un modelo diferente (modelo 2) porque se llamó a **SERIALIZE** de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="36c86-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="36c86-254">Hello importante es que si pasar varios eventos de datos demasiado**SERIALIZE,** , a continuación, se supone que cada evento es una propiedad en un único objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="36c86-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="36c86-255">mejor método de Hello depende de y cómo pensar en el modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="36c86-256">Si va a enviar "eventos" toohello en la nube y cada evento contiene un conjunto de propiedades definido, primer enfoque de hello hace mucho sentido.</span><span class="sxs-lookup"><span data-stu-id="36c86-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="36c86-257">En ese caso utilizaría **DECLARE\_STRUCT** toodefine Hola estructura de cada evento y, a continuación, incluirlos en el modelo con hello **WITH\_datos** macro.</span><span class="sxs-lookup"><span data-stu-id="36c86-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="36c86-258">A continuación, enviar cada evento como hicimos en hello primer ejemplo.</span><span class="sxs-lookup"><span data-stu-id="36c86-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="36c86-259">En este enfoque solo pasaría un evento único datos demasiado**SERIALIZADOR**.</span><span class="sxs-lookup"><span data-stu-id="36c86-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="36c86-260">Si piensa sobre el modelo de una manera orientada a objetos, puede satisfacer segundo enfoque de Hola se.</span><span class="sxs-lookup"><span data-stu-id="36c86-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="36c86-261">En este caso, Hola elementos definidos mediante **WITH\_datos** Hola "propiedades" del objeto.</span><span class="sxs-lookup"><span data-stu-id="36c86-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="36c86-262">Pasar cualquier subconjunto de eventos demasiado**SERIALIZE** que le gusta, dependiendo de la cantidad de estado de "del objeto" desea toosend toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="36c86-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="36c86-263">Ningún enfoque es bueno ni malo.</span><span class="sxs-lookup"><span data-stu-id="36c86-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="36c86-264">Solo debes tener en cuenta cómo hello **serializador** funciona de la biblioteca y un nuevo enfoque de modelado de Hola de selección que mejor se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="36c86-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="36c86-265">Administración de mensajes</span><span class="sxs-lookup"><span data-stu-id="36c86-265">Message handling</span></span>
<span data-ttu-id="36c86-266">Hasta ahora en este artículo solo se han tratado el envío eventos tooIoT concentrador y no se ha resuelto recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="36c86-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="36c86-267">Hola razón para que esto es lo que necesitamos tooknow acerca de la recepción de mensajes ha sido cubierto en gran medida en un [anteriormente artículo](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="36c86-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="36c86-268">Como se explicaba en ese artículo, los mensajes se procesan mediante el registro de una función de devolución de llamada de mensaje:</span><span class="sxs-lookup"><span data-stu-id="36c86-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="36c86-269">A continuación, puede escribir la función de devolución de llamada de Hola que se invoca cuando se recibe un mensaje:</span><span class="sxs-lookup"><span data-stu-id="36c86-269">You then write hello callback function that’s invoked when a message is received:</span></span>

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

<span data-ttu-id="36c86-270">Esta implementación de **IoTHubMessage** llamadas Hola función específica para cada acción en el modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="36c86-271">Por ejemplo, si el modelo define esta acción:</span><span class="sxs-lookup"><span data-stu-id="36c86-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="36c86-272">Debe definir una función con esta firma:</span><span class="sxs-lookup"><span data-stu-id="36c86-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="36c86-273">**SetAirResistance** , a continuación, se llama cuando se envía ese mensaje tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="36c86-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="36c86-274">Aún se lo que no hemos explicado es qué versión de Hola serializado de aspecto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="36c86-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="36c86-275">¿En otras palabras, si desea toosend una **SetAirResistance** dispositivo de tooyour de mensaje, lo que ese aspecto tiene?</span><span class="sxs-lookup"><span data-stu-id="36c86-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="36c86-276">Si va a enviar un dispositivo de tooa de mensaje, podría hacerlo a través de SDK del servicio Hola IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="36c86-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="36c86-277">Todavía necesita tooknow qué cadena toosend tooinvoke una acción concreta.</span><span class="sxs-lookup"><span data-stu-id="36c86-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="36c86-278">formato general de Hola para enviar un mensaje aparece como sigue:</span><span class="sxs-lookup"><span data-stu-id="36c86-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="36c86-279">Va a enviar un objeto JSON serializado con dos propiedades: **nombre** es Hola nombre de acción de hello (mensaje) y **parámetros** contiene parámetros de Hola de esa acción.</span><span class="sxs-lookup"><span data-stu-id="36c86-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="36c86-280">Por ejemplo, tooinvoke **SetAirResistance** puede enviar este dispositivo de tooa mensaje:</span><span class="sxs-lookup"><span data-stu-id="36c86-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="36c86-281">nombre de la acción de Hello debe coincidir exactamente con una acción definida en el modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="36c86-282">nombres de parámetro de Hello deben coincidir también.</span><span class="sxs-lookup"><span data-stu-id="36c86-282">hello parameter names must match as well.</span></span> <span data-ttu-id="36c86-283">Tenga en cuenta que existe una distinción de mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="36c86-283">Also note case sensitivity.</span></span> <span data-ttu-id="36c86-284">**Name** y **Parameters** van siempre en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="36c86-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="36c86-285">Que el caso de hello toomatch seguro de su nombre de acción y los parámetros en el modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="36c86-286">En este ejemplo, el nombre de la acción de hello es "SetAirResistance" y no "setairresistance".</span><span class="sxs-lookup"><span data-stu-id="36c86-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="36c86-287">Hola dos otras acciones **TurnFanOn** y **TurnFanOff** puede invocarse mediante el envío de estos dispositivos de tooa de mensajes:</span><span class="sxs-lookup"><span data-stu-id="36c86-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="36c86-288">En esta sección se describe todo lo que necesita tooknow cuando el envío de eventos y recibir mensajes con Hola **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="36c86-289">Antes de continuar, vamos a examinar algunos parámetros que puede configurar que controlan lo grande que es su modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="36c86-290">Configuración de macros</span><span class="sxs-lookup"><span data-stu-id="36c86-290">Macro configuration</span></span>
<span data-ttu-id="36c86-291">Si usas hello **serializador** biblioteca una parte importante de hello SDK toobe en cuenta se encuentra en la biblioteca de azure-c-compartido-utilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="36c86-292">Si ha clonado repositorio hello Azure-iot-sdk-c desde GitHub con opción de hello--recursiva, encontrará esta biblioteca de utilidad compartida aquí:</span><span class="sxs-lookup"><span data-stu-id="36c86-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="36c86-293">Si no ha clonado biblioteca hello, lo encontrará [aquí](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="36c86-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="36c86-294">Biblioteca de utilidad compartida hello, encontrará Hola después de la carpeta:</span><span class="sxs-lookup"><span data-stu-id="36c86-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="36c86-295">Esta carpeta contiene una solución de Visual Studio denominada **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="36c86-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="36c86-296">programa Hello en esta solución genera hello **macro\_utils.h** archivo.</span><span class="sxs-lookup"><span data-stu-id="36c86-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="36c86-297">Hay una macro predeterminado\_archivo utils.h incluido con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="36c86-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="36c86-298">Esta solución permite toomodify algunos parámetros y, a continuación, vuelva a crear Hola basado en estos parámetros de archivo de encabezado.</span><span class="sxs-lookup"><span data-stu-id="36c86-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="36c86-299">Hola dos parámetros clave toobe preocupan son **nArithmetic** y **nMacroParameters** que se definen en estas dos líneas que se encuentra en la macro\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="36c86-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="36c86-300">Estos valores son parámetros de hello predeterminados incluidos con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="36c86-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="36c86-301">Cada parámetro tiene Hola siguiente significado:</span><span class="sxs-lookup"><span data-stu-id="36c86-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="36c86-302">nMacroParameters: controla el número de parámetros que puede tener en una definición de macro DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="36c86-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="36c86-303">nArithmetic: número total de controles Hola de miembros permitidos en un modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="36c86-304">motivo de Hello que estos parámetros son importantes es porque controlan lo grande que puede ser el modelo.</span><span class="sxs-lookup"><span data-stu-id="36c86-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="36c86-305">Por ejemplo, tenga en cuenta esta definición de modelo:</span><span class="sxs-lookup"><span data-stu-id="36c86-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="36c86-306">Como se mencionó antes, **DECLARE\_MODEL** es simplemente una macro de C.</span><span class="sxs-lookup"><span data-stu-id="36c86-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="36c86-307">Hola nombres de modelo de Hola y Hola **WITH\_datos** instrucción (todavía otra macro) es parámetros de **DECLARE\_modelo**.</span><span class="sxs-lookup"><span data-stu-id="36c86-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="36c86-308">**nMacroParameters** define la cantidad de parámetros que puede incluirse en **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="36c86-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="36c86-309">Esto permite definir de manera efectiva cuántas declaraciones de evento y acción puede tener.</span><span class="sxs-lookup"><span data-stu-id="36c86-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="36c86-310">Por lo tanto, con el límite predeterminado de Hola de 124 Esto significa que puede definir un modelo con una combinación de aproximadamente 60 acciones y eventos de datos.</span><span class="sxs-lookup"><span data-stu-id="36c86-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="36c86-311">Si intentas tooexceed este límite, recibirá errores de compilador que tengan un aspecto similar toothis:</span><span class="sxs-lookup"><span data-stu-id="36c86-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="36c86-312">Hola **nArithmetic** parámetro es más sobre el funcionamiento interno de Hola de lenguaje de macros de hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="36c86-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="36c86-313">Controla el número total de Hola de miembros que puede haber en el modelo, incluidos los **DECLARE_STRUCT** macros.</span><span class="sxs-lookup"><span data-stu-id="36c86-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="36c86-314">Si comienza a ver errores del compilador como este, debería intentar aumentar el valor de **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="36c86-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="36c86-315">Si desea toochange estos parámetros, modifique los valores de hello en macro hello\_archivo utils.tt, recompile Hola macro\_utils\_h\_generator.sln solución y Hola ejecución el programa compilado.</span><span class="sxs-lookup"><span data-stu-id="36c86-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="36c86-316">Al hacer esto, una macro nueva\_utils.h archivo generado y lo coloca en Hola.\\ Common\\directorio inc.</span><span class="sxs-lookup"><span data-stu-id="36c86-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="36c86-317">En la versión nuevo Hola de orden toouse de macro\_utils.h, remove hello **serializador** paquete de NuGet con la solución y, en su lugar incluir hello **serializador** proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36c86-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="36c86-318">Esto permite la toocompile código contra el código fuente de Hola de biblioteca de serializador de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="36c86-319">Esto incluye la macro Hola actualiza\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="36c86-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="36c86-320">Si desea toodo para **simplesample\_amqp**, iniciar mediante la eliminación de paquete de NuGet hello para la biblioteca de serializador de Hola de solución de hello:</span><span class="sxs-lookup"><span data-stu-id="36c86-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="36c86-321">A continuación, agregue esta solución de Visual Studio tooyour de proyecto:</span><span class="sxs-lookup"><span data-stu-id="36c86-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="36c86-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="36c86-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="36c86-323">Cuando haya terminado, su solución debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="36c86-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="36c86-324">Ahora cuando se compila la solución, hello actualizado macro\_utils.h se incluye en el archivo binario.</span><span class="sxs-lookup"><span data-stu-id="36c86-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="36c86-325">Tenga en cuenta que, si se aumentan estos valores mucho, se podrían exceder los límites del compilador.</span><span class="sxs-lookup"><span data-stu-id="36c86-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="36c86-326">toothis punto, hello **nMacroParameters** es Hola parámetro principal con qué toobe que se trate.</span><span class="sxs-lookup"><span data-stu-id="36c86-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="36c86-327">especificación de C99 Hola especifica que un mínimo de 127 parámetros se permiten en una definición de macro.</span><span class="sxs-lookup"><span data-stu-id="36c86-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="36c86-328">Hello Microsoft compilador sigue la especificación de hello exactamente (y tiene un límite de 127), por lo que no será capaz de tooincrease **nMacroParameters** más allá del valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="36c86-329">Otros compiladores le puede permitir toodo así (por ejemplo, compilador de GNU hello es compatible con un límite más alto).</span><span class="sxs-lookup"><span data-stu-id="36c86-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="36c86-330">Hasta ahora hemos cubierto casi todo lo que necesita tooknow acerca de cómo toowrite código con hello **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="36c86-331">Antes de concluir, vamos a revisar algunos temas de artículos anteriores sobre los que es posible que se esté preguntando.</span><span class="sxs-lookup"><span data-stu-id="36c86-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="36c86-332">Hola las API de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="36c86-332">hello lower-level APIs</span></span>
<span data-ttu-id="36c86-333">aplicación de ejemplo de Hola en la que se centra en este artículo es **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="36c86-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="36c86-334">Este ejemplo usa Hola eventos de nivel superior (hello no-"LL") las API toosend y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="36c86-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="36c86-335">Si usa estas API, se ejecuta un subproceso en segundo plano que se encarga de enviar eventos y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="36c86-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="36c86-336">Sin embargo, puede usar Hola nivel inferior (LL) API tooeliminate este subproceso en segundo plano y tener un control explícito al enviar eventos o recibir mensajes de la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="36c86-337">Como se describe en un [artículo anterior](iot-hub-device-sdk-c-iothubclient.md), hay un conjunto de funciones que consta de hello APIs de nivel superior:</span><span class="sxs-lookup"><span data-stu-id="36c86-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="36c86-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="36c86-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="36c86-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="36c86-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="36c86-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="36c86-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="36c86-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="36c86-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="36c86-342">Estas API se muestran en **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="36c86-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="36c86-343">Hay un conjunto similar de API de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="36c86-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="36c86-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="36c86-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="36c86-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="36c86-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="36c86-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="36c86-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="36c86-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="36c86-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="36c86-348">Tenga en cuenta que trabajo de las API de nivel inferior de Hola Hola exactamente como se describe en los artículos de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="36c86-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="36c86-349">Puede usar el primer conjunto de API de hello si desea que un toohandle de subproceso de fondo eventos de enviar y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="36c86-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="36c86-350">Use el segundo conjunto de API de hello si desea que un control explícito sobre al enviar y recibir datos desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="36c86-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="36c86-351">Cualquier conjunto de trabajo de las API igualmente bien con hello **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="36c86-352">Para obtener un ejemplo de cómo hello las API de nivel inferior se usan con hello **serializador** biblioteca, vea hello **simplesample\_http** aplicación.</span><span class="sxs-lookup"><span data-stu-id="36c86-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="36c86-353">Otros temas</span><span class="sxs-lookup"><span data-stu-id="36c86-353">Additional topics</span></span>
<span data-ttu-id="36c86-354">Algunos otros temas que merece la pena mencionar de nuevo son el control de propiedades, el uso de credenciales de dispositivo alternativas y las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="36c86-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="36c86-355">Todos estos temas se trataron en un [artículo anterior](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="36c86-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="36c86-356">Hello punto más importante es que todas estas características funcionan en hello misma manera con hello **serializador** biblioteca como lo hacen con hello **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="36c86-357">Por ejemplo, si desea eventos tooan de tooattach propiedades del modelo, se utiliza **IoTHubMessage\_propiedades** y **mapa**\_**AddorUpdate**, Hola misma forma en que se ha descrito anteriormente:</span><span class="sxs-lookup"><span data-stu-id="36c86-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="36c86-358">Si generó un suceso Hola de hello **serializador** biblioteca o creados manualmente mediante hello **IoTHubClient** no importa la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="36c86-359">Para hello alternar las credenciales del dispositivo, usando **IoTHubClient\_LL\_crear** funciona tan bien como **IoTHubClient\_CreateFromConnectionString** para asignar un **el centro de IOT\_cliente\_controlar**.</span><span class="sxs-lookup"><span data-stu-id="36c86-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="36c86-360">Por último, si usas hello **serializador** biblioteca, puede establecer opciones de configuración con **IoTHubClient\_LL\_SetOption** tal y como lo hizo cuando se usa hello **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="36c86-361">Una característica que sea único toohello **serializador** library son inicialización Hola API.</span><span class="sxs-lookup"><span data-stu-id="36c86-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="36c86-362">Para poder empezar a trabajar con la biblioteca de hello, debe llamar a **serializador\_init**:</span><span class="sxs-lookup"><span data-stu-id="36c86-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="36c86-363">Esto se hace justo antes de llamar a **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="36c86-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="36c86-364">De forma similar, cuando haya acabado trabajar con la biblioteca de hello, última llamada de hello conseguirá que es demasiado**serializador\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="36c86-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="36c86-365">En caso contrario, Hola a todos los de otras funcionalidades enumeradas anteriormente trabajo mismo Hola Hola **serializador** biblioteca como lo hacen en hello **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="36c86-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="36c86-366">Para obtener más información acerca de cualquiera de estos temas, vea hello [artículo anterior](iot-hub-device-sdk-c-iothubclient.md) en esta serie.</span><span class="sxs-lookup"><span data-stu-id="36c86-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36c86-367">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="36c86-367">Next steps</span></span>
<span data-ttu-id="36c86-368">Este artículo se describe en aspectos exclusivos de detalle Hola de hello **serializador** biblioteca contenido en hello **dispositivos de IoT de Azure SDK para C**. Con información de hello proporcionada debe tener una buena comprensión de cómo toouse modela toosend eventos y recibir mensajes desde centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="36c86-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="36c86-369">Con esto concluye también serie de tres partes de hello en cómo las aplicaciones de toodevelop con Hola **dispositivos de IoT de Azure SDK para C**. Esto debe ser suficiente información toonot solo introducción pero ofrecerle una explicación exhaustiva sobre el funcionamiento de las API de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c86-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="36c86-370">Para obtener información adicional, hay algunos ejemplos en hello que SDK no se trata aquí.</span><span class="sxs-lookup"><span data-stu-id="36c86-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="36c86-371">En caso contrario, Hola [documentación del SDK de](https://github.com/Azure/azure-iot-sdk-c) es un buen recurso para obtener información adicional.</span><span class="sxs-lookup"><span data-stu-id="36c86-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="36c86-372">toolearn más sobre el desarrollo de centro de IoT, vea hello [SDK de Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="36c86-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="36c86-373">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="36c86-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="36c86-374">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="36c86-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

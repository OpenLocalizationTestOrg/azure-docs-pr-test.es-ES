---
title: 'SDK de dispositivo IoT de Azure para C: serializador | Microsoft Docs'
description: "Describe cómo usar la biblioteca de serializador del SDK de dispositivo IoT de Azure para C con el fin de crear aplicaciones para dispositivos que se comunican con un centro de IoT Hub."
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
ms.openlocfilehash: aa03c29c54d75538b1fdf987cac5f09d5d344f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="af298-103">SDK de dispositivo IoT de Azure para C: más información sobre el serializador</span><span class="sxs-lookup"><span data-stu-id="af298-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="af298-104">En el [primer el artículo](iot-hub-device-sdk-c-intro.md) de esta serie se presentaba el **SDK de dispositivo IoT de Azure**. A este le siguió un artículo que proporcionaba una descripción más detallada de [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="af298-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="af298-105">En este artículo terminaremos de analizar el SDK y proporcionaremos una descripción más detallada del componente que queda: la biblioteca de **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="af298-106">En el artículo de introducción se describía cómo usar la biblioteca de **serializador** para enviar eventos al Centro de IoT y recibir mensajes de él.</span><span class="sxs-lookup"><span data-stu-id="af298-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="af298-107">En este artículo ampliaremos esta discusión con una explicación más completa de cómo modelar los datos con el macrolenguaje de **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="af298-108">También incluiremos en él más detalles sobre cómo la biblioteca serializa los mensajes (y, en algunos casos, cómo se puede controlar el comportamiento de serialización).</span><span class="sxs-lookup"><span data-stu-id="af298-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="af298-109">Asimismo, describiremos algunos parámetros que se pueden modificar que determinan el tamaño de los modelos que se crean.</span><span class="sxs-lookup"><span data-stu-id="af298-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="af298-110">Terminaremos examinando de nuevo algunos de los temas tratados en artículos anteriores, como el control de los mensajes y las propiedades.</span><span class="sxs-lookup"><span data-stu-id="af298-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="af298-111">Como veremos, estas características funcionan del mismo modo con la biblioteca de **serializador** que con la biblioteca de **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="af298-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="af298-112">Todo lo que se describe en este artículo se basa en los ejemplos del SDK del **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="af298-113">Si desea continuar, consulte las aplicaciones **simplesample\_amqp** y **simplesample\_http** que se incluyen en el SDK de dispositivo IoT de Azure para C.</span><span class="sxs-lookup"><span data-stu-id="af298-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="af298-114">Puede encontrar el [**SDK de dispositivo IoT de Azure para C**](https://github.com/Azure/azure-iot-sdk-c) en el repositorio de GitHub y ver los detalles de la API en la [referencia de la API de C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="af298-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="af298-115">El lenguaje de modelado</span><span class="sxs-lookup"><span data-stu-id="af298-115">The modeling language</span></span>
<span data-ttu-id="af298-116">En el [artículo de introducción](iot-hub-device-sdk-c-intro.md) de esta serie se presentaba el lenguaje de modelado del **SDK de dispositivo IoT de Azure para C** mediante el ejemplo proporcionado en la aplicación **simplesample\_amqp**:</span><span class="sxs-lookup"><span data-stu-id="af298-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="af298-117">Como puede observar, el lenguaje de modelado se basa en macros de C.</span><span class="sxs-lookup"><span data-stu-id="af298-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="af298-118">La definición comienza siempre con **BEGIN\_NAMESPACE** y termina siempre con **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="af298-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="af298-119">Es habitual asignar un nombre al espacio de nombres de su compañía o, como en este ejemplo, al proyecto en el que trabaja.</span><span class="sxs-lookup"><span data-stu-id="af298-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="af298-120">Lo que hay dentro del espacio de nombres son definiciones de modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="af298-121">En este caso, hay un único modelo para un anemómetro.</span><span class="sxs-lookup"><span data-stu-id="af298-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="af298-122">Una vez más, el modelo puede tener cualquier nombre pero, normalmente, se denomina para el dispositivo o el tipo de datos que quiere intercambiar con el Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="af298-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="af298-123">Los modelos contienen una definición de los eventos que puede insertar en el IoT Hub (los *datos*), así como de los mensajes que puede recibir de él (las *acciones*).</span><span class="sxs-lookup"><span data-stu-id="af298-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="af298-124">Como puede ver por el ejemplo, los eventos tienen un tipo y un nombre; las acciones tienen un nombre y parámetros opcionales (cada uno con un tipo).</span><span class="sxs-lookup"><span data-stu-id="af298-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="af298-125">Lo que no se demuestra en este ejemplo son tipos de datos adicionales que se admiten en el SDK.</span><span class="sxs-lookup"><span data-stu-id="af298-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="af298-126">Los trataremos a continuación.</span><span class="sxs-lookup"><span data-stu-id="af298-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="af298-127">El IoT Hub hace referencia a los datos que un dispositivo envía a dicho centro como *eventos*, mientras que el lenguaje de modelado hace referencia a ellos como *datos* (definidos mediante **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="af298-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="af298-128">De igual forma, el IoT Hub hace referencia a los datos que se envían a los dispositivos como *mensajes*, mientras que el modelado de datos hace referencia a ellos como *acciones* (definidas mediante **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="af298-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="af298-129">Tenga en cuenta que estos términos pueden usarse indistintamente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="af298-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="af298-130">Tipos de datos admitidos</span><span class="sxs-lookup"><span data-stu-id="af298-130">Supported data types</span></span>
<span data-ttu-id="af298-131">Se admiten los siguientes tipos de datos en modelos creados con la biblioteca de **serializador** :</span><span class="sxs-lookup"><span data-stu-id="af298-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="af298-132">Tipo</span><span class="sxs-lookup"><span data-stu-id="af298-132">Type</span></span> | <span data-ttu-id="af298-133">Description</span><span class="sxs-lookup"><span data-stu-id="af298-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="af298-134">double</span><span class="sxs-lookup"><span data-stu-id="af298-134">double</span></span> |<span data-ttu-id="af298-135">número de punto flotante de doble precisión</span><span class="sxs-lookup"><span data-stu-id="af298-135">double precision floating point number</span></span> |
| <span data-ttu-id="af298-136">int</span><span class="sxs-lookup"><span data-stu-id="af298-136">int</span></span> |<span data-ttu-id="af298-137">entero de 32 bits</span><span class="sxs-lookup"><span data-stu-id="af298-137">32 bit integer</span></span> |
| <span data-ttu-id="af298-138">float</span><span class="sxs-lookup"><span data-stu-id="af298-138">float</span></span> |<span data-ttu-id="af298-139">número de punto flotante de precisión simple</span><span class="sxs-lookup"><span data-stu-id="af298-139">single precision floating point number</span></span> |
| <span data-ttu-id="af298-140">long</span><span class="sxs-lookup"><span data-stu-id="af298-140">long</span></span> |<span data-ttu-id="af298-141">entero largo</span><span class="sxs-lookup"><span data-stu-id="af298-141">long integer</span></span> |
| <span data-ttu-id="af298-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="af298-142">int8\_t</span></span> |<span data-ttu-id="af298-143">entero de 8 bits</span><span class="sxs-lookup"><span data-stu-id="af298-143">8 bit integer</span></span> |
| <span data-ttu-id="af298-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="af298-144">int16\_t</span></span> |<span data-ttu-id="af298-145">entero de 16 bits</span><span class="sxs-lookup"><span data-stu-id="af298-145">16 bit integer</span></span> |
| <span data-ttu-id="af298-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="af298-146">int32\_t</span></span> |<span data-ttu-id="af298-147">entero de 32 bits</span><span class="sxs-lookup"><span data-stu-id="af298-147">32 bit integer</span></span> |
| <span data-ttu-id="af298-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="af298-148">int64\_t</span></span> |<span data-ttu-id="af298-149">entero de 64 bits</span><span class="sxs-lookup"><span data-stu-id="af298-149">64 bit integer</span></span> |
| <span data-ttu-id="af298-150">booleano</span><span class="sxs-lookup"><span data-stu-id="af298-150">bool</span></span> |<span data-ttu-id="af298-151">boolean</span><span class="sxs-lookup"><span data-stu-id="af298-151">boolean</span></span> |
| <span data-ttu-id="af298-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="af298-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="af298-153">Cadena ASCII</span><span class="sxs-lookup"><span data-stu-id="af298-153">ASCII string</span></span> |
| <span data-ttu-id="af298-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="af298-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="af298-155">desplazamiento de fecha y hora</span><span class="sxs-lookup"><span data-stu-id="af298-155">date time offset</span></span> |
| <span data-ttu-id="af298-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="af298-156">EDM\_GUID</span></span> |<span data-ttu-id="af298-157">GUID</span><span class="sxs-lookup"><span data-stu-id="af298-157">GUID</span></span> |
| <span data-ttu-id="af298-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="af298-158">EDM\_BINARY</span></span> |<span data-ttu-id="af298-159">binary</span><span class="sxs-lookup"><span data-stu-id="af298-159">binary</span></span> |
| <span data-ttu-id="af298-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="af298-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="af298-161">tipo de dato complejo</span><span class="sxs-lookup"><span data-stu-id="af298-161">complex data type</span></span> |

<span data-ttu-id="af298-162">Comencemos con el último tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="af298-162">Let’s start with the last data type.</span></span> <span data-ttu-id="af298-163">**DECLARE\_STRUCT** permite definir tipos de datos complejos, que son agrupaciones de los otros tipos primitivos.</span><span class="sxs-lookup"><span data-stu-id="af298-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="af298-164">Estas agrupaciones nos permiten definir un modelo parecido a este:</span><span class="sxs-lookup"><span data-stu-id="af298-164">These groupings allow us to define a model that looks like this:</span></span>

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

<span data-ttu-id="af298-165">Nuestro modelo contiene un evento de datos único de tipo **TestType**.</span><span class="sxs-lookup"><span data-stu-id="af298-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="af298-166">**TestType** es un tipo complejo que incluye varios miembros que, de forma colectiva, muestran los tipos primitivos admitidos por el lenguaje de modelado de **serializador**.</span><span class="sxs-lookup"><span data-stu-id="af298-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="af298-167">Con un modelo como este podemos escribir código para enviar datos al Centro de IoT, que tendría este aspecto:</span><span class="sxs-lookup"><span data-stu-id="af298-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="af298-168">Básicamente, lo que hacemos es asignar un valor a todos los miembros de la estructura **Test** y, luego, llamar a **SendAsync** para enviar el evento de datos de **Test** a la nube.</span><span class="sxs-lookup"><span data-stu-id="af298-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="af298-169">**SendAsync** es una función auxiliar que envía un solo evento de datos al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="af298-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
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

<span data-ttu-id="af298-170">Esta función serializa el evento de datos dado y lo envía al IoT Hub mediante **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="af298-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="af298-171">Este es el mismo código que hemos examinado en artículos anteriores (**SendAsync** encapsula la lógica en una función adecuada).</span><span class="sxs-lookup"><span data-stu-id="af298-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="af298-172">Otra función auxiliar que se usa en el código anterior es **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="af298-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="af298-173">Esta función transforma el tiempo especificado en un valor de tipo **EDM\_DATE\_TIME\_OFFSET**:</span><span class="sxs-lookup"><span data-stu-id="af298-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="af298-174">Si ejecuta este código, se envía el siguiente mensaje al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="af298-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="af298-175">Observe que la serialización es JSON, que es el formato generado por la biblioteca de **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="af298-176">Observe también que cada miembro del objeto JSON serializado coincide con los miembros de **TestType** que definimos en nuestro modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="af298-177">Los valores también coinciden exactamente con los usados en el código.</span><span class="sxs-lookup"><span data-stu-id="af298-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="af298-178">Sin embargo, observe que los datos binarios están codificados en base64: "AQID" es la codificación en base64 de {0 x 01, 0 x 02, 0 x 03}.</span><span class="sxs-lookup"><span data-stu-id="af298-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="af298-179">En este ejemplo se demuestra la ventaja de usar la biblioteca de **serializador** , y es que nos permite enviar JSON a la nube, sin tener que tratar explícitamente con la serialización en nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="af298-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="af298-180">De lo único de lo que nos tenemos que preocupar es de configurar los valores de los eventos de datos de nuestro modelo y, luego, llamar a API sencillas para enviar esos eventos a la nube.</span><span class="sxs-lookup"><span data-stu-id="af298-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="af298-181">Con esta información podemos definir modelos que comprendan el intervalo de tipos de datos compatibles, incluidos los tipos complejos (podríamos incluso incluir tipos complejos dentro de otros tipos complejos).</span><span class="sxs-lookup"><span data-stu-id="af298-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="af298-182">No obstante, el JSON serializado generado por el ejemplo anterior nos lleva a un punto importante.</span><span class="sxs-lookup"><span data-stu-id="af298-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="af298-183">*El modo en que* enviamos datos con la biblioteca de **serializador** determina exactamente cómo se forma el JSON.</span><span class="sxs-lookup"><span data-stu-id="af298-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="af298-184">Este punto en particular es de lo que hablaremos a continuación.</span><span class="sxs-lookup"><span data-stu-id="af298-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="af298-185">Más información sobre la serialización</span><span class="sxs-lookup"><span data-stu-id="af298-185">More about serialization</span></span>
<span data-ttu-id="af298-186">En la sección anterior se resalta un ejemplo de la salida generada por la biblioteca de **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="af298-187">En esta sección explicaremos cómo la biblioteca serializa los datos y cómo puede controlar este comportamiento mediante las API de serialización.</span><span class="sxs-lookup"><span data-stu-id="af298-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="af298-188">Para avanzar en la discusión sobre la serialización, trabajaremos con un nuevo modelo basado en un termostato.</span><span class="sxs-lookup"><span data-stu-id="af298-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="af298-189">Primero vamos a proporcionar alguna información de contexto sobre el escenario que tratamos de abordar.</span><span class="sxs-lookup"><span data-stu-id="af298-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="af298-190">Queremos modelar un termostato que mida la temperatura y la humedad.</span><span class="sxs-lookup"><span data-stu-id="af298-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="af298-191">Cada fragmento de datos se va a enviar al Centro de IoT de una manera diferente.</span><span class="sxs-lookup"><span data-stu-id="af298-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="af298-192">De forma predeterminada, el termostato introduce un evento de temperatura cada 2 minutos y un evento de humedad, cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="af298-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="af298-193">Cuando se introduce uno de estos eventos, se debe incluir una marca de tiempo que indique el tiempo durante el cual se midió la temperatura o humedad correspondientes.</span><span class="sxs-lookup"><span data-stu-id="af298-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="af298-194">Dado este escenario, demostraremos dos formas diferentes de modelar los datos y explicaremos el efecto que tiene el modelado en el resultado serializado.</span><span class="sxs-lookup"><span data-stu-id="af298-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="af298-195">Modelo 1</span><span class="sxs-lookup"><span data-stu-id="af298-195">Model 1</span></span>
<span data-ttu-id="af298-196">Esta es la primera versión de un modelo que admite el escenario anterior:</span><span class="sxs-lookup"><span data-stu-id="af298-196">Here's the first version of a model that supports the previous scenario:</span></span>

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

<span data-ttu-id="af298-197">Observe que el modelo incluye dos eventos de datos: **Temperature** y **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="af298-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="af298-198">A diferencia de los ejemplos anteriores, el tipo de cada evento es una estructura definida mediante **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="af298-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="af298-199">**TemperatureEvent** incluye una medida de la temperatura y una marca de tiempo; **HumidityEvent** contiene una medida de humedad y una marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="af298-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="af298-200">Este modelo nos proporciona una manera natural de modelar los datos para el escenario descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af298-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="af298-201">Cuando enviemos un evento a la nube, enviaremos un par temperatura/marca de tiempo o humedad/marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="af298-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="af298-202">Podemos enviar un evento de temperatura a la nube mediante un código similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="af298-202">We can send a temperature event to the cloud using code such as the following:</span></span>

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

<span data-ttu-id="af298-203">Usaremos valores codificados de forma rígida para temperatura y humedad en el código de ejemplo; pero imagine que en realidad vamos a recuperar estos valores mediante el muestreo de los sensores correspondientes en el termostato.</span><span class="sxs-lookup"><span data-stu-id="af298-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="af298-204">El código anterior usa la aplicación auxiliar **GetDateTimeOffset** que se especificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af298-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="af298-205">Por motivos que más tarde aclararemos, este código separa explícitamente la tarea de serializar y enviar el evento.</span><span class="sxs-lookup"><span data-stu-id="af298-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="af298-206">El código anterior serializa el evento de temperatura en un búfer.</span><span class="sxs-lookup"><span data-stu-id="af298-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="af298-207">Entonces, **sendMessage** es una función auxiliar (incluida en **simplesample\_amqp**) que envía el evento a IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="af298-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

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

<span data-ttu-id="af298-208">Este código es un subconjunto de la aplicación auxiliar **SendAsync** descrita en la sección anterior, por lo que no volveremos aquí sobre ella de nuevo.</span><span class="sxs-lookup"><span data-stu-id="af298-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="af298-209">Al ejecutar el código anterior para enviar el evento de temperatura, esta forma serializada del evento se envía al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="af298-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="af298-210">Vamos a enviar una temperatura que es de tipo **TemperatureEvent** y esa estructura contiene un miembro **Temperature** y **Time**.</span><span class="sxs-lookup"><span data-stu-id="af298-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="af298-211">Esto se refleja directamente en los datos serializados.</span><span class="sxs-lookup"><span data-stu-id="af298-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="af298-212">Del mismo modo, podemos enviar un evento de humedad con este código:</span><span class="sxs-lookup"><span data-stu-id="af298-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="af298-213">La forma serializada que se envía al Centro de IoT tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="af298-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="af298-214">Nuevamente, es lo que se esperaba.</span><span class="sxs-lookup"><span data-stu-id="af298-214">Again, this is as expected.</span></span>

<span data-ttu-id="af298-215">Con este modelo, puede imaginar lo fácil que se podrían agregar eventos adicionales.</span><span class="sxs-lookup"><span data-stu-id="af298-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="af298-216">Define más estructuras mediante **DECLARE\_STRUCT** e incluye el evento correspondiente en el modelo mediante **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="af298-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="af298-217">Ahora vamos a modificar el modelo para que incluya los mismos datos pero con una estructura diferente.</span><span class="sxs-lookup"><span data-stu-id="af298-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="af298-218">Modelo 2</span><span class="sxs-lookup"><span data-stu-id="af298-218">Model 2</span></span>
<span data-ttu-id="af298-219">Considere este modelo como una alternativa al anterior:</span><span class="sxs-lookup"><span data-stu-id="af298-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="af298-220">En este caso hemos eliminado las macros **DECLARE\_STRUCT** y simplemente va a definir los elementos de datos de nuestro escenario con tipos simples del lenguaje de modelado.</span><span class="sxs-lookup"><span data-stu-id="af298-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="af298-221">Solo por el momento, omitiremos el evento **Time** .</span><span class="sxs-lookup"><span data-stu-id="af298-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="af298-222">Dejando este a un lado, este es el código para especificar **Temperature**:</span><span class="sxs-lookup"><span data-stu-id="af298-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

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

<span data-ttu-id="af298-223">Este código envía el siguiente evento serializado al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="af298-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="af298-224">Y el código para enviar el evento de humedad tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="af298-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="af298-225">Este código envía esto al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="af298-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="af298-226">Hasta ahora, no hay novedades.</span><span class="sxs-lookup"><span data-stu-id="af298-226">So far there are still no surprises.</span></span> <span data-ttu-id="af298-227">Ahora vamos a cambiar cómo usamos la macro SERIALIZE.</span><span class="sxs-lookup"><span data-stu-id="af298-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="af298-228">La macro **SERIALIZE** puede tomar varios eventos de datos como argumentos.</span><span class="sxs-lookup"><span data-stu-id="af298-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="af298-229">Esto nos permite serializar los eventos **Temperature** y **Humidity** juntos y enviarlos al IoT Hub en una llamada:</span><span class="sxs-lookup"><span data-stu-id="af298-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="af298-230">Podría suponer que el resultado de este código es que dos eventos de datos se envían al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="af298-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="af298-231">[</span><span class="sxs-lookup"><span data-stu-id="af298-231">[</span></span>

<span data-ttu-id="af298-232">{"Temperature":75},</span><span class="sxs-lookup"><span data-stu-id="af298-232">{"Temperature":75},</span></span>

<span data-ttu-id="af298-233">{"Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="af298-233">{"Humidity":45}</span></span>

<span data-ttu-id="af298-234">]</span><span class="sxs-lookup"><span data-stu-id="af298-234">]</span></span>

<span data-ttu-id="af298-235">En otras palabras, puede esperar que este código sea lo mismo que enviar **Temperature** y **Humidity** por separado.</span><span class="sxs-lookup"><span data-stu-id="af298-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="af298-236">Solo por comodidad se pasan ambos eventos a **SERIALIZE** en la misma llamada.</span><span class="sxs-lookup"><span data-stu-id="af298-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="af298-237">Sin embargo, ese no es el caso.</span><span class="sxs-lookup"><span data-stu-id="af298-237">However, that’s not the case.</span></span> <span data-ttu-id="af298-238">Por el contrario, el código anterior envía este único evento de datos al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="af298-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="af298-239">{"Temperature":75, "Humidity":45}</span><span class="sxs-lookup"><span data-stu-id="af298-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="af298-240">Esto puede parecer extraño debido a que nuestro modelo define **Temperature** y **Humidity** como dos eventos *independientes*:</span><span class="sxs-lookup"><span data-stu-id="af298-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="af298-241">Más concretamente, no modelamos estos eventos cuando **Temperature** y **Humidity** están en la misma estructura:</span><span class="sxs-lookup"><span data-stu-id="af298-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="af298-242">Si usáramos este modelo, sería más fácil entender cómo **Temperature** y **Humidity** se enviarían en el mismo mensaje serializado.</span><span class="sxs-lookup"><span data-stu-id="af298-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="af298-243">No obstante, es posible que no quede claro por qué esto funciona de esa forma cuando se pasan ambos eventos de datos a **SERIALIZE** con el modelo 2.</span><span class="sxs-lookup"><span data-stu-id="af298-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="af298-244">Este comportamiento es más fácil de entender si sabe las suposiciones que realiza la biblioteca de **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="af298-245">Para que esto tenga sentido, volvamos a nuestro modelo:</span><span class="sxs-lookup"><span data-stu-id="af298-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="af298-246">Considere este modelo en términos de orientación a objetos.</span><span class="sxs-lookup"><span data-stu-id="af298-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="af298-247">En este caso, estamos modelando un dispositivo físico (un termostato) y ese dispositivo incluye atributos como **Temperature** y **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="af298-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="af298-248">Podemos enviar todo el estado de nuestro modelo con código como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="af298-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="af298-249">Suponiendo que los valores de Temperature, Humidity y Time estén establecidos, veríamos que se envía un evento como éste al Centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="af298-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="af298-250">A veces, quizás solo quiera enviar *algunas* propiedades del modelo a la nube (esto es especialmente cierto si el modelo contiene un gran número de eventos de datos).</span><span class="sxs-lookup"><span data-stu-id="af298-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="af298-251">Resulta útil enviar solo un subconjunto de eventos de datos, como en el ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="af298-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="af298-252">Se genera exactamente el mismo evento serializado que si hubiéramos definido **TemperatureEvent** con un miembro **Temperature** y **Time**, como hicimos con el modelo 1.</span><span class="sxs-lookup"><span data-stu-id="af298-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="af298-253">En este caso, pudimos generar exactamente el mismo evento serializado con un modelo diferente (modelo 2) porque llamamos a **SERIALIZE** de una manera diferente.</span><span class="sxs-lookup"><span data-stu-id="af298-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="af298-254">Lo importante aquí es que si se pasan varios eventos de datos a **SERIALIZE,** , se supone que cada evento es una propiedad en un único objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="af298-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="af298-255">El mejor enfoque dependerá de usted y de su forma de pensar sobre el modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="af298-256">Si envía "eventos" a la nube y cada evento contiene un conjunto definido de propiedades, entonces el primer enfoque cobra mucho sentido.</span><span class="sxs-lookup"><span data-stu-id="af298-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="af298-257">En ese caso, usaría **DECLARE\_STRUCT** para definir la estructura de cada evento y luego incluirlos en el modelo con la macro **WITH\_DATA**.</span><span class="sxs-lookup"><span data-stu-id="af298-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="af298-258">A continuación, enviaría cada evento como hicimos en el primer ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="af298-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="af298-259">En este enfoque, solo pasaría un evento de datos a **SERIALIZADOR**.</span><span class="sxs-lookup"><span data-stu-id="af298-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="af298-260">Si piensa en su modelo como orientado a objetos, entonces el segundo enfoque puede ser adecuado para usted.</span><span class="sxs-lookup"><span data-stu-id="af298-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="af298-261">En este caso, los elementos definidos mediante **WITH\_DATA** son las "propiedades" del objeto.</span><span class="sxs-lookup"><span data-stu-id="af298-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="af298-262">Pasaría cualquier subconjunto de eventos de su elección a **SERIALIZE** , según la cantidad de estado del "objeto" que quiera enviar a la nube.</span><span class="sxs-lookup"><span data-stu-id="af298-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="af298-263">Ningún enfoque es bueno ni malo.</span><span class="sxs-lookup"><span data-stu-id="af298-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="af298-264">Lo importante es saber cómo funciona la biblioteca de **serializador** y seleccionar el enfoque de modelado que mejor se ajuste a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="af298-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="af298-265">Administración de mensajes</span><span class="sxs-lookup"><span data-stu-id="af298-265">Message handling</span></span>
<span data-ttu-id="af298-266">Hasta ahora solo hemos examinado en este artículo el envío de eventos al Centro de IoT y no hemos hablado de la recepción de mensajes.</span><span class="sxs-lookup"><span data-stu-id="af298-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="af298-267">La razón de ello es que lo que necesitamos saber sobre la recepción de mensajes se ha tratado en gran medida en un [artículo anterior](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="af298-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="af298-268">Como se explicaba en ese artículo, los mensajes se procesan mediante el registro de una función de devolución de llamada de mensaje:</span><span class="sxs-lookup"><span data-stu-id="af298-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="af298-269">Luego, se escribe la función de devolución de llamada que se invoca cuando se recibe un mensaje:</span><span class="sxs-lookup"><span data-stu-id="af298-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="af298-270">Esta implementación de **IoTHubMessage** llama a la función específica para cada acción del modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="af298-271">Por ejemplo, si el modelo define esta acción:</span><span class="sxs-lookup"><span data-stu-id="af298-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="af298-272">Debe definir una función con esta firma:</span><span class="sxs-lookup"><span data-stu-id="af298-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="af298-273">**SetAirResistance** cuando ese mensaje se envía al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="af298-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="af298-274">Lo que no hemos explicado aún es cuál es el aspecto de la versión serializada del mensaje.</span><span class="sxs-lookup"><span data-stu-id="af298-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="af298-275">En otras palabras, si desea enviar un mensaje **SetAirResistance** a su dispositivo, ¿cómo se hará?</span><span class="sxs-lookup"><span data-stu-id="af298-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="af298-276">Si va a enviar un mensaje a un dispositivo, debería hacerlo a través del SDK del servicio IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="af298-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="af298-277">Necesitará saber aun así qué cadena se envía para invocar una acción determinada.</span><span class="sxs-lookup"><span data-stu-id="af298-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="af298-278">El formato general para enviar un mensaje aparece del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="af298-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="af298-279">Si envía un objeto JSON serializado con dos propiedades: **Name** es el nombre de la acción (mensaje) y **Parameters** contiene los parámetros de esa acción.</span><span class="sxs-lookup"><span data-stu-id="af298-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="af298-280">Por ejemplo, para invocar **SetAirResistance** , puede enviar este mensaje a un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="af298-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="af298-281">El nombre de la acción debe coincidir exactamente con una acción definida en el modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="af298-282">Los nombres de los parámetros deben coincidir también.</span><span class="sxs-lookup"><span data-stu-id="af298-282">The parameter names must match as well.</span></span> <span data-ttu-id="af298-283">Tenga en cuenta que existe una distinción de mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="af298-283">Also note case sensitivity.</span></span> <span data-ttu-id="af298-284">**Name** y **Parameters** van siempre en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="af298-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="af298-285">Asegúrese de que las mayúsculas y minúsculas coincidan en el nombre de la acción y los parámetros del modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="af298-286">En este ejemplo, el nombre de la acción es "SetAirResistance" y no "setairresistance".</span><span class="sxs-lookup"><span data-stu-id="af298-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="af298-287">Las otras dos acciones **TurnFanOn** y **TurnFanOff** se pueden invocar mediante el envío de estos mensajes a un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="af298-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="af298-288">En esta sección se describe todo lo que necesita saber al enviar eventos y recibir mensajes con la biblioteca de **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="af298-289">Antes de continuar, vamos a examinar algunos parámetros que puede configurar que controlan lo grande que es su modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="af298-290">Configuración de macros</span><span class="sxs-lookup"><span data-stu-id="af298-290">Macro configuration</span></span>
<span data-ttu-id="af298-291">Si está usando la biblioteca de **serializador**, una parte importante del SDK que se debe tener en cuenta se encuentra en la biblioteca azure-c-shared-utility.</span><span class="sxs-lookup"><span data-stu-id="af298-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="af298-292">Si ha clonado el repositorio Azure-iot-sdk-c desde GitHub con la opción --recursive, encontrará esta biblioteca de utilidad compartida aquí:</span><span class="sxs-lookup"><span data-stu-id="af298-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="af298-293">Si no ha clonado la biblioteca, podrá encontrarla [aquí](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="af298-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="af298-294">Dentro de la biblioteca de utilidad compartida, encontrará la siguiente carpeta:</span><span class="sxs-lookup"><span data-stu-id="af298-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="af298-295">Esta carpeta contiene una solución de Visual Studio denominada **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="af298-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="af298-296">El programa de esta solución genera el archivo **macro\_utils.h**.</span><span class="sxs-lookup"><span data-stu-id="af298-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="af298-297">Hay un archivo macro\_utils.h predeterminado incluido con el SDK.</span><span class="sxs-lookup"><span data-stu-id="af298-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="af298-298">Esta solución le permite modificar algunos parámetros y luego volver a crear el archivo de encabezado en función de ellos.</span><span class="sxs-lookup"><span data-stu-id="af298-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="af298-299">Los dos parámetros clave que se deben tener en cuenta son **nArithmetic** y **nMacroParameters**, que se definen en estas dos líneas que se encuentran en macro\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="af298-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="af298-300">Estos valores son los parámetros predeterminados incluidos con el SDK.</span><span class="sxs-lookup"><span data-stu-id="af298-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="af298-301">Cada parámetro tiene el significado siguiente:</span><span class="sxs-lookup"><span data-stu-id="af298-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="af298-302">nMacroParameters: controla el número de parámetros que puede tener en una definición de macro DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="af298-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="af298-303">nArithmetic: controla el número total de miembros permitidos en un modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="af298-304">El motivo de que estos parámetros sean importantes es que controlan lo grande que puede ser el modelo.</span><span class="sxs-lookup"><span data-stu-id="af298-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="af298-305">Por ejemplo, tenga en cuenta esta definición de modelo:</span><span class="sxs-lookup"><span data-stu-id="af298-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="af298-306">Como se mencionó antes, **DECLARE\_MODEL** es simplemente una macro de C.</span><span class="sxs-lookup"><span data-stu-id="af298-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="af298-307">Los nombres del modelo y la instrucción **WITH\_DATA** (todavía otra macro) son parámetros de **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="af298-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="af298-308">**nMacroParameters** define la cantidad de parámetros que puede incluirse en **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="af298-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="af298-309">Esto permite definir de manera efectiva cuántas declaraciones de evento y acción puede tener.</span><span class="sxs-lookup"><span data-stu-id="af298-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="af298-310">Con el límite predeterminado de 124, significa que puede definir un modelo con una combinación de unas 60 acciones y eventos de datos.</span><span class="sxs-lookup"><span data-stu-id="af298-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="af298-311">Si intenta superar este límite, obtendrá errores de compilación parecidos a estos:</span><span class="sxs-lookup"><span data-stu-id="af298-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="af298-312">El parámetro **nArithmetic** tiene más que ver con el funcionamiento interno del lenguaje de macros que con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="af298-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="af298-313">Controla el número total de miembros que puede tener en el modelo, incluidas las macros **DECLARE_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="af298-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="af298-314">Si comienza a ver errores del compilador como este, debería intentar aumentar el valor de **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="af298-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="af298-315">Si desea cambiar estos parámetros, modifique los valores del archivo macro\_utils.tt, vuelva a compilar la solución macro\_utils\_h\_generator.sln y ejecute el programa compilado.</span><span class="sxs-lookup"><span data-stu-id="af298-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="af298-316">Al hacerlo, se genera un nuevo archivo macro\_utils.h y se coloca en el directorio .\\common\\inc.</span><span class="sxs-lookup"><span data-stu-id="af298-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="af298-317">Para poder usar la nueva versión de macro\_utils.h, quite el paquete NuGet de **serializador** de la solución y, en su lugar, incluya el proyecto de Visual Studio de **serializador**.</span><span class="sxs-lookup"><span data-stu-id="af298-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="af298-318">Esto permite a su código compilarse con el código fuente de la biblioteca de serializador.</span><span class="sxs-lookup"><span data-stu-id="af298-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="af298-319">Incluye la macro\_utils.h. actualizada.</span><span class="sxs-lookup"><span data-stu-id="af298-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="af298-320">Si desea hacer esto para **simplesample\_amqp**, empiece quitando el paquete NuGet para la biblioteca de serializador de la solución:</span><span class="sxs-lookup"><span data-stu-id="af298-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="af298-321">Luego agregue este proyecto a la solución de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="af298-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="af298-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="af298-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="af298-323">Cuando haya terminado, su solución debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="af298-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="af298-324">Ahora, cuando se compila la solución, la macro\_utils.h actualizada se incluye en el archivo binario.</span><span class="sxs-lookup"><span data-stu-id="af298-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="af298-325">Tenga en cuenta que, si se aumentan estos valores mucho, se podrían exceder los límites del compilador.</span><span class="sxs-lookup"><span data-stu-id="af298-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="af298-326">En este punto, **nMacroParameters** es el parámetro principal del que nos tenemos que ocupar.</span><span class="sxs-lookup"><span data-stu-id="af298-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="af298-327">La especificación C99 especifica que se permiten 127 parámetros como mínimo en una definición de macro.</span><span class="sxs-lookup"><span data-stu-id="af298-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="af298-328">El compilador de Microsoft sigue la especificación exactamente (y tiene un límite de 127) por lo que no podrá aumentar **nMacroParameters** por encima de su valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="af298-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="af298-329">Es posible que otros compiladores le permitan hacerlo (por ejemplo, el compilador GNU admite un límite más alto).</span><span class="sxs-lookup"><span data-stu-id="af298-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="af298-330">Hasta ahora hemos visto casi todo lo que necesita saber sobre cómo escribir código con la biblioteca de **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="af298-331">Antes de concluir, vamos a revisar algunos temas de artículos anteriores sobre los que es posible que se esté preguntando.</span><span class="sxs-lookup"><span data-stu-id="af298-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="af298-332">API de nivel inferior</span><span class="sxs-lookup"><span data-stu-id="af298-332">The lower-level APIs</span></span>
<span data-ttu-id="af298-333">La aplicación de ejemplo en la que se centró este artículo es **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="af298-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="af298-334">En este ejemplo se usan las API de nivel superior (las no "LL") para enviar eventos y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="af298-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="af298-335">Si usa estas API, se ejecuta un subproceso en segundo plano que se encarga de enviar eventos y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="af298-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="af298-336">Sin embargo, puede usar las API de nivel inferior (LL) para eliminar este subproceso en segundo plano y tener un control explícito sobre cuándo envía eventos o recibe mensajes de la nube.</span><span class="sxs-lookup"><span data-stu-id="af298-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="af298-337">Como se describió en un [artículo anterior](iot-hub-device-sdk-c-iothubclient.md), hay conjuntos de funciones que constan de API de nivel superior:</span><span class="sxs-lookup"><span data-stu-id="af298-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="af298-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="af298-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="af298-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="af298-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="af298-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="af298-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="af298-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="af298-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="af298-342">Estas API se muestran en **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="af298-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="af298-343">Hay un conjunto similar de API de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="af298-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="af298-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="af298-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="af298-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="af298-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="af298-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="af298-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="af298-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="af298-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="af298-348">Tenga en cuenta que las API de nivel inferior funcionan exactamente como se describió en los artículos anteriores.</span><span class="sxs-lookup"><span data-stu-id="af298-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="af298-349">Puede usar el primer conjunto de API, si quiere que un subproceso en segundo plano controle el envío de eventos y la recepción de mensajes.</span><span class="sxs-lookup"><span data-stu-id="af298-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="af298-350">Si quiere un control explícito sobre cuándo envía y recibe datos del Centro de IoT, usará el segundo conjunto de API.</span><span class="sxs-lookup"><span data-stu-id="af298-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="af298-351">Cualquier conjunto de API funciona igual de bien con la biblioteca de **serializador** .</span><span class="sxs-lookup"><span data-stu-id="af298-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="af298-352">Para ver un ejemplo de cómo se usan las API de nivel inferior con la biblioteca de **serializador**, vea la aplicación **simplesample\_http**.</span><span class="sxs-lookup"><span data-stu-id="af298-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="af298-353">Otros temas</span><span class="sxs-lookup"><span data-stu-id="af298-353">Additional topics</span></span>
<span data-ttu-id="af298-354">Algunos otros temas que merece la pena mencionar de nuevo son el control de propiedades, el uso de credenciales de dispositivo alternativas y las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="af298-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="af298-355">Todos estos temas se trataron en un [artículo anterior](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="af298-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="af298-356">Lo que hay que destacar es que todas estas características funcionan igual con la biblioteca de **serializador** que con la biblioteca de **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="af298-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="af298-357">Por ejemplo, si desea adjuntar propiedades a un evento del modelo, use **IoTHubMessage\_Properties** y **Map**\_**AddorUpdate** de la misma forma que se describió anteriormente:</span><span class="sxs-lookup"><span data-stu-id="af298-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="af298-358">Da igual que el evento se generara con la biblioteca de **serializador** o se creara de forma manual con la biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="af298-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="af298-359">En cuanto a las credenciales de dispositivo alternativas, el uso de **IoTHubClient\_LL\_Create** funciona igual de bien que **IoTHubClient\_CreateFromConnectionString** para asignar **IOTHUB\_CLIENT\_HANDLE**.</span><span class="sxs-lookup"><span data-stu-id="af298-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="af298-360">Por último, si usa la biblioteca de **serializador**, puede establecer opciones de configuración con **IoTHubClient\_LL\_SetOption** lo mismo que hizo al usar la biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="af298-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="af298-361">Una característica que es exclusiva de la biblioteca de **serializador** son las API de inicialización.</span><span class="sxs-lookup"><span data-stu-id="af298-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="af298-362">Antes de empezar a trabajar con la biblioteca, debe llamar a **serializer\_init**:</span><span class="sxs-lookup"><span data-stu-id="af298-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="af298-363">Esto se hace justo antes de llamar a **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="af298-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="af298-364">Del mismo modo, cuando termine de trabajar con la biblioteca, la última llamada que hará es a **serializer\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="af298-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="af298-365">Por lo demás, todas las demás características enumeradas anteriormente funcionan igual en la biblioteca de **serializador** que en la biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="af298-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="af298-366">Para más información sobre cualquiera de estos temas, consulte el [artículo anterior](iot-hub-device-sdk-c-iothubclient.md) de esta serie.</span><span class="sxs-lookup"><span data-stu-id="af298-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af298-367">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af298-367">Next steps</span></span>
<span data-ttu-id="af298-368">En este artículo se describen en detalle los aspectos únicos de la biblioteca de **serializador** contenida en el **SDK de dispositivo IoT de Azure para C**. Con la información proporcionada, habrá comprendido perfectamente cómo usar los modelos para enviar eventos y recibir mensajes del Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="af298-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="af298-369">Con esto también concluye la serie de tres partes sobre cómo desarrollar aplicaciones con el **SDK de dispositivo IoT de Azure para C**. Esta información debería ser suficiente no solo para ayudarle en sus primeros pasos sino también para proporcionarle una comprensión profunda de cómo funcionan las API.</span><span class="sxs-lookup"><span data-stu-id="af298-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="af298-370">Para obtener información adicional, existen algunos ejemplos en el SDK que no se tratan aquí.</span><span class="sxs-lookup"><span data-stu-id="af298-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="af298-371">Por lo demás, la [documentación del SDK](https://github.com/Azure/azure-iot-sdk-c) es un buen recurso para conseguir información adicional.</span><span class="sxs-lookup"><span data-stu-id="af298-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="af298-372">Para más información acerca del desarrollo para IoT Hub, consulte los [SDK de IoT Hub][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="af298-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="af298-373">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="af298-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="af298-374">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="af298-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

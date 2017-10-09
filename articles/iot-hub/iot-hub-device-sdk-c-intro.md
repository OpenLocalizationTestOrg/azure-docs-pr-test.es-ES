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
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="7180d-103">SDK de dispositivo IoT de Azure para C</span><span class="sxs-lookup"><span data-stu-id="7180d-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="7180d-104">Hola **dispositivos de IoT de Azure SDK** es un conjunto de bibliotecas diseñado el proceso de hello toosimplify de enviar mensajes de tooand recibir los mensajes de Hola **centro de IoT de Azure** servicio.</span><span class="sxs-lookup"><span data-stu-id="7180d-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="7180d-105">Hay distintas variaciones de hello SDK, como destino una plataforma concreta, pero este artículo describen hello **dispositivos de IoT de Azure SDK para C**.</span><span class="sxs-lookup"><span data-stu-id="7180d-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="7180d-106">dispositivo de Hello IoT de Azure SDK para C se escribe en ANSI C (C99) toomaximize portabilidad.</span><span class="sxs-lookup"><span data-stu-id="7180d-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="7180d-107">Esta característica hace Hola bibliotecas adecuadas toooperate en varias plataformas y dispositivos, especialmente cuando se minimiza el disco y consumo de memoria es una prioridad.</span><span class="sxs-lookup"><span data-stu-id="7180d-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="7180d-108">Hay una amplia gama de plataformas en qué Hola SDK se ha probado (vea hello [Azure Certified para el catálogo de dispositivos de IoT](https://catalog.azureiotsuite.com/) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="7180d-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="7180d-109">Aunque en este artículo incluye tutoriales de código de ejemplo que se ejecuta en la plataforma de Windows hello, código de hello descrito en este artículo es idéntico a lo largo intervalo de Hola de las plataformas compatibles.</span><span class="sxs-lookup"><span data-stu-id="7180d-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="7180d-110">Este artículo presenta toohello arquitectura de SDK de dispositivos de IoT de Azure Hola de C. Muestra cómo enviar datos tooIoT centro de biblioteca de dispositivos de tooinitialize hello y recibir los mensajes de.</span><span class="sxs-lookup"><span data-stu-id="7180d-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="7180d-111">información de Hello en este artículo debería ser suficiente tooget iniciado mediante Hola SDK, pero también proporciona punteros tooadditional información acerca de las bibliotecas de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="7180d-112">Arquitectura del SDK</span><span class="sxs-lookup"><span data-stu-id="7180d-112">SDK architecture</span></span>

<span data-ttu-id="7180d-113">Puede encontrar Hola [ **dispositivos de IoT de Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositorio y ver los detalles de la API de Hola Hola [referencia de la API de C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="7180d-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="7180d-114">versión más reciente de Hola de bibliotecas de hello puede encontrarse en hello **maestro** rama del repositorio de hello:</span><span class="sxs-lookup"><span data-stu-id="7180d-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="7180d-115">Hola implementación básica de hello SDK es Hola **el centro de IOT\_cliente** carpeta que contiene la implementación de Hola de capa de API más bajo de Hola Hola SDK: Hola **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7180d-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="7180d-116">Hola **IoTHubClient** biblioteca contiene las API de implementación de mensajería sin formato para enviar mensajes tooIoT concentrador y recibir mensajes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7180d-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="7180d-117">Quien use esta biblioteca es responsable de la implementación de la serialización de mensajes, pero otros detalles de la comunicación con IoT Hub se controlan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7180d-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="7180d-118">Hola **serializador** carpeta contiene funciones auxiliares y ejemplos que muestran cómo tooserialize datos antes de enviar el uso del centro de IoT de tooAzure Hola biblioteca de cliente.</span><span class="sxs-lookup"><span data-stu-id="7180d-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="7180d-119">uso de Hola de serializador de hello no es obligatorio y se proporciona como una comodidad.</span><span class="sxs-lookup"><span data-stu-id="7180d-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="7180d-120">Hola toouse **serializador** biblioteca, define un modelo que especifica datos toosend tooIoT hello y centro de mensajes de saludo espera tooreceive de él.</span><span class="sxs-lookup"><span data-stu-id="7180d-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="7180d-121">Una vez definido el modelo de hello, Hola SDK proporciona una superficie de API que permite tooeasily trabajo con el dispositivo a la nube y mensajes en la nube a dispositivo sin preocuparse de Hola detalles de serialización.</span><span class="sxs-lookup"><span data-stu-id="7180d-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="7180d-122">biblioteca de Hello depende de otras bibliotecas de código abierto que implementan el transporte mediante protocolos como MQTT y AMQP.</span><span class="sxs-lookup"><span data-stu-id="7180d-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="7180d-123">Hola **IoTHubClient** biblioteca depende de otras bibliotecas de código abierto:</span><span class="sxs-lookup"><span data-stu-id="7180d-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="7180d-124">Hola [Azure C compartido utilidad](https://github.com/Azure/azure-c-shared-utility) biblioteca, que proporciona la funcionalidad común para realizar tareas básicas (como cadenas, manipulación de lista y E/S) necesaria a través de varios SDK de C relacionadas con Azure.</span><span class="sxs-lookup"><span data-stu-id="7180d-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="7180d-125">Hola [uAMQP Azure](https://github.com/Azure/azure-uamqp-c) biblioteca, que es una implementación de cliente de AMQP optimizada para dispositivos de limitación de recursos.</span><span class="sxs-lookup"><span data-stu-id="7180d-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="7180d-126">Hola [uMQTT Azure](https://github.com/Azure/azure-umqtt-c) biblioteca, que es una biblioteca de propósito general implementar hello MQTT protocolo y optimizado para dispositivos de limitación de recursos.</span><span class="sxs-lookup"><span data-stu-id="7180d-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="7180d-127">Uso de estas bibliotecas es más fácil toounderstand examinando el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7180d-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="7180d-128">Hola las secciones siguientes le guiará por varias aplicaciones de ejemplo de Hola que se incluyen en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="7180d-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="7180d-129">En este tutorial debe proporcionarle un buen sentirse para hello varias funciones de niveles arquitectónicos de Hola de Hola SDK y un Hola de toohow de introducción las API de funcionar.</span><span class="sxs-lookup"><span data-stu-id="7180d-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="7180d-130">Antes de ejecutar los ejemplos de hello</span><span class="sxs-lookup"><span data-stu-id="7180d-130">Before you run hello samples</span></span>

<span data-ttu-id="7180d-131">Antes de poder ejecutar los ejemplos de hello en dispositivo de hello IoT de Azure SDK para C, debe [crear una instancia del servicio del centro de IoT hello](iot-hub-create-through-portal.md) en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7180d-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="7180d-132">A continuación, complete Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="7180d-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="7180d-133">Preparación del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="7180d-133">Prepare your development environment</span></span>
* <span data-ttu-id="7180d-134">Obtención de las credenciales del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7180d-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="7180d-135">Preparación del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="7180d-135">Prepare your development environment</span></span>

<span data-ttu-id="7180d-136">Los paquetes se proporcionan para plataformas comunes (por ejemplo, NuGet para Windows o apt_get para Debian y Ubuntu) y ejemplos de hello usan estos paquetes cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="7180d-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="7180d-137">En algunos casos, necesitará toocompile Hola SDK para o en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7180d-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="7180d-138">Si necesita toocompile Hola SDK, consulte [preparar el entorno de desarrollo](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) en el repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="7180d-139">código de aplicación de ejemplo de tooobtain hello, descarga una copia del programa Hola SDK desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="7180d-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="7180d-140">Obtenga una copia de origen Hola de hello **maestro** rama de hello [repositorio de GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="7180d-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="7180d-141">Obtener las credenciales del dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="7180d-141">Obtain hello device credentials</span></span>

<span data-ttu-id="7180d-142">Ahora que tiene código fuente de ejemplo de Hola, hello toodo de lo siguiente es tooget un conjunto de credenciales de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7180d-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="7180d-143">Para un dispositivo toobe puede tooaccess un centro de IoT, primero debe agregar Hola dispositivo toohello del registro de identidad de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7180d-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="7180d-144">Al agregar un dispositivo, obtendrá un conjunto de credenciales de dispositivo que necesita para el centro de IoT de hello dispositivo toobe tooconnect capaz de toohello.</span><span class="sxs-lookup"><span data-stu-id="7180d-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="7180d-145">aplicaciones de ejemplo de Hola se describe en la sección siguiente Hola espera que estas credenciales en forma de Hola de un **cadena de conexión de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="7180d-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="7180d-146">Hay varias toohelp de herramientas de código abierto que administra el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7180d-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="7180d-147">Una aplicación de Windows llamada [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="7180d-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="7180d-148">Una herramienta de la CLI de node.js multiplataforma llamada [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="7180d-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="7180d-149">Este tutorial usa Hola gráfica *explorer dispositivo* herramienta.</span><span class="sxs-lookup"><span data-stu-id="7180d-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="7180d-150">También puede usar hello *el centro de IOT explorador* herramienta si lo prefiere toouse una herramienta CLI.</span><span class="sxs-lookup"><span data-stu-id="7180d-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="7180d-151">herramienta de explorador del dispositivo de Hello usa hello Azure IoT servicio bibliotecas tooperform distintas funciones en el centro de IoT, incluida la adición de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7180d-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="7180d-152">Si usas tooadd un dispositivo de la herramienta de explorador del dispositivo hello, obtendrá una cadena de conexión para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7180d-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="7180d-153">Necesita esta aplicación de ejemplo de conexión cadena toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="7180d-154">Si no está familiarizado con la herramienta de explorador del dispositivo de hello, Hola procedimiento describe cómo toouse tooadd un dispositivo y obtener una cadena de conexión de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7180d-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="7180d-155">herramienta de explorador de dispositivos de hello tooinstall, consulte [cómo toouse Hola explorador del dispositivo para los dispositivos del centro de IoT](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="7180d-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="7180d-156">Al ejecutar el programa Hola, verá esta interfaz:</span><span class="sxs-lookup"><span data-stu-id="7180d-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="7180d-157">Escriba su **cadena de conexión del centro de IoT** Hola primero campo y haga clic en **actualización**.</span><span class="sxs-lookup"><span data-stu-id="7180d-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="7180d-158">Este paso configura la herramienta de Hola para que puedan comunicarse con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7180d-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="7180d-159">Cuando se configura la cadena de conexión de centro de IoT hello, haga clic en hello **administración** ficha:</span><span class="sxs-lookup"><span data-stu-id="7180d-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="7180d-160">Esta ficha es donde se administran los dispositivos de hello registrados en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7180d-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="7180d-161">Crear un dispositivo, haga clic en hello **crear** botón.</span><span class="sxs-lookup"><span data-stu-id="7180d-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="7180d-162">Se muestra un cuadro de diálogo con un conjunto de claves (principal y secundaria) previamente rellenadas.</span><span class="sxs-lookup"><span data-stu-id="7180d-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="7180d-163">Escriba un valor en **Device ID** (Id. de dispositivo) y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="7180d-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="7180d-164">Cuando se crea el dispositivo de hello, dispositivos de hello lista actualizaciones con todos los dispositivos de hello registrado, incluidos Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="7180d-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="7180d-165">Si hace clic con el botón derecho en el dispositivo nuevo, verá este menú:</span><span class="sxs-lookup"><span data-stu-id="7180d-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="7180d-166">Si elige **copiar la cadena de conexión del dispositivo seleccionado**, cadena de conexión de dispositivo de hello es copiada toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="7180d-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="7180d-167">Mantener una copia de la cadena de conexión de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="7180d-168">Se necesita cuando se ejecutan aplicaciones de ejemplo de Hola descritas en hello las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="7180d-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="7180d-169">Cuando haya completado los pasos de hello anteriores, está listo toostart ejecutar algún código.</span><span class="sxs-lookup"><span data-stu-id="7180d-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="7180d-170">Ambos ejemplos tienen una constante al principio de hello del archivo de código fuente principal de Hola que permite tooenter una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="7180d-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="7180d-171">Por ejemplo, Hola línea correspondiente de hello **el centro de IOT\_cliente\_ejemplo\_mqtt** aplicación aparece como sigue.</span><span class="sxs-lookup"><span data-stu-id="7180d-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="7180d-172">Utilizar la biblioteca en IoTHubClient Hola</span><span class="sxs-lookup"><span data-stu-id="7180d-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="7180d-173">Dentro de hello **el centro de IOT\_cliente** carpeta Hola [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repositorio, hay un **ejemplos** carpeta que contenga una aplicación denominada **el centro de IOT\_cliente\_ejemplo\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="7180d-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="7180d-174">versión de Windows Hello de hello **el centro de IOT\_cliente\_ejemplo\_mqtt** aplicación incluye Hola después de solución de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="7180d-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="7180d-175">Si abre este proyecto en Visual Studio de 2017, acepte mensajes hello toohello tooretarget Hola proyecto última versión.</span><span class="sxs-lookup"><span data-stu-id="7180d-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="7180d-176">Esta solución contiene un proyecto.</span><span class="sxs-lookup"><span data-stu-id="7180d-176">This solution contains a single project.</span></span> <span data-ttu-id="7180d-177">En esta solución hay cuatro paquetes de NuGet instalados:</span><span class="sxs-lookup"><span data-stu-id="7180d-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="7180d-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="7180d-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="7180d-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="7180d-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="7180d-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="7180d-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="7180d-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="7180d-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="7180d-182">Siempre debe hello **Microsoft.Azure.C.SharedUtility** cuando se trabaja con hello SDK del paquete.</span><span class="sxs-lookup"><span data-stu-id="7180d-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="7180d-183">Este ejemplo usa el protocolo MQTT de hello, por lo tanto, debe incluir hello **Microsoft.Azure.umqtt** y **Microsoft.Azure.IoTHub.MqttTransport** (no hay equivalente paquetes para HTTP y AMQP de paquetes ).</span><span class="sxs-lookup"><span data-stu-id="7180d-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="7180d-184">Dado que el ejemplo de Hola usa hello **IoTHubClient** biblioteca, también debe incluir hello **Microsoft.Azure.IoTHub.IoTHubClient** paquete de la solución.</span><span class="sxs-lookup"><span data-stu-id="7180d-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="7180d-185">Implementación de hello para la aplicación de ejemplo de Hola se puede encontrar en hello **el centro de IOT\_cliente\_ejemplo\_mqtt.c** archivo de código fuente.</span><span class="sxs-lookup"><span data-stu-id="7180d-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="7180d-186">pasos siguientes Hello utilizan este toowalk de aplicación de ejemplo le guían a través de los requisitos hello toouse **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7180d-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="7180d-187">Inicializar la biblioteca de Hola</span><span class="sxs-lookup"><span data-stu-id="7180d-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="7180d-188">Antes de empezar a trabajar con bibliotecas de hello, puede que necesite tooperform algunas operaciones de inicialización específica de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="7180d-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="7180d-189">Por ejemplo, si tiene previsto toouse AMQP en Linux debe inicializar la biblioteca OpenSSL de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="7180d-190">Hola ejemplos de hello [repositorio de GitHub](https://github.com/Azure/azure-iot-sdk-c) llamar a la función de utilidad hello **plataforma\_init** cuando Hola cliente inicia y llamar a hello **plataforma\_deinit**  función antes de salir.</span><span class="sxs-lookup"><span data-stu-id="7180d-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="7180d-191">Estas funciones se declaran en el archivo de encabezado de hello platform.h.</span><span class="sxs-lookup"><span data-stu-id="7180d-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="7180d-192">Examine las definiciones de Hola de estas funciones para la plataforma de destino en hello [repositorio](https://github.com/Azure/azure-iot-sdk-c) toodetermine si es necesario tooinclude cualquier código de inicialización específica de la plataforma en el cliente.</span><span class="sxs-lookup"><span data-stu-id="7180d-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="7180d-193">en primer lugar, toostart trabajar con bibliotecas de hello, asignar un identificador de cliente de centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="7180d-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="7180d-194">Pasar una copia de la cadena de conexión de dispositivo de Hola que obtuvo en función de hello dispositivo explorador herramienta toothis.</span><span class="sxs-lookup"><span data-stu-id="7180d-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="7180d-195">También se designa toouse de protocolo de comunicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="7180d-196">En este ejemplo se utiliza MQTT, pero también se pueden usar AMQP y HTTP.</span><span class="sxs-lookup"><span data-stu-id="7180d-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="7180d-197">Cuando haya válido **el centro de IOT\_cliente\_controlar**, puede iniciar una llamada a toosend de las API de Hola y recibir mensajes tooand centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7180d-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="7180d-198">Envío de mensajes</span><span class="sxs-lookup"><span data-stu-id="7180d-198">Send messages</span></span>

<span data-ttu-id="7180d-199">aplicación de ejemplo de Hola configura un centro de IoT de bucle toosend mensajes tooyour.</span><span class="sxs-lookup"><span data-stu-id="7180d-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="7180d-200">Hola siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="7180d-200">hello following snippet:</span></span>

- <span data-ttu-id="7180d-201">Crea un mensaje.</span><span class="sxs-lookup"><span data-stu-id="7180d-201">Creates a message.</span></span>
- <span data-ttu-id="7180d-202">Agrega un mensaje de toohello de propiedad.</span><span class="sxs-lookup"><span data-stu-id="7180d-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="7180d-203">Envía un mensaje.</span><span class="sxs-lookup"><span data-stu-id="7180d-203">Sends a message.</span></span>

<span data-ttu-id="7180d-204">Primero, cree un mensaje:</span><span class="sxs-lookup"><span data-stu-id="7180d-204">First, create a message:</span></span>

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

<span data-ttu-id="7180d-205">Cada vez que se envía un mensaje, especifique una función de devolución de llamada de tooa de referencia que se invoca cuando se envían datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="7180d-206">En este ejemplo, se llama la función de devolución de llamada de hello **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="7180d-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="7180d-207">Hola siguiente fragmento de código muestra esta función de devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="7180d-207">hello following snippet shows this callback function:</span></span>

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

<span data-ttu-id="7180d-208">Tenga en cuenta Hola llamada toohello **IoTHubMessage\_destruir** función cuando haya terminado con el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="7180d-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="7180d-209">Esta función libera recursos de hello asignados cuando se creó el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="7180d-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="7180d-210">Recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="7180d-210">Receive messages</span></span>

<span data-ttu-id="7180d-211">La recepción de mensajes es una operación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="7180d-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="7180d-212">En primer lugar, registrar hello tooinvoke de devolución de llamada cuando el dispositivo de hello recibe un mensaje:</span><span class="sxs-lookup"><span data-stu-id="7180d-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

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

<span data-ttu-id="7180d-213">Hola último parámetro es un toowhatever de puntero void que desee.</span><span class="sxs-lookup"><span data-stu-id="7180d-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="7180d-214">En el ejemplo hello, es un entero de tooan de puntero, pero podría ser un puntero tooa estructura de datos más compleja.</span><span class="sxs-lookup"><span data-stu-id="7180d-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="7180d-215">Este parámetro permite toooperate de función de devolución de llamada de hello en estado compartido con un llamador de Hola de esta función.</span><span class="sxs-lookup"><span data-stu-id="7180d-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="7180d-216">Cuando el dispositivo de hello recibe un mensaje, hello función de devolución de llamada registrada se invoca.</span><span class="sxs-lookup"><span data-stu-id="7180d-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="7180d-217">Dicha función de devolución de llamada recupera:</span><span class="sxs-lookup"><span data-stu-id="7180d-217">This callback function retrieves:</span></span>

* <span data-ttu-id="7180d-218">Id. de mensaje de Hola y el Id. de correlación del mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="7180d-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="7180d-219">contenido del mensaje Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-219">hello message content.</span></span>
* <span data-ttu-id="7180d-220">Las propiedades personalizadas de mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="7180d-220">Any custom properties from hello message.</span></span>

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

<span data-ttu-id="7180d-221">Hola de uso **IoTHubMessage\_GetByteArray** mensaje de saludo de función tooretrieve, que en este ejemplo es una cadena.</span><span class="sxs-lookup"><span data-stu-id="7180d-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="7180d-222">Cancelar la inicialización Hola biblioteca</span><span class="sxs-lookup"><span data-stu-id="7180d-222">Uninitialize hello library</span></span>

<span data-ttu-id="7180d-223">Cuando haya terminado de enviar eventos y recibir mensajes, se puede cancelar la inicialización Hola IoT biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7180d-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="7180d-224">toodo por lo tanto, emita Hola después de la llamada de función:</span><span class="sxs-lookup"><span data-stu-id="7180d-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="7180d-225">Esta llamada se libere recursos Hola previamente asignados por hello **IoTHubClient\_CreateFromConnectionString** (función).</span><span class="sxs-lookup"><span data-stu-id="7180d-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="7180d-226">Como puede ver, es fácil toosend y recibir mensajes con hello **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7180d-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="7180d-227">biblioteca de Hello controla los detalles de hello de la comunicación con el centro de IoT, incluidos lo toouse de protocolo (desde la perspectiva de Hola de desarrollador de hello, esta es una opción de configuración simple).</span><span class="sxs-lookup"><span data-stu-id="7180d-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="7180d-228">Hola **IoTHubClient** biblioteca también proporciona un control preciso sobre cómo datos de hello tooserialize el dispositivo envía tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="7180d-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="7180d-229">En algunos casos, este nivel de control representa una ventaja, pero en otros es un detalle de implementación que no desea toobe preocupan.</span><span class="sxs-lookup"><span data-stu-id="7180d-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="7180d-230">Si ese es el caso de hello, puede considerar el uso de hello **serializador** biblioteca, que se describe en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="7180d-231">Utilizar la biblioteca de serializador de Hola</span><span class="sxs-lookup"><span data-stu-id="7180d-231">Use hello serializer library</span></span>

<span data-ttu-id="7180d-232">Hola conceptualmente **serializador** biblioteca se ubica en la parte superior hello **IoTHubClient** biblioteca Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="7180d-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="7180d-233">Usa hello **IoTHubClient** biblioteca para hello subyacente comunicación con el centro de IoT, pero agrega capacidades de modelado que eliminan la carga de Hola de trabajar con la serialización del mensaje del programador de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="7180d-234">Un ejemplo ilustra mejor el funcionamiento de esta biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7180d-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="7180d-235">Hola interior **serializador** carpeta Hola [repositorio de azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), es un **ejemplos** carpeta que contenga una aplicación denominada **simplesample \_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="7180d-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="7180d-236">la versión de Windows Hello de este ejemplo incluye Hola después de solución de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="7180d-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="7180d-237">Si abre este proyecto en Visual Studio de 2017, acepte mensajes hello toohello tooretarget Hola proyecto última versión.</span><span class="sxs-lookup"><span data-stu-id="7180d-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="7180d-238">Al igual que con el ejemplo anterior de hello, éste incluye varios paquetes de NuGet:</span><span class="sxs-lookup"><span data-stu-id="7180d-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="7180d-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="7180d-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="7180d-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="7180d-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="7180d-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="7180d-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="7180d-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="7180d-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="7180d-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="7180d-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="7180d-244">Ha visto la mayoría de estos paquetes en el ejemplo de Hola a anterior, pero **Microsoft.Azure.IoTHub.Serializer** es nuevo.</span><span class="sxs-lookup"><span data-stu-id="7180d-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="7180d-245">Este paquete es necesario cuando se utiliza hello **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7180d-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="7180d-246">Implementación de Hola de aplicación de ejemplo de Hola se puede encontrar en hello **simplesample\_mqtt.c** archivo.</span><span class="sxs-lookup"><span data-stu-id="7180d-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="7180d-247">Hello secciones siguientes le guían por partes principales de Hola de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7180d-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="7180d-248">Inicializar la biblioteca de Hola</span><span class="sxs-lookup"><span data-stu-id="7180d-248">Initialize hello library</span></span>

<span data-ttu-id="7180d-249">toostart trabajar con hello **serializador** biblioteca, llamada Hola inicialización API:</span><span class="sxs-lookup"><span data-stu-id="7180d-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

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

<span data-ttu-id="7180d-250">Hola llamada toohello **serializador\_init** función es una llamada de un solo uso e inicializa Hola biblioteca subyacente.</span><span class="sxs-lookup"><span data-stu-id="7180d-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="7180d-251">A continuación, se llama a hello **IoTHubClient\_LL\_CreateFromConnectionString** función, que es Hola misma API como en hello **IoTHubClient** ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7180d-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="7180d-252">Esta llamada establece la cadena de conexión del dispositivo (esta llamada es también donde elegir protocolo Hola desea toouse).</span><span class="sxs-lookup"><span data-stu-id="7180d-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="7180d-253">Este ejemplo utiliza MQTT como transporte de hello, pero podría utilizar AMQP o HTTP.</span><span class="sxs-lookup"><span data-stu-id="7180d-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="7180d-254">Por último, llame hello **crear\_modelo\_instancia** función.</span><span class="sxs-lookup"><span data-stu-id="7180d-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="7180d-255">**WeatherStation** es Hola espacio de nombres del modelo de Hola y **ContosoAnemometer** es Hola nombre del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="7180d-256">Una vez creada la instancia de modelo de hello, puede usar toostart enviar y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="7180d-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="7180d-257">Sin embargo, es importante toounderstand qué es un modelo.</span><span class="sxs-lookup"><span data-stu-id="7180d-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="7180d-258">Definir el modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="7180d-258">Define hello model</span></span>

<span data-ttu-id="7180d-259">Un modelo en hello **serializador** biblioteca define los mensajes de Hola que el dispositivo puede enviar tooIoT mensajes hello y concentrador, denominado *acciones* Hola modeling language, que se puede recibir.</span><span class="sxs-lookup"><span data-stu-id="7180d-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="7180d-260">Definir un modelo con un conjunto de macros de C en hello **simplesample\_mqtt** aplicación de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7180d-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="7180d-261">Hola **comenzar\_espacio de nombres** y **final\_espacio de nombres** macros ambos desconectar el espacio de nombres de Hola de modelo de hello como argumento.</span><span class="sxs-lookup"><span data-stu-id="7180d-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="7180d-262">Se espera que haya nada entre estas macros es una definición de Hola de su modelo o modelos y estructuras de datos de Hola que usan modelos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="7180d-263">En este ejemplo, hay un único modelo denominado **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="7180d-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="7180d-264">Este modelo define dos conjuntos de datos que el dispositivo puede enviar tooIoT concentrador: **DeviceId** y **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="7180d-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="7180d-265">También define tres acciones (mensajes) que el dispositivo puede recibir: **TurnFanOn**, **TurnFanOff** y **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="7180d-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="7180d-266">Cada elemento de datos tiene un tipo y cada acción tiene un nombre (y, opcionalmente, un conjunto de parámetros).</span><span class="sxs-lookup"><span data-stu-id="7180d-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="7180d-267">datos de Hola y las acciones definidas en el modelo de hello definen una superficie de API que puede usar toosend mensajes tooIoT concentrador y responder toomessages enviado toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7180d-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="7180d-268">El uso de este modelo se entiende mejor con un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7180d-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="7180d-269">Envío de mensajes</span><span class="sxs-lookup"><span data-stu-id="7180d-269">Send messages</span></span>

<span data-ttu-id="7180d-270">modelo de Hello define los datos de hello puede enviar tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="7180d-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="7180d-271">En este ejemplo, que significa que uno de hello dos elementos de datos definidos mediante hello **WITH_DATA** macro.</span><span class="sxs-lookup"><span data-stu-id="7180d-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="7180d-272">Hay varios pasos a necesario toosend **DeviceId** y **WindSpeed** centro de IoT tooan de valores.</span><span class="sxs-lookup"><span data-stu-id="7180d-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="7180d-273">Hola en primer lugar es datos de hello tooset desea toosend:</span><span class="sxs-lookup"><span data-stu-id="7180d-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="7180d-274">Hello modelo que se definió anteriormente le permite valores de hello tooset estableciendo los miembros de un **struct**.</span><span class="sxs-lookup"><span data-stu-id="7180d-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="7180d-275">A continuación, serializar mensajes de bienvenida que desee toosend:</span><span class="sxs-lookup"><span data-stu-id="7180d-275">Next, serialize hello message you want toosend:</span></span>

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

<span data-ttu-id="7180d-276">Este código serializa el búfer de dispositivo para la nube tooa hello (que se hace referencia por **destino**).</span><span class="sxs-lookup"><span data-stu-id="7180d-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="7180d-277">código de Hello, a continuación, invoca hello **sendMessage** función toosend Hola mensaje tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="7180d-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

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


<span data-ttu-id="7180d-278">Hola segundo parámetro toolast de **IoTHubClient\_LL\_SendEventAsync** es una función de devolución de llamada de tooa de referencia que se llama cuando se envían correctamente datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="7180d-279">Aquí se muestra la función de devolución de llamada de hello en el ejemplo hello:</span><span class="sxs-lookup"><span data-stu-id="7180d-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="7180d-280">Hola segundo parámetro es un contexto de toouser puntero; Hola mismo puntero pasa demasiado**IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="7180d-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="7180d-281">En este caso, el contexto de hello es un contador simple, pero puede ser que desee.</span><span class="sxs-lookup"><span data-stu-id="7180d-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="7180d-282">Eso es todo lo hay mensajes de dispositivo a la nube de toosending.</span><span class="sxs-lookup"><span data-stu-id="7180d-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="7180d-283">Hello sólo lo dejado toocover es cómo tooreceive mensajes.</span><span class="sxs-lookup"><span data-stu-id="7180d-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="7180d-284">Recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="7180d-284">Receive messages</span></span>

<span data-ttu-id="7180d-285">Recibir un mensaje funciona del mismo modo toohello funcionamiento de mensajes de Hola **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7180d-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="7180d-286">En primer lugar, se registra una función de devolución de llamada de mensaje:</span><span class="sxs-lookup"><span data-stu-id="7180d-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="7180d-287">A continuación, puede escribir la función de devolución de llamada de Hola que se invoca cuando se recibe un mensaje:</span><span class="sxs-lookup"><span data-stu-id="7180d-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

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

<span data-ttu-id="7180d-288">Este código es reutilizable, ha Hola mismo para cualquier solución.</span><span class="sxs-lookup"><span data-stu-id="7180d-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="7180d-289">Esta función recibe mensajes de bienvenida y se encarga de enrutarlo toohello función adecuada a través de la llamada de hello demasiado**EXECUTE\_comando**.</span><span class="sxs-lookup"><span data-stu-id="7180d-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="7180d-290">función Hello que se llama en este momento depende de definición de Hola de acciones de hello en el modelo.</span><span class="sxs-lookup"><span data-stu-id="7180d-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="7180d-291">Cuando se define una acción en el modelo, que se requiere tooimplement una función que se llama cuando el dispositivo recibe mensajes de bienvenida del correspondiente.</span><span class="sxs-lookup"><span data-stu-id="7180d-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="7180d-292">Por ejemplo, si el modelo define esta acción:</span><span class="sxs-lookup"><span data-stu-id="7180d-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="7180d-293">Defina una función con esta firma:</span><span class="sxs-lookup"><span data-stu-id="7180d-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="7180d-294">Tenga en cuenta cómo Hola nombre de función hello coincide con hello de acción de hello en el modelo de Hola y que Hola parámetros de función hello son Hola especificado para la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="7180d-295">primer parámetro de Hello siempre es necesario y contiene una instancia de toohello del puntero del modelo.</span><span class="sxs-lookup"><span data-stu-id="7180d-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="7180d-296">Cuando el dispositivo de hello recibe un mensaje que coincide con esta firma, se llama función correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="7180d-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="7180d-297">Por lo tanto, además de tener tooinclude Hola reutilizable código de **IoTHubMessage**, recibir mensajes es cuestión de definir una función sencilla para cada acción definida en el modelo.</span><span class="sxs-lookup"><span data-stu-id="7180d-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="7180d-298">Cancelar la inicialización Hola biblioteca</span><span class="sxs-lookup"><span data-stu-id="7180d-298">Uninitialize hello library</span></span>

<span data-ttu-id="7180d-299">Cuando haya terminado de enviar los datos y recibir mensajes, se puede cancelar la inicialización Hola IoT biblioteca:</span><span class="sxs-lookup"><span data-stu-id="7180d-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="7180d-300">Cada una de estas tres funciones se alinea con hello tres funciones de inicialización que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7180d-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="7180d-301">Llamar a estas API garantiza que se liberan los recursos asignados previamente.</span><span class="sxs-lookup"><span data-stu-id="7180d-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7180d-302">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7180d-302">Next Steps</span></span>

<span data-ttu-id="7180d-303">En este artículo se trata aspectos básicos de hello del uso de bibliotecas de Hola Hola **dispositivos de IoT de Azure SDK para C**. Que proporcionaba con suficiente toounderstand información qué se incluye en el SDK de Hola, su arquitectura y cómo tooget a trabajar con hello ejemplos de Windows.</span><span class="sxs-lookup"><span data-stu-id="7180d-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="7180d-304">artículo siguiente Hola continúa descripción Hola de hello SDK explicando [más información acerca de la biblioteca de hello IoTHubClient](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="7180d-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="7180d-305">toolearn más sobre el desarrollo de centro de IoT, vea hello [SDK de Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="7180d-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="7180d-306">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="7180d-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7180d-307">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="7180d-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

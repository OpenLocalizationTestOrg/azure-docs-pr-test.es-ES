---
title: SDK de dispositivo IoT de Azure para C | Microsoft Docs
description: "Introducción al SDK de dispositivo IoT de Azure para C e información sobre cómo crear aplicaciones para dispositivos que se comunican con un centro de IoT Hub."
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
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="1e1ef-103">SDK de dispositivo IoT de Azure para C</span><span class="sxs-lookup"><span data-stu-id="1e1ef-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="1e1ef-104">**SDK de dispositivo IoT de Azure para C** es un conjunto de bibliotecas diseñadas para simplificar el proceso de envío y recepción de mensajes desde el servicio **Azure IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="1e1ef-105">Hay distintas variantes del SDK, cada una dirigida a una plataforma concreta, pero este artículo describe el **SDK de dispositivo IoT de Azure para C**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="1e1ef-106">El SDK de dispositivo IoT de Azure para C está escrito en ANSI C (C99) para maximizar su portabilidad.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="1e1ef-107">Esta característica hace que las bibliotecas sean idóneas para operar en varias plataformas y dispositivos, especialmente si la prioridad es minimizar la superficie de la memoria y del disco.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="1e1ef-108">Existe una amplia gama de plataformas en las que se ha probado el SDK (consulte [Catálogo de dispositivos de Azure Certified for IoT](https://catalog.azureiotsuite.com/) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="1e1ef-109">Aunque este artículo incluye tutoriales con código de ejemplo que se ejecuta en la plataforma Windows, el código que describe en él es idéntico en todas las plataformas compatibles.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="1e1ef-110">En este artículo se presenta la arquitectura del SDK de dispositivo IoT de Azure para C. En él se muestra cómo inicializar la biblioteca de dispositivos, enviar datos a IoT Hub y recibir mensajes de dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="1e1ef-111">La información de este artículo debería ser suficiente para comenzar a usar el SDK, pero también se proporcionan referencias a información adicional sobre las bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="1e1ef-112">Arquitectura del SDK</span><span class="sxs-lookup"><span data-stu-id="1e1ef-112">SDK architecture</span></span>

<span data-ttu-id="1e1ef-113">Puede encontrar el [**SDK de dispositivo IoT de Azure para C**](https://github.com/Azure/azure-iot-sdk-c) en el repositorio de GitHub y ver los detalles de la API en la [referencia de la API de C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="1e1ef-114">La versión más reciente de las bibliotecas se puede encontrar en la rama **master** del repositorio:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="1e1ef-115">La implementación básica del SDK está en la carpeta **iothub\_client** que contiene la implementación de la capa inferior de la API del SDK: la biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="1e1ef-116">La biblioteca **IoTHubClient** contiene las API que implementan la mensajería sin formato tanto para enviar mensajes a IoT Hub como para recibirlos de él.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="1e1ef-117">Quien use esta biblioteca es responsable de la implementación de la serialización de mensajes, pero otros detalles de la comunicación con IoT Hub se controlan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="1e1ef-118">La carpeta **serializer** contiene funciones auxiliares y ejemplos que muestran cómo serializar los datos antes de enviarlos a Azure IoT Hub mediante la biblioteca de cliente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="1e1ef-119">El uso del serializador no es obligatorio y se proporciona como un recurso que puede resultar práctico.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="1e1ef-120">Para usar la biblioteca **serializer**, defina un modelo que especifique los datos que se envían a IoT Hub y los mensajes que se esperan recibir de él.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="1e1ef-121">Una vez definido el modelo, el SDK proporciona una superficie de API que permite trabajar fácilmente con mensajes del dispositivo a la nube y de la nube al dispositivo sin tener que preocuparse por los detalles de la serialización.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="1e1ef-122">La biblioteca depende de otras bibliotecas de código abierto que implementan el transporte mediante protocolos como MQTT y AMQP.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="1e1ef-123">La biblioteca **IoTHubClient** depende de otras bibliotecas de código abierto:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="1e1ef-124">La biblioteca [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility), que proporciona una funcionalidad común para las tareas básicas (como cadenas, manipulación de listas y E/S) necesarias en varios SDK de C relacionados con Azure.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="1e1ef-125">La biblioteca [Azure uAMQP](https://github.com/Azure/azure-uamqp-c), que es una implementación del lado cliente de AMQP optimizada para los dispositivos de restricción de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="1e1ef-126">La biblioteca [Azure uMQTT](https://github.com/Azure/azure-umqtt-c), que es una biblioteca de uso general que implementa el protocolo MQTT y que está optimizada para los dispositivos de restricción de recursos.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="1e1ef-127">El uso de estas bibliotecas se entiende más fácilmente si se examina el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="1e1ef-128">Las siguientes secciones le guiarán a través de varias aplicaciones de ejemplo que se incluyen en el SDK.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="1e1ef-129">Este tutorial le permitirá hacerse una idea muy aproximada de las distintas funcionalidades de las capas arquitectónicas del SDK y proporcionará una introducción al funcionamiento de las API.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="1e1ef-130">Antes de ejecutar los ejemplos</span><span class="sxs-lookup"><span data-stu-id="1e1ef-130">Before you run the samples</span></span>

<span data-ttu-id="1e1ef-131">Antes de ejecutar los ejemplos en el SDK de dispositivo IoT de Azure para C, debe [crear una instancia del servicio IoT Hub](iot-hub-create-through-portal.md) en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="1e1ef-132">Después complete las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="1e1ef-133">Preparación del entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-133">Prepare your development environment</span></span>
* <span data-ttu-id="1e1ef-134">Obtención de las credenciales del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="1e1ef-135">Preparación del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="1e1ef-135">Prepare your development environment</span></span>

<span data-ttu-id="1e1ef-136">Se proporcionan paquetes para plataformas comunes (como NuGet para Windows o apt_get para Debian y Ubuntu) y los ejemplos usan estos paquetes cuando estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="1e1ef-137">En algunos casos, es preciso compilar el SDK para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="1e1ef-138">Si necesita compilar el SDK, consulte [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) (Preparación de un entorno de desarrollo) en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="1e1ef-139">Para obtener el código de la aplicación de ejemplo, descargue una copia del SDK de GitHub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="1e1ef-140">Obtenga su copia del código fuente de la rama **master** del [repositorio de GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="1e1ef-141">Obtención de las credenciales del dispositivo</span><span class="sxs-lookup"><span data-stu-id="1e1ef-141">Obtain the device credentials</span></span>

<span data-ttu-id="1e1ef-142">Ahora que tiene el código fuente de ejemplo, lo siguiente que debe hacer es obtener un conjunto de credenciales del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="1e1ef-143">Para que un dispositivo pueda acceder a un centro de IoT, primero debe agregar el dispositivo al registro de identidad del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="1e1ef-144">Al agregar el dispositivo, se obtiene un conjunto de credenciales del dispositivo que se necesitan para que el dispositivo se pueda conectar al servicio IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="1e1ef-145">Las aplicaciones de ejemplo de la siguiente sección esperan que estas credenciales tengan la forma de una **cadena de conexión de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="1e1ef-146">Hay varias herramientas de código abierto que le ayudan a administrar IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="1e1ef-147">Una aplicación de Windows llamada [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="1e1ef-148">Una herramienta de la CLI de node.js multiplataforma llamada [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="1e1ef-149">En este tutorial se utiliza la herramienta gráfica *device explorer*.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="1e1ef-150">Sin embargo, si prefiere usar una herramienta CLI también puede usar la herramienta *iothub-explorer*.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="1e1ef-151">La herramienta device explorer usa las bibliotecas del servicio Azure IoT para realizar varias funciones en IoT Hub, entre las que se incluye la adición de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="1e1ef-152">Si usa la herramienta device explorer para agregar un dispositivo, obtiene una cadena de conexión para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="1e1ef-153">Esta cadena de conexión se necesita para ejecutar las aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="1e1ef-154">Si no está familiarizado con la herramienta device explorer, el siguiente procedimiento describe cómo usarla para agregar un dispositivo y obtener la cadena de conexión del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="1e1ef-155">Para instalar la herramienta device explorer, consulte [How to use Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) (Uso de la herramienta device explorer para dispositivos de IoT Hub).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="1e1ef-156">Al ejecutar el programa se ve esta interfaz:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="1e1ef-157">Escriba su **cadena de conexión del IoT Hub** en el primer campo y haga clic en **Update** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="1e1ef-158">Este paso configura la herramienta para que pueda comunicarse con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="1e1ef-159">Cuando se configura la cadena de conexión de IoT Hub, haga clic en la pestaña **Management** (Administración):</span><span class="sxs-lookup"><span data-stu-id="1e1ef-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="1e1ef-160">En esta pestaña se administran los dispositivos registrados en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="1e1ef-161">Para crear un dispositivo, haga clic en el botón **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="1e1ef-162">Se muestra un cuadro de diálogo con un conjunto de claves (principal y secundaria) previamente rellenadas.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="1e1ef-163">Escriba un valor en **Device ID** (Id. de dispositivo) y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="1e1ef-164">Cuando se crea el dispositivo, la lista de dispositivos se actualiza con todos los dispositivos registrados, incluido el que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="1e1ef-165">Si hace clic con el botón derecho en el dispositivo nuevo, verá este menú:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="1e1ef-166">Si elige la opción **Copy connection string for selected device** (Copiar cadena de conexión de dispositivo seleccionado), la cadena de conexión del dispositivo se copia en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="1e1ef-167">Mantenga una copia de la cadena de conexión de dispositivo,</span><span class="sxs-lookup"><span data-stu-id="1e1ef-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="1e1ef-168">ya que se necesita al ejecutar las aplicaciones de ejemplo que se describen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="1e1ef-169">Cuando haya completados los pasos anteriores, estará listo para empezar a ejecutar código.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="1e1ef-170">Ambos ejemplos tienen una constante en la parte superior del archivo de código fuente principal, que permite especificar una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="1e1ef-171">Por ejemplo, la línea correspondiente de la aplicación **iothub\_client\_sample\_mqtt** es como la siguiente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="1e1ef-172">Uso de la biblioteca IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="1e1ef-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="1e1ef-173">Dentro de la carpeta **iothub\_client**, en el repositorio [azure-iot-sdks](https://github.com/azure/azure-iot-sdk-c), hay una carpeta **samples** que contiene una aplicación denominada **iothub\_client\_sample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="1e1ef-174">La versión de Windows de la aplicación **iothub\_client\_sample\_mqtt** incluye la siguiente solución de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="1e1ef-175">Si abre este proyecto en Visual Studio de 2017, acepte las indicaciones para redestinar el proyecto a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="1e1ef-176">Esta solución contiene un proyecto.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-176">This solution contains a single project.</span></span> <span data-ttu-id="1e1ef-177">En esta solución hay cuatro paquetes de NuGet instalados:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="1e1ef-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="1e1ef-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="1e1ef-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="1e1ef-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="1e1ef-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="1e1ef-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="1e1ef-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="1e1ef-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="1e1ef-182">El paquete **Microsoft.Azure.C.SharedUtility** siempre es necesario al trabajar con el SDK.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="1e1ef-183">Este ejemplo usa el protocolo MQTT, por lo que es necesario incluir los paquetes **Microsoft.Azure.umqtt** y **Microsoft.Azure.IoTHub.MqttTransport** (hay paquetes equivalentes para MQTT y HTTP).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="1e1ef-184">Como en el ejemplo se usa la biblioteca **IoTHubClient**, se debe incluir también el paquete **Microsoft.Azure.IoTHub.IoTHubClient** en la solución.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="1e1ef-185">La implementación de la aplicación de ejemplo en se encuentra en el archivo de código fuente **iothub\_client\_sample\_mqtt.c**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="1e1ef-186">En los siguientes pasos se usa esta aplicación de ejemplo para guiarle por los requisitos necesarios para usar la biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="1e1ef-187">Inicialización de la biblioteca</span><span class="sxs-lookup"><span data-stu-id="1e1ef-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="1e1ef-188">Antes de empezar a trabajar con las bibliotecas, puede que necesite realizar alguna tarea de inicialización específica de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="1e1ef-189">Por ejemplo, si tiene previsto usar AMQP en Linux, debe inicializar la biblioteca OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="1e1ef-190">Los ejemplos del [repositorio de GitHub](https://github.com/Azure/azure-iot-sdk-c) llaman a la función **platform\_init** de la utilidad cuando el cliente se inicia y llaman a la función **platform\_deinit** antes de salir.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="1e1ef-191">Estas funciones se declaran en el archivo de encabezado platform.h.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="1e1ef-192">Examine las definiciones de estas funciones para la plataforma de destino del [repositorio](https://github.com/Azure/azure-iot-sdk-c) para determinar si necesita incluir código de inicialización específico de la plataforma en el cliente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="1e1ef-193">Para empezar a trabajar con las bibliotecas, primero asigne un identificador de cliente de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="1e1ef-194">Pase a esta función una copia de la cadena de conexión del dispositivo que obtuvo de la herramienta device explorer.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="1e1ef-195">Designe también el protocolo de comunicaciones que va a usar.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="1e1ef-196">En este ejemplo se utiliza MQTT, pero también se pueden usar AMQP y HTTP.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="1e1ef-197">Cuando tenga un valor **IOTHUB\_CLIENT\_HANDLE** válido, puede empezar a llamar a las API para enviar mensajes a IoT Hub y recibirlos de este.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="1e1ef-198">Envío de mensajes</span><span class="sxs-lookup"><span data-stu-id="1e1ef-198">Send messages</span></span>

<span data-ttu-id="1e1ef-199">La aplicación de ejemplo configura un bucle para enviar mensajes a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="1e1ef-200">El siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-200">The following snippet:</span></span>

- <span data-ttu-id="1e1ef-201">Crea un mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-201">Creates a message.</span></span>
- <span data-ttu-id="1e1ef-202">Agrega una propiedad al mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-202">Adds a property to the message.</span></span>
- <span data-ttu-id="1e1ef-203">Envía un mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-203">Sends a message.</span></span>

<span data-ttu-id="1e1ef-204">Primero, cree un mensaje:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="1e1ef-205">Cada vez que envía un mensaje, especifica una referencia a una función de devolución de llamada que se invoca cuando se envían los datos.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="1e1ef-206">En este ejemplo, la función de devolución de llamada de llama **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="1e1ef-207">El siguiente fragmento de código muestra dicha función:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-207">The following snippet shows this callback function:</span></span>

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

<span data-ttu-id="1e1ef-208">Observe la llamada a la función **IoTHubMessage\_Destroy** cuando termine con el mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="1e1ef-209">Esta función libera los recursos asignados al crear el mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="1e1ef-210">Recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="1e1ef-210">Receive messages</span></span>

<span data-ttu-id="1e1ef-211">La recepción de mensajes es una operación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="1e1ef-212">En primer lugar, se registra la devolución de llamada que se invocará cuando el dispositivo recibe un mensaje:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-212">First, you register the callback to invoke when the device receives a message:</span></span>

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

<span data-ttu-id="1e1ef-213">El último parámetro es un puntero nulo a lo que quiera.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="1e1ef-214">En el ejemplo, es un puntero a un entero, pero podría ser un puntero a una estructura de datos más compleja.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="1e1ef-215">Este parámetro permite que la función de devolución de llamada funcione en un estado compartido con el autor de la llamada de esta función.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="1e1ef-216">Cuando el dispositivo recibe un mensaje, se invoca la función de devolución de llamada registrada.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="1e1ef-217">Dicha función de devolución de llamada recupera:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-217">This callback function retrieves:</span></span>

* <span data-ttu-id="1e1ef-218">El identificador del mensaje y el identificador de correlación del mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="1e1ef-219">El contenido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-219">The message content.</span></span>
* <span data-ttu-id="1e1ef-220">Todas las propiedades personalizadas del mensaje.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-220">Any custom properties from the message.</span></span>

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
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
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

<span data-ttu-id="1e1ef-221">Use la función **IoTHubMessage\_GetByteArray** para recuperar el mensaje, que en este ejemplo es una cadena.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="1e1ef-222">Anulación de la inicialización de la biblioteca</span><span class="sxs-lookup"><span data-stu-id="1e1ef-222">Uninitialize the library</span></span>

<span data-ttu-id="1e1ef-223">Cuando haya terminado de enviar eventos y recibir de mensajes, puede anular la inicialización de la biblioteca de IoT.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="1e1ef-224">Para ello, emita la siguiente llamada de función:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="1e1ef-225">Esto libera los recursos asignados que previamente ha asignado la función **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="1e1ef-226">Como puede ver, es fácil enviar y recibir mensajes con la biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="1e1ef-227">La biblioteca controla los detalles de la comunicación con el Centro de IoT, incluido el protocolo que debe usar (desde la perspectiva del desarrollador, es una opción de configuración simple).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="1e1ef-228">La biblioteca **IoTHubClient** también proporciona un control preciso sobre el modo de serializar los datos que el dispositivo envía a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="1e1ef-229">En algunos casos este nivel de control es una ventaja, pero en otros es un detalle de la implementación por el que no desea preocuparse.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="1e1ef-230">En ese caso, puede considerar la posibilidad de usar la biblioteca **serializer**, que se describe en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="1e1ef-231">Uso de la biblioteca serializer</span><span class="sxs-lookup"><span data-stu-id="1e1ef-231">Use the serializer library</span></span>

<span data-ttu-id="1e1ef-232">Conceptualmente, la biblioteca **serializer** se encuentra encima de la biblioteca **IoTHubClient** en el SDK.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="1e1ef-233">Usa la biblioteca **IoTHubClient** para la comunicación subyacente con el Centro de IoT, pero incorpora funcionalidades de modelado que eliminan la carga de tratar con la serialización de mensajes del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="1e1ef-234">Un ejemplo ilustra mejor el funcionamiento de esta biblioteca.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="1e1ef-235">Dentro de la carpeta **serializer**, en el repositorio [azure-iot-sdks](https://github.com/Azure/azure-iot-sdk-c), hay una carpeta llamada **samples** que contiene una aplicación denominada **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="1e1ef-236">La versión de Windows de este ejemplo incluye la solución de Visual Studio siguiente:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="1e1ef-237">Si abre este proyecto en Visual Studio de 2017, acepte las indicaciones para redestinar el proyecto a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="1e1ef-238">Al igual que con el ejemplo anterior, esta incluye varios paquetes de NuGet:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="1e1ef-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="1e1ef-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="1e1ef-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="1e1ef-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="1e1ef-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="1e1ef-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="1e1ef-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="1e1ef-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="1e1ef-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="1e1ef-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="1e1ef-244">La mayoría de estos paquetes los ha visto en el ejemplo anterior, pero **Microsoft.Azure.IoTHub.Serializer** es nuevo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="1e1ef-245">Este paquete se requiere cuando se usa la biblioteca **serializer**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="1e1ef-246">La implementación de la aplicación de ejemplo se encuentra en el archivo **simplesample\_mqtt.c**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="1e1ef-247">Las secciones siguientes le guiarán por las partes principales de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="1e1ef-248">Inicialización de la biblioteca</span><span class="sxs-lookup"><span data-stu-id="1e1ef-248">Initialize the library</span></span>

<span data-ttu-id="1e1ef-249">Para empezar a trabajar con la biblioteca **serializer**, llame a las API de inicialización:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

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

<span data-ttu-id="1e1ef-250">La llamada a la función **serializer\_init** es de las que se realiza una sola vez e inicializa la biblioteca subyacente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="1e1ef-251">Después, se llama a la función **IoTHubClient\_LL\_CreateFromConnectionString**, que es la misma API del ejemplo **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="1e1ef-252">Esta llamada establece la cadena de conexión del dispositivo (también es donde se elige el protocolo que se desea usar).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="1e1ef-253">En este ejemplo se utiliza MQTT como transporte, pero se podrían utilizar AMQP o HTTP.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="1e1ef-254">Por último, llame a la función **CREATE\_MODEL\_INSTANCE**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="1e1ef-255">**WeatherStation** es el espacio de nombres del modelo y **ContosoAnemometer** es el nombre del modelo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="1e1ef-256">Una vez que se crea la instancia del modelo, se puede usar para empezar a enviar y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="1e1ef-257">Sin embargo, es importante entender qué es un modelo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="1e1ef-258">Definición del modelo</span><span class="sxs-lookup"><span data-stu-id="1e1ef-258">Define the model</span></span>

<span data-ttu-id="1e1ef-259">Un modelo de la biblioteca **serializer** define los mensajes que el dispositivo puede enviar a IoT Hub y los mensajes, denominados *acciones* en el lenguaje de modelado, que puede recibir.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="1e1ef-260">Un modelo se define mediante un conjunto de macros de C como en la aplicación de ejemplo **simplesample\_mqtt**:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="1e1ef-261">Ambas macros **BEGIN\_NAMESPACE** y **END\_NAMESPACE** toman el espacio de nombres del modelo como argumento.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="1e1ef-262">Se espera que todo lo que haya entre estas macros sea la definición del modelo, o modelos, y las estructuras de datos que usan los modelos.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="1e1ef-263">En este ejemplo, hay un único modelo denominado **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="1e1ef-264">Este modelo define dos partes de datos que el dispositivo puede enviar a IoT Hub: **DeviceId** y **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="1e1ef-265">También define tres acciones (mensajes) que el dispositivo puede recibir: **TurnFanOn**, **TurnFanOff** y **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="1e1ef-266">Cada elemento de datos tiene un tipo y cada acción tiene un nombre (y, opcionalmente, un conjunto de parámetros).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="1e1ef-267">Los datos y las acciones definidos en el modelo definen una superficie de API que se puede usar para enviar mensajes a IoT Hub y para responder a los mensajes que se envían al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="1e1ef-268">El uso de este modelo se entiende mejor con un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="1e1ef-269">Envío de mensajes</span><span class="sxs-lookup"><span data-stu-id="1e1ef-269">Send messages</span></span>

<span data-ttu-id="1e1ef-270">El modelo define los datos que puede enviar a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="1e1ef-271">En este ejemplo, eso significa que uno de los dos elementos de datos se define mediante la macro **WITH_DATA**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="1e1ef-272">Para enviar los valores **DeviceId** y **WindSpeed** a IoT Hub, es preciso seguir varios pasos.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="1e1ef-273">El primero es establecer los datos que se desean enviar:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="1e1ef-274">El modelo que definió anteriormente le permite establecer los valores mediante el establecimiento de los miembros de un tipo **struct**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="1e1ef-275">A continuación, serialice el mensaje que desee enviar:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="1e1ef-276">Este código serializa el dispositivo a la nube a un búfer (al que hace referencia **destination**).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="1e1ef-277">Luego, el código invoca a la función **sendMessage** para enviar el mensaje a IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="1e1ef-278">Del segundo al último parámetros de **IoTHubClient\_LL\_SendEventAsync** son una referencia a una función de devolución de llamada a la que se llama cuando los datos se envían correctamente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="1e1ef-279">Esta es la función de devolución de llamada del ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="1e1ef-280">El segundo parámetro es un puntero que lleva al contexto de usuario, el mismo puntero que se pasó a **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="1e1ef-281">En este caso, el contexto es un contador sencillo, pero puede ser lo que desee.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="1e1ef-282">Eso es todo lo necesario para enviar mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="1e1ef-283">Lo único que queda describir es cómo recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="1e1ef-284">Recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="1e1ef-284">Receive messages</span></span>

<span data-ttu-id="1e1ef-285">La recepción de un mensaje es similar a cómo funcionan los mensajes en la biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="1e1ef-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="1e1ef-286">En primer lugar, se registra una función de devolución de llamada de mensaje:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="1e1ef-287">Luego, se escribe la función de devolución de llamada que se invoca cuando se recibe un mensaje:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="1e1ef-288">Este código es repetitivo, lo que significa que es el mismo para cualquier solución.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="1e1ef-289">Esta función recibe el mensaje y se encarga de enrutarlo a la función adecuada mediante la llamada a **EXECUTE\_COMMAND**.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="1e1ef-290">La función a la que se llama en este punto depende de la definición de las acciones del modelo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="1e1ef-291">Cuando se define una acción en el modelo, es necesario implementar una función a la que se llama cuando el dispositivo recibe el mensaje correspondiente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="1e1ef-292">Por ejemplo, si el modelo define esta acción:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="1e1ef-293">Defina una función con esta firma:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="1e1ef-294">Observe que el nombre de la función coincide con el nombre de la acción en el modelo y que los parámetros de la función coinciden con los parámetros especificados para la acción.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="1e1ef-295">El primer parámetro siempre es necesario y contiene un puntero a la instancia del modelo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="1e1ef-296">Cuando el dispositivo recibe un mensaje que coincide con esta firma, se llama a la función correspondiente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="1e1ef-297">Por lo tanto, aparte de tener que incluir el código reutilizable de **IoTHubMessage**, para recibir mensajes solo hay que definir una función sencilla para cada acción definida en el modelo.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="1e1ef-298">Anulación de la inicialización de la biblioteca</span><span class="sxs-lookup"><span data-stu-id="1e1ef-298">Uninitialize the library</span></span>

<span data-ttu-id="1e1ef-299">Cuando haya terminado el envío de datos y la recepción de mensajes, puede anular la inicialización de la biblioteca de IoT:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="1e1ef-300">Cada una de estas tres funciones se corresponde con las tres funciones de inicialización descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="1e1ef-301">Llamar a estas API garantiza que se liberan los recursos asignados previamente.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e1ef-302">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e1ef-302">Next Steps</span></span>

<span data-ttu-id="1e1ef-303">Este artículo contiene los aspectos básicos del uso de las bibliotecas en el **SDK de dispositivo IoT de Azure para C**. Se le ha proporcionado información suficiente para conocer lo que incluye el SDK, su arquitectura y cómo empezar a trabajar con los ejemplos de Windows.</span><span class="sxs-lookup"><span data-stu-id="1e1ef-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="1e1ef-304">El siguiente artículo continúa la descripción del SDK y explica [más información sobre la biblioteca IoTHubClient](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="1e1ef-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="1e1ef-305">Para más información acerca del desarrollo para IoT Hub, consulte los [SDK de IoT Hub][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="1e1ef-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="1e1ef-306">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="1e1ef-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1e1ef-307">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1e1ef-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

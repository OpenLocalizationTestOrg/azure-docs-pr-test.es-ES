---
title: "Información de los SDK de IoT de Azure | Microsoft Docs"
description: "Guía del desarrollador: Información y vínculos a los diversos SDK de dispositivos y servicios IoT de Azure que puede usar para compilar aplicaciones de back-end y de aplicaciones de dispositivo."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bcbf4b9633f58293edb19aeb33dec6602ac4ec8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="e6ecb-103">SDK de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="e6ecb-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="e6ecb-104">Hay tres categorías de SDK para trabajar con IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="e6ecb-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="e6ecb-105">Los **SDK de dispositivos** permiten diseñar aplicaciones que se ejecuten en sus dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="e6ecb-106">Estas aplicaciones envían telemetría a IoT Hub y, de manera opcional, reciben mensajes de dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="e6ecb-107">Los **SDK de servicios** permiten administrar IoT Hub y, si se desea, enviar mensajes a los dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="e6ecb-108">**Azure IoT Edge** permite crear puertas de enlace para habilitar dispositivos que no utilicen uno de los protocolos compatibles, o bien cuando se necesite procesar mensajes en el perímetro.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-108">**Azure IoT Edge** enables you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="e6ecb-109">Los SDK se incluyen para admitir varios lenguajes de programación.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="e6ecb-110">SDK de dispositivos IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="e6ecb-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="e6ecb-111">Los SDK de dispositivos IoT de Microsoft Azure contienen código que facilita la creación dispositivos y aplicaciones que se conectan a servicios del Centro de IoT de Azure y que este administra.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="e6ecb-112">Los siguientes SDK de dispositivos IoT de Azure están disponibles para su descarga desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="e6ecb-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="e6ecb-113">[SDK de dispositivos IoT de Azure para C][lnk-c-device-sdk] escrito en ANSI C (C99) para portabilidad y amplia compatibilidad de plataformas.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="e6ecb-114">Hay dos bibliotecas de cliente de dispositivo para C, **iothub_client**de bako nivel y **serializer**.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-114">There are two device client libraries for C, the low-level **iothub_client** and the **serializer**.</span></span>
* <span data-ttu-id="e6ecb-115">[SDK de dispositivos IoT de Azure para .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="e6ecb-116">[SDK de dispositivos IoT de Azure para Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="e6ecb-117">[SDK de dispositivo IoT de Azure para Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="e6ecb-118">[SDK de dispositivo IoT de Azure para Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="e6ecb-119">Consulte los archivos Léame en los repositorios de GitHub para obtener información sobre el uso de administradores de paquetes específicos de la plataforma y el lenguaje para instalar los archivos binarios y dependencias en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-119">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="e6ecb-120">Compatibilidad de hardware y de plataformas de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e6ecb-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="e6ecb-121">Para más información sobre la compatibilidad del SDK con dispositivos de hardware específicos, consulte [Catálogo de dispositivos de Azure Certified for IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="e6ecb-121">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="e6ecb-122">SDK de servicios IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="e6ecb-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="e6ecb-123">Los SDK de servicios IoT de Azure contienen código que facilitan la creación de aplicaciones que interactúan directamente con IoT Hub para administrar dispositivos y seguridad.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-123">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="e6ecb-124">Los siguientes SDK de servicios IoT de Azure están disponibles para su descarga desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="e6ecb-124">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="e6ecb-125">[SDK de servicios IoT de Azure para .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="e6ecb-126">[SDK de servicios IoT de Azure para Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="e6ecb-127">[SDK de servicios IoT de Azure para Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="e6ecb-128">[SDK de servicios IoT de Azure para Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="e6ecb-129">[SDK de servicios de Azure IoT para C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="e6ecb-130">Consulte los archivos Léame en los repositorios de GitHub para obtener información sobre el uso de administradores de paquetes específicos de la plataforma y el lenguaje para instalar los archivos binarios y dependencias en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-130">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="e6ecb-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="e6ecb-131">Azure IoT Edge</span></span>

<span data-ttu-id="e6ecb-132">Azure IoT Edge contiene la infraestructura y los módulos necesarios para crear soluciones de puerta de enlace IoT.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-132">Azure IoT Edge contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="e6ecb-133">Puede ampliar IoT Edge para crear puertas de enlace aptas para cualquier escenario de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-133">You can extend IoT Edge to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="e6ecb-134">Puede descargar [Azure IoT Edge][lnk-iot-edge] desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="e6ecb-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="e6ecb-135">Documentación de referencia de la API en línea</span><span class="sxs-lookup"><span data-stu-id="e6ecb-135">Online API reference documentation</span></span>

<span data-ttu-id="e6ecb-136">La siguiente lista contiene vínculos a documentación en línea de referencia de API para bibliotecas de dispositivo, servicio y puerta de enlace IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="e6ecb-136">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="e6ecb-137">[.NET de Internet de las cosas (IoT)][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="e6ecb-138">[REST de IoT Hub][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="e6ecb-139">[SDK de dispositivo IoT de Azure para C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="e6ecb-140">[SDK de dispositivo IoT de Azure para Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="e6ecb-141">[SDK de servicios IoT de Azure para Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="e6ecb-142">[SDK de dispositivo IoT de Azure para Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="e6ecb-143">[SDK de servicios IoT de Azure para Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="e6ecb-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6ecb-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6ecb-145">Next steps</span></span>

<span data-ttu-id="e6ecb-146">Otros temas de referencia en la Guía del desarrollador de IoT Hub son:</span><span class="sxs-lookup"><span data-stu-id="e6ecb-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="e6ecb-147">[IoT Hub endpoints][lnk-devguide-endpoints] (Puntos de conexión de IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="e6ecb-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="e6ecb-148">[Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos y trabajos][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="e6ecb-149">[Cuotas y limitación][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="e6ecb-150">[Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="e6ecb-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

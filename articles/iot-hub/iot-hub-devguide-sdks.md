---
title: Hola aaaUnderstand SDK de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - información sobre y vínculos toohello IoT de Azure dispositivo y el servicio SDK que pueden usar toobuild aplicaciones para dispositivos y aplicaciones de back-end."
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
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="02a45-103">SDK de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="02a45-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="02a45-104">Hay tres categorías de SDK para trabajar con IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="02a45-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="02a45-105">**SDK de dispositivos** le permiten aplicaciones toobuild que se ejecutan en los dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="02a45-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="02a45-106">Estas aplicaciones envían centro de IoT de telemetría tooyour y, opcionalmente, reciban mensajes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="02a45-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="02a45-107">**Servicio SDK** habilitar toomanage el centro de IoT y, opcionalmente, enviar mensajes de dispositivos de IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="02a45-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="02a45-108">**Borde de Azure IoT** permite toobuild dispositivos de tooenable puertas de enlace que no use uno de los protocolos de hello compatible o cuando necesite tooprocess mensajes en el borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="02a45-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="02a45-109">SDK están proporciona toosupport varios lenguajes de programación.</span><span class="sxs-lookup"><span data-stu-id="02a45-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="02a45-110">SDK de dispositivos IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="02a45-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="02a45-111">Hola SDK de dispositivos de Microsoft Azure IoT contienen código que facilita la creación dispositivos y aplicaciones que se conectan tooand se administran mediante servicios de centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="02a45-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="02a45-112">Hello SDK de dispositivos de IoT de Azure siguiente es toodownload disponible desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="02a45-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="02a45-113">[SDK de dispositivos IoT de Azure para C][lnk-c-device-sdk] escrito en ANSI C (C99) para portabilidad y amplia compatibilidad de plataformas.</span><span class="sxs-lookup"><span data-stu-id="02a45-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="02a45-114">Hay dos bibliotecas de cliente de dispositivo para C, hello bajo nivel **iothub_client** hello y **serializador**.</span><span class="sxs-lookup"><span data-stu-id="02a45-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="02a45-115">[SDK de dispositivos IoT de Azure para .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="02a45-116">[SDK de dispositivos IoT de Azure para Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="02a45-117">[SDK de dispositivo IoT de Azure para Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="02a45-118">[SDK de dispositivo IoT de Azure para Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="02a45-119">Vea archivos Léame de hello en repositorios de GitHub de Hola para obtener información sobre el uso de idioma y los archivos binarios de paquete específico de la plataforma administradores tooinstall y dependencias en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="02a45-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="02a45-120">Compatibilidad de hardware y de plataformas de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="02a45-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="02a45-121">Para obtener más información sobre la compatibilidad SDK con dispositivos de hardware específicos, vea hello [Azure Certified para el catálogo de dispositivos de IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="02a45-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="02a45-122">SDK de servicios IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="02a45-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="02a45-123">servicio de Hello IoT de Azure SDK contiene toofacilitate código compilar las aplicaciones que interactúan directamente con la seguridad y los dispositivos de centro de IoT toomanage.</span><span class="sxs-lookup"><span data-stu-id="02a45-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="02a45-124">Hello siguientes SDK de servicio de IoT de Azure es toodownload disponible desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="02a45-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="02a45-125">[SDK de servicios IoT de Azure para .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="02a45-126">[SDK de servicios IoT de Azure para Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="02a45-127">[SDK de servicios IoT de Azure para Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="02a45-128">[SDK de servicios IoT de Azure para Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="02a45-129">[SDK de servicios de Azure IoT para C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="02a45-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="02a45-130">Vea archivos Léame de hello en repositorios de GitHub de Hola para obtener información sobre el uso de idioma y los archivos binarios de paquete específico de la plataforma administradores tooinstall y dependencias en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="02a45-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="02a45-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="02a45-131">Azure IoT Edge</span></span>

<span data-ttu-id="02a45-132">Borde de IoT de Azure contiene Hola infraestructura y módulos toocreate soluciones de puerta de enlace IoT.</span><span class="sxs-lookup"><span data-stu-id="02a45-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="02a45-133">Puede ampliar el escenario to-end adaptadas a su gusto tooany de borde IoT toocreate puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="02a45-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="02a45-134">Puede descargar [Azure IoT Edge][lnk-iot-edge] desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="02a45-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="02a45-135">Documentación de referencia de la API en línea</span><span class="sxs-lookup"><span data-stu-id="02a45-135">Online API reference documentation</span></span>

<span data-ttu-id="02a45-136">Hello lista siguiente contiene documentación de referencia de API de vínculos tooonline de dispositivo, servicio y bibliotecas de puerta de enlace de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="02a45-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="02a45-137">[.NET de Internet de las cosas (IoT)][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="02a45-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="02a45-138">[REST de IoT Hub][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="02a45-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="02a45-139">[SDK de dispositivo IoT de Azure para C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="02a45-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="02a45-140">[SDK de dispositivo IoT de Azure para Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="02a45-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="02a45-141">[SDK de servicios IoT de Azure para Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="02a45-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="02a45-142">[SDK de dispositivo IoT de Azure para Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="02a45-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="02a45-143">[SDK de servicios IoT de Azure para Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="02a45-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="02a45-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="02a45-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="02a45-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02a45-145">Next steps</span></span>

<span data-ttu-id="02a45-146">Otros temas de referencia en la Guía del desarrollador de IoT Hub son:</span><span class="sxs-lookup"><span data-stu-id="02a45-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="02a45-147">[IoT Hub endpoints][lnk-devguide-endpoints] (Puntos de conexión de IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="02a45-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="02a45-148">[Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos y trabajos][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="02a45-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="02a45-149">[Cuotas y limitación][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="02a45-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="02a45-150">[Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="02a45-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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

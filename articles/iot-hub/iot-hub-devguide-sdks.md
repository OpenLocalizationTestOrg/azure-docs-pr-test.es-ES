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
# <a name="understand-and-use-azure-iot-sdks"></a>SDK de IoT de Azure

Hay tres categorías de SDK para trabajar con IoT Hub:

* **SDK de dispositivos** le permiten aplicaciones toobuild que se ejecutan en los dispositivos de IoT. Estas aplicaciones envían centro de IoT de telemetría tooyour y, opcionalmente, reciban mensajes desde el centro de IoT.

* **Servicio SDK** habilitar toomanage el centro de IoT y, opcionalmente, enviar mensajes de dispositivos de IoT tooyour.

* **Borde de Azure IoT** permite toobuild dispositivos de tooenable puertas de enlace que no use uno de los protocolos de hello compatible o cuando necesite tooprocess mensajes en el borde de Hola.

SDK están proporciona toosupport varios lenguajes de programación.

## <a name="azure-iot-device-sdks"></a>SDK de dispositivos IoT de Azure

Hola SDK de dispositivos de Microsoft Azure IoT contienen código que facilita la creación dispositivos y aplicaciones que se conectan tooand se administran mediante servicios de centro de IoT de Azure.

Hello SDK de dispositivos de IoT de Azure siguiente es toodownload disponible desde GitHub:

* [SDK de dispositivos IoT de Azure para C][lnk-c-device-sdk] escrito en ANSI C (C99) para portabilidad y amplia compatibilidad de plataformas. Hay dos bibliotecas de cliente de dispositivo para C, hello bajo nivel **iothub_client** hello y **serializador**.
* [SDK de dispositivos IoT de Azure para .NET][lnk-dotnet-device-sdk]
* [SDK de dispositivos IoT de Azure para Java][lnk-java-device-sdk]
* [SDK de dispositivo IoT de Azure para Node.js][lnk-node-device-sdk]
* [SDK de dispositivo IoT de Azure para Python][lnk-python-device-sdk]

> [!NOTE]
> Vea archivos Léame de hello en repositorios de GitHub de Hola para obtener información sobre el uso de idioma y los archivos binarios de paquete específico de la plataforma administradores tooinstall y dependencias en el equipo de desarrollo.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>Compatibilidad de hardware y de plataformas de sistema operativo

Para obtener más información sobre la compatibilidad SDK con dispositivos de hardware específicos, vea hello [Azure Certified para el catálogo de dispositivos de IoT][lnk-certified].

## <a name="azure-iot-service-sdks"></a>SDK de servicios IoT de Azure

servicio de Hello IoT de Azure SDK contiene toofacilitate código compilar las aplicaciones que interactúan directamente con la seguridad y los dispositivos de centro de IoT toomanage.

Hello siguientes SDK de servicio de IoT de Azure es toodownload disponible desde GitHub:

* [SDK de servicios IoT de Azure para .NET][lnk-dotnet-service-sdk]
* [SDK de servicios IoT de Azure para Node.js][lnk-node-service-sdk]
* [SDK de servicios IoT de Azure para Java][lnk-java-service-sdk]
* [SDK de servicios IoT de Azure para Python][lnk-python-service-sdk]
* [SDK de servicios de Azure IoT para C][lnk-c-service-sdk]

> [!NOTE]
> Vea archivos Léame de hello en repositorios de GitHub de Hola para obtener información sobre el uso de idioma y los archivos binarios de paquete específico de la plataforma administradores tooinstall y dependencias en el equipo de desarrollo.

## <a name="azure-iot-edge"></a>Azure IoT Edge

Borde de IoT de Azure contiene Hola infraestructura y módulos toocreate soluciones de puerta de enlace IoT. Puede ampliar el escenario to-end adaptadas a su gusto tooany de borde IoT toocreate puertas de enlace.

Puede descargar [Azure IoT Edge][lnk-iot-edge] desde GitHub.

## <a name="online-api-reference-documentation"></a>Documentación de referencia de la API en línea

Hello lista siguiente contiene documentación de referencia de API de vínculos tooonline de dispositivo, servicio y bibliotecas de puerta de enlace de IoT de Azure:

* [.NET de Internet de las cosas (IoT)][lnk-dotnet-ref]
* [REST de IoT Hub][lnk-rest-ref]
* [SDK de dispositivo IoT de Azure para C][lnk-c-ref]
* [SDK de dispositivo IoT de Azure para Java][lnk-java-ref]
* [SDK de servicios IoT de Azure para Java][lnk-java-service-ref]
* [SDK de dispositivo IoT de Azure para Node.js][lnk-node-ref]
* [SDK de servicios IoT de Azure para Node.js][lnk-node-service-ref]
* [Azure IoT Edge][lnk-gateway-ref]

## <a name="next-steps"></a>Pasos siguientes

Otros temas de referencia en la Guía del desarrollador de IoT Hub son:

* [IoT Hub endpoints][lnk-devguide-endpoints] (Puntos de conexión de IoT Hub)
* [Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos y trabajos][lnk-devguide-query]
* [Cuotas y limitación][lnk-devguide-quotas]
* [Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt]

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

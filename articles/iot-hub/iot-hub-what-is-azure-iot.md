---
title: soluciones de aaaAzure para Internet de las cosas (IoT Suite) | Documentos de Microsoft
description: "Información general sobre la arquitectura de una solución de IoT de ejemplo y cómo se relaciona con toodevices, Hola servicio del centro de IoT de Azure, SDK de dispositivos de IoT de Azure, SDK de servicio de IoT de Azure y otros servicios de Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a>Pasos siguientes

Azure IoT Hub es un servicio de Azure que permite la comunicación bidireccional fiable y segura entre el back-end de la solución y millones de dispositivos. Permite back-end de soluciones de Hola para:

* Recibir telemetría a escala de los dispositivos.
* Enrutar datos desde el procesador de eventos de flujo de tooa de dispositivos.
* Recibir cargas de archivos de los dispositivos.
* Enviar mensajes de la nube al dispositivo toospecific dispositivos.

Puede usar tooimplement centro de IoT finalizar su propia solución de nuevo. Además, centro de IoT incluye un dispositivos de tooprovision del registro usadas de identidad, sus credenciales de seguridad y su centro de IoT de derechos tooconnect toohello. toolearn más información acerca del centro de IoT, consulte [¿qué es el centro de IoT?] [lnk-iot-hub].

toolearn cómo centro de IoT de Azure permite la administración de dispositivos basada en estándares tooremotely administrar, configurar y actualizar los dispositivos, consulte [información general de administración de dispositivos con el centro de IoT][lnk-device-management].

tooimplement las aplicaciones de cliente en una amplia variedad de plataformas de hardware de dispositivos y sistemas operativos, puede usar dispositivos de IoT de Azure de hello SDK. dispositivo de Hello SDK incluye bibliotecas que facilitan el envío telemetría tooan IoT hub y la recepción en la nube al dispositivo de mensajes. Cuando se utilizan dispositivos de hello SDK, puede elegir entre varios toocommunicate de protocolos de red con el centro de IoT. toolearn más información, vea hello [obtener información acerca del dispositivo SDK][lnk-device-sdks].

tooget iniciado escribiendo código y ejecutar algunos ejemplos, vea hello [empezar a trabajar con el centro de IoT] [ lnk-getstarted] tutorial.

También puede interesarle [Conjunto de aplicaciones de IoT de Azure][lnk-iot-suite], que es una colección de soluciones preconfiguradas. Conjunto de IoT permite tooget a trabajar rápidamente y escalar IoT proyectos tooaddress IoT escenarios comunes, como la supervisión remota, la administración de activos y el mantenimiento predictivo.

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md

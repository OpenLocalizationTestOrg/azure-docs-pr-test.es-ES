---
title: Opciones de aaaAzure centro de IoT dispositivo a la nube | Documentos de Microsoft
description: "Guía del desarrollador - instrucciones sobre al cargar mensajes del dispositivo a la nube de toouse, las propiedades notificados o archivo para las comunicaciones de nube al dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Guía de comunicación de dispositivo a nube
Al enviar información de hello dispositivo aplicación toohello solución back-end, el centro de IoT expone tres opciones:

* [Mensajes de dispositivo a nube][lnk-d2c], para telemetría y alertas de series temporales.
* [Notifica propiedades] [ lnk-twins] para proporcionar información de estado de dispositivo como capacidades disponibles, las condiciones o estado de Hola de flujos de trabajo de ejecución prolongada. Por ejemplo, configuración y actualizaciones de software.
* [Cargas de archivos] [ lnk-fileupload] en medios lotes de telemetría grandes y archivos cargados por los dispositivos conectados de forma intermitente o comprimidos toosave ancho de banda.

Aquí es una comparación detallada de hello diversas opciones de comunicación de dispositivos a la nube.

|  | Mensajes de dispositivo a nube | Propiedades notificadas | Cargas de archivos |
| ---- | ------- | ---------- | ---- |
| Escenario | Serie temporal de telemetría y alertas. Por ejemplo, lotes de datos del sensor de 256 KB enviados cada cinco minutos. | Funcionalidades disponibles y condiciones. Por ejemplo, hello actual dispositivo modo de conectividad como red de telefonía móvil o Wi-Fi. Sincronización de flujos de trabajo de ejecución prolongada, como configuración y actualizaciones de software. | Archivos multimedia. Lotes de telemetría (generalmente comprimidos) de gran tamaño. |
| Almacenamiento y recuperación | Almacena temporalmente IoT hub, los días de too7. Solo lectura secuencial. | Almacena IoT hub en gemelas de dispositivo de Hola. Puede recuperar con hello [lenguaje de consultas del centro de IoT][lnk-query]. | Almacenadas en la cuenta de Azure Storage proporcionada por el usuario. |
| Tamaño | Los mensajes de too256 KB. | El tamaño máximo de las propiedades notificadas es 8 KB. | Tamaño máximo de archivo admitido por Azure Blob Storage. |
| Frecuencia | Alta. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. | Mediana. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. | Baja. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. |
| Protocol | Disponible en todos los protocolos. | Actualmente solo está disponible cuando se usa MQTT. | Disponible cuando se utiliza cualquier protocolo, pero requiere HTTP en el dispositivo de Hola. |

Es posible que una aplicación requiere información de envío de tooboth como una serie temporal de telemetría o alerta y también toomake estén disponibles en gemelas de dispositivo de Hola. En este escenario, puede elegir uno de hello siguientes opciones:

* aplicación de dispositivo de Hello envía un mensaje de dispositivo para la nube y notifica un cambio de propiedad.
* Hola solución back-end puede almacenar información de hello en las etiquetas del doble del dispositivo de hello cuando recibe mensajes de bienvenida.

Puesto que los mensajes del dispositivo a la nube permiten un rendimiento mucho mayor que las actualizaciones de dispositivo gemelas, a veces es deseable tooavoid actualización gemelas de dispositivo de Hola para cada mensaje de dispositivo a la nube.


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md

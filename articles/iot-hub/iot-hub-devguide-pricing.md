---
title: precios de Azure IoT Hub aaaUnderstand | Documentos de Microsoft
description: "Guía del desarrollador: información sobre cómo funcionan los precios y la medición con IoT Hub (se incluyen ejemplos)."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Información de precios de IoT Hub de Azure

[Centro de IoT de Azure precios] [ lnk-pricing] proporciona información general de hello en diferentes SKU y los precios de centro de IoT. Este artículo contiene información adicional acerca de cómo los mensajes de Hola que funcionalidades centro de IoT se miden como IoT hub.

## <a name="charges-per-operation"></a>Cargos por operación

| Operación | Información de facturación | 
| --------- | ------------------- |
| Operaciones de registro de identidad <br/> (crear, recuperar, enumerar, actualizar, eliminar) | No se aplicará ningún cargo. |
| Mensajes de dispositivo a nube | Los mensajes enviados correctamente se cobran en fragmentos de 4 KB por cada ingreso en IoT Hub; por ejemplo, un mensaje de 6 KB se cobra como dos mensajes. |
| Mensajes de nube a dispositivo | Los mensajes enviados correctamente se cobran en fragmentos de 4 KB; por ejemplo, un mensaje de 6 KB se cobra como dos mensajes. |
| Cargas de archivos | Transferencia de archivo tooAzure almacenamiento no se mide por centro de IoT. Los mensajes de inicio y finalización de transferencia de archivos se cobran como mensajes medidos en incrementos de 4 KB. Por ejemplo, transferir un archivo de 10 MB se cobran dos mensajes en suma toohello el costo de almacenamiento de Azure. |
| Métodos directos | Las solicitudes de métodos correctas se cobrarán en fragmentos de 4 KB; las respuestas con cuerpos no vacíos se cobran en fragmentos de 4 KB como mensajes adicionales. Dispositivos de toodisconnected de las solicitudes se cargan como mensajes en bloques de 4 KB. Por ejemplo, se aplicarán cargos a un método con un cuerpo de 6 KB que da como resultado una respuesta sin cuerpo de dispositivo de hello, como dos mensajes; un método con un cuerpo de 6 KB que da como resultado una respuesta de 1 KB de dispositivo de Hola se carga como dos mensajes de solicitud de hello y otro mensaje de respuesta de Hola. |
| Lecturas de dispositivos gemelos | Gemelas dispositivo lee desde el dispositivo de Hola y de solución de hello volver final se le cobrará como mensajes en fragmentos de 512 bytes. Por ejemplo, la lectura de un dispositivo gemelo de 6 KB se cobra como 12 mensajes. |
| Actualizaciones de dispositivos gemelos (etiquetas y propiedades) | Actualizaciones del dispositivo gemelas de Hola y Hola de dispositivos se cargan como mensajes en fragmentos de 512 bytes. Por ejemplo, la lectura de un dispositivo gemelo de 6 KB se cobra como 12 mensajes. |
| Consultas de dispositivos gemelos | Las consultas se cargan como mensajes según el tamaño de los resultados hello en fragmentos de 512 bytes. |
| Operaciones de trabajos <br/> (crear, actualizar, enumerar, eliminar) | No se aplicará ningún cargo. |
| Operaciones por dispositivo de trabajos | Las operaciones de trabajos (como actualizaciones de dispositivos gemelos y métodos) se cobran del modo habitual. Por ejemplo, un trabajo que dé como resultado 1000 llamadas de método con solicitudes de 1 KB y respuestas con cuerpo vacío se cobra como 1000 mensajes. |

> [!NOTE]
> Todos los tamaños se calculan teniendo en cuenta el tamaño de la carga de hello en bytes (tramas de protocolo se omiten). En el caso de mensajes (que tienen propiedades y cuerpo) tamaño Hola se calcula de forma independiente del protocolo, como se describe en hello [centro de IoT Guía del desarrollador de mensajería][lnk-message-size].

## <a name="example-1"></a>Ejemplo 1

Un dispositivo envía un mensaje de dispositivo para la nube de 1 KB por minuto tooIoT concentrador, que, a continuación, se lee con análisis de transmisiones de Azure. Hola solución back-end invoca un método (con una carga de 512 bytes) en el dispositivo de hello cada tootrigger de diez minutos una acción específica. dispositivo de Hello responde toohello método con un resultado de 200 bytes.

dispositivo de Hello consume 1 mensaje * 60 minutos * 24 horas = 1440 mensajes al día para mensajes de dispositivo a la nube de hello y 2 solicitud y respuesta * 6 veces por hora * 24 horas = 288 mensajes para los métodos de hello, para un total de mensajes de 1728 al día.

## <a name="example-2"></a>Ejemplo 2

Un dispositivo envía un mensaje del dispositivo a la nube de 100 KB cada hora. También actualiza su dispositivo gemelo con cargas útiles de 1 KB cada cuatro horas. solución de Hello volver finalizar, una vez al día, lecturas Hola 14 KB dispositivo gemelas y actualiza con las configuraciones de toochange de cargas de 512 bytes.

dispositivo de Hello consume 25 mensajes de (100KB / 4KB) * 24 horas para mensajes del dispositivo a la nube, además de 1 mensaje * 6 veces al día para las actualizaciones de dispositivo gemelas, para un total de 156 mensajes al día.
Hello back-end de soluciones consume gemelas de dispositivo de 28 mensajes (14KB/0,5 KB) tooread hello, además de 1 mensaje tooupdate que, para un total de 29 mensajes.

En total, dispositivos de Hola y Hola solución back-end consumen 185 mensajes al día.


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md

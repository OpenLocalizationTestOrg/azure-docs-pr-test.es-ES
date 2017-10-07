---
title: cargar el archivo aaaUse hello tooconfigure de portal de Azure | Documentos de Microsoft
description: "Cómo toouse Hola tooconfigure portal Azure carga el archivo de tooenable del centro de IoT desde dispositivos conectados. Incluye información acerca de cómo configurar la cuenta de almacenamiento de Azure de destino de Hola."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>Configurar cargas de archivos del centro de IoT con hello portal de Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Carga de archivos

Hola toouse [funcionalidad de carga de archivos en el centro de IoT][lnk-upload], primero debe asociar una cuenta de almacenamiento de Azure con el centro. Seleccione **cargar el archivo** toodisplay una lista de propiedades de carga de archivo para el centro de IoT de Hola que se está modificando.

![Archivo de vista del centro de IoT cargar la configuración en el portal de Hola][13]

**Contenedor de almacenamiento**: Use Hola tooselect portal Azure de un contenedor de blobs en una cuenta de almacenamiento de Azure con su tooassociate de suscripción de Azure actual con el centro de IoT. Si es necesario, puede crear una cuenta de almacenamiento de Azure en hello **cuentas de almacenamiento** contenedor hoja y blob en hello **contenedores** hoja. Centro de IoT genera automáticamente el URI de SAS con el contenedor de blobs de toothis de permisos de escritura para dispositivos toouse cuando cargan archivos.

![Ver contenedores de almacenamiento para cargar el archivo en el portal de Hola][14]

**Recibir notificaciones para los archivos cargados**: habilitar o deshabilitar las notificaciones de carga de archivo a través de alternancia de Hola.

**SAS TTL**: esta opción es hello time-to-live de hello SAS URI devuelto toohello dispositivo por centro de IoT. Establecer tooone hora de forma predeterminada, pero pueden ser valores tooother personalizados con control deslizante de Hola.

**Notificación de configuración de TTL predeterminado de archivos**: Hola tiempo de vida de una notificación de carga de archivo antes de que expire. Establecer tooone día de forma predeterminada, pero pueden ser valores tooother personalizados con control deslizante de Hola.

**Número máximo de entregas de notificación de archivos**: número de Hola de tiempo de espera hello toodeliver de intentos de centro de IoT una notificación de carga de archivo. Establecer too10 de forma predeterminada, pero pueden ser valores tooother personalizados con control deslizante Hola.

![Configurar la carga de archivos del centro de IoT en portal de Hola][15]

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de las capacidades de carga de archivo Hola de centro de IoT, consulte [cargar archivos desde un dispositivo] [ lnk-upload] Hola Guía del desarrollador de centro de IoT.

Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:

* [Administración masiva de dispositivos de IoT][lnk-bulk]
* [Métricas de IoT Hub][lnk-metrics]
* [Supervisión de operaciones][lnk-monitor]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con IoT Edge][lnk-iotedge]
* [Proteger la solución de IoT de hello masa][lnk-securing]

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md

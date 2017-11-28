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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="37725-104">Configurar cargas de archivos del centro de IoT con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="37725-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="37725-105">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="37725-105">File upload</span></span>

<span data-ttu-id="37725-106">Hola toouse [funcionalidad de carga de archivos en el centro de IoT][lnk-upload], primero debe asociar una cuenta de almacenamiento de Azure con el centro.</span><span class="sxs-lookup"><span data-stu-id="37725-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="37725-107">Seleccione **cargar el archivo** toodisplay una lista de propiedades de carga de archivo para el centro de IoT de Hola que se está modificando.</span><span class="sxs-lookup"><span data-stu-id="37725-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![Archivo de vista del centro de IoT cargar la configuración en el portal de Hola][13]

<span data-ttu-id="37725-109">**Contenedor de almacenamiento**: Use Hola tooselect portal Azure de un contenedor de blobs en una cuenta de almacenamiento de Azure con su tooassociate de suscripción de Azure actual con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="37725-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="37725-110">Si es necesario, puede crear una cuenta de almacenamiento de Azure en hello **cuentas de almacenamiento** contenedor hoja y blob en hello **contenedores** hoja.</span><span class="sxs-lookup"><span data-stu-id="37725-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="37725-111">Centro de IoT genera automáticamente el URI de SAS con el contenedor de blobs de toothis de permisos de escritura para dispositivos toouse cuando cargan archivos.</span><span class="sxs-lookup"><span data-stu-id="37725-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Ver contenedores de almacenamiento para cargar el archivo en el portal de Hola][14]

<span data-ttu-id="37725-113">**Recibir notificaciones para los archivos cargados**: habilitar o deshabilitar las notificaciones de carga de archivo a través de alternancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="37725-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="37725-114">**SAS TTL**: esta opción es hello time-to-live de hello SAS URI devuelto toohello dispositivo por centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="37725-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="37725-115">Establecer tooone hora de forma predeterminada, pero pueden ser valores tooother personalizados con control deslizante de Hola.</span><span class="sxs-lookup"><span data-stu-id="37725-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="37725-116">**Notificación de configuración de TTL predeterminado de archivos**: Hola tiempo de vida de una notificación de carga de archivo antes de que expire.</span><span class="sxs-lookup"><span data-stu-id="37725-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="37725-117">Establecer tooone día de forma predeterminada, pero pueden ser valores tooother personalizados con control deslizante de Hola.</span><span class="sxs-lookup"><span data-stu-id="37725-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="37725-118">**Número máximo de entregas de notificación de archivos**: número de Hola de tiempo de espera hello toodeliver de intentos de centro de IoT una notificación de carga de archivo.</span><span class="sxs-lookup"><span data-stu-id="37725-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="37725-119">Establecer too10 de forma predeterminada, pero pueden ser valores tooother personalizados con control deslizante Hola.</span><span class="sxs-lookup"><span data-stu-id="37725-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![Configurar la carga de archivos del centro de IoT en portal de Hola][15]

## <a name="next-steps"></a><span data-ttu-id="37725-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37725-121">Next steps</span></span>

<span data-ttu-id="37725-122">Para obtener más información acerca de las capacidades de carga de archivo Hola de centro de IoT, consulte [cargar archivos desde un dispositivo] [ lnk-upload] Hola Guía del desarrollador de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="37725-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="37725-123">Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="37725-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="37725-124">[Administración masiva de dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="37725-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="37725-125">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="37725-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="37725-126">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="37725-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="37725-127">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="37725-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="37725-128">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="37725-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="37725-129">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="37725-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="37725-130">[Proteger la solución de IoT de hello masa][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="37725-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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

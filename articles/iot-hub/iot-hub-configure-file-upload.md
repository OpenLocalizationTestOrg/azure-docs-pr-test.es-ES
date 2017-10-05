---
title: Uso de Azure Portal para configurar la carga de archivos | Microsoft Docs
description: "Describe cómo usar Azure Portal para configurar el centro de IoT Hub con el fin de habilitar las cargas de archivo desde dispositivos conectados. Incluye información sobre cómo configurar la cuenta de Azure Storage."
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
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="52366-104">Configuración de cargas de archivos de IoT Hub mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="52366-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="52366-105">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="52366-105">File upload</span></span>

<span data-ttu-id="52366-106">Para utilizar la [funcionalidad de carga de archivos en el centro de IoT Hub][lnk-upload], primero debe asociar una cuenta de Azure Storage con su centro.</span><span class="sxs-lookup"><span data-stu-id="52366-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="52366-107">Seleccione **Carga de archivos** para mostrar una lista de las propiedades de carga de archivos para el IoT Hub que se está modificando.</span><span class="sxs-lookup"><span data-stu-id="52366-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![Visualización de la configuración de carga de archivos de IoT Hub en el portal][13]

<span data-ttu-id="52366-109">**Contenedor de almacenamiento:** Use Azure Portal para seleccionar un contenedor de blobs en una cuenta de Azure Storage de su suscripción actual de Azure con el fin de asociarlo a su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="52366-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="52366-110">Si es necesario, puede crear una cuenta de Azure Storage en la hoja **Cuentas de almacenamiento** y el contenedor de blobs en la hoja **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="52366-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="52366-111">El Centro de IoT genera automáticamente identificadores URI de SAS con permisos de escritura en este contenedor de blobs para los dispositivos que se utilizarán cuando se carguen archivos.</span><span class="sxs-lookup"><span data-stu-id="52366-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![Visualización de contenedores de almacenamiento para la carga de archivos en el portal][14]

<span data-ttu-id="52366-113">**Receive notifications for uploaded files**(Recibir notificaciones para archivos cargados): habilite o deshabilite las notificaciones de carga de archivos mediante el botón de alternancia.</span><span class="sxs-lookup"><span data-stu-id="52366-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="52366-114">**SAS TTL**(TTL SAS): este valor es el periodo de vida de los URI de SAS que el Centro de IoT devuelve al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="52366-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="52366-115">Se establece en una hora de forma predeterminada, pero se puede personalizar con otros valores mediante el control deslizante.</span><span class="sxs-lookup"><span data-stu-id="52366-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="52366-116">**File notification settings default TTL**(TTL predeterminado de configuración de notificación de archivos): el periodo de vida de una notificación de carga de archivos antes de que caduque.</span><span class="sxs-lookup"><span data-stu-id="52366-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="52366-117">Se establece en un día de forma predeterminada, pero se puede personalizar con otros valores mediante el control deslizante.</span><span class="sxs-lookup"><span data-stu-id="52366-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="52366-118">**File notification maximum delivery count**(Número máximo de entregas de notificaciones de archivo): el número de veces que el Centro de IoT tratará de entregar una notificación de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="52366-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="52366-119">Se establece en 10 días de forma predeterminada, pero se puede personalizar con otros valores mediante el control deslizante.</span><span class="sxs-lookup"><span data-stu-id="52366-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![Configuración de la carga de archivos de IoT Hub en el portal][15]

## <a name="next-steps"></a><span data-ttu-id="52366-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52366-121">Next steps</span></span>

<span data-ttu-id="52366-122">Para información sobre las funcionalidades de carga archivos de IoT Hub, consulte [Upload files from a device][lnk-upload] (Carga de archivos desde un dispositivo) en la guía para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="52366-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="52366-123">Siga estos vínculos para más información sobre la administración del Centro de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="52366-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="52366-124">[Administración masiva de dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="52366-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="52366-125">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="52366-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="52366-126">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="52366-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="52366-127">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="52366-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="52366-128">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="52366-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="52366-129">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="52366-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="52366-130">[Protección total de la solución de IoT][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="52366-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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

---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 4: Table Storage | Microsoft Docs"
description: "Guardar mensajes Intel NUC tooyour centro de IoT, escribirlos tooAzure el almacenamiento de tabla y, a continuación, leerlos desde la nube de Hola."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: recuperar datos de la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="e4bf4-104">Lectura de mensajes guardados en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="e4bf4-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e4bf4-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="e4bf4-105">What you will do</span></span>

- <span data-ttu-id="e4bf4-106">Ejecutar la aplicación de ejemplo de puerta de enlace de hello en la puerta de enlace que envía el centro de IoT tooyour de mensajes.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="e4bf4-107">A continuación, ejecutar código de ejemplo en los mensajes de Hola host tooread de equipo en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-107">Then run a sample code on your host computer tooread hello messages in your Azure Table storage.</span></span> 

<span data-ttu-id="e4bf4-108">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e4bf4-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e4bf4-109">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="e4bf4-109">What you will learn</span></span>

<span data-ttu-id="e4bf4-110">¿Cómo toouse hello gulp herramienta toorun Hola ejemplo código tooread mensajes en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e4bf4-111">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="e4bf4-111">What you need</span></span>

<span data-ttu-id="e4bf4-112">Deben tener correctamente hello las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e4bf4-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="e4bf4-113">[Crear cuenta de almacenamiento de Azure de Hola y aplicación de Azure función hello](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="e4bf4-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="e4bf4-114">[Ejecutar la aplicación de ejemplo de puerta de enlace de hello](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span><span class="sxs-lookup"><span data-stu-id="e4bf4-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="e4bf4-115">[Lectura de mensajes desde el IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="e4bf4-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="e4bf4-116">Obtener cadenas de conexión de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e4bf4-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="e4bf4-117">Al principio de esta lección, creó correctamente una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="e4bf4-118">cadena de conexión de hello tooget de cuenta de almacenamiento de Azure de hello, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e4bf4-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="e4bf4-119">Enumere todas las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="e4bf4-120">Obtenga la cadena de conexión de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="e4bf4-121">Usar puerta de enlace de iot como valor de Hola de `{resource group name}` si no cambia el valor de hello en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-121">Use iot-gateway as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="e4bf4-122">Configurar conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="e4bf4-122">Configure hello device connection</span></span>

<span data-ttu-id="e4bf4-123">Hola de actualización `config-azure.json` de archivos para que el código de ejemplo de Hola que se ejecuta en el equipo de host de hello puede leer el mensaje en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="e4bf4-124">tooconfigure Hola conexión del dispositivo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e4bf4-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="e4bf4-125">Archivo de configuración de dispositivo abierto hello `config-azure.json` ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e4bf4-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuración](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="e4bf4-127">Reemplace `[Azure storage connection string]` con hello cadena de conexión de almacenamiento de Azure que ha adquirido.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="e4bf4-128">`[IoT hub connection string]` ya se debe haber sustituido en la sección [Lectura de mensajes en Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) de la lección 3.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="e4bf4-129">Lectura de mensajes en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="e4bf4-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="e4bf4-130">Ejecutar la aplicación de ejemplo de puerta de enlace de Hola y leer mensajes de almacenamiento de tabla de Azure, Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e4bf4-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="e4bf4-131">El centro de IoT desencadena el mensaje de toosave de aplicación de función de Azure en el almacenamiento de la tabla de Azure cuando llega un mensaje nuevo.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="e4bf4-132">Hola `gulp run` comando ejecuta la aplicación de ejemplo de puerta de enlace que envía el centro de IoT tooyour de mensajes.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="e4bf4-133">Con `table-storage` parámetro, también genera un Hola de tooreceive de proceso secundario guarda el mensaje en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="e4bf4-134">mensajes de saludo que se envían y reciben son Hola mostrados al instante en todos los mismo ventana en la consola Hola equipo host.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="e4bf4-135">instancia de aplicación de ejemplo de Hola se cerrará automáticamente en 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![Lectura en Gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="e4bf4-137">Resumen</span><span class="sxs-lookup"><span data-stu-id="e4bf4-137">Summary</span></span>

<span data-ttu-id="e4bf4-138">Mensajes de saludo de tooread de código de ejemplo de Hola haya ejecutado en el almacenamiento de Azure tabla guardado por la aplicación de la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bf4-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>

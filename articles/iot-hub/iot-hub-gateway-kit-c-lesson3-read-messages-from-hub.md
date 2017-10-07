---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 3: Lectura de mensajes | Microsoft Docs"
description: "Ejecutar código de ejemplo en los mensajes de saludo de tooread de equipo de host desde el centro de IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube hello, recopilación de datos en la nube, servicio de nube de iot, datos de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="7a803-104">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7a803-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7a803-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="7a803-105">What you will do</span></span>

- <span data-ttu-id="7a803-106">Ejecutar código de ejemplo en el host de equipo tooread mensajes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7a803-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="7a803-107">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7a803-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7a803-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="7a803-108">What you will learn</span></span>

<span data-ttu-id="7a803-109">¿Cómo toouse hello gulp mensajes de tooread herramienta desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7a803-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7a803-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="7a803-110">What you need</span></span>

- <span data-ttu-id="7a803-111">Hola aplicación de ejemplo Bilitar que se ejecutó correctamente en la lección 3.</span><span class="sxs-lookup"><span data-stu-id="7a803-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="7a803-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="7a803-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="7a803-113">cadena de conexión de dispositivo de Hello participa en el centro de IoT de dispositivo (SensorTag de TI o dispositivo simulado) tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="7a803-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="7a803-114">Hola cadena de conexión de base de datos central de IoT es registro, identidad toohello tooconnect usado en los dispositivos de Hola de IoT hub toomanage que se permiten tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7a803-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="7a803-115">Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7a803-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="7a803-116">Use `iot-gateway` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a803-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="7a803-117">Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7a803-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="7a803-118">`{my hub name}`es el nombre de Hola que especificó en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="7a803-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="7a803-119">Configurar conexión de dispositivo de hello para el código de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="7a803-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="7a803-120">Archivo de configuración de dispositivo de actualización hello `config-azure.json` para que pueda leer mensajes desde el centro de IoT en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="7a803-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="7a803-121">toodo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7a803-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="7a803-122">Abra `config-azure.json` en código de Visual Studio mediante la ejecución de hello siguiente comando en una ventana de consola:</span><span class="sxs-lookup"><span data-stu-id="7a803-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="7a803-123">Realizar Hola después reemplazos en hello `config-azure.json` archivo:</span><span class="sxs-lookup"><span data-stu-id="7a803-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![captura de pantalla de configuración de azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="7a803-125">Reemplace `[IoT hub connection string]` con hello cadena de conexión de base de datos central de IoT que ha adquirido.</span><span class="sxs-lookup"><span data-stu-id="7a803-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="7a803-126">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7a803-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="7a803-127">Si tiene un SensorTag de TI, asegúrese de que ya ha encendido su SensorTag.</span><span class="sxs-lookup"><span data-stu-id="7a803-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="7a803-128">Ejecutar la aplicación de ejemplo de puerta de enlace de Hola y leer mensajes de centro de IoT por hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7a803-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="7a803-129">comando de Hello ejecuta Hola Bilitar ejemplo de aplicación que lee y empaqueta los datos de temperatura del dispositivo simulado o SensorTag y envía el centro de IoT de hello mensaje tooyour cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="7a803-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="7a803-130">También genera un mensaje de saludo de tooreceive de proceso secundario.</span><span class="sxs-lookup"><span data-stu-id="7a803-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="7a803-131">mensajes de saludo que se envían y reciben son Hola mostrados al instante en todos los mismo ventana en la consola Hola equipo host.</span><span class="sxs-lookup"><span data-stu-id="7a803-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="7a803-132">instancia de aplicación de ejemplo de Hola se cerrará automáticamente en 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="7a803-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![Aplicación de ejemplo BLE con mensajes enviados y recibidos](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="7a803-134">Resumen</span><span class="sxs-lookup"><span data-stu-id="7a803-134">Summary</span></span>

<span data-ttu-id="7a803-135">Ha ejecutado un tooread de código de ejemplo mensajes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7a803-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="7a803-136">Ya está listo tooread mensajes de saludo que se almacenan en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="7a803-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a803-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7a803-137">Next steps</span></span>
[<span data-ttu-id="7a803-138">Creación de una instancia de Azure Function App y una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7a803-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)



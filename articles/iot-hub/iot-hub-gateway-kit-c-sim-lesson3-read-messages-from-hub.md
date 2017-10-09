---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 3: Lectura de mensajes | Microsoft Docs"
description: "Ejecutar código de ejemplo en los mensajes de saludo de tooread de equipo de host desde el centro de IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube hello, recopilación de datos en la nube, servicio de nube de iot, datos de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="27ad6-104">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="27ad6-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="27ad6-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="27ad6-105">What you will do</span></span>

- <span data-ttu-id="27ad6-106">Ejecutar código de ejemplo en el host de equipo tooread mensajes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="27ad6-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="27ad6-107">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="27ad6-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="27ad6-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="27ad6-108">What you will learn</span></span>

<span data-ttu-id="27ad6-109">¿Cómo toouse hello gulp mensajes de tooread herramienta desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="27ad6-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="27ad6-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="27ad6-110">What you need</span></span>

- <span data-ttu-id="27ad6-111">ejemplo de Hola a dispositivo simulado en [configurar y ejecutar una nube del dispositivo simulado cargar la aplicación de ejemplo](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="27ad6-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="27ad6-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="27ad6-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="27ad6-113">cadena de conexión de dispositivo de Hello participa en el centro de IoT de dispositivo simulado tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="27ad6-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="27ad6-114">Hola cadena de conexión de base de datos central de IoT es registro, identidad toohello tooconnect usado en los dispositivos de Hola de IoT hub toomanage que se permiten tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="27ad6-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="27ad6-115">Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="27ad6-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="27ad6-116">Use `iot-gateway` como valor de Hola de `{resource group name}` si no cambia.</span><span class="sxs-lookup"><span data-stu-id="27ad6-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="27ad6-117">Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="27ad6-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="27ad6-118">`{my hub name}`es el nombre de Hola que especificó en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="27ad6-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="27ad6-119">Configurar conexión de dispositivo de hello para el código de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="27ad6-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="27ad6-120">Actualizar configuraciones de conexión de IoT hub- and dispositivo en `config-azure.json` realizando Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27ad6-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="27ad6-121">Abra `config-azure.json` en código de Visual Studio mediante la ejecución de hello siguiente comando en una ventana de consola:</span><span class="sxs-lookup"><span data-stu-id="27ad6-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="27ad6-122">Realizar Hola después reemplazos en hello `config-azure.json` archivo:</span><span class="sxs-lookup"><span data-stu-id="27ad6-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![captura de pantalla de configuración de azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="27ad6-124">Reemplace `[IoT hub connection string]` con hello cadena de conexión de base de datos central de IoT.</span><span class="sxs-lookup"><span data-stu-id="27ad6-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="27ad6-125">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="27ad6-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="27ad6-126">Ejecutar aplicación de ejemplo de Hola simulada dispositivos y leer mensajes de centro de IoT por hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="27ad6-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="27ad6-127">comando de Hola ejecuta una aplicación Hola que envíe el centro de IoT de mensajes tooyour cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="27ad6-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="27ad6-128">También genera un mensaje de saludo de tooreceive de proceso secundario.</span><span class="sxs-lookup"><span data-stu-id="27ad6-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="27ad6-129">mensajes de saludo que se envían y reciben son Hola mostrados al instante en todos los mismo ventana en la consola Hola equipo host.</span><span class="sxs-lookup"><span data-stu-id="27ad6-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="27ad6-130">se cerrará la aplicación Hello en 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="27ad6-130">hello application will exit in 40 seconds.</span></span>

![Aplicación de ejemplo simulada con mensajes enviados y recibidos](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="27ad6-132">Resumen</span><span class="sxs-lookup"><span data-stu-id="27ad6-132">Summary</span></span>

<span data-ttu-id="27ad6-133">Ha ejecutado correctamente el centro de IoT tooyour datos de toosend de la aplicación de ejemplo de Hola con dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="27ad6-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="27ad6-134">También ha leído los mensajes de saludo que se han enviado tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="27ad6-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27ad6-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="27ad6-135">Next steps</span></span>
[<span data-ttu-id="27ad6-136">Creación de una instancia de Azure Function App y una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="27ad6-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)



---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 3: Lectura de mensajes | Microsoft Docs"
description: "Ejecute el código de ejemplo en el equipo host para leer los mensajes en IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube, recopilación de datos en la nube, servicio en la nube de iot, datos de iot"
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
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="224a5-104">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="224a5-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="224a5-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="224a5-105">What you will do</span></span>

- <span data-ttu-id="224a5-106">Ejecute el código de ejemplo en el equipo host para leer los mensajes en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="224a5-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="224a5-107">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="224a5-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="224a5-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="224a5-108">What you will learn</span></span>

<span data-ttu-id="224a5-109">Uso de la herramienta Gulp para leer mensajes en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="224a5-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="224a5-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="224a5-110">What you need</span></span>

- <span data-ttu-id="224a5-111">El ejemplo de dispositivo simulado en [Configuración y ejecución de una aplicación de ejemplo de carga en la nube del dispositivo simulado](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="224a5-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="224a5-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="224a5-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="224a5-113">El dispositivo simulado utiliza la cadena de conexión del dispositivo para conectarse a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="224a5-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="224a5-114">La cadena de conexión de IoT Hub se utiliza para conectar con el registro de identidad en IoT Hub para administrar los dispositivos que pueden conectarse con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="224a5-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="224a5-115">Enumere todas las instancias de IoT Hub del grupo de recursos mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="224a5-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="224a5-116">Use `iot-gateway` como valor de `{resource group name}`, en caso de que no lo haya modificado.</span><span class="sxs-lookup"><span data-stu-id="224a5-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="224a5-117">Obtenga la cadena de conexión de IoT Hub mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="224a5-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="224a5-118">`{my hub name}` es el nombre que especificó en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="224a5-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="224a5-119">Configuración de la conexión de dispositivos para el código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="224a5-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="224a5-120">Actualice las configuraciones de IoT Hub y de la conexión de dispositivos en `config-azure.json` mediante estos pasos:</span><span class="sxs-lookup"><span data-stu-id="224a5-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="224a5-121">Abra `config-azure.json` en Visual Studio Code mediante la ejecución del siguiente comando en una ventana de consola:</span><span class="sxs-lookup"><span data-stu-id="224a5-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="224a5-122">Realice las sustituciones siguientes en el archivo `config-azure.json`:</span><span class="sxs-lookup"><span data-stu-id="224a5-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![captura de pantalla de configuración de azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="224a5-124">Reemplace `[IoT hub connection string]` con la cadena de conexión de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="224a5-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="224a5-125">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="224a5-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="224a5-126">Ejecute la aplicación de ejemplo del dispositivo simulado y lea los mensajes de IoT Hub mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="224a5-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="224a5-127">El comando ejecuta la aplicación que envía mensajes a IoT Hub cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="224a5-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="224a5-128">También genera un proceso secundario para recibir el mensaje.</span><span class="sxs-lookup"><span data-stu-id="224a5-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="224a5-129">Todos los mensajes que se envían y reciben se muestran al instante en la misma ventana de consola del equipo host.</span><span class="sxs-lookup"><span data-stu-id="224a5-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="224a5-130">La aplicación se cerrará en 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="224a5-130">The application will exit in 40 seconds.</span></span>

![Aplicación de ejemplo simulada con mensajes enviados y recibidos](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="224a5-132">Resumen</span><span class="sxs-lookup"><span data-stu-id="224a5-132">Summary</span></span>

<span data-ttu-id="224a5-133">Ha ejecutado correctamente la aplicación de ejemplo para enviar datos a IoT Hub con el dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="224a5-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="224a5-134">También ha leído los mensajes que se han enviado a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="224a5-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="224a5-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="224a5-135">Next steps</span></span>
[<span data-ttu-id="224a5-136">Creación de una instancia de Azure Function App y una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="224a5-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)



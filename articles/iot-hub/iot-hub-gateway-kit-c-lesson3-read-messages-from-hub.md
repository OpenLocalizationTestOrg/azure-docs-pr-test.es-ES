---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 3: Lectura de mensajes | Microsoft Docs"
description: "Ejecute el código de ejemplo en el equipo host para leer los mensajes en IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube, recopilación de datos en la nube, servicio en la nube de iot, datos de iot"
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
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="42e9e-104">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="42e9e-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="42e9e-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="42e9e-105">What you will do</span></span>

- <span data-ttu-id="42e9e-106">Ejecute el código de ejemplo en el equipo host para leer los mensajes en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="42e9e-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="42e9e-107">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="42e9e-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="42e9e-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="42e9e-108">What you will learn</span></span>

<span data-ttu-id="42e9e-109">Uso de la herramienta Gulp para leer mensajes en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="42e9e-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="42e9e-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="42e9e-110">What you need</span></span>

- <span data-ttu-id="42e9e-111">La aplicación de ejemplo BLE que se ejecutó correctamente en la lección 3.</span><span class="sxs-lookup"><span data-stu-id="42e9e-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="42e9e-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="42e9e-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="42e9e-113">El dispositivo (SensorTag de TI o dispositivo simulado) utiliza la cadena de conexión del dispositivo para conectarse a la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="42e9e-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="42e9e-114">La cadena de conexión de IoT Hub se utiliza para conectar con el registro de identidades en IoT Hub para administrar los dispositivos que pueden conectarse con su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="42e9e-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="42e9e-115">Enumere todas las instancias de IoT Hub del grupo de recursos mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="42e9e-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="42e9e-116">Use `iot-gateway` como valor de `{resource group name}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="42e9e-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="42e9e-117">Obtenga la cadena de conexión de IoT Hub mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="42e9e-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="42e9e-118">`{my hub name}` es el nombre que especificó en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="42e9e-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="42e9e-119">Configuración de la conexión de dispositivos para el código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="42e9e-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="42e9e-120">Actualice el archivo de configuración de dispositivos `config-azure.json` para que pueda leer mensajes desde su instancia de IoT Hub en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="42e9e-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="42e9e-121">Para ello, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="42e9e-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="42e9e-122">Abra `config-azure.json` en Visual Studio Code mediante la ejecución del siguiente comando en una ventana de consola:</span><span class="sxs-lookup"><span data-stu-id="42e9e-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="42e9e-123">Realice las sustituciones siguientes en el archivo `config-azure.json`:</span><span class="sxs-lookup"><span data-stu-id="42e9e-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![captura de pantalla de configuración de azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="42e9e-125">Reemplace `[IoT hub connection string]` con la cadena de conexión de IoT Hub obtenida.</span><span class="sxs-lookup"><span data-stu-id="42e9e-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="42e9e-126">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="42e9e-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="42e9e-127">Si tiene un SensorTag de TI, asegúrese de que ya ha encendido su SensorTag.</span><span class="sxs-lookup"><span data-stu-id="42e9e-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="42e9e-128">Ejecute la aplicación de ejemplo de la puerta de enlace y lea los mensajes de IoT Hub mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="42e9e-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="42e9e-129">El comando ejecuta la aplicación de ejemplo BLE que lee y empaqueta los datos de temperatura del dispositivo simulado o SensorTag, y envía el mensaje a su instancia de IoT Hub cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="42e9e-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="42e9e-130">También genera un proceso secundario para recibir el mensaje.</span><span class="sxs-lookup"><span data-stu-id="42e9e-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="42e9e-131">Todos los mensajes que se envían y se reciben se muestran al instante en la misma ventana de consola del equipo host.</span><span class="sxs-lookup"><span data-stu-id="42e9e-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="42e9e-132">La instancia de la aplicación de ejemplo se cerrará automáticamente en 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="42e9e-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![Aplicación de ejemplo BLE con mensajes enviados y recibidos](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="42e9e-134">Resumen</span><span class="sxs-lookup"><span data-stu-id="42e9e-134">Summary</span></span>

<span data-ttu-id="42e9e-135">Ha ejecutado un código de ejemplo para leer los mensajes de su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="42e9e-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="42e9e-136">Está listo para leer los mensajes que se almacenan en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="42e9e-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42e9e-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42e9e-137">Next steps</span></span>
[<span data-ttu-id="42e9e-138">Creación de una instancia de Azure Function App y una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="42e9e-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)



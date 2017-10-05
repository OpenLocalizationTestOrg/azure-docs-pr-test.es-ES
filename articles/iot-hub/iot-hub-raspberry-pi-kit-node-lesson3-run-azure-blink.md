---
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 3: Ejecución del ejemplo | Microsoft Docs"
description: "Implemente y ejecute una aplicación de ejemplo para Raspberry Pi 3 que envíe mensajes a IoT Hub y haga parpadear el LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: pi en la nube con parpadeo del led, parpadeo del led desde la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="02bf9-104">Ejecución de una aplicación de ejemplo para enviar mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="02bf9-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="02bf9-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="02bf9-105">What you will do</span></span>
<span data-ttu-id="02bf9-106">En este artículo, se explica cómo implementar y ejecutar una aplicación de ejemplo en Raspberry Pi 3 que envía mensajes a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02bf9-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="02bf9-107">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="02bf9-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="02bf9-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="02bf9-108">What you will learn</span></span>
<span data-ttu-id="02bf9-109">Aprenderá a utilizar la herramienta de Gulp para implementar y ejecutar la aplicación de ejemplo Node.js en Pi.</span><span class="sxs-lookup"><span data-stu-id="02bf9-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="02bf9-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="02bf9-110">What you need</span></span>
* <span data-ttu-id="02bf9-111">Para comenzar esta tarea, debe haber completado correctamente el tutorial [Creación de una instancia de Azure Function App y una cuenta de Azure Storage para procesar y guardar mensajes de IoT Hub](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="02bf9-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="02bf9-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="02bf9-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="02bf9-113">La cadena de conexión de dispositivos se utiliza para conectar Pi con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02bf9-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="02bf9-114">La cadena de conexión de IoT Hub se utiliza para conectar con el registro de identidad en IoT Hub para administrar los dispositivos que pueden conectarse con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02bf9-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="02bf9-115">Enumere todos los centros de IoT Hub del grupo de recursos ejecutando el siguiente comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="02bf9-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="02bf9-116">Use `iot-sample` como valor de `{resource group name}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="02bf9-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="02bf9-117">Obtenga la cadena de conexión de IoT Hub ejecutando el siguiente comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="02bf9-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="02bf9-118">`{my hub name}` es el nombre que especificó cuando creó el centro de IoT Hub y registró Pi.</span><span class="sxs-lookup"><span data-stu-id="02bf9-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="02bf9-119">Obtenga la cadena de conexión de dispositivos ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="02bf9-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="02bf9-120">Use `myraspberrypi` como valor de `{device id}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="02bf9-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="02bf9-121">Configuración de la conexión de dispositivos</span><span class="sxs-lookup"><span data-stu-id="02bf9-121">Configure the device connection</span></span>
1. <span data-ttu-id="02bf9-122">Inicialice el archivo de configuración con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="02bf9-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="02bf9-123">Abra el archivo de configuración de dispositivos `config-raspberrypi.json` en Visual Studio Code ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="02bf9-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="02bf9-125">Realice las sustituciones siguientes en el archivo `config-raspberrypi.json`:</span><span class="sxs-lookup"><span data-stu-id="02bf9-125">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="02bf9-126">Reemplace **[device hostname or IP address]** por la dirección IP o el nombre de host del dispositivo que obtuvo de `device-discovery-cli` o por el valor heredado de la configuración del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="02bf9-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="02bf9-127">Reemplace **[IoT device connection string]** con el valor de `device connection string` que ha obtenido.</span><span class="sxs-lookup"><span data-stu-id="02bf9-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="02bf9-128">Reemplace **[IoT hub connection string]** con el valor de `iot hub connection string` que ha obtenido.</span><span class="sxs-lookup"><span data-stu-id="02bf9-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="02bf9-129">Actualice el archivo `config-raspberrypi.json` para que pueda implementar la aplicación de ejemplo desde el equipo.</span><span class="sxs-lookup"><span data-stu-id="02bf9-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="02bf9-130">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="02bf9-130">Deploy and run the sample application</span></span>
<span data-ttu-id="02bf9-131">Implemente y ejecute la aplicación de ejemplo en PI mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="02bf9-131">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="02bf9-132">Comprobación del funcionamiento de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="02bf9-132">Verify that the sample application works</span></span>
<span data-ttu-id="02bf9-133">El LED conectado a Pi debería parpadear cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="02bf9-133">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="02bf9-134">Cada vez que el LED parpadea, la aplicación de ejemplo envía un mensaje a IoT Hub y comprueba que el mensaje se envió correctamente a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02bf9-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="02bf9-135">Además, todos los mensajes que reciba IoT Hub se imprimirán en la ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="02bf9-135">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="02bf9-136">La aplicación de ejemplo se finaliza automáticamente después de enviar 20 mensajes.</span><span class="sxs-lookup"><span data-stu-id="02bf9-136">The sample application terminates automatically after sending 20 messages.</span></span>

![Aplicación de ejemplo con mensajes enviados y recibidos](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="02bf9-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="02bf9-138">Summary</span></span>
<span data-ttu-id="02bf9-139">Ha implementado y ejecutado la nueva aplicación de ejemplo de activación del parpadeo en Pi para enviar al centro de IoT Hub mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="02bf9-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="02bf9-140">Ahora, puede supervisar los mensajes a medida que se escriben en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="02bf9-140">You can now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02bf9-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02bf9-141">Next steps</span></span>
<span data-ttu-id="02bf9-142">[Read messages persisted in Azure Storage](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md) (Lectura de los mensajes guardados en Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="02bf9-142">[Read messages persisted in Azure Storage](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)</span></span>


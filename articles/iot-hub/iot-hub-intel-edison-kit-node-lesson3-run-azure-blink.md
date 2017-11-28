---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 3: Envío de mensajes | Microsoft Docs"
description: "Implemente y ejecute una aplicación de ejemplo para Intel Edison que envíe mensajes a IoT Hub y haga parpadear el LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "servicio en la nube de IoT, envío de datos de Arduino a la nube"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d4b520b9a1852a285b1e10b5b35447a54313af9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="1f6eb-104">Ejecución de una aplicación de ejemplo para enviar mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="1f6eb-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1f6eb-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="1f6eb-105">What you will do</span></span>
<span data-ttu-id="1f6eb-106">En este artículo, se explica cómo implementar y ejecutar una aplicación de ejemplo en Intel Edison que envía mensajes a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="1f6eb-107">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="1f6eb-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1f6eb-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="1f6eb-108">What you will learn</span></span>
<span data-ttu-id="1f6eb-109">Aprenderá a utilizar la herramienta de Gulp para implementar y ejecutar la aplicación de ejemplo en C en Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1f6eb-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="1f6eb-110">What you need</span></span>
* <span data-ttu-id="1f6eb-111">Para comenzar esta tarea, debe haber completado correctamente el tutorial [Creación de una instancia de Azure Function App y una cuenta de Azure Storage para procesar y guardar mensajes de IoT Hub][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="1f6eb-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="1f6eb-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="1f6eb-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="1f6eb-113">La cadena de conexión del dispositivo se utiliza para conectar Intel Edison con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="1f6eb-114">La cadena de conexión de IoT Hub se utiliza para conectar el centro de IoT Hub con la identidad de dispositivo que representa a Intel Edison en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="1f6eb-115">Enumere todos los centros de IoT Hub del grupo de recursos ejecutando el siguiente comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="1f6eb-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="1f6eb-116">Use `iot-sample` como valor de `{resource group name}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="1f6eb-117">Obtenga la cadena de conexión de IoT Hub ejecutando el siguiente comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="1f6eb-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="1f6eb-118">`{my hub name}` es el nombre que especificó cuando creó el centro de IoT Hub y registró Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="1f6eb-119">Obtenga la cadena de conexión de dispositivos ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1f6eb-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="1f6eb-120">Use `myinteledison` como valor de `{device id}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="1f6eb-121">Configuración de la conexión de dispositivos</span><span class="sxs-lookup"><span data-stu-id="1f6eb-121">Configure the device connection</span></span>
1. <span data-ttu-id="1f6eb-122">Inicialice el archivo de configuración con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="1f6eb-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="1f6eb-123">Abra el archivo de configuración de dispositivos `config-edison.json` en Visual Studio Code ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="1f6eb-123">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="1f6eb-125">Realice las sustituciones siguientes en el archivo `config-edison.json`:</span><span class="sxs-lookup"><span data-stu-id="1f6eb-125">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="1f6eb-126">Reemplace **[nombre de host del dispositivo o dirección IP]** por la dirección IP del dispositivo que anotó cuando configuró el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-126">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="1f6eb-127">Reemplace **[IoT device connection string]** con el valor de `device connection string` que ha obtenido.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="1f6eb-128">Reemplace **[IoT hub connection string]** con el valor de `iot hub connection string` que ha obtenido.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1f6eb-129">`azure_storage_connection_string` no es necesario en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="1f6eb-130">Déjelo como está.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-130">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="1f6eb-131">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1f6eb-131">Deploy and run the sample application</span></span>
<span data-ttu-id="1f6eb-132">Implemente y ejecute la aplicación de ejemplo en Intel Edison usando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="1f6eb-132">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="1f6eb-133">Comprobación del funcionamiento de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1f6eb-133">Verify that the sample application works</span></span>
<span data-ttu-id="1f6eb-134">El LED conectado a Intel Edison debería parpadear cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-134">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="1f6eb-135">Cada vez que el LED parpadea, la aplicación de ejemplo envía un mensaje a IoT Hub y comprueba que el mensaje se envió correctamente a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-135">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="1f6eb-136">Además, todos los mensajes que reciba IoT Hub se imprimirán en la ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-136">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="1f6eb-137">La aplicación de ejemplo se finaliza automáticamente después de enviar 20 mensajes.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-137">The sample application terminates automatically after sending 20 messages.</span></span>

![Aplicación de ejemplo con mensajes enviados y recibidos][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="1f6eb-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="1f6eb-139">Summary</span></span>
<span data-ttu-id="1f6eb-140">Ha implementado y ejecutado la nueva aplicación de ejemplo de activación del parpadeo en Intel Edison para enviar al centro de IoT Hub mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-140">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="1f6eb-141">Ahora, puede supervisar los mensajes a medida que se escriben en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1f6eb-141">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f6eb-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1f6eb-142">Next steps</span></span>
<span data-ttu-id="1f6eb-143">[Lectura de los mensajes que se conservan en Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="1f6eb-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md
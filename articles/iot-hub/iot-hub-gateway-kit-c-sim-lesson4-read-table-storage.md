---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 4: Table Storage | Microsoft Docs"
description: "Guarde mensajes de Intel NUC en su IoT Hub, escríbalos en una tabla de Azure Table Storage y, después, léalos desde la nube."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: recuperar datos de la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: de5fae794c195132e2a487c0095845c756aa28e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="8f569-104">Lectura de mensajes guardados en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="8f569-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8f569-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="8f569-105">What you will do</span></span>

- <span data-ttu-id="8f569-106">Ejecute la aplicación de ejemplo de puerta de enlace en la puerta de enlace que envía mensajes a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8f569-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="8f569-107">Ejecute un ejemplo de código en el equipo host para leer los mensajes en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="8f569-107">Run sample code on your host computer to read messages in your Azure Table storage.</span></span>

<span data-ttu-id="8f569-108">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8f569-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8f569-109">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8f569-109">What you will learn</span></span>

<span data-ttu-id="8f569-110">Cómo utilizar la herramienta Gulp para ejecutar el ejemplo de código con la finalidad de leer mensajes en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="8f569-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8f569-111">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="8f569-111">What you need</span></span>

<span data-ttu-id="8f569-112">Ha realizado correctamente las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="8f569-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="8f569-113">[Creación de una cuenta de almacenamiento de Azure y una Azure Function App](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="8f569-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="8f569-114">[Ejecución de la aplicación de ejemplo de puerta de enlace](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="8f569-114">[Run the gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="8f569-115">[Lectura de mensajes desde el IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="8f569-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="8f569-116">Obtener cadenas de conexión de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8f569-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="8f569-117">Al principio de esta lección, creó correctamente una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f569-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="8f569-118">Para obtener la cadena de conexión de la cuenta de almacenamiento de Azure, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8f569-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="8f569-119">Enumere todas las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8f569-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="8f569-120">Obtenga la cadena de conexión de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8f569-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="8f569-121">Use `iot-gateway` como el valor de `{resource group name}` si no lo cambió en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="8f569-121">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="8f569-122">Configuración de la conexión de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8f569-122">Configure the device connection</span></span>

<span data-ttu-id="8f569-123">Actualice el archivo `config-azure.json` para que el ejemplo de código que se ejecuta en el equipo host pueda leer el mensaje de su instancia de Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="8f569-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="8f569-124">Para configurar la conexión de dispositivos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8f569-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="8f569-125">Genere el archivo de configuración del dispositivo `config-azure.json` mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8f569-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuración](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="8f569-127">Sustituya `[Azure storage connection string]` por la cadena de conexión de Azure Storage obtenida.</span><span class="sxs-lookup"><span data-stu-id="8f569-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="8f569-128">`[IoT hub connection string]` ya se debe haber sustituido en la sección [Lectura de mensajes en Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) de la lección 3.</span><span class="sxs-lookup"><span data-stu-id="8f569-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="8f569-129">Lectura de mensajes en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="8f569-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="8f569-130">Ejecute la aplicación de ejemplo de puerta de enlace y lea mensajes en Azure Table Storage mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8f569-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="8f569-131">IoT Hub desencadena la instancia de Azure Function App para guardar el mensaje en Azure Table Storage cuando llega un mensaje nuevo.</span><span class="sxs-lookup"><span data-stu-id="8f569-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="8f569-132">El comando `gulp run` ejecuta la aplicación de ejemplo de puerta de enlace que envía mensajes a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8f569-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="8f569-133">Con el parámetro `table-storage`, también genera un proceso secundario para recibir el mensaje guardado en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="8f569-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="8f569-134">Todos los mensajes que se envían y reciben se muestran al instante en la misma ventana de consola del equipo host.</span><span class="sxs-lookup"><span data-stu-id="8f569-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="8f569-135">La instancia de la aplicación de ejemplo se cerrará automáticamente en 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="8f569-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![Lectura en Gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="8f569-137">Resumen</span><span class="sxs-lookup"><span data-stu-id="8f569-137">Summary</span></span>

<span data-ttu-id="8f569-138">Ha ejecutado el ejemplo de código para leer los mensajes en Azure Table Storage guardados por la aplicación de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8f569-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>

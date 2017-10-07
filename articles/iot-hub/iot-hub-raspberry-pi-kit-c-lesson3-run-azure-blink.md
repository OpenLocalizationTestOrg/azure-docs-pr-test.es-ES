---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 3: ejecutar el ejemplo | Documentos de Microsoft"
description: "Implemente y ejecute un tooRaspberry de aplicación de ejemplo 3 de Pi que envía el centro de IoT tooyour de mensajes y parpadea Hola LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: pi en la nube con parpadeo del led, parpadeo del led desde la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="28a34-104">Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube</span><span class="sxs-lookup"><span data-stu-id="28a34-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="28a34-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="28a34-105">What you will do</span></span>
<span data-ttu-id="28a34-106">En este artículo le mostrará cómo toodeploy y ejecute una aplicación de ejemplo en frambuesa Pi 3 que envía mensajes tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="28a34-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="28a34-107">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="28a34-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="28a34-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="28a34-108">What you will learn</span></span>
<span data-ttu-id="28a34-109">Obtendrá información sobre cómo hello toouse gulp toodeploy de herramienta y ejecutar la aplicación de Node.js de ejemplo de Hola en Pi.</span><span class="sxs-lookup"><span data-stu-id="28a34-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="28a34-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="28a34-110">What you need</span></span>
* <span data-ttu-id="28a34-111">Antes de iniciar esta tarea, debe haber completado correctamente [crear una aplicación de Azure de función y un centro de IoT de almacenamiento cuenta tooprocess y el almacén de mensajes](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="28a34-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="28a34-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="28a34-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="28a34-113">cadena de conexión de dispositivo de Hello participa en el centro de IoT de Pi tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="28a34-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="28a34-114">Hola cadena de conexión de base de datos central de IoT es registro, identidad toohello tooconnect usado en los dispositivos de Hola de IoT hub toomanage que se permiten tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="28a34-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="28a34-115">Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="28a34-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="28a34-116">Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="28a34-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="28a34-117">Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de CLI de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="28a34-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="28a34-118">`{my hub name}`es el nombre de Hola que especificó cuando creó el centro de IoT y había registrado Pi.</span><span class="sxs-lookup"><span data-stu-id="28a34-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="28a34-119">Obtener la cadena de conexión de dispositivo de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="28a34-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="28a34-120">Use `myraspberrypi` como valor de Hola de `{device id}` si no cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="28a34-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="28a34-121">Configurar conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="28a34-121">Configure hello device connection</span></span>
1. <span data-ttu-id="28a34-122">Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="28a34-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="28a34-123">Ejecute también **gulp install-tools** si no lo hizo en la lección 1.</span><span class="sxs-lookup"><span data-stu-id="28a34-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="28a34-124">Archivo de configuración de dispositivos de hello abierto `config-raspberrypi.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="28a34-124">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="28a34-126">Realizar Hola después reemplazos en hello `config-raspberrypi.json` archivo:</span><span class="sxs-lookup"><span data-stu-id="28a34-126">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="28a34-127">Reemplace **[nombre de host de dispositivo o dirección IP]** con el nombre de host o dirección de la IP del dispositivo Hola que se obtuvo al `device-discovery-cli` o con el valor de hello heredado al configurar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="28a34-127">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="28a34-128">Reemplace **[cadena de conexión de dispositivos de IoT]** con hello `device connection string` obtenidas.</span><span class="sxs-lookup"><span data-stu-id="28a34-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="28a34-129">Reemplace **[cadena de conexión de base de datos central de IoT]** con hello `iot hub connection string` obtenidas.</span><span class="sxs-lookup"><span data-stu-id="28a34-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="28a34-130">`azure_storage_connection_string` no es necesario en este artículo.</span><span class="sxs-lookup"><span data-stu-id="28a34-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="28a34-131">Déjelo como está.</span><span class="sxs-lookup"><span data-stu-id="28a34-131">Keep it as is.</span></span>

<span data-ttu-id="28a34-132">Hola de actualización `config-raspberrypi.json` de archivos para que pueda implementar la aplicación de ejemplo de Hola desde su equipo.</span><span class="sxs-lookup"><span data-stu-id="28a34-132">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="28a34-133">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="28a34-133">Deploy and run hello sample application</span></span>
<span data-ttu-id="28a34-134">Implementar y ejecutar la aplicación de ejemplo de Hola en Pi ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="28a34-134">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="28a34-135">Compruebe que la aplicación de ejemplo de Hola funciona</span><span class="sxs-lookup"><span data-stu-id="28a34-135">Verify that hello sample application works</span></span>
<span data-ttu-id="28a34-136">Debería ver Hola LED que está conectado tooPi parpadea cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="28a34-136">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="28a34-137">Cada vez que Hola LED parpadea, aplicación de ejemplo de Hola envía un centro de IoT tooyour de mensaje y comprueba que ese mensaje Hola se ha enviado correctamente tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="28a34-137">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="28a34-138">Además, cada mensaje recibido por el centro de IoT Hola se imprime en la ventana de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="28a34-138">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="28a34-139">aplicación de ejemplo de Hola finaliza automáticamente después de enviar 20 mensajes.</span><span class="sxs-lookup"><span data-stu-id="28a34-139">hello sample application terminates automatically after sending 20 messages.</span></span>

![Aplicación de ejemplo con mensajes enviados y recibidos](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="28a34-141">Resumen</span><span class="sxs-lookup"><span data-stu-id="28a34-141">Summary</span></span>
<span data-ttu-id="28a34-142">Ha implementado y ejecute nueva aplicación de ejemplo de intermitencia Hola en Centro de IoT tooyour de Pi toosend mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="28a34-142">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="28a34-143">Ahora, supervisar los mensajes tal y como se escriben toohello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="28a34-143">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28a34-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28a34-144">Next steps</span></span>
<span data-ttu-id="28a34-145">[Read messages persisted in Azure Storage](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md) (Lectura de los mensajes guardados en Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="28a34-145">[Read messages persisted in Azure Storage](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)</span></span>


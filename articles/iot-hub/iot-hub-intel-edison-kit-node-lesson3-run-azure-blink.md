---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 3: enviar mensajes | Documentos de Microsoft"
description: "Implemente y ejecute un tooIntel de aplicación de ejemplo Edison que envía el centro de IoT tooyour de mensajes y parpadea Hola LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servicio de nube de IOT, arduino enviar datos toocloud
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
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="8c95f-104">Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube</span><span class="sxs-lookup"><span data-stu-id="8c95f-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8c95f-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="8c95f-105">What you will do</span></span>
<span data-ttu-id="8c95f-106">En este artículo le mostrará cómo toodeploy y ejecute una aplicación de ejemplo en Edison de Intel que envía mensajes tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8c95f-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="8c95f-107">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8c95f-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8c95f-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8c95f-108">What you will learn</span></span>
<span data-ttu-id="8c95f-109">Aprenderá cómo hello toouse gulp toodeploy de herramienta y ejecutar la aplicación de C de ejemplo de Hola en Edison.</span><span class="sxs-lookup"><span data-stu-id="8c95f-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8c95f-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="8c95f-110">What you need</span></span>
* <span data-ttu-id="8c95f-111">Antes de iniciar esta tarea, debe haber completado correctamente [crear una aplicación de Azure de función y un centro de IoT de almacenamiento cuenta tooprocess y el almacén de mensajes][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="8c95f-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="8c95f-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="8c95f-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="8c95f-113">cadena de conexión de dispositivo de Hello es usado tooconnect centro de IoT Edison tooyour.</span><span class="sxs-lookup"><span data-stu-id="8c95f-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="8c95f-114">Hola la cadena de conexión de base de datos central de IoT es tooconnect usado su identidad de dispositivos de IoT hub toohello que representa Edison en el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="8c95f-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="8c95f-115">Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="8c95f-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="8c95f-116">Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c95f-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="8c95f-117">Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de CLI de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="8c95f-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="8c95f-118">`{my hub name}`es el nombre de Hola que especificó cuando creó el centro de IoT y había registrado a Edison.</span><span class="sxs-lookup"><span data-stu-id="8c95f-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="8c95f-119">Obtener la cadena de conexión de dispositivo de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8c95f-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="8c95f-120">Use `myinteledison` como valor de Hola de `{device id}` si no cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c95f-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="8c95f-121">Configurar conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="8c95f-121">Configure hello device connection</span></span>
1. <span data-ttu-id="8c95f-122">Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8c95f-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="8c95f-123">Archivo de configuración de dispositivos de hello abierto `config-edison.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8c95f-123">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="8c95f-125">Realizar Hola después reemplazos en hello `config-edison.json` archivo:</span><span class="sxs-lookup"><span data-stu-id="8c95f-125">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="8c95f-126">Reemplace **[nombre de host de dispositivo o dirección IP]** con la dirección IP del dispositivo Hola marcados como inactivos cuando se configura el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8c95f-126">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="8c95f-127">Reemplace **[cadena de conexión de dispositivos de IoT]** con hello `device connection string` obtenidas.</span><span class="sxs-lookup"><span data-stu-id="8c95f-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="8c95f-128">Reemplace **[cadena de conexión de base de datos central de IoT]** con hello `iot hub connection string` obtenidas.</span><span class="sxs-lookup"><span data-stu-id="8c95f-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c95f-129">`azure_storage_connection_string` no es necesario en este artículo.</span><span class="sxs-lookup"><span data-stu-id="8c95f-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="8c95f-130">Déjelo como está.</span><span class="sxs-lookup"><span data-stu-id="8c95f-130">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="8c95f-131">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="8c95f-131">Deploy and run hello sample application</span></span>
<span data-ttu-id="8c95f-132">Implementar y ejecutar la aplicación de ejemplo de Hola en Edison ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8c95f-132">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="8c95f-133">Compruebe que la aplicación de ejemplo de Hola funciona</span><span class="sxs-lookup"><span data-stu-id="8c95f-133">Verify that hello sample application works</span></span>
<span data-ttu-id="8c95f-134">Debería ver Hola LED que está conectado tooEdison parpadea cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="8c95f-134">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="8c95f-135">Cada vez que Hola LED parpadea, aplicación de ejemplo de Hola envía un centro de IoT tooyour de mensaje y comprueba que ese mensaje Hola se ha enviado correctamente tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8c95f-135">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="8c95f-136">Además, cada mensaje recibido por el centro de IoT Hola se imprime en la ventana de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c95f-136">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="8c95f-137">aplicación de ejemplo de Hola finaliza automáticamente después de enviar 20 mensajes.</span><span class="sxs-lookup"><span data-stu-id="8c95f-137">hello sample application terminates automatically after sending 20 messages.</span></span>

![Aplicación de ejemplo con mensajes enviados y recibidos][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="8c95f-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="8c95f-139">Summary</span></span>
<span data-ttu-id="8c95f-140">Se ha implementado y ejecutar nueva aplicación de ejemplo de intermitencia hello en Edison centro de IoT de tooyour toosend mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="8c95f-140">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="8c95f-141">Ahora, supervisar los mensajes tal y como se escriben toohello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8c95f-141">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c95f-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c95f-142">Next steps</span></span>
<span data-ttu-id="8c95f-143">[Lectura de los mensajes que se conservan en Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="8c95f-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md
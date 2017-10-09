---
title: "Conectar Arduino tooAzure IoT - lección 2: registrar el dispositivo | Documentos de Microsoft"
description: Crear un grupo de recursos, crear un centro de IoT de Azure y registrar Adafruit compacto M0 Wi-Fi en el centro de IoT de Azure de hello mediante Hola CLI de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "conexión arduino toocloud, centro de iot de azure, internet de nube de cosas, centro de iot de azure crear un dispositivo, arduino en la nube"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="be3e9-104">Creación de una instancia de IoT Hub de Azure y registro de Adafruit Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="be3e9-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="be3e9-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="be3e9-105">What you will do</span></span>
* <span data-ttu-id="be3e9-106">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="be3e9-106">Create a resource group.</span></span>
* <span data-ttu-id="be3e9-107">Crear el centro de IoT de Azure en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="be3e9-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="be3e9-108">Agregar el centro de IoT de Azure de Arduino panel toohello mediante hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="be3e9-108">Add your Arduino board toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="be3e9-109">Cuando usas hello Azure CLI tooadd su centro de IoT Arduino panel tooyour, servicio de hello genera una clave para su tooauthenticate de panel Arduino con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="be3e9-109">When you use hello Azure CLI tooadd your Arduino board tooyour IoT hub, hello service generates a key for your Arduino board tooauthenticate with hello service.</span></span> <span data-ttu-id="be3e9-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshoot].</span><span class="sxs-lookup"><span data-stu-id="be3e9-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="be3e9-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="be3e9-111">What you will learn</span></span>
<span data-ttu-id="be3e9-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="be3e9-112">In this article, you will learn:</span></span>
* <span data-ttu-id="be3e9-113">¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="be3e9-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="be3e9-114">¿Cómo toocreate una identidad de dispositivo para su Arduino del panel en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="be3e9-114">How toocreate a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="be3e9-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="be3e9-115">What you need</span></span>
* <span data-ttu-id="be3e9-116">Una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="be3e9-116">An Azure account</span></span>
* <span data-ttu-id="be3e9-117">Un equipo con hello CLI de Azure instalado</span><span class="sxs-lookup"><span data-stu-id="be3e9-117">A computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="be3e9-118">Creación de un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="be3e9-118">Create your IoT hub</span></span>
<span data-ttu-id="be3e9-119">IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT.</span><span class="sxs-lookup"><span data-stu-id="be3e9-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="be3e9-120">toocreate su centro de IoT, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="be3e9-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="be3e9-121">Inicie sesión en tooyour cuenta de Azure ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="be3e9-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="be3e9-122">Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="be3e9-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="be3e9-123">Establecer suscripción predeterminada de Hola que desea toouse ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="be3e9-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="be3e9-124">`subscription ID or name`puede encontrarse en la salida de hello de hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="be3e9-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="be3e9-125">Registrar un proveedor Hola ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="be3e9-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="be3e9-126">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="be3e9-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="be3e9-127">Debe registrar proveedor de Hola para poder implementar Hola recursos de Azure que Hola ofertas de proveedor.</span><span class="sxs-lookup"><span data-stu-id="be3e9-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="be3e9-128">Crear un grupo de recursos denominado ejemplo iot en región del oeste de Estados Unidos de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="be3e9-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="be3e9-129">`westus`es la ubicación de hello crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="be3e9-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="be3e9-130">Si desea toouse en otra ubicación, puede ejecutar `az account list-locations -o table` toosee todos Hola ubicaciones de Azure admite.</span><span class="sxs-lookup"><span data-stu-id="be3e9-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="be3e9-131">Crear un centro de IoT en grupo de recursos de ejemplo de iot de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="be3e9-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="be3e9-132">De forma predeterminada, herramienta de hello crea un centro de IoT en el nivel de precios de Hola.</span><span class="sxs-lookup"><span data-stu-id="be3e9-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="be3e9-133">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="be3e9-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="be3e9-134">nombre de Hola de su centro de IoT debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="be3e9-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="be3e9-135">Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="be3e9-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="be3e9-136">Registro de la placa de Arduino en el centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="be3e9-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="be3e9-137">Cada dispositivo que envía el centro de IoT tooyour de mensajes y recibe mensajes desde el centro de IoT debe estar registrado con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="be3e9-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="be3e9-138">Registre la placa de Arduino en su instancia de IoT Hub ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="be3e9-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="be3e9-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="be3e9-139">Summary</span></span>
<span data-ttu-id="be3e9-140">Ha creado un centro de IoT Hub y ha registrado la placa de Arduino con una identidad de dispositivo en este centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="be3e9-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="be3e9-141">Ya está listo toolearn cómo toosend mensajes desde el centro de IoT Arduino tooyour de panel.</span><span class="sxs-lookup"><span data-stu-id="be3e9-141">You're ready toolearn how toosend messages from your Arduino board tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be3e9-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be3e9-142">Next steps</span></span>
<span data-ttu-id="be3e9-143">[Crear una aplicación de Azure de función y un centro de IoT de almacenamiento de Azure cuenta tooprocess y el almacén de mensajes][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="be3e9-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
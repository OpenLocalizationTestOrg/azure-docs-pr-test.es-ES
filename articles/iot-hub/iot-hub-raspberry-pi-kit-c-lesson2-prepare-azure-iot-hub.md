---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 2: registrar el dispositivo | Documentos de Microsoft"
description: Crear un grupo de recursos, crear un centro de IoT de Azure y registrar Pi en el centro de IoT de Azure de hello mediante Hola CLI de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "nube de raspberry pi, conexión a la nube de pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="900a2-104">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="900a2-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="900a2-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="900a2-105">What you will do</span></span>
* <span data-ttu-id="900a2-106">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="900a2-106">Create a resource group.</span></span>
* <span data-ttu-id="900a2-107">Crear el centro de IoT de Azure en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="900a2-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="900a2-108">Agregar el centro de IoT de Azure de toohello de frambuesa Pi 3 mediante hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="900a2-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="900a2-109">Cuando se usa el centro de IoT de hello Azure CLI tooadd Pi tooyour, servicio de hello genera una clave para tooauthenticate Pi con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="900a2-109">When you use hello Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="900a2-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="900a2-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="900a2-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="900a2-111">What you will learn</span></span>
<span data-ttu-id="900a2-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="900a2-112">In this article, you will learn:</span></span>
* <span data-ttu-id="900a2-113">¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="900a2-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="900a2-114">¿Cómo toocreate una identidad de dispositivo de Pi en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="900a2-114">How toocreate a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="900a2-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="900a2-115">What you need</span></span>
* <span data-ttu-id="900a2-116">Una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="900a2-116">An Azure account</span></span>
* <span data-ttu-id="900a2-117">Un equipo Mac o en un equipo Windows con hello CLI de Azure instalado</span><span class="sxs-lookup"><span data-stu-id="900a2-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="900a2-118">Creación de un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="900a2-118">Create your IoT hub</span></span>
<span data-ttu-id="900a2-119">IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT.</span><span class="sxs-lookup"><span data-stu-id="900a2-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="900a2-120">toocreate su centro de IoT, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="900a2-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="900a2-121">Inicie sesión en tooyour cuenta de Azure ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="900a2-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="900a2-122">Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="900a2-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="900a2-123">Establecer suscripción predeterminada de Hola que desea toouse ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="900a2-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="900a2-124">`subscription ID or name`puede encontrarse en la salida de hello de hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="900a2-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="900a2-125">Registrar un proveedor Hola ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="900a2-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="900a2-126">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="900a2-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="900a2-127">Debe registrar proveedor de Hola para poder implementar Hola recursos de Azure que Hola ofertas de proveedor.</span><span class="sxs-lookup"><span data-stu-id="900a2-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="900a2-128">Crear un grupo de recursos denominado ejemplo iot en región del oeste de Estados Unidos de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="900a2-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="900a2-129">`westus`es la ubicación de hello crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="900a2-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="900a2-130">Si desea toouse en otra ubicación, puede ejecutar `az account list-locations -o table` toosee todos Hola ubicaciones de Azure admite.</span><span class="sxs-lookup"><span data-stu-id="900a2-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="900a2-131">Crear un centro de IoT en grupo de recursos de ejemplo de iot de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="900a2-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="900a2-132">De forma predeterminada, herramienta de hello crea un centro de IoT en el nivel de precios de Hola.</span><span class="sxs-lookup"><span data-stu-id="900a2-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="900a2-133">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="900a2-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="900a2-134">nombre de Hola de su centro de IoT debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="900a2-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="900a2-135">Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="900a2-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="900a2-136">Registro de Pi en el centro de IoT hub</span><span class="sxs-lookup"><span data-stu-id="900a2-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="900a2-137">Cada dispositivo que envía el centro de IoT tooyour de mensajes y recibe mensajes desde el centro de IoT debe estar registrado con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="900a2-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="900a2-138">Registre Pi en el centro de ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="900a2-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="900a2-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="900a2-139">Summary</span></span>
<span data-ttu-id="900a2-140">Ha creado un centro de IoT Hub y ha registrado Pi con una identidad de dispositivo en este centro.</span><span class="sxs-lookup"><span data-stu-id="900a2-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="900a2-141">Ya está listo toolearn cómo toosend mensajes Pi tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="900a2-141">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="900a2-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="900a2-142">Next steps</span></span>
<span data-ttu-id="900a2-143">[Crear una aplicación de Azure de función y un centro de IoT de almacenamiento de Azure cuenta tooprocess y el almacén de mensajes](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="900a2-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>


---
featureFlags: usabilla
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 2: registrar el dispositivo | Documentos de Microsoft"
description: Crear un grupo de recursos, crear un centro de IoT de Azure y registrar Pi en hello del registro de identidad de centro de IoT mediante la CLI de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "nube de raspberry pi, conexión a la nube de pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="7c730-104">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="7c730-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="7c730-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="7c730-105">What you will do</span></span>
* <span data-ttu-id="7c730-106">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7c730-106">Create a resource group.</span></span>
* <span data-ttu-id="7c730-107">Crear el centro de IoT de Azure en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c730-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="7c730-108">Agregar el centro de IoT de Azure de toohello de frambuesa Pi 3 mediante hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="7c730-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="7c730-109">Cuando se usa el centro de IoT de Azure CLI tooadd Pi tooyour, servicio de hello genera una clave para tooauthenticate Pi con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c730-109">When you use Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="7c730-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7c730-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7c730-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="7c730-111">What you will learn</span></span>
<span data-ttu-id="7c730-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7c730-112">In this article, you will learn:</span></span>
* <span data-ttu-id="7c730-113">¿Cómo toouse CLI de Azure toocreate un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="7c730-113">How toouse Azure CLI toocreate an IoT hub</span></span>
* <span data-ttu-id="7c730-114">¿Cómo toocreate una identidad de dispositivo de Pi en el centro de IoT</span><span class="sxs-lookup"><span data-stu-id="7c730-114">How toocreate a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7c730-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="7c730-115">What you need</span></span>
* <span data-ttu-id="7c730-116">Una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="7c730-116">An Azure account</span></span>
* <span data-ttu-id="7c730-117">Un equipo Mac o en un equipo Windows con hello CLI de Azure instalado</span><span class="sxs-lookup"><span data-stu-id="7c730-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="7c730-118">Creación de un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7c730-118">Create your IoT hub</span></span>
<span data-ttu-id="7c730-119">IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT.</span><span class="sxs-lookup"><span data-stu-id="7c730-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="7c730-120">toocreate su centro de IoT, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7c730-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="7c730-121">Inicie sesión en tooyour cuenta de Azure ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7c730-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="7c730-122">Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="7c730-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="7c730-123">Establecer suscripción predeterminada de Hola que desea toouse ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7c730-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="7c730-124">`subscription ID or name`puede encontrarse en la salida de hello de hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="7c730-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="7c730-125">Registrar un proveedor Hola ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c730-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="7c730-126">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c730-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="7c730-127">Debe registrar proveedor de Hola para poder implementar Hola recursos de Azure que Hola ofertas de proveedor.</span><span class="sxs-lookup"><span data-stu-id="7c730-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="7c730-128">Crear un grupo de recursos denominado ejemplo iot en región del oeste de Estados Unidos de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7c730-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="7c730-129">`westus`es la ubicación de hello crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7c730-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="7c730-130">Si desea toouse en otra ubicación, puede ejecutar `az account list-locations -o table` toosee todos Hola ubicaciones de Azure admite.</span><span class="sxs-lookup"><span data-stu-id="7c730-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="7c730-131">Crear un centro de IoT en grupo de recursos de ejemplo de iot de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7c730-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="7c730-132">De forma predeterminada, herramienta de hello crea un centro de IoT en el nivel de precios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c730-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="7c730-133">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="7c730-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="7c730-134">nombre de Hola de su centro de IoT debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="7c730-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="7c730-135">Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c730-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="7c730-136">Registro de Pi en el centro de IoT hub</span><span class="sxs-lookup"><span data-stu-id="7c730-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="7c730-137">Cada dispositivo que envía el centro de IoT tooyour de mensajes y recibe mensajes desde el centro de IoT debe estar registrado con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="7c730-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="7c730-138">Utilizará CLI de Azure tooregister su Pi y crear un certificado autofirmado de X.509 para la autenticación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7c730-138">You will use Azure CLI tooregister your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="7c730-139">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7c730-139">Run hello following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="7c730-140">Resumen</span><span class="sxs-lookup"><span data-stu-id="7c730-140">Summary</span></span>
<span data-ttu-id="7c730-141">Ha creado un centro de IoT Hub y ha registrado Pi con una identidad de dispositivo en este centro.</span><span class="sxs-lookup"><span data-stu-id="7c730-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="7c730-142">Ya está listo toolearn cómo toosend mensajes Pi tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7c730-142">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c730-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c730-143">Next steps</span></span>
[<span data-ttu-id="7c730-144">Crear una aplicación de Azure de función y una tooprocess de cuenta de almacenamiento de Azure y almacenar mensajes de centro de IoT</span><span class="sxs-lookup"><span data-stu-id="7c730-144">Create an Azure function app and an Azure storage account tooprocess and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)


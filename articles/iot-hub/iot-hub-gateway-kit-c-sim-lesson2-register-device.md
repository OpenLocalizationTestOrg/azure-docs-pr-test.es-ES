---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 2: Registro del dispositivo | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, nube de internet de las cosas, dispositivo de creación de azure iot hub, sensortag de ti, ble de ti"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="1b7f3-103">Creación de una instancia de Azure IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="1b7f3-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="1b7f3-104">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="1b7f3-104">What you will do</span></span>

- <span data-ttu-id="1b7f3-105">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1b7f3-105">Create a resource group</span></span>
- <span data-ttu-id="1b7f3-106">Crear su primera instancia de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1b7f3-106">Create your first IoT hub</span></span>
- <span data-ttu-id="1b7f3-107">Registre el dispositivo en el centro de IoT mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="1b7f3-108">Al registrar el dispositivo en el centro de IoT, Hola servicio del centro de IoT de Azure genera una clave para su tooauthenticate toouse de dispositivo con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="1b7f3-109">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1b7f3-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1b7f3-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="1b7f3-110">What you will learn</span></span>

<span data-ttu-id="1b7f3-111">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b7f3-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="1b7f3-112">¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="1b7f3-113">¿Cómo tooregister un dispositivo en un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1b7f3-114">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="1b7f3-114">What you need</span></span>

- <span data-ttu-id="1b7f3-115">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-115">An active Azure subscription.</span></span> <span data-ttu-id="1b7f3-116">Si no tiene ninguna cuenta de Azure, puede crear una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="1b7f3-117">Debe tener Hola que CLI de Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="1b7f3-118">Crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="1b7f3-118">Create an IoT hub</span></span>

<span data-ttu-id="1b7f3-119">toocreate un centro de IoT, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1b7f3-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="1b7f3-120">Inicie sesión en tooyour cuenta de Azure ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="1b7f3-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="1b7f3-121">Una vez que se haya iniciado sesión correctamente, se mostrarán todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="1b7f3-122">Establezca el valor predeterminado de hello suscripción de Azure que quiere toouse, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1b7f3-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="1b7f3-123">`subscription ID or name`puede encontrarse en la salida de hello de hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="1b7f3-124">Registrar un proveedor Hola ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="1b7f3-125">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="1b7f3-126">Debe registrar proveedor de Hola para poder implementar Hola recursos de Azure que Hola ofertas de proveedor.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="1b7f3-127">Cree un grupo de recursos denominado `iot-gateway` en región del oeste de Estados Unidos de Hola ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="1b7f3-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="1b7f3-128">`westus`es la ubicación de hello crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="1b7f3-129">Si desea toouse en otra ubicación, puede ejecutar `az account list-locations -o table` toosee todos Hola ubicaciones de Azure admite.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="1b7f3-130">Crear un centro de IoT en hello `iot-gateway` grupo de recursos mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1b7f3-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="1b7f3-131">De forma predeterminada, herramienta de hello crea un centro de IoT en el nivel de precios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="1b7f3-132">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="1b7f3-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="1b7f3-133">nombre de Hola de su centro de IoT debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="1b7f3-134">Solo puede crear una edición F1 de Azure IoT Hub en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="1b7f3-135">Registro del dispositivo en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1b7f3-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="1b7f3-136">Cada dispositivo que envía el centro de IoT tooyour de mensajes y recibe mensajes desde el centro de IoT debe estar registrado con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="1b7f3-137">Registre el dispositivo en IoT Hub ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b7f3-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="1b7f3-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="1b7f3-138">Summary</span></span>

<span data-ttu-id="1b7f3-139">Ha creado una instancia de IoT Hub y ha registrado en ella el dispositivo local con una identidad de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="1b7f3-140">Ya está listo toolearn cómo tooconfigure y ejecutar una puerta de enlace ejemplo aplicación toosend de datos desde el centro de IoT de dispositivo físico tooyour Hola en la nube.</span><span class="sxs-lookup"><span data-stu-id="1b7f3-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b7f3-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b7f3-141">Next steps</span></span>
[<span data-ttu-id="1b7f3-142">Configuración y ejecución de una aplicación de ejemplo de carga a la nube de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="1b7f3-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)
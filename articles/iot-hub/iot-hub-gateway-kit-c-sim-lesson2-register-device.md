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
ms.openlocfilehash: 5557989453eb47e4c3a287b26603eff040eb1d96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="56453-103">Creación de una instancia de Azure IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="56453-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="56453-104">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="56453-104">What you will do</span></span>

- <span data-ttu-id="56453-105">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="56453-105">Create a resource group</span></span>
- <span data-ttu-id="56453-106">Crear su primera instancia de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="56453-106">Create your first IoT hub</span></span>
- <span data-ttu-id="56453-107">Registrar el dispositivo en IoT Hub mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="56453-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="56453-108">Al registrar el dispositivo en IoT Hub, el servicio Azure IoT Hub genera una clave para que el dispositivo la use cuando se autentique con el servicio.</span><span class="sxs-lookup"><span data-stu-id="56453-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="56453-109">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="56453-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="56453-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="56453-110">What you will learn</span></span>

<span data-ttu-id="56453-111">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="56453-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="56453-112">Cómo usar la CLI de Azure para crear una instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="56453-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="56453-113">Cómo registrar un dispositivo en un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="56453-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="56453-114">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="56453-114">What you need</span></span>

- <span data-ttu-id="56453-115">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="56453-115">An active Azure subscription.</span></span> <span data-ttu-id="56453-116">Si no tiene ninguna cuenta de Azure, puede crear una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="56453-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="56453-117">Debe tener instalada la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="56453-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="56453-118">Crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="56453-118">Create an IoT hub</span></span>

<span data-ttu-id="56453-119">Para crear una instancia de IoT Hub, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="56453-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="56453-120">Inicie sesión en la cuenta de Azure mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="56453-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="56453-121">Una vez que se haya iniciado sesión correctamente, se mostrarán todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="56453-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="56453-122">Establezca la suscripción predeterminada de Azure que va a usar ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="56453-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="56453-123">El valor de `subscription ID or name` puede verse en la salida del comando `az login` o del comando `az account list`.</span><span class="sxs-lookup"><span data-stu-id="56453-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="56453-124">Registre el proveedor con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="56453-124">Register the provider by running the following command.</span></span> <span data-ttu-id="56453-125">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56453-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="56453-126">Debe registrar el proveedor para poder implementar el recurso de Azure que este le ofrece.</span><span class="sxs-lookup"><span data-stu-id="56453-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="56453-127">Cree un grupo de recursos denominado `iot-gateway` en la región oeste de EE. UU. ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="56453-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="56453-128">`westus` es la ubicación en la que se crea el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="56453-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="56453-129">Si desea utilizar otra ubicación, puede ejecutar `az account list-locations -o table` para ver todas las ubicaciones admitidas por Azure.</span><span class="sxs-lookup"><span data-stu-id="56453-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="56453-130">Cree una instancia de IoT Hub en el grupo de recursos `iot-gateway` mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="56453-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="56453-131">De forma predeterminada, la herramienta crea la instancia de IoT Hub con el plan de tarifa Gratis.</span><span class="sxs-lookup"><span data-stu-id="56453-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="56453-132">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="56453-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="56453-133">El nombre de su instancia de IoT Hub debe única globalmente.</span><span class="sxs-lookup"><span data-stu-id="56453-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="56453-134">Solo puede crear una edición F1 de Azure IoT Hub en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="56453-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="56453-135">Registro del dispositivo en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="56453-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="56453-136">Todos los dispositivos que envían mensajes al centro de IoT Hub y los reciben de este deben estar registrados con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="56453-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="56453-137">Registre el dispositivo en IoT Hub ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="56453-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="56453-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="56453-138">Summary</span></span>

<span data-ttu-id="56453-139">Ha creado una instancia de IoT Hub y ha registrado en ella el dispositivo local con una identidad de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="56453-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="56453-140">Está listo para aprender a configurar y ejecutar una aplicación de ejemplo de puerta de enlace para enviar datos desde el dispositivo físico a la instancia de IoT Hub en la nube.</span><span class="sxs-lookup"><span data-stu-id="56453-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56453-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56453-141">Next steps</span></span>
[<span data-ttu-id="56453-142">Configuración y ejecución de una aplicación de ejemplo de carga a la nube de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="56453-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)
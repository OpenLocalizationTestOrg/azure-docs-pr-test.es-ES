---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 2: Registro del dispositivo | Microsoft Docs"
description: Cree un grupo de recursos, cree una instancia de IoT Hub de Azure y registre Pi en IoT Hub de Azure mediante la CLI de Azure.
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
ms.openlocfilehash: d7bfd8f6ae8d15dfe09f06a40a4ab415ff2e0a7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="0bc0c-104">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="0bc0c-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0bc0c-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="0bc0c-105">What you will do</span></span>
* <span data-ttu-id="0bc0c-106">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-106">Create a resource group.</span></span>
* <span data-ttu-id="0bc0c-107">Cree una instancia de IoT Hub de Azure en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="0bc0c-108">Agregue Raspberry Pi 3 al centro de Azure IoT Hub mediante la interfaz de la línea de comandos de Azure (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="0bc0c-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="0bc0c-109">Si utiliza la CLI de Azure para agregar Pi al centro de IoT Hub, el servicio generará una clave para autenticar Pi en el servicio.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-109">When you use the Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="0bc0c-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0bc0c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0bc0c-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="0bc0c-111">What you will learn</span></span>
<span data-ttu-id="0bc0c-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0bc0c-112">In this article, you will learn:</span></span>
* <span data-ttu-id="0bc0c-113">Cómo usar la CLI de Azure para crear un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0bc0c-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="0bc0c-114">Cómo crear una identidad de dispositivos para Pi en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0bc0c-114">How to create a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0bc0c-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="0bc0c-115">What you need</span></span>
* <span data-ttu-id="0bc0c-116">Una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="0bc0c-116">An Azure account</span></span>
* <span data-ttu-id="0bc0c-117">Un equipo Mac o un equipo Windows con la CLI de Azure instalada</span><span class="sxs-lookup"><span data-stu-id="0bc0c-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="0bc0c-118">Creación de un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0bc0c-118">Create your IoT hub</span></span>
<span data-ttu-id="0bc0c-119">IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="0bc0c-120">Para crear el centro de IoT Hub, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0bc0c-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="0bc0c-121">Inicie sesión en la cuenta de Azure mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0bc0c-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="0bc0c-122">Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="0bc0c-123">Establezca la suscripción predeterminada que desea usar mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0bc0c-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="0bc0c-124">El valor de `subscription ID or name` puede verse en la salida del comando `az login` o del comando `az account list`.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="0bc0c-125">Registre el proveedor con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-125">Register the provider by running the following command.</span></span> <span data-ttu-id="0bc0c-126">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="0bc0c-127">Debe registrar el proveedor para poder implementar el recurso de Azure que este le ofrece.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="0bc0c-128">Cree un grupo de recursos denominado "iot-sample" en la región oeste de EE. UU. ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0bc0c-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="0bc0c-129">`westus` es la ubicación en la que se crea el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="0bc0c-130">Si desea utilizar otra ubicación, puede ejecutar `az account list-locations -o table` para ver todas las ubicaciones admitidas por Azure.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="0bc0c-131">Cree una instancia de IoT Hub en el grupo de recursos iot-sample ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0bc0c-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="0bc0c-132">De forma predeterminada, la herramienta crea la instancia de IoT Hub con el plan de tarifa Gratis.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="0bc0c-133">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="0bc0c-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="0bc0c-134">El nombre de su instancia de IoT Hub debe única globalmente.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="0bc0c-135">Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="0bc0c-136">Registro de Pi en el centro de IoT hub</span><span class="sxs-lookup"><span data-stu-id="0bc0c-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="0bc0c-137">Todos los dispositivos que envían mensajes al centro de IoT Hub y los reciben de este deben estar registrados con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="0bc0c-138">Registre Pi en el centro de ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0bc0c-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="0bc0c-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="0bc0c-139">Summary</span></span>
<span data-ttu-id="0bc0c-140">Ha creado un centro de IoT Hub y ha registrado Pi con una identidad de dispositivo en este centro.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="0bc0c-141">Ya está preparado para aprender a enviar mensajes desde Pi a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0bc0c-141">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bc0c-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0bc0c-142">Next steps</span></span>
<span data-ttu-id="0bc0c-143">[Creación de una instancia de Azure Function App y una cuenta de Azure Storage para procesar y almacenar mensajes de IoT Hub](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="0bc0c-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>


---
featureFlags: usabilla
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 2: Registro del dispositivo | Microsoft Docs"
description: Cree un grupo de recursos, cree un centro de IoT Hub de Azure y registre Pi en este centro mediante la CLI de Azure.
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
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="04297-104">Creación de un centro de IoT y registro de Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="04297-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="04297-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="04297-105">What you will do</span></span>
* <span data-ttu-id="04297-106">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="04297-106">Create a resource group.</span></span>
* <span data-ttu-id="04297-107">Cree una instancia de IoT Hub de Azure en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="04297-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="04297-108">Agregue Raspberry Pi 3 al centro de Azure IoT Hub mediante la interfaz de la línea de comandos de Azure (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="04297-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="04297-109">Si utiliza la CLI de Azure para agregar Pi al centro de IoT Hub, el servicio generará una clave para autenticar Pi en el servicio.</span><span class="sxs-lookup"><span data-stu-id="04297-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="04297-110">Si tiene problemas, puede encontrar soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="04297-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="04297-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="04297-111">What you will learn</span></span>
<span data-ttu-id="04297-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04297-112">In this article, you will learn:</span></span>
* <span data-ttu-id="04297-113">Uso de la CLI de Azure para crear un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="04297-113">How to use Azure CLI to create an IoT hub</span></span>
* <span data-ttu-id="04297-114">Creación de una identidad de dispositivos para Pi en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="04297-114">How to create a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="04297-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="04297-115">What you need</span></span>
* <span data-ttu-id="04297-116">Una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="04297-116">An Azure account</span></span>
* <span data-ttu-id="04297-117">Un equipo Mac o un equipo Windows con la CLI de Azure instalada</span><span class="sxs-lookup"><span data-stu-id="04297-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="04297-118">Creación de un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="04297-118">Create your IoT hub</span></span>
<span data-ttu-id="04297-119">IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT.</span><span class="sxs-lookup"><span data-stu-id="04297-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="04297-120">Para crear el centro de IoT Hub, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="04297-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="04297-121">Inicie sesión en la cuenta de Azure mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="04297-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="04297-122">Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="04297-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="04297-123">Establezca la suscripción predeterminada que desea usar mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="04297-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="04297-124">El valor de `subscription ID or name` puede verse en la salida del comando `az login` o del comando `az account list`.</span><span class="sxs-lookup"><span data-stu-id="04297-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="04297-125">Registre el proveedor con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="04297-125">Register the provider by running the following command.</span></span> <span data-ttu-id="04297-126">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04297-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="04297-127">Debe registrar el proveedor para poder implementar el recurso de Azure que este le ofrece.</span><span class="sxs-lookup"><span data-stu-id="04297-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="04297-128">Cree un grupo de recursos denominado "iot-sample" en la región oeste de EE. UU. ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="04297-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="04297-129">`westus` es la ubicación en la que se crea el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="04297-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="04297-130">Si desea utilizar otra ubicación, puede ejecutar `az account list-locations -o table` para ver todas las ubicaciones admitidas por Azure.</span><span class="sxs-lookup"><span data-stu-id="04297-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="04297-131">Cree una instancia de IoT Hub en el grupo de recursos iot-sample ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="04297-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="04297-132">De forma predeterminada, la herramienta crea la instancia de IoT Hub con el plan de tarifa Gratis.</span><span class="sxs-lookup"><span data-stu-id="04297-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="04297-133">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="04297-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="04297-134">El nombre de su instancia de IoT Hub debe única globalmente.</span><span class="sxs-lookup"><span data-stu-id="04297-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="04297-135">Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="04297-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="04297-136">Registro de Pi en el centro de IoT hub</span><span class="sxs-lookup"><span data-stu-id="04297-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="04297-137">Todos los dispositivos que envían mensajes al centro de IoT Hub y los reciben de este deben estar registrados con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="04297-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="04297-138">Debe usar la CLI de Azure para registrar Pi y crear un certificado X.509 autofirmado para autenticar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="04297-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="04297-139">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="04297-139">Run the following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="04297-140">Resumen</span><span class="sxs-lookup"><span data-stu-id="04297-140">Summary</span></span>
<span data-ttu-id="04297-141">Ha creado un centro de IoT Hub y ha registrado Pi con una identidad de dispositivo en este centro.</span><span class="sxs-lookup"><span data-stu-id="04297-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="04297-142">Ya está preparado para aprender a enviar mensajes desde Pi a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04297-142">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04297-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04297-143">Next steps</span></span>
[<span data-ttu-id="04297-144">Creación de una instancia de Azure Function App y una cuenta de Azure Storage para procesar y almacenar mensajes de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="04297-144">Create an Azure function app and an Azure storage account to process and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)


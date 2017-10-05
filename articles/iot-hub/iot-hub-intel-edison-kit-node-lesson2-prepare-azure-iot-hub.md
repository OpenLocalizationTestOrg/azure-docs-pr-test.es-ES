---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 2: Registro del dispositivo | Microsoft Docs"
description: Cree un grupo de recursos, cree una instancia de IoT Hub de Azure y registre Edison en IoT Hub de Azure mediante la CLI de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: c1465cc2-d0d9-4326-967c-64d95b61dd54
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 81584c1b7314c4331ac059b8e3ed782970588ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="08ebc-103">Creación de un centro de IoT Hub y registro de Intel Edison</span><span class="sxs-lookup"><span data-stu-id="08ebc-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="08ebc-104">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="08ebc-104">What you will do</span></span>
* <span data-ttu-id="08ebc-105">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="08ebc-105">Create a resource group.</span></span>
* <span data-ttu-id="08ebc-106">Cree una instancia de IoT Hub de Azure en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="08ebc-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="08ebc-107">Agregue Intel Edison al centro de IoT Hub de Azure mediante la interfaz de la línea de comandos de Azure (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="08ebc-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="08ebc-108">Cuando utiliza la CLI de Azure para agregar Edison a IoT Hub, el servicio genera una clave para que Edison se autentique con el servicio.</span><span class="sxs-lookup"><span data-stu-id="08ebc-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="08ebc-109">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="08ebc-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="08ebc-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="08ebc-110">What you will learn</span></span>
<span data-ttu-id="08ebc-111">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="08ebc-111">In this article, you will learn:</span></span>
* <span data-ttu-id="08ebc-112">Cómo usar la CLI de Azure para crear un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="08ebc-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="08ebc-113">Cómo crear una identidad de dispositivos para Edison en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="08ebc-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="08ebc-114">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="08ebc-114">What you need</span></span>
* <span data-ttu-id="08ebc-115">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="08ebc-115">An Azure account.</span></span> <span data-ttu-id="08ebc-116">Si no tiene ninguna cuenta de Azure, cree una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="08ebc-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="08ebc-117">Debe tener instalada la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="08ebc-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="08ebc-118">Creación de un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="08ebc-118">Create your IoT hub</span></span>
<span data-ttu-id="08ebc-119">IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT.</span><span class="sxs-lookup"><span data-stu-id="08ebc-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="08ebc-120">Para crear el centro de IoT Hub, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="08ebc-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="08ebc-121">Inicie sesión en la cuenta de Azure mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="08ebc-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="08ebc-122">Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="08ebc-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="08ebc-123">Establezca la suscripción predeterminada que desea usar mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="08ebc-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="08ebc-124">El valor de `subscription ID or name` puede verse en la salida del comando `az login` o del comando `az account list`.</span><span class="sxs-lookup"><span data-stu-id="08ebc-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="08ebc-125">Registre el proveedor con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="08ebc-125">Register the provider by running the following command.</span></span> <span data-ttu-id="08ebc-126">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="08ebc-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="08ebc-127">Debe registrar el proveedor para poder implementar el recurso de Azure que este le ofrece.</span><span class="sxs-lookup"><span data-stu-id="08ebc-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="08ebc-128">Cree un grupo de recursos denominado "iot-sample" en la región oeste de EE. UU. ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="08ebc-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="08ebc-129">`westus` es la ubicación en la que se crea el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="08ebc-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="08ebc-130">Si desea utilizar otra ubicación, puede ejecutar `az account list-locations -o table` para ver todas las ubicaciones admitidas por Azure.</span><span class="sxs-lookup"><span data-stu-id="08ebc-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="08ebc-131">Cree una instancia de IoT Hub en el grupo de recursos iot-sample ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="08ebc-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="08ebc-132">De forma predeterminada, la herramienta crea la instancia de IoT Hub con el plan de tarifa Gratis.</span><span class="sxs-lookup"><span data-stu-id="08ebc-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="08ebc-133">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="08ebc-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="08ebc-134">El nombre de su instancia de IoT Hub debe única globalmente.</span><span class="sxs-lookup"><span data-stu-id="08ebc-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="08ebc-135">Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="08ebc-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="08ebc-136">Registro de Edison en un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="08ebc-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="08ebc-137">Todos los dispositivos que envían mensajes al centro de IoT Hub y los reciben de este deben estar registrados con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="08ebc-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="08ebc-138">Registre Edison en su centro de IoT Hub ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="08ebc-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="08ebc-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="08ebc-139">Summary</span></span>
<span data-ttu-id="08ebc-140">Ha creado un centro de IoT Hub y ha registrado Edison con una identidad de dispositivo en este centro.</span><span class="sxs-lookup"><span data-stu-id="08ebc-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="08ebc-141">Ya está preparado para aprender a enviar mensajes desde Edison a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="08ebc-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08ebc-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08ebc-142">Next steps</span></span>
<span data-ttu-id="08ebc-143">[Creación de una instancia de Azure Function App y una cuenta de Azure Storage para procesar y almacenar mensajes de IoT Hub][process-and-store-iot-hub-messages]</span><span class="sxs-lookup"><span data-stu-id="08ebc-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
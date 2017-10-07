---
title: "Connect Intel Edison (C) tooAzure IoT - lección 2: registrar el dispositivo | Documentos de Microsoft"
description: Crear un grupo de recursos, crear un centro de IoT de Azure y registrar a Edison en Centro de IoT de Azure de hello mediante Hola CLI de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="cf65f-103">Creación de un centro de IoT Hub y registro de Intel Edison</span><span class="sxs-lookup"><span data-stu-id="cf65f-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cf65f-104">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="cf65f-104">What you will do</span></span>
* <span data-ttu-id="cf65f-105">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cf65f-105">Create a resource group.</span></span>
* <span data-ttu-id="cf65f-106">Crear el centro de IoT de Azure en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf65f-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="cf65f-107">Agregar el centro de IoT de Azure de toohello de Intel Edison mediante hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="cf65f-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="cf65f-108">Cuando usas hello Azure CLI tooadd centro de IoT tooyour Edison, servicio de hello genera una clave para tooauthenticate Edison con servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="cf65f-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="cf65f-109">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="cf65f-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cf65f-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="cf65f-110">What you will learn</span></span>
<span data-ttu-id="cf65f-111">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cf65f-111">In this article, you will learn:</span></span>
* <span data-ttu-id="cf65f-112">¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cf65f-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="cf65f-113">¿Cómo toocreate una identidad de dispositivo para Edison en su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cf65f-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cf65f-114">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="cf65f-114">What you need</span></span>
* <span data-ttu-id="cf65f-115">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf65f-115">An Azure account.</span></span> <span data-ttu-id="cf65f-116">Si no tiene ninguna cuenta de Azure, cree una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="cf65f-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="cf65f-117">Debe tener Hola que CLI de Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="cf65f-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="cf65f-118">Creación de un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cf65f-118">Create your IoT hub</span></span>
<span data-ttu-id="cf65f-119">IoT Hub de Azure ayuda a conectar, supervisar y administrar millones de activos de IoT.</span><span class="sxs-lookup"><span data-stu-id="cf65f-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="cf65f-120">toocreate su centro de IoT, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="cf65f-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="cf65f-121">Inicie sesión en tooyour cuenta de Azure ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="cf65f-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="cf65f-122">Una vez que la sesión se ha iniciado correctamente, aparecen todas las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="cf65f-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="cf65f-123">Establecer suscripción predeterminada de Hola que desea toouse ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="cf65f-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="cf65f-124">`subscription ID or name`puede encontrarse en la salida de hello de hello `az login` o hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="cf65f-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="cf65f-125">Registrar un proveedor Hola ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf65f-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="cf65f-126">Los proveedores de recursos son servicios que proporcionan recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf65f-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="cf65f-127">Debe registrar proveedor de Hola para poder implementar Hola recursos de Azure que Hola ofertas de proveedor.</span><span class="sxs-lookup"><span data-stu-id="cf65f-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="cf65f-128">Crear un grupo de recursos denominado ejemplo iot en región del oeste de Estados Unidos de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cf65f-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="cf65f-129">`westus`es la ubicación de hello crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cf65f-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="cf65f-130">Si desea toouse en otra ubicación, puede ejecutar `az account list-locations -o table` toosee todos Hola ubicaciones de Azure admite.</span><span class="sxs-lookup"><span data-stu-id="cf65f-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="cf65f-131">Crear un centro de IoT en grupo de recursos de ejemplo de iot de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cf65f-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="cf65f-132">De forma predeterminada, herramienta de hello crea un centro de IoT en el nivel de precios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf65f-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="cf65f-133">Para más información, consulte los [precios de Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="cf65f-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="cf65f-134">nombre de Hola de su centro de IoT debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="cf65f-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="cf65f-135">Solamente puede crear una edición F1 de Azure IoT Hub en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf65f-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="cf65f-136">Registro de Edison en un centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cf65f-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="cf65f-137">Cada dispositivo que envía el centro de IoT tooyour de mensajes y recibe mensajes desde el centro de IoT debe estar registrado con un identificador único.</span><span class="sxs-lookup"><span data-stu-id="cf65f-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="cf65f-138">Registre Edison en su centro de IoT Hub ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="cf65f-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="cf65f-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="cf65f-139">Summary</span></span>
<span data-ttu-id="cf65f-140">Ha creado un centro de IoT Hub y ha registrado Edison con una identidad de dispositivo en este centro.</span><span class="sxs-lookup"><span data-stu-id="cf65f-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="cf65f-141">Ya está listo toolearn cómo toosend mensajes Edison tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cf65f-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf65f-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf65f-142">Next steps</span></span>
<span data-ttu-id="cf65f-143">[Crear una aplicación de Azure de función y un centro de IoT de almacenamiento de Azure cuenta tooprocess y el almacén de mensajes][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="cf65f-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
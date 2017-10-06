---
title: "conversión de aaaData en puerta de enlace de IoT con borde de IoT de Azure | Documentos de Microsoft"
description: "Usar formato de Hola de tooconvert de puerta de enlace de IoT de datos de sensor a través de un módulo personalizado de borde de IoT de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conversión de datos de puerta de enlace de iot, transformación de datos de puerta de enlace de iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="4d8ca-104">Uso de la puerta de enlace de IoT para la transformación de datos de sensor con Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="4d8ca-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="4d8ca-105">Antes de empezar este tutorial, asegúrese de que se haya completado Hola siguientes lecciones en secuencia:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="4d8ca-106">Configuración de Intel NUC como una puerta de enlace de IoT</span><span class="sxs-lookup"><span data-stu-id="4d8ca-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="4d8ca-107">Usar IoT puerta de enlace tooconnect cosas toohello cloud - SensorTag tooAzure centro de IoT</span><span class="sxs-lookup"><span data-stu-id="4d8ca-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="4d8ca-108">Un objetivo de una puerta de enlace de Iot es tooprocess recopilan datos antes de enviarlo toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="4d8ca-109">Borde de IoT de Azure incorpora módulos que pueden ser el flujo de trabajo de procesamiento de datos de tooform creado y montado Hola.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="4d8ca-110">Un módulo recibe un mensaje, realiza alguna acción en él y, a continuación, moverlo para otros tooprocess módulos.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="4d8ca-111">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="4d8ca-111">What you learn</span></span>

<span data-ttu-id="4d8ca-112">Obtenga información acerca cómo toocreate una tooconvert módulo mensajes de Hola SensorTag en un formato diferente.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="4d8ca-113">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="4d8ca-113">What you do</span></span>

* <span data-ttu-id="4d8ca-114">Crear un módulo tooconvert un mensaje recibido en formato de .json Hola.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="4d8ca-115">Compile el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-115">Compile hello module.</span></span>
* <span data-ttu-id="4d8ca-116">Agregar aplicación de ejemplo de Hola módulo toohello Bilitar del borde de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="4d8ca-117">Ejecutar la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4d8ca-118">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="4d8ca-118">What you need</span></span>

* <span data-ttu-id="4d8ca-119">Hola tutoriales completada en orden:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="4d8ca-120">Configuración de Intel NUC como una puerta de enlace de IoT</span><span class="sxs-lookup"><span data-stu-id="4d8ca-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="4d8ca-121">Usar IoT puerta de enlace tooconnect cosas toohello cloud - SensorTag tooAzure centro de IoT</span><span class="sxs-lookup"><span data-stu-id="4d8ca-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="4d8ca-122">Un cliente de SSH que se ejecute en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="4d8ca-123">En Windows se recomienda PuTTY.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="4d8ca-124">Linux y macOS ya vienen con un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="4d8ca-125">dirección IP de Hola y Hola username y password tooaccess Hola puerta de enlace de cliente de SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="4d8ca-126">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="4d8ca-127">Creación de un módulo</span><span class="sxs-lookup"><span data-stu-id="4d8ca-127">Create a module</span></span>

1. <span data-ttu-id="4d8ca-128">En el equipo de host de hello, ejecutar el cliente de SSH de Hola y conectar la puerta de enlace de IoT toohello.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="4d8ca-129">Clonar archivos de código fuente de hello del módulo de conversión de Hola desde GitHub toohello directorio particular de puerta de enlace de IoT Hola ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="4d8ca-130">Se trata de un módulo nativo de Azure borde escrito en lenguaje de programación de C de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="4d8ca-131">módulo de Hello convierte formato Hola de mensajes recibidos en hello sigue uno:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="4d8ca-132">Compile el módulo de Hola</span><span class="sxs-lookup"><span data-stu-id="4d8ca-132">Compile hello module</span></span>

<span data-ttu-id="4d8ca-133">módulo de hello toocompile, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="4d8ca-134">Obtendrá un `libmy_module.so` archivo una vez completada la compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="4d8ca-135">Tome nota de la ruta de acceso absoluta de Hola de este archivo.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="4d8ca-136">Agregar aplicación de ejemplo de Hola módulo toohello BLE</span><span class="sxs-lookup"><span data-stu-id="4d8ca-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="4d8ca-137">Carpeta de ejemplos de toohello vaya ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="4d8ca-138">Abra el archivo de configuración de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="4d8ca-139">Agregar un módulo mediante la inserción de hello después toohello código `modules` sección.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="4d8ca-140">Reemplace `[Your libmy_module.so path]` en el código de hello con ruta de acceso absoluta de Hola de hello libmy_module.so' archivo.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="4d8ca-141">Reemplace el código de hello en hello `links` sección con hello sigue uno:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-141">Replace hello code in hello `links` section with hello following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="4d8ca-142">Presione `ESC`y, a continuación, escriba `:wq` archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="4d8ca-143">Ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="4d8ca-143">Run hello sample application</span></span>

1. <span data-ttu-id="4d8ca-144">Encendido hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="4d8ca-145">Establecer variable de entorno de hello SSL_CERT_FILE ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="4d8ca-146">Ejecutar la aplicación de ejemplo de Hola con el módulo agregado Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4d8ca-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="4d8ca-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d8ca-147">Next steps</span></span>

<span data-ttu-id="4d8ca-148">Se haya correctamente uso Hola IoT puerta de enlace tooconvert mensaje de saludo de SensorTag en formato de .json Hola.</span><span class="sxs-lookup"><span data-stu-id="4d8ca-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

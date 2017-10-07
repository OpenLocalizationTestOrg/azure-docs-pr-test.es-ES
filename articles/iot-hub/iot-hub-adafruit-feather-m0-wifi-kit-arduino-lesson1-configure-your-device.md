---
title: "Connect Arduino (C) tooAzure IoT - lección 1: Configurar dispositivo | Documentos de Microsoft"
description: Configure Adafruit Feather M0 WiFi por primera vez.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configurar, conectar arduino toopc, el programa de instalación arduino, panel de arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="46f67-104">Configuración del dispositivo</span><span class="sxs-lookup"><span data-stu-id="46f67-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="46f67-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="46f67-105">What you will do</span></span>
<span data-ttu-id="46f67-106">Configurar el panel de Adafruit compacto M0 Wi-Fi Arduino para usarlos por primera vez ensamblando panel hello, activando una.</span><span class="sxs-lookup"><span data-stu-id="46f67-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="46f67-107">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="46f67-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="46f67-108">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="46f67-108">What you need</span></span>
<span data-ttu-id="46f67-109">toocomplete esta operación, necesita Hola siguientes piezas el Starter Kit de Adafruit compacto M0 Wi-Fi:</span><span class="sxs-lookup"><span data-stu-id="46f67-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="46f67-110">Hola panel Adafruit compacto M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="46f67-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="46f67-111">Un cable USB A tooType de Micro B</span><span class="sxs-lookup"><span data-stu-id="46f67-111">A Micro B tooType A USB cable</span></span>

![USB Micro B a Tipo A][kit]

<span data-ttu-id="46f67-113">También necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="46f67-113">You also need:</span></span>

* <span data-ttu-id="46f67-114">Un equipo con Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="46f67-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="46f67-115">Una conexión inalámbrica para su tooconnect de panel Arduino a.</span><span class="sxs-lookup"><span data-stu-id="46f67-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="46f67-116">Una herramienta de configuración de toodownload de conexión de Internet.</span><span class="sxs-lookup"><span data-stu-id="46f67-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="46f67-117">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="46f67-117">What you will learn</span></span>
<span data-ttu-id="46f67-118">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="46f67-118">In this article, you will learn:</span></span>

* <span data-ttu-id="46f67-119">Cómo tooassemble su panel de Arduino y la energía se hacia arriba para hello siguiendo lecciones.</span><span class="sxs-lookup"><span data-stu-id="46f67-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="46f67-120">¿Cómo tooadd permisos de puerto serie en Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="46f67-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="46f67-121">Conectar el equipo de tooyour Arduino panel</span><span class="sxs-lookup"><span data-stu-id="46f67-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="46f67-122">Enchufe cable USB micro de hello en puerto USB de micro superior Hola.</span><span class="sxs-lookup"><span data-stu-id="46f67-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Puerto microUSB superior][top-micro-usb-port]

2. <span data-ttu-id="46f67-124">Plug Hola otro extremo del cable USB en el equipo.</span><span class="sxs-lookup"><span data-stu-id="46f67-124">Plug hello other end of USB cable into your computer.</span></span>

   ![Cable USB conectado a un equipo][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="46f67-126">Adición de permisos de puerto serie en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="46f67-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="46f67-127">Puede omitir esta sección si utiliza Windows o Mac OS.</span><span class="sxs-lookup"><span data-stu-id="46f67-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="46f67-128">Para Ubuntu, deberá Hola siguiendo los pasos toomake usuario de linux normal de hello tenga toooperate de permisos de hello en el puerto USB de hello de la placa de Arduino.</span><span class="sxs-lookup"><span data-stu-id="46f67-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="46f67-129">Ahora como usuario normal del terminal:</span><span class="sxs-lookup"><span data-stu-id="46f67-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="46f67-130">Verá algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="46f67-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="46f67-131">Hola "0" puede ser un número diferente, o se podrían devolver varias entradas.</span><span class="sxs-lookup"><span data-stu-id="46f67-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="46f67-132">En los primeros datos de casos Hola Hola necesitamos es `uucp`, Hola en segundo lugar es `dialout`, que es propietario del grupo de Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="46f67-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="46f67-133">Agregar grupo de usuarios toohello toohello:</span><span class="sxs-lookup"><span data-stu-id="46f67-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="46f67-134">Donde `group-name` es Hola se encontraron datos en el primer paso de Hola y `username` es el nombre de usuario de linux.</span><span class="sxs-lookup"><span data-stu-id="46f67-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="46f67-135">Necesitará toolog y de nuevo para este cambio tootake efecto y el programa de instalación de hello completa.</span><span class="sxs-lookup"><span data-stu-id="46f67-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="46f67-136">Resumen</span><span class="sxs-lookup"><span data-stu-id="46f67-136">Summary</span></span>
<span data-ttu-id="46f67-137">En este artículo, ha aprendido cómo tooconfigure el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="46f67-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="46f67-138">Hola siguiente tarea es software como preparación para ejecutar una aplicación de ejemplo en el panel de Arduino y herramientas que necesitan tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="46f67-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![El hardware está listo.][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="46f67-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46f67-140">Next steps</span></span>
<span data-ttu-id="46f67-141">[Obtener herramientas de Hola][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="46f67-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
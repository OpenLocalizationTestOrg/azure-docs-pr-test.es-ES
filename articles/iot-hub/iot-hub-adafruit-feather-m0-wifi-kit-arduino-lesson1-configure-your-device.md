---
title: "Conexión de Arduino (C) a Azure IoT - Lección 1: Configuración del dispositivo | Microsoft Docs"
description: Configure Adafruit Feather M0 WiFi por primera vez.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "configuración de Arduino, conexión de Arduino al equipo, configuración de Arduino, placa Arduino"
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
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="fbd98-104">Configuración del dispositivo</span><span class="sxs-lookup"><span data-stu-id="fbd98-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fbd98-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="fbd98-105">What you will do</span></span>
<span data-ttu-id="fbd98-106">Ensamble la placa y enciéndala para configurar la placa Arduino de Adafruit Feather M0 WiFi por primera vez.</span><span class="sxs-lookup"><span data-stu-id="fbd98-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="fbd98-107">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="fbd98-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fbd98-108">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="fbd98-108">What you need</span></span>
<span data-ttu-id="fbd98-109">Para completar esta operación, necesita las siguientes piezas del kit de inicio de Adafruit Feather M0 WiFi:</span><span class="sxs-lookup"><span data-stu-id="fbd98-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="fbd98-110">La placa Adafruit Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="fbd98-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="fbd98-111">Un cable USB Micro B a Tipo A.</span><span class="sxs-lookup"><span data-stu-id="fbd98-111">A Micro B to Type A USB cable</span></span>

![USB Micro B a Tipo A][kit]

<span data-ttu-id="fbd98-113">También necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbd98-113">You also need:</span></span>

* <span data-ttu-id="fbd98-114">Un equipo con Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="fbd98-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="fbd98-115">Una conexión inalámbrica para que la placa Arduino se conecte a los siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="fbd98-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="fbd98-116">Una conexión a Internet para descargar la herramienta de configuración.</span><span class="sxs-lookup"><span data-stu-id="fbd98-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fbd98-117">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="fbd98-117">What you will learn</span></span>
<span data-ttu-id="fbd98-118">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbd98-118">In this article, you will learn:</span></span>

* <span data-ttu-id="fbd98-119">Cómo ensamblar la placa Arduino y encenderla en las lecciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="fbd98-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="fbd98-120">Cómo agregar permisos de puerto serie en Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="fbd98-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="fbd98-121">Conexión de la placa Arduino a su equipo</span><span class="sxs-lookup"><span data-stu-id="fbd98-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="fbd98-122">Conecte el cable microUSB al puerto microUSB superior.</span><span class="sxs-lookup"><span data-stu-id="fbd98-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Puerto microUSB superior][top-micro-usb-port]

2. <span data-ttu-id="fbd98-124">Conecte el otro extremo del cable USB al equipo.</span><span class="sxs-lookup"><span data-stu-id="fbd98-124">Plug the other end of USB cable into your computer.</span></span>

   ![Cable USB conectado a un equipo][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="fbd98-126">Adición de permisos de puerto serie en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="fbd98-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="fbd98-127">Puede omitir esta sección si utiliza Windows o Mac OS.</span><span class="sxs-lookup"><span data-stu-id="fbd98-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="fbd98-128">Para Ubuntu, necesita realizar los siguientes pasos para asegurarse de que el usuario de Linux normal tiene los permisos para que funcione en el puerto USB de su placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="fbd98-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="fbd98-129">Ahora como usuario normal del terminal:</span><span class="sxs-lookup"><span data-stu-id="fbd98-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="fbd98-130">Verá algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbd98-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="fbd98-131">"0" puede ser un número diferente o se podrían devolver varias entradas.</span><span class="sxs-lookup"><span data-stu-id="fbd98-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="fbd98-132">En el primer caso, los datos que necesitamos son `uucp`, en el segundo son `dialout`, que es el propietario del grupo del archivo.</span><span class="sxs-lookup"><span data-stu-id="fbd98-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="fbd98-133">Adición del usuario al grupo:</span><span class="sxs-lookup"><span data-stu-id="fbd98-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="fbd98-134">Donde `group-name` son los datos encontrados en el primer paso, y `username` es el nombre de usuario de Linux.</span><span class="sxs-lookup"><span data-stu-id="fbd98-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="fbd98-135">Tiene que cerrar sesión y volver a iniciarla para que este cambio surta efecto y se complete la instalación.</span><span class="sxs-lookup"><span data-stu-id="fbd98-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="fbd98-136">Resumen</span><span class="sxs-lookup"><span data-stu-id="fbd98-136">Summary</span></span>
<span data-ttu-id="fbd98-137">En este artículo, ha aprendido cómo configurar la placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="fbd98-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="fbd98-138">En la siguiente tarea, instalará las herramientas y el software necesarios como preparativo para ejecutar una aplicación de ejemplo en la placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="fbd98-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![El hardware está listo.][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="fbd98-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbd98-140">Next steps</span></span>
<span data-ttu-id="fbd98-141">[Obtención de las herramientas][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="fbd98-141">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
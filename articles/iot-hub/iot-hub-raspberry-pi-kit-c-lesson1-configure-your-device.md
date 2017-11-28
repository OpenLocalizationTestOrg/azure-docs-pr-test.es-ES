---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 1: Configuración del dispositivo | Microsoft Docs"
description: "Configure Raspberry Pi 3 para utilizarla por primera vez e instale el sistema operativo gratuito Raspbian, que está optimizado para el hardware de la Raspberry Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "instalación de raspbian, descarga de raspbian, cómo instalar raspbian, configuración de raspbian, instalar raspbian para raspberry pi, instalar so para raspberry pi, instalar tarjeta sd para raspberry pi, conexión de raspberry pi, conectar a raspberry pi, conectividad de raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="45e1a-104">Configuración del dispositivo</span><span class="sxs-lookup"><span data-stu-id="45e1a-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="45e1a-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="45e1a-105">What you will do</span></span>
<span data-ttu-id="45e1a-106">Configure la Pi para utilizarla por primera vez e instale el sistema operativo Raspbian.</span><span class="sxs-lookup"><span data-stu-id="45e1a-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="45e1a-107">Raspbian es un sistema operativo gratuito que está optimizado para el hardware de Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="45e1a-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="45e1a-108">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="45e1a-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="45e1a-109">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="45e1a-109">What you will learn</span></span>
<span data-ttu-id="45e1a-110">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="45e1a-110">In this article, you will learn:</span></span>

* <span data-ttu-id="45e1a-111">Cómo instalar Raspbian en la Pi</span><span class="sxs-lookup"><span data-stu-id="45e1a-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="45e1a-112">Cómo encender la Pi mediante un cable USB</span><span class="sxs-lookup"><span data-stu-id="45e1a-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="45e1a-113">Cómo conectar la Pi a la red mediante un cable Ethernet o una red inalámbrica</span><span class="sxs-lookup"><span data-stu-id="45e1a-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="45e1a-114">Cómo agregar un LED a la placa de pruebas y conectarlo a la Pi</span><span class="sxs-lookup"><span data-stu-id="45e1a-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="45e1a-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="45e1a-115">What you need</span></span>
<span data-ttu-id="45e1a-116">Para completar esta operación, necesita las siguientes piezas del kit de inicio de Raspberry Pi 3:</span><span class="sxs-lookup"><span data-stu-id="45e1a-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="45e1a-117">La placa Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="45e1a-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="45e1a-118">La tarjeta microSD de 16 GB</span><span class="sxs-lookup"><span data-stu-id="45e1a-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="45e1a-119">La fuente de alimentación de 5 V y 2 A con un cable microUSB de 6 pies</span><span class="sxs-lookup"><span data-stu-id="45e1a-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="45e1a-120">La placa de pruebas</span><span class="sxs-lookup"><span data-stu-id="45e1a-120">The breadboard</span></span>
* <span data-ttu-id="45e1a-121">Los cables conectores</span><span class="sxs-lookup"><span data-stu-id="45e1a-121">Connector wires</span></span>
* <span data-ttu-id="45e1a-122">Una resistencia de 560 Ohm</span><span class="sxs-lookup"><span data-stu-id="45e1a-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="45e1a-123">Un LED difuso de 10 mm</span><span class="sxs-lookup"><span data-stu-id="45e1a-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="45e1a-124">El cable Ethernet</span><span class="sxs-lookup"><span data-stu-id="45e1a-124">The Ethernet cable</span></span>

![Los elementos del kit de inicio](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="45e1a-126">También necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="45e1a-126">You also need:</span></span>

* <span data-ttu-id="45e1a-127">Una conexión cableada o inalámbrica para que la Pi se conecte a los siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="45e1a-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="45e1a-128">Un adaptador de USB a SD o una tarjeta miniSD para grabar la imagen del SO en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="45e1a-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="45e1a-129">Un equipo con Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="45e1a-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="45e1a-130">El equipo se usa para instalar Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="45e1a-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="45e1a-131">Una conexión a Internet para descargar las herramientas y el software necesarios.</span><span class="sxs-lookup"><span data-stu-id="45e1a-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="45e1a-132">Instalación de Raspbian en la tarjeta microSD</span><span class="sxs-lookup"><span data-stu-id="45e1a-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="45e1a-133">Prepare la tarjeta microSD para instalar la imagen de Raspbian.</span><span class="sxs-lookup"><span data-stu-id="45e1a-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="45e1a-134">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="45e1a-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="45e1a-135">[Descargue](https://www.raspberrypi.org/downloads/raspbian/) el archivo .zip para Raspbian Jessie con Pixel.</span><span class="sxs-lookup"><span data-stu-id="45e1a-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="45e1a-136">Extraiga la imagen de Raspbian en una carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="45e1a-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="45e1a-137">Instale Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="45e1a-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="45e1a-138">[Descargue](https://www.etcher.io) e instale la utilidad de grabadora de tarjetas SD Etcher.</span><span class="sxs-lookup"><span data-stu-id="45e1a-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="45e1a-139">Ejecute Etcher y seleccione la imagen de Raspbian que extrajo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="45e1a-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="45e1a-140">Seleccione la unidad de la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="45e1a-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="45e1a-141">Tenga en cuenta que es posible que Etcher ya haya seleccionado la unidad correcta.</span><span class="sxs-lookup"><span data-stu-id="45e1a-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="45e1a-142">Haga clic en **Flash** para instalar Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="45e1a-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="45e1a-143">Quite la tarjeta microSD del equipo cuando se complete la instalación.</span><span class="sxs-lookup"><span data-stu-id="45e1a-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="45e1a-144">Es seguro quitar la tarjeta microSD directamente porque Etcher expulsa o desmonta la tarjeta microSD automáticamente al acabar.</span><span class="sxs-lookup"><span data-stu-id="45e1a-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="45e1a-145">Inserte la tarjeta microSD en la PI.</span><span class="sxs-lookup"><span data-stu-id="45e1a-145">Insert the microSD card into your Pi.</span></span>

![Inserción de la tarjeta SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="45e1a-147">Encendido de la Pi</span><span class="sxs-lookup"><span data-stu-id="45e1a-147">Turn on Pi</span></span>
<span data-ttu-id="45e1a-148">Encienda la Pi mediante un cable microUSB y la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="45e1a-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Encendido](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="45e1a-150">Es importante utilizar la fuente de alimentación del kit, que tiene al menos 2 A, para asegurarse de que el dispositivo Raspberry cuente con la energía suficiente como para funcionar correctamente.</span><span class="sxs-lookup"><span data-stu-id="45e1a-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="45e1a-151">Habilite SSH</span><span class="sxs-lookup"><span data-stu-id="45e1a-151">Enable SSH</span></span>
<span data-ttu-id="45e1a-152">A partir de la versión de noviembre de 2016, Raspbian tiene el servidor SSH deshabilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="45e1a-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="45e1a-153">Debe habilitarlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="45e1a-153">You need to enable it manually.</span></span> <span data-ttu-id="45e1a-154">Puede consultar las [instrucciones oficiales](https://www.raspberrypi.org/documentation/remote-access/ssh/) o conectar un monitor e ir a **Preferences -> Raspberry Pi Configuration** (Preferencias -> Configuración de Raspberry Pi) para habilitar SSH.</span><span class="sxs-lookup"><span data-stu-id="45e1a-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="45e1a-155">Conexión de Raspberry Pi 3 a la red</span><span class="sxs-lookup"><span data-stu-id="45e1a-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="45e1a-156">Puede conectar la Pi a una red cableada o a una red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="45e1a-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="45e1a-157">Asegúrese de que la Pi se conecta a la misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="45e1a-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="45e1a-158">Por ejemplo, puede conectar el dispositivo al mismo conmutador al que está conectado su equipo.</span><span class="sxs-lookup"><span data-stu-id="45e1a-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="45e1a-159">Conexión a una red cableada</span><span class="sxs-lookup"><span data-stu-id="45e1a-159">Connect to a wired network</span></span>
<span data-ttu-id="45e1a-160">Utilice el cable Ethernet para conectar la Pi a la red cableada.</span><span class="sxs-lookup"><span data-stu-id="45e1a-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="45e1a-161">Los dos LED de la Pi se encienden si se establece la conexión.</span><span class="sxs-lookup"><span data-stu-id="45e1a-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Conexión mediante un cable Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="45e1a-163">Conexión a una red inalámbrica</span><span class="sxs-lookup"><span data-stu-id="45e1a-163">Connect to a wireless network</span></span>
<span data-ttu-id="45e1a-164">Siga las [instrucciones](https://www.raspberrypi.org/learning/software-guide/wifi/) de Raspberry Pi Foundation para conectar la Pi a la red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="45e1a-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="45e1a-165">Estas instrucciones requieren que primero conecte un monitor y un teclado a la Pi.</span><span class="sxs-lookup"><span data-stu-id="45e1a-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="45e1a-166">Conexión del LED a la Pi</span><span class="sxs-lookup"><span data-stu-id="45e1a-166">Connect the LED to Pi</span></span>
<span data-ttu-id="45e1a-167">Para completar esta tarea, utilice la [placa de pruebas](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), los cables conectores, el LED y la resistencia.</span><span class="sxs-lookup"><span data-stu-id="45e1a-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="45e1a-168">Conecte estas piezas a los puertos de [entrada y salida de uso general](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) de la Pi.</span><span class="sxs-lookup"><span data-stu-id="45e1a-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Placa de pruebas, LED y resistencia](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="45e1a-170">Conecte la pata más corta del LED a la **GND de los GPIO (pin 6)**.</span><span class="sxs-lookup"><span data-stu-id="45e1a-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="45e1a-171">Conecte la pata más larga del LED a una de la resistencia.</span><span class="sxs-lookup"><span data-stu-id="45e1a-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="45e1a-172">Conecte la otra pata de la resistencia a los **GPIO 4 (pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="45e1a-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="45e1a-173">Tenga en cuenta que la polaridad LED es importante.</span><span class="sxs-lookup"><span data-stu-id="45e1a-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="45e1a-174">Esta opción de polaridad comúnmente se conoce como "bajo activo".</span><span class="sxs-lookup"><span data-stu-id="45e1a-174">This polarity setting is commonly known as Active Low.</span></span>

![Diagrama de asignación de pines](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="45e1a-176">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="45e1a-176">Congratulations!</span></span> <span data-ttu-id="45e1a-177">Ha configurado correctamente la Pi.</span><span class="sxs-lookup"><span data-stu-id="45e1a-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="45e1a-178">Resumen</span><span class="sxs-lookup"><span data-stu-id="45e1a-178">Summary</span></span>
<span data-ttu-id="45e1a-179">En este artículo, ha aprendido a configurar la Pi instalando Raspbian, conectándola a una red y agregando un LED a la Pi.</span><span class="sxs-lookup"><span data-stu-id="45e1a-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="45e1a-180">Tenga en cuenta que todavía el LED no se encenderá.</span><span class="sxs-lookup"><span data-stu-id="45e1a-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="45e1a-181">En la siguiente tarea, instalará las herramientas y el software necesarios como preparativo para ejecutar una aplicación de ejemplo en la Pi.</span><span class="sxs-lookup"><span data-stu-id="45e1a-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![El hardware está listo.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="45e1a-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45e1a-183">Next steps</span></span>
[<span data-ttu-id="45e1a-184">Obtener las herramientas</span><span class="sxs-lookup"><span data-stu-id="45e1a-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)


---
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 1: Configurar dispositivo | Documentos de Microsoft"
description: "Configure frambuesa Pi 3 para usarlo por primera vez e instale hello Raspbian OS, un sistema operativo disponible que esté optimizado para hello hardware frambuesa Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "instalación raspbian, descarga raspbian, cómo tooinstall raspbian, raspbian el programa de instalación, frambuesas pi instalación raspbian, frambuesas pi instalar os, frambuesas pi sd tarjeta install, frambuesas pi connect, conectar conectividad de pi de pi, frambuesas tooraspberry"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="0a5ac-104">Configuración del dispositivo</span><span class="sxs-lookup"><span data-stu-id="0a5ac-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0a5ac-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="0a5ac-105">What you will do</span></span>
<span data-ttu-id="0a5ac-106">Configure Pi para usarlos por primera vez e instale el sistema operativo de hello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="0a5ac-107">Raspbian es un sistema operativo disponible que esté optimizado para hello hardware frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="0a5ac-108">Si tiene problemas, se pueden buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0a5ac-108">If you have any problems, you can seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0a5ac-109">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="0a5ac-109">What you will learn</span></span>
<span data-ttu-id="0a5ac-110">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a5ac-110">In this article, you will learn:</span></span>

* <span data-ttu-id="0a5ac-111">Cómo tooinstall Raspbian sobre Pi.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="0a5ac-112">¿Cómo toopower seguridad Pi mediante un cable USB.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="0a5ac-113">¿Cómo tooconnect Pi toohello de red mediante un cable Ethernet o una red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="0a5ac-114">Cómo breadboard tooadd un toohello LED y conéctelo tooPi.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="0a5ac-115">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="0a5ac-115">What you will need</span></span>
<span data-ttu-id="0a5ac-116">toocomplete esta operación, necesita Hola siguientes partes de los Starter Kit de frambuesa Pi 3:</span><span class="sxs-lookup"><span data-stu-id="0a5ac-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="0a5ac-117">Hola placa de frambuesa Pi 3</span><span class="sxs-lookup"><span data-stu-id="0a5ac-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="0a5ac-118">tarjeta microSD de 16 GB de Hola</span><span class="sxs-lookup"><span data-stu-id="0a5ac-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="0a5ac-119">Hola 5 voltios 2 amp alimentación con cable de hello pie 6 micro USB</span><span class="sxs-lookup"><span data-stu-id="0a5ac-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="0a5ac-120">breadboard Hola</span><span class="sxs-lookup"><span data-stu-id="0a5ac-120">hello breadboard</span></span>
* <span data-ttu-id="0a5ac-121">Los cables conectores</span><span class="sxs-lookup"><span data-stu-id="0a5ac-121">Connector wires</span></span>
* <span data-ttu-id="0a5ac-122">Una resistencia de 560 Ohm</span><span class="sxs-lookup"><span data-stu-id="0a5ac-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="0a5ac-123">Un LED difuso de 10 mm</span><span class="sxs-lookup"><span data-stu-id="0a5ac-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="0a5ac-124">Hola cable Ethernet</span><span class="sxs-lookup"><span data-stu-id="0a5ac-124">hello Ethernet cable</span></span>

![Los elementos del kit de inicio](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="0a5ac-126">También necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a5ac-126">You also need:</span></span>

* <span data-ttu-id="0a5ac-127">Una conexión con cable o inalámbrica para Pi tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="0a5ac-128">Un SD USB adaptador o miniSD tarjeta tooburn Hola imagen de sistema operativo en tarjeta microSD de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-128">A USB-SD adapter or miniSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="0a5ac-129">Un equipo con Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="0a5ac-130">equipo de Hello es usado tooinstall Raspbian en tarjeta microSD de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="0a5ac-131">Un toodownload de conexión de Internet Hola software y herramientas que necesitan.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="0a5ac-132">Instalar Raspbian en tarjeta microSD de Hola</span><span class="sxs-lookup"><span data-stu-id="0a5ac-132">Install Raspbian on hello microSD card</span></span>
<span data-ttu-id="0a5ac-133">Preparar la tarjeta microSD de hello para la instalación de la imagen de Raspbian Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="0a5ac-134">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="0a5ac-135">[Descargar](https://www.raspberrypi.org/downloads/raspbian/) archivo .zip de hello para Raspbian Jessie con píxeles.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="0a5ac-136">Extraer hello Raspbian imagen tooa carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="0a5ac-137">Instalar Raspbian toohello microSD tarjeta.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="0a5ac-138">[Descargar](https://www.etcher.io) e instalar la utilidad de grabadora de tarjeta de hello SD de creación.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="0a5ac-139">Ejecute creación y seleccione la imagen de Raspbian Hola que ha extraído en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="0a5ac-140">Seleccione la unidad de tarjeta microSD Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="0a5ac-141">Tenga en cuenta que creación probablemente ya seleccionó unidad correcta Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="0a5ac-142">Haga clic en **Flash** tooinstall Raspbian toohello microSD tarjeta.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="0a5ac-143">Quitar tarjeta microSD de hello del equipo cuando se completa la instalación.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="0a5ac-144">Es tarjeta microSD de tooremove seguro Hola directamente porque creación expulsa automáticamente o desmonta tarjeta microSD de hello tras la finalización.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-144">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="0a5ac-145">Inserte la tarjeta microSD de hello en Pi.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-145">Insert hello microSD card into Pi.</span></span>

![Inserte una tarjeta SD Hola](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="0a5ac-147">Encendido de la Pi</span><span class="sxs-lookup"><span data-stu-id="0a5ac-147">Turn on Pi</span></span>
<span data-ttu-id="0a5ac-148">Activar Pi mediante cable USB micro de Hola y fuente de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Encendido](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="0a5ac-150">Es importante toouse Hola de alimentación en el kit de Hola por lo menos 2A toomake seguro de que su frambuesa tiene suficiente energía toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="0a5ac-151">Habilite SSH</span><span class="sxs-lookup"><span data-stu-id="0a5ac-151">Enable SSH</span></span>
<span data-ttu-id="0a5ac-152">A partir de la versión de noviembre de 2016 de hello, Raspbian tiene servidor SSH Hola deshabilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="0a5ac-153">Necesita tooenable lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-153">You need tooenable it manually.</span></span> <span data-ttu-id="0a5ac-154">Puede hacer referencia a toohello [oficiales instrucciones](https://www.raspberrypi.org/documentation/remote-access/ssh/) o conectar un monitor y vaya demasiado**Preferencias -> configuración de frambuesa Pi** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="0a5ac-155">Conectar red toohello de frambuesa Pi 3</span><span class="sxs-lookup"><span data-stu-id="0a5ac-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="0a5ac-156">Puede conectarse tooa Pi con el cable de red o red inalámbrica tooa.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="0a5ac-157">Asegúrese de que ese Pi está conectado toohello misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="0a5ac-158">Por ejemplo, puede conectarse toohello Pi a que mismo conmutador que el equipo está conectado.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="0a5ac-159">Conectar tooa de red cableada</span><span class="sxs-lookup"><span data-stu-id="0a5ac-159">Connect tooa wired network</span></span>
<span data-ttu-id="0a5ac-160">Utilice Hola Ethernet por cable tooconnect tooyour de Pi de red cableada.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="0a5ac-161">Hello dos LED de Pi activar si se establece conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Conexión mediante un cable Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="0a5ac-163">Conectar red inalámbrica tooa</span><span class="sxs-lookup"><span data-stu-id="0a5ac-163">Connect tooa wireless network</span></span>
<span data-ttu-id="0a5ac-164">Siga hello [instrucciones](https://www.raspberrypi.org/learning/software-guide/wifi/) de red inalámbrica de hello frambuesa Pi Foundation tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="0a5ac-165">Estas instrucciones requieren toofirst conectar un monitor y un teclado tooPi.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="0a5ac-166">Conectar Hola LED tooPi</span><span class="sxs-lookup"><span data-stu-id="0a5ac-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="0a5ac-167">toocomplete esta tarea, utilice hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), Hola cables de conector, LED de Hola y Hola resistencia.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="0a5ac-168">Conéctelos toohello [entrada/salida de propósito general](https://www.raspberrypi.org/documentation/usage/gpio/) puertos (GPIO) de Pi.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Placa de pruebas, LED y resistencia](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="0a5ac-170">Conectar la autenticación mutua más corto de Hola de hello LED demasiado**GPIO GND (Pin 6)**.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="0a5ac-171">Conectar la autenticación mutua en más de autenticación mutua de tooone LED de resistencia de Hola Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="0a5ac-172">Conectar Hola otra sección de resistencia de hello demasiado**GPIO 4 (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="0a5ac-173">Tenga en cuenta que la polaridad Hola LED es importante.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="0a5ac-174">Esta opción de polaridad comúnmente se conoce como "bajo activo".</span><span class="sxs-lookup"><span data-stu-id="0a5ac-174">This polarity setting is commonly known as Active Low.</span></span>

![Diagrama de asignación de pines](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="0a5ac-176">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="0a5ac-176">Congratulations!</span></span> <span data-ttu-id="0a5ac-177">Ha configurado correctamente la Pi.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="0a5ac-178">Resumen</span><span class="sxs-lookup"><span data-stu-id="0a5ac-178">Summary</span></span>
<span data-ttu-id="0a5ac-179">En este artículo, ha aprendido cómo Pi tooconfigure mediante la instalación Raspbian, conexión Pi tooa de la red y conecta un tooPi LED.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="0a5ac-180">Tenga en cuenta que Hola que LED aún no ilumina.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="0a5ac-181">Hola siguiente tarea es software en preparación para la ejecución de una aplicación de ejemplo sobre Pi y herramientas que necesitan tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="0a5ac-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![El hardware está listo.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="0a5ac-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a5ac-183">Next steps</span></span>
[<span data-ttu-id="0a5ac-184">Obtener herramientas de Hola</span><span class="sxs-lookup"><span data-stu-id="0a5ac-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)


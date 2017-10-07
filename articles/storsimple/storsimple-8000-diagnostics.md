---
title: dispositivo de StorSimple 8000 tootroubleshoot herramienta aaaDiagnostics | Documentos de Microsoft
description: "Describe los modos de dispositivo de StorSimple de Hola y explica cómo toouse Windows PowerShell para StorSimple toochange Hola modo del dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="b040e-103">Usar Hola herramienta de diagnóstico de StorSimple tootroubleshoot 8000 series problemas del dispositivo</span><span class="sxs-lookup"><span data-stu-id="b040e-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="b040e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b040e-104">Overview</span></span>

<span data-ttu-id="b040e-105">Hola herramienta de diagnóstico de StorSimple diagnostica problemas relacionados toosystem, rendimiento, red y estado del componente de hardware para un dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="b040e-106">herramienta de diagnóstico de Hola se puede usar en distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="b040e-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="b040e-107">Estos escenarios incluyen la planeación de la carga de trabajo, implementar un dispositivo de StorSimple, evaluar el entorno de red de Hola y determinar el rendimiento de Hola de un dispositivo operativo.</span><span class="sxs-lookup"><span data-stu-id="b040e-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="b040e-108">En este artículo se proporciona información general de la herramienta de diagnóstico de Hola y describe cómo se puede utilizar la herramienta Hola con un dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="b040e-109">herramienta de diagnóstico de Hello sirve principalmente para dispositivos de StorSimple 8000 series locales (8100 y 8600).</span><span class="sxs-lookup"><span data-stu-id="b040e-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="b040e-110">Ejecución de la herramienta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b040e-110">Run diagnostics tool</span></span>

<span data-ttu-id="b040e-111">Esta herramienta se puede ejecutar mediante la interfaz de Windows PowerShell de hello de dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="b040e-112">Hay dos maneras de tooaccess Hola interfaz local del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b040e-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="b040e-113">[Consola serie del dispositivo use PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b040e-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="b040e-114">[Acceso remoto a herramienta de Hola a través de hello Windows PowerShell para StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b040e-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="b040e-115">En este artículo, se supone que se ha conectado toohello consola serie del dispositivo mediante PuTTY.</span><span class="sxs-lookup"><span data-stu-id="b040e-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="b040e-116">herramienta de diagnóstico de hello toorun</span><span class="sxs-lookup"><span data-stu-id="b040e-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="b040e-117">Una vez que se ha conectado toohello de interfaz de Windows PowerShell del dispositivo de hello, realizar Hola siguiendo los pasos toorun Hola cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b040e-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="b040e-118">Inicie sesión en la consola serie del dispositivo toohello siguiendo los pasos de hello en [consola serie del dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b040e-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="b040e-119">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="b040e-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="b040e-120">Si no se especifica el parámetro de ámbito de hello, Hola cmdlet ejecuta todas las pruebas de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="b040e-121">Estas pruebas incluyen el sistema, el estado de los componentes de hardware, la red y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b040e-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="b040e-122">toorun solo una prueba concreta, especifique el parámetro de ámbito de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="b040e-123">Por ejemplo, toorun solo Hola prueba de red, tipo</span><span class="sxs-lookup"><span data-stu-id="b040e-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="b040e-124">Seleccione y copie la salida de hello de hello PuTTY ventana en un archivo de texto para su posterior análisis.</span><span class="sxs-lookup"><span data-stu-id="b040e-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="b040e-125">Herramienta de diagnóstico de escenarios toouse Hola</span><span class="sxs-lookup"><span data-stu-id="b040e-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="b040e-126">Utilice Hola diagnósticos herramienta tootroubleshoot Hola red, el rendimiento, el sistema y hardware mantenimiento del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="b040e-127">Algunos posibles escenarios son:</span><span class="sxs-lookup"><span data-stu-id="b040e-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="b040e-128">**Dispositivo sin conexión**: su dispositivo de StorSimple de la serie 8000 está desconectado.</span><span class="sxs-lookup"><span data-stu-id="b040e-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="b040e-129">Sin embargo, desde la interfaz de Windows PowerShell de hello, parece que ambos controladores Hola están activados y ejecutándose.</span><span class="sxs-lookup"><span data-stu-id="b040e-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="b040e-130">También puede utilizar esta herramienta toothen determinar el estado de la red de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="b040e-131">No utilice esta configuración de red y el rendimiento de tooassess de herramienta en un dispositivo antes de registro de hello (o la configuración mediante el Asistente para la instalación).</span><span class="sxs-lookup"><span data-stu-id="b040e-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="b040e-132">Una dirección IP válida se asigna toohello dispositivo durante el registro y el Asistente para la instalación.</span><span class="sxs-lookup"><span data-stu-id="b040e-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="b040e-133">Puede ejecutar este cmdlet en un dispositivo que no esté registrado para conocer el estado del hardware y del sistema.</span><span class="sxs-lookup"><span data-stu-id="b040e-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="b040e-134">Utilice el parámetro de ámbito de hello, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b040e-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="b040e-135">**Problemas del dispositivo persistente** -están experimentando problemas de dispositivo que parezcan toopersist.</span><span class="sxs-lookup"><span data-stu-id="b040e-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="b040e-136">Por ejemplo, error en el registro.</span><span class="sxs-lookup"><span data-stu-id="b040e-136">For instance, registration is failing.</span></span> <span data-ttu-id="b040e-137">Puede también tratarse de problemas del dispositivo después de hello dispositivo registrado correctamente y en funcionamiento durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="b040e-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="b040e-138">En este caso, puede usar esta herramienta para la solución de problemas preliminar antes de registrar una solicitud de servicio con el soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b040e-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="b040e-139">Le recomendamos que ejecute esta salida de hello de herramienta y la captura de esta herramienta.</span><span class="sxs-lookup"><span data-stu-id="b040e-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="b040e-140">A continuación, puede proporcionar esta salida tooSupport tooexpedite solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="b040e-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="b040e-141">Si existe algún error en el componente de hardware o el clúster, debe registrar una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="b040e-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="b040e-142">**Rendimiento bajo del dispositivo**: el dispositivo de StorSimple es lento.</span><span class="sxs-lookup"><span data-stu-id="b040e-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="b040e-143">En este caso, ejecute este cmdlet con tooperformance de conjunto de parámetros de ámbito.</span><span class="sxs-lookup"><span data-stu-id="b040e-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="b040e-144">Analizar la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="b040e-144">Analyze hello output.</span></span> <span data-ttu-id="b040e-145">Obtener en la nube hello las latencias de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="b040e-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="b040e-146">Hola uso notificado latencias como máximo destino factible, factor en cierta sobrecarga para el procesamiento de datos interno de hello y, a continuación, implementar las cargas de trabajo de hello en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="b040e-147">Para obtener más información, consulte demasiado[usar Hola red prueba tootroubleshoot dispositivo rendimiento](#network-test).</span><span class="sxs-lookup"><span data-stu-id="b040e-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="b040e-148">Salidas de ejemplo y prueba de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b040e-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="b040e-149">Prueba de hardware</span><span class="sxs-lookup"><span data-stu-id="b040e-149">Hardware test</span></span>

<span data-ttu-id="b040e-150">Esta prueba determina el estado de Hola de componentes de hardware de hello, el firmware USM Hola y el firmware de disco de hello ejecutando en el sistema.</span><span class="sxs-lookup"><span data-stu-id="b040e-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="b040e-151">componentes de hardware de Hello notificados son los componentes de esa prueba Hola errores o no están presentes en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="b040e-152">versiones de firmware de disco y el firmware USM Hola se notifican para hello controlador 0, 1 de controlador y componentes comparten en el sistema.</span><span class="sxs-lookup"><span data-stu-id="b040e-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="b040e-153">Para obtener una lista completa de los componentes de hardware, vaya a:</span><span class="sxs-lookup"><span data-stu-id="b040e-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="b040e-154">Componentes de la caja principal</span><span class="sxs-lookup"><span data-stu-id="b040e-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="b040e-155">Componentes de la caja EBOD</span><span class="sxs-lookup"><span data-stu-id="b040e-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="b040e-156">Si prueba de hardware de hello informa de componentes con errores, [iniciar sesión en una solicitud de servicio con Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b040e-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="b040e-157">La salida de ejemplo de la prueba de hardware se ejecuta en un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="b040e-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="b040e-158">Esta es una salida de ejemplo de un dispositivo de StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="b040e-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="b040e-159">En el dispositivo de modelo de hello 8100, Hola alojamiento de EBOD no está presente.</span><span class="sxs-lookup"><span data-stu-id="b040e-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="b040e-160">Por lo tanto, no se notifican los componentes del controlador EBOD Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-160">Hence, hello EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="b040e-161">Prueba del sistema</span><span class="sxs-lookup"><span data-stu-id="b040e-161">System test</span></span>

<span data-ttu-id="b040e-162">Esta prueba notifica información del sistema hello, hello las actualizaciones disponibles, información de clúster de Hola e información del servicio de hello para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="b040e-163">información del sistema Hola incluye modelo hello, número de serie del dispositivo, zona horaria, el estado del controlador y versión de detallado del software de hello ejecutando en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="b040e-164">Hola toounderstand distintos parámetros del sistema se notifican como salida de hello, vaya demasiado[interpretar la información del sistema](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="b040e-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="b040e-165">disponibilidad de la actualización de Hello informa de si los modos normal y el mantenimiento de hello están disponibles y sus nombres de paquete asociado.</span><span class="sxs-lookup"><span data-stu-id="b040e-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="b040e-166">Si `RegularUpdates` y `MaintenanceModeUpdates` son `false`, esto indica que no hay disponibles actualizaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="b040e-167">El dispositivo está actualizado.</span><span class="sxs-lookup"><span data-stu-id="b040e-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="b040e-168">información de clúster de Hello contiene información de hello en diversos componentes lógicos de todos los grupos de clúster HCS hello y sus Estados respectivos.</span><span class="sxs-lookup"><span data-stu-id="b040e-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="b040e-169">Si ve un grupo de clúster sin conexión en esta sección del informe de hello, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b040e-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="b040e-170">información de servicio de Hello incluye nombres de Hola y Estados del programa Hola a todos los HCS y servicios de elementos de configuración que se ejecutan en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="b040e-171">Esta información es útil para hello Microsoft Support para solucionar el problema con un dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="b040e-172">Salida de ejemplo de la prueba del sistema ejecutada en un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="b040e-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="b040e-173">Este es un resultado de ejemplo de Hola sistema serie de pruebas en un dispositivo 8100.</span><span class="sxs-lookup"><span data-stu-id="b040e-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="b040e-174">Prueba de red</span><span class="sxs-lookup"><span data-stu-id="b040e-174">Network test</span></span>

<span data-ttu-id="b040e-175">Esta prueba valida Hola estado de interfaces de red de hello, puertos, DNS y NTP conectividad con el servidor, SSL certificado, las credenciales de cuenta de almacenamiento, servidores de actualización de toohello de conectividad y conectividad de proxy web en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="b040e-176">Salida de ejemplo de la prueba de red solo cuando está habilitado DATA0</span><span class="sxs-lookup"><span data-stu-id="b040e-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="b040e-177">Este es un resultado de ejemplo de dispositivo 8100 Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="b040e-178">Puede ver en la salida de hello que:</span><span class="sxs-lookup"><span data-stu-id="b040e-178">You can see in hello output that:</span></span>
* <span data-ttu-id="b040e-179">Solo las interfaces de red DATA 0 y DATA 1 están habilitadas y configuradas.</span><span class="sxs-lookup"><span data-stu-id="b040e-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="b040e-180">2-5 de datos no están habilitados en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="b040e-181">configuración del servidor DNS Hello es válida y Hola dispositivo puede conectarse a través del servidor DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="b040e-182">Hola conectividad con el servidor NTP también es correcto.</span><span class="sxs-lookup"><span data-stu-id="b040e-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="b040e-183">Los puertos 80 y 443 están abiertos.</span><span class="sxs-lookup"><span data-stu-id="b040e-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="b040e-184">Sin embargo, el puerto 9354 está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="b040e-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="b040e-185">En función de hello [requisitos de sistema de red](storsimple-system-requirements.md), necesita tooopen este puerto para la comunicación de bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="b040e-186">certificación de Hello SSL es válido.</span><span class="sxs-lookup"><span data-stu-id="b040e-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="b040e-187">puede conectar el dispositivo de Hello toohello cuenta de almacenamiento: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="b040e-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="b040e-188">servidores de tooUpdate de conectividad de Hello es válido.</span><span class="sxs-lookup"><span data-stu-id="b040e-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="b040e-189">proxy de Hello web no está configurado en este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="b040e-190">Salida de ejemplo de la prueba de red cuando se habilitan DATA0 y DATA1</span><span class="sxs-lookup"><span data-stu-id="b040e-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="b040e-191">Prueba de rendimiento</span><span class="sxs-lookup"><span data-stu-id="b040e-191">Performance test</span></span>

<span data-ttu-id="b040e-192">Esta prueba informes de rendimiento de hello en la nube a través de las latencias de lectura y escritura de hello en la nube para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="b040e-193">Esta herramienta puede ser tooestablish usa una línea de base de rendimiento en la nube de Hola que se puede lograr con StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="b040e-194">Hola herramienta informes Hola máximo rendimiento (escenario de mejor caso para las latencias de lectura y escritura) que puede obtener la conexión.</span><span class="sxs-lookup"><span data-stu-id="b040e-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="b040e-195">Como herramienta de hello notifica un rendimiento máximo alcanzable hello, podemos usar Hola notifique las latencias de lectura y escritura como destinos al implementar hello las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b040e-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="b040e-196">prueba de Hello simula tamaños de blob de hello asociados con los tipos de otro volumen de hello en dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="b040e-197">Los niveles normales y las copias de seguridad de volúmenes anclados localmente usan un tamaño de blob de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="b040e-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="b040e-198">Los volúmenes en capas con la opción de archivado marcada usan un tamaño de datos de blob de 512 KB.</span><span class="sxs-lookup"><span data-stu-id="b040e-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="b040e-199">Si el dispositivo tiene configurado volúmenes anclados localmente y en niveles, solo Hola prueba too64 KB blob correspondiente se ejecuta el tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="b040e-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="b040e-200">toouse esta herramienta, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b040e-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="b040e-201">En primer lugar, cree una mezcla de volúmenes en capas y volúmenes anclados localmente con la opción de archivado marcada.</span><span class="sxs-lookup"><span data-stu-id="b040e-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="b040e-202">Esta acción garantiza que esa herramienta Hola ejecuta pruebas de Hola de 64 KB y 512 KB tamaños de blob.</span><span class="sxs-lookup"><span data-stu-id="b040e-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="b040e-203">Ejecute el cmdlet de hello después de haber creado y configurado los volúmenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="b040e-204">Escriba:</span><span class="sxs-lookup"><span data-stu-id="b040e-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="b040e-205">Tome nota de las latencias de lectura y escritura de hello notificados por herramienta Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="b040e-206">Esta prueba puede tardar varios toorun minutos antes de notificar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="b040e-207">Si las latencias de conexión de hello son todos en hello intervalo esperado, hello latencias notificadas por hello herramienta pueden utilizarse como destino factible máximo al implementar las cargas de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="b040e-208">Estime cierta sobrecarga en el procesamiento de datos interno.</span><span class="sxs-lookup"><span data-stu-id="b040e-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="b040e-209">Si las latencias de lectura y escritura de hello notifican por la herramienta de diagnóstico de hello son altas:</span><span class="sxs-lookup"><span data-stu-id="b040e-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="b040e-210">Configurar el análisis de almacenamiento para los servicios blob y analizar Hola salida toounderstand Hola latencias de hello cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b040e-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="b040e-211">Para obtener instrucciones detalladas, consulte demasiado[habilitar y configurar el análisis de almacenamiento](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b040e-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="b040e-212">Si esas latencias también son números toohello alta y comparable que recibió de hello herramienta de diagnóstico de StorSimple, a continuación, deberá toolog una solicitud de servicio con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b040e-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="b040e-213">Si se están quedando sin las latencias de cuenta de almacenamiento de hello, póngase en contacto con su tooinvestigate de administrador de red emite alguna latencia en la red.</span><span class="sxs-lookup"><span data-stu-id="b040e-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="b040e-214">Salida de ejemplo de una prueba de rendimiento ejecutada en un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="b040e-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="b040e-215">Apéndice: interpretación de la información del sistema</span><span class="sxs-lookup"><span data-stu-id="b040e-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="b040e-216">Aquí es una tabla que describe qué Hola diversos parámetros de Windows PowerShell en información del sistema Hola se asignan a.</span><span class="sxs-lookup"><span data-stu-id="b040e-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="b040e-217">Parámetro de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b040e-217">PowerShell Parameter</span></span>    | <span data-ttu-id="b040e-218">Descripción</span><span class="sxs-lookup"><span data-stu-id="b040e-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="b040e-219">Id. de instancia</span><span class="sxs-lookup"><span data-stu-id="b040e-219">Instance ID</span></span>             | <span data-ttu-id="b040e-220">Cada controlador lleva asociado un identificador único o un GUID.</span><span class="sxs-lookup"><span data-stu-id="b040e-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="b040e-221">Nombre</span><span class="sxs-lookup"><span data-stu-id="b040e-221">Name</span></span>                    | <span data-ttu-id="b040e-222">nombre descriptivo de Hello de dispositivo de hello conforme a la configuración a través del portal de Azure de Hola durante la implementación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="b040e-223">nombre descriptivo de Hello predeterminado es el número de serie del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="b040e-224">Modelo</span><span class="sxs-lookup"><span data-stu-id="b040e-224">Model</span></span>                   | <span data-ttu-id="b040e-225">modelo de Hola de su dispositivo de la serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="b040e-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="b040e-226">modelo de Hello puede ser 8100 o 8600.</span><span class="sxs-lookup"><span data-stu-id="b040e-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="b040e-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="b040e-227">SerialNumber</span></span>            | <span data-ttu-id="b040e-228">número de serie del dispositivo de Hola se asigna en el generador de Hola y 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b040e-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="b040e-229">Por ejemplo, 8600-SHX0991003G44HT indica:</span><span class="sxs-lookup"><span data-stu-id="b040e-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="b040e-230">8600: es el modelo de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="b040e-231">¿SHX – fabricación Hola sitio.</span><span class="sxs-lookup"><span data-stu-id="b040e-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="b040e-232">0991003: indica un producto específico.</span><span class="sxs-lookup"><span data-stu-id="b040e-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="b040e-233">Últimos 5 dígitos son G44HT-Hola incrementa toocreate números de serie exclusivos.</span><span class="sxs-lookup"><span data-stu-id="b040e-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="b040e-234">Es posible que no sea un conjunto secuencial.</span><span class="sxs-lookup"><span data-stu-id="b040e-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="b040e-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="b040e-235">TimeZone</span></span>                | <span data-ttu-id="b040e-236">Hola dispositivo la zona de horaria que esté establecida en hello portal de Azure durante la implementación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="b040e-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="b040e-237">CurrentController</span></span>       | <span data-ttu-id="b040e-238">controlador de Hola que son de interfaz de Windows PowerShell de hello toothrough conectados del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="b040e-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="b040e-239">ActiveController</span></span>        | <span data-ttu-id="b040e-240">controlador de Hola que está activa en el dispositivo y controla todas las operaciones de red y disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="b040e-241">Puede ser el Controlador 0 o el Controlador 1.</span><span class="sxs-lookup"><span data-stu-id="b040e-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="b040e-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="b040e-242">Controller0Status</span></span>       | <span data-ttu-id="b040e-243">estado de saludo del controlador 0 en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="b040e-244">estado del controlador Hola puede ser normal, en modo de recuperación, o es inaccesible.</span><span class="sxs-lookup"><span data-stu-id="b040e-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="b040e-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="b040e-245">Controller1Status</span></span>       | <span data-ttu-id="b040e-246">estado de saludo del controlador 1 en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="b040e-247">estado del controlador Hola puede ser normal, en modo de recuperación, o es inaccesible.</span><span class="sxs-lookup"><span data-stu-id="b040e-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="b040e-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="b040e-248">SystemMode</span></span>              | <span data-ttu-id="b040e-249">Hola estado general del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="b040e-250">estado del dispositivo Hola puede ser normal, mantenimiento, o dado de baja (corresponde toodeactivated Hola portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="b040e-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="b040e-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="b040e-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="b040e-252">Hola descriptivo cadena correspondiente versión de software de dispositivo de toohello.</span><span class="sxs-lookup"><span data-stu-id="b040e-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="b040e-253">Para un sistema que se ejecuta Update 4, versión de software descriptivo Hola sería StorSimple 8000 Series Update 4.0.</span><span class="sxs-lookup"><span data-stu-id="b040e-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="b040e-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="b040e-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="b040e-255">versión de software de Hello HCS ejecutando en su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="b040e-256">Por ejemplo, hello tooStorSimple correspondiente de una versión de software HCS 8000 Series Update 4.0 es 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="b040e-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="b040e-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="b040e-257">ApiVersion</span></span>              | <span data-ttu-id="b040e-258">versión de software de Hola de API de Windows PowerShell del dispositivo HCS Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="b040e-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="b040e-259">VhdVersion</span></span>              | <span data-ttu-id="b040e-260">versión de software de Hola de imagen de fábrica de Hola que hello de dispositivo se distribuyó con.</span><span class="sxs-lookup"><span data-stu-id="b040e-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="b040e-261">Si restablece los valores predeterminados del dispositivo toofactory, a continuación, se ejecuta esta versión de software.</span><span class="sxs-lookup"><span data-stu-id="b040e-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="b040e-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="b040e-262">OSVersion</span></span>               | <span data-ttu-id="b040e-263">versión de software de Hola de sistema operativo Hola Windows Server que ejecuta en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="b040e-264">dispositivo de StorSimple de Hola se basa en Windows Server 2012 R2 que corresponde too6.3.9600 Hola.</span><span class="sxs-lookup"><span data-stu-id="b040e-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="b040e-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="b040e-265">CisAgentVersion</span></span>         | <span data-ttu-id="b040e-266">versión de Hola para su agente de elementos de configuración que se ejecuta en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="b040e-267">Este agente ayuda a comunicarse con el servicio de StorSimple Manager Hola ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="b040e-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="b040e-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="b040e-268">MdsAgentVersion</span></span>         | <span data-ttu-id="b040e-269">Hola versión correspondiente toohello Mds agente se ejecuta en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="b040e-270">Este agente mueve datos toohello supervisión y diagnóstico de servicio (MDS).</span><span class="sxs-lookup"><span data-stu-id="b040e-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="b040e-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="b040e-271">Lsisas2Version</span></span>          | <span data-ttu-id="b040e-272">Hola controladores de toohello LSI correspondientes de la versión en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="b040e-273">Capacity</span><span class="sxs-lookup"><span data-stu-id="b040e-273">Capacity</span></span>                | <span data-ttu-id="b040e-274">capacidad total de Hello de dispositivo de hello en bytes.</span><span class="sxs-lookup"><span data-stu-id="b040e-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="b040e-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="b040e-275">RemoteManagementMode</span></span>    | <span data-ttu-id="b040e-276">Indica si el dispositivo de hello puede administrarse de manera remota a través de la interfaz de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b040e-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="b040e-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="b040e-277">FipsMode</span></span>                | <span data-ttu-id="b040e-278">Indica si se habilita el modo de Estados Unidos información procesamiento estándar Federal (FIPS) de hello en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b040e-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="b040e-279">estándar de Hello FIPS 140 define los algoritmos criptográficos aprobados para su uso por los sistemas de equipo de Gobierno Federal nos para la protección de Hola de los datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="b040e-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="b040e-280">Para dispositivos que ejecutan Update 4 o posterior, el modo FIPS está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b040e-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b040e-281">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b040e-281">Next steps</span></span>

* <span data-ttu-id="b040e-282">Obtenga información acerca de hello [sintaxis del cmdlet Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="b040e-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="b040e-283">Más información acerca de cómo demasiado[solucionar problemas de implementación](storsimple-troubleshoot-deployment.md) en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b040e-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>

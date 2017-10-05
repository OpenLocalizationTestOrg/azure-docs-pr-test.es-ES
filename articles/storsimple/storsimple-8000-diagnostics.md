---
title: "Herramienta de diagnóstico para la solución de problemas de dispositivos de StorSimple 8000 | Microsoft Docs"
description: "Describe los modos de dispositivo StorSimple y explica cómo usar Windows PowerShell para StorSimple para cambiar el modo del dispositivo."
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
ms.openlocfilehash: 8fae7bb357f8e5e8eff249edfe3a2aaafe04283c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="72747-103">Use la herramienta de diagnóstico de StorSimple para solucionar los problemas de los dispositivos de la serie 8000.</span><span class="sxs-lookup"><span data-stu-id="72747-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="72747-104">Información general</span><span class="sxs-lookup"><span data-stu-id="72747-104">Overview</span></span>

<span data-ttu-id="72747-105">La herramienta de diagnóstico de StorSimple diagnostica problemas relacionados con el sistema, el rendimiento, la red y el estado de los componentes de hardware de un dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="72747-106">Esta herramienta se puede usar en diversos escenarios.</span><span class="sxs-lookup"><span data-stu-id="72747-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="72747-107">Estos escenarios incluyen el planeamiento de la carga de trabajo, la implementación de un dispositivo de StorSimple, la evaluación del entorno de red y la determinación del rendimiento de un dispositivo operativo.</span><span class="sxs-lookup"><span data-stu-id="72747-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="72747-108">En este artículo se proporciona información general de la herramienta de diagnóstico y se describe cómo puede usarla con un dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="72747-109">La herramienta de diagnóstico va dirigida principalmente a la serie dispositivos locales de StorSimple de la serie 8000 (8100 y 8600).</span><span class="sxs-lookup"><span data-stu-id="72747-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="72747-110">Ejecución de la herramienta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="72747-110">Run diagnostics tool</span></span>

<span data-ttu-id="72747-111">Esta herramienta se puede ejecutar mediante la interfaz de Windows PowerShell del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="72747-112">Hay dos maneras de acceder a la interfaz local del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="72747-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="72747-113">[Uso de PuTTY para conectarse a la consola serie del dispositivo](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="72747-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="72747-114">[Acceso remoto a la herramienta mediante Windows PowerShell para StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="72747-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="72747-115">En este artículo, se supone que se ha conectado a la consola serie del dispositivo mediante PuTTY.</span><span class="sxs-lookup"><span data-stu-id="72747-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="72747-116">Para ejecutar la herramienta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="72747-116">To run the diagnostics tool</span></span>

<span data-ttu-id="72747-117">Cuando se haya conectado a la interfaz de Windows PowerShell del dispositivo, realice los pasos siguientes para ejecutar el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="72747-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="72747-118">Inicie sesión en la consola serie del dispositivo siguiendo los pasos detallados en [Uso de PuTTY para conectarse a la consola serie del dispositivo](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="72747-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="72747-119">Escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="72747-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="72747-120">Si no se especifica el parámetro de ámbito, el cmdlet ejecuta todas las pruebas de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="72747-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="72747-121">Estas pruebas incluyen el sistema, el estado de los componentes de hardware, la red y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="72747-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="72747-122">Para ejecutar solo una prueba concreta, especifique el parámetro de ámbito.</span><span class="sxs-lookup"><span data-stu-id="72747-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="72747-123">Por ejemplo, para ejecutar solo la prueba de red, escriba</span><span class="sxs-lookup"><span data-stu-id="72747-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="72747-124">Seleccione y copie el resultado de la ventana PuTTY en un archivo de texto para analizarlo más a fondo.</span><span class="sxs-lookup"><span data-stu-id="72747-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="72747-125">Escenarios de uso de la herramienta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="72747-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="72747-126">Use la herramienta de diagnóstico para solucionar los problemas de estado de la red, el rendimiento, el sistema y el hardware.</span><span class="sxs-lookup"><span data-stu-id="72747-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="72747-127">Algunos posibles escenarios son:</span><span class="sxs-lookup"><span data-stu-id="72747-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="72747-128">**Dispositivo sin conexión**: su dispositivo de StorSimple de la serie 8000 está desconectado.</span><span class="sxs-lookup"><span data-stu-id="72747-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="72747-129">Sin embargo, en la interfaz de Windows PowerShell, parece que ambos controladores están funcionando.</span><span class="sxs-lookup"><span data-stu-id="72747-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="72747-130">Puede usar esta herramienta para determinar el estado de la red.</span><span class="sxs-lookup"><span data-stu-id="72747-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="72747-131">No use esta herramienta para evaluar la configuración del rendimiento y de la red en un dispositivo antes del registro (o la configuración mediante el Asistente para la instalación).</span><span class="sxs-lookup"><span data-stu-id="72747-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="72747-132">Durante el Asistente para la instalación y el registro se asigna una dirección IP válida.</span><span class="sxs-lookup"><span data-stu-id="72747-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="72747-133">Puede ejecutar este cmdlet en un dispositivo que no esté registrado para conocer el estado del hardware y del sistema.</span><span class="sxs-lookup"><span data-stu-id="72747-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="72747-134">Use el parámetro de ámbito, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="72747-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="72747-135">**Problemas constantes en el dispositivo**: está experimentando problemas en el dispositivo que no desaparecen.</span><span class="sxs-lookup"><span data-stu-id="72747-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="72747-136">Por ejemplo, error en el registro.</span><span class="sxs-lookup"><span data-stu-id="72747-136">For instance, registration is failing.</span></span> <span data-ttu-id="72747-137">Pueden tratarse también de problemas que aparecen después de que el dispositivo se ha registrado correctamente y lleva algún tiempo funcionando.</span><span class="sxs-lookup"><span data-stu-id="72747-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="72747-138">En este caso, puede usar esta herramienta para la solución de problemas preliminar antes de registrar una solicitud de servicio con el soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="72747-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="72747-139">Se recomienda ejecutar esta herramienta y capturar su salida.</span><span class="sxs-lookup"><span data-stu-id="72747-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="72747-140">Así se la podrá proporcionar al equipo de soporte técnico para acelerar la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="72747-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="72747-141">Si existe algún error en el componente de hardware o el clúster, debe registrar una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="72747-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="72747-142">**Rendimiento bajo del dispositivo**: el dispositivo de StorSimple es lento.</span><span class="sxs-lookup"><span data-stu-id="72747-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="72747-143">En este caso, ejecute este cmdlet con el parámetro de ámbito establecido en rendimiento.</span><span class="sxs-lookup"><span data-stu-id="72747-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="72747-144">Analice la salida.</span><span class="sxs-lookup"><span data-stu-id="72747-144">Analyze the output.</span></span> <span data-ttu-id="72747-145">Obtenga las latencias de lectura y escritura en la nube.</span><span class="sxs-lookup"><span data-stu-id="72747-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="72747-146">Use las latencias notificadas como el objetivo máximo que se puede conseguir, estime alguna sobrecarga en el procesamiento de datos interno y luego implemente las cargas de trabajo en el sistema.</span><span class="sxs-lookup"><span data-stu-id="72747-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="72747-147">Para más información, vaya a [Uso de la prueba de red para solucionar los problemas de rendimiento del dispositivo](#network-test).</span><span class="sxs-lookup"><span data-stu-id="72747-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="72747-148">Salidas de ejemplo y prueba de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="72747-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="72747-149">Prueba de hardware</span><span class="sxs-lookup"><span data-stu-id="72747-149">Hardware test</span></span>

<span data-ttu-id="72747-150">Esta prueba determina el estado de los componentes de hardware, el firmware de USM y el firmware de disco que se ejecutan en el sistema.</span><span class="sxs-lookup"><span data-stu-id="72747-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="72747-151">Los componentes de hardware notificados son aquellos componentes que no superaron la prueba o no están presentes en el sistema.</span><span class="sxs-lookup"><span data-stu-id="72747-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="72747-152">Las versiones de firmware de disco y firmware de USM se notifican para el Controlador 0, el Controlador 1 y los componentes compartidos del sistema.</span><span class="sxs-lookup"><span data-stu-id="72747-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="72747-153">Para obtener una lista completa de los componentes de hardware, vaya a:</span><span class="sxs-lookup"><span data-stu-id="72747-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="72747-154">Componentes de la caja principal</span><span class="sxs-lookup"><span data-stu-id="72747-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="72747-155">Componentes de la caja EBOD</span><span class="sxs-lookup"><span data-stu-id="72747-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="72747-156">Si la prueba de hardware informa de componentes con errores, [registre una solicitud de servicio con el soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="72747-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="72747-157">La salida de ejemplo de la prueba de hardware se ejecuta en un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="72747-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="72747-158">Esta es una salida de ejemplo de un dispositivo de StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="72747-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="72747-159">En el dispositivo modelo 8100, la caja de EBOD no está presente.</span><span class="sxs-lookup"><span data-stu-id="72747-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="72747-160">Por lo tanto, no se notifican los componentes del controlador de EBOD.</span><span class="sxs-lookup"><span data-stu-id="72747-160">Hence, the EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="72747-161">Prueba del sistema</span><span class="sxs-lookup"><span data-stu-id="72747-161">System test</span></span>

<span data-ttu-id="72747-162">Esta prueba muestra la información del sistema, las actualizaciones disponibles, la información del clúster y la información de servicio del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="72747-163">La información del sistema incluye el modelo, el número de serie del dispositivo, la zona horaria, el estado del controlador y la versión detallada del software que se ejecuta en el sistema.</span><span class="sxs-lookup"><span data-stu-id="72747-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="72747-164">Para entender los distintos parámetros del sistema notificados en la salida, vaya a [Interpretación de la información del sistema](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="72747-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="72747-165">La disponibilidad de actualizaciones informa de si están disponibles los modos normal y de mantenimiento y sus nombres de paquete asociados.</span><span class="sxs-lookup"><span data-stu-id="72747-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="72747-166">Si `RegularUpdates` y `MaintenanceModeUpdates` son `false`, significa que las actualizaciones no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="72747-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="72747-167">El dispositivo está actualizado.</span><span class="sxs-lookup"><span data-stu-id="72747-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="72747-168">La información del clúster contiene la información sobre los diversos componentes lógicos de todos los grupos de clústeres de HCS y sus estados respectivos.</span><span class="sxs-lookup"><span data-stu-id="72747-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="72747-169">Si observa un grupo de clústeres sin conexión en esta sección del informe, [póngase en contacto con el soporte técnico de Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="72747-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="72747-170">La información del servicio incluye los nombres y los estados de todos los servicios HCS y CiS que se ejecutan en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="72747-171">Esta información es útil para el soporte técnico de Microsoft en la solución de problemas del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="72747-172">Salida de ejemplo de la prueba del sistema ejecutada en un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="72747-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="72747-173">Esta es una salida de ejemplo de la prueba del sistema que se ejecuta en un dispositivo 8100.</span><span class="sxs-lookup"><span data-stu-id="72747-173">Here is a sample output of the system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="72747-174">Prueba de red</span><span class="sxs-lookup"><span data-stu-id="72747-174">Network test</span></span>

<span data-ttu-id="72747-175">Esta prueba valida el estado de las interfaces de red, los puertos, la conectividad del servidor DNS y NTP, el certificado SSL, las credenciales de cuenta de almacenamiento, la conectividad a los servidores de actualización y la conectividad del servidor proxy web en el dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="72747-176">Salida de ejemplo de la prueba de red solo cuando está habilitado DATA0</span><span class="sxs-lookup"><span data-stu-id="72747-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="72747-177">Esta es la salida de ejemplo del dispositivo 8100.</span><span class="sxs-lookup"><span data-stu-id="72747-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="72747-178">En la salida, puede apreciar que:</span><span class="sxs-lookup"><span data-stu-id="72747-178">You can see in the output that:</span></span>
* <span data-ttu-id="72747-179">Solo las interfaces de red DATA 0 y DATA 1 están habilitadas y configuradas.</span><span class="sxs-lookup"><span data-stu-id="72747-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="72747-180">Las interfaces de DATA 2 a 5 no están habilitadas en el portal.</span><span class="sxs-lookup"><span data-stu-id="72747-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="72747-181">La configuración del servidor DNS es válida y el dispositivo puede conectarse mediante el servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="72747-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="72747-182">La conectividad del servidor NTP también es correcta.</span><span class="sxs-lookup"><span data-stu-id="72747-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="72747-183">Los puertos 80 y 443 están abiertos.</span><span class="sxs-lookup"><span data-stu-id="72747-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="72747-184">Sin embargo, el puerto 9354 está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="72747-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="72747-185">En función de los [requisitos de red del sistema](storsimple-system-requirements.md), deberá abrir este puerto para la comunicación del bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="72747-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="72747-186">La certificación SSL es válida.</span><span class="sxs-lookup"><span data-stu-id="72747-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="72747-187">El dispositivo puede conectarse a la cuenta de almacenamiento: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="72747-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="72747-188">La conectividad a los servidores de actualización es válida.</span><span class="sxs-lookup"><span data-stu-id="72747-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="72747-189">El proxy web no está configurado en este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="72747-190">Salida de ejemplo de la prueba de red cuando se habilitan DATA0 y DATA1</span><span class="sxs-lookup"><span data-stu-id="72747-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="72747-191">Prueba de rendimiento</span><span class="sxs-lookup"><span data-stu-id="72747-191">Performance test</span></span>

<span data-ttu-id="72747-192">Esta prueba muestra el rendimiento en la nube mediante las latencias de lectura y escritura en la nube en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="72747-193">Esta herramienta puede usarse para establecer una línea de base del rendimiento en la nube que se puede alcanzar con StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="72747-194">La herramienta notifica el rendimiento máximo (escenario de mejor caso para latencias de lectura y escritura) que puede obtener para la conexión.</span><span class="sxs-lookup"><span data-stu-id="72747-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="72747-195">Como la herramienta notifica el rendimiento máximo que se puede obtener, podemos usar las latencias detectadas de lectura y escritura como objetivos al implementar las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="72747-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="72747-196">La prueba simula los tamaños de blob asociados con los diferentes tipos de volúmenes en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="72747-197">Los niveles normales y las copias de seguridad de volúmenes anclados localmente usan un tamaño de blob de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="72747-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="72747-198">Los volúmenes en capas con la opción de archivado marcada usan un tamaño de datos de blob de 512 KB.</span><span class="sxs-lookup"><span data-stu-id="72747-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="72747-199">Si su dispositivo tiene configurados volúmenes anclados localmente y en capas, solo se ejecuta la prueba correspondiente al tamaño de datos de blob de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="72747-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="72747-200">Para usar esta herramienta, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="72747-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="72747-201">En primer lugar, cree una mezcla de volúmenes en capas y volúmenes anclados localmente con la opción de archivado marcada.</span><span class="sxs-lookup"><span data-stu-id="72747-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="72747-202">Esta acción garantiza que la herramienta ejecuta las pruebas para tamaños de blob de 64 KB y 512 KB.</span><span class="sxs-lookup"><span data-stu-id="72747-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="72747-203">Ejecute el cmdlet cuando haya creado y configurado los volúmenes.</span><span class="sxs-lookup"><span data-stu-id="72747-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="72747-204">Escriba:</span><span class="sxs-lookup"><span data-stu-id="72747-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="72747-205">Anote las latencias de lectura y escritura detectadas por la herramienta.</span><span class="sxs-lookup"><span data-stu-id="72747-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="72747-206">Esta prueba puede tardar varios minutos en ejecutarse antes de notificar los resultados.</span><span class="sxs-lookup"><span data-stu-id="72747-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="72747-207">Si las latencias de conexión están todas en el intervalo esperado, las latencias detectadas por la herramienta se pueden usar como objetivo máximo alcanzable al implementar las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="72747-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="72747-208">Estime cierta sobrecarga en el procesamiento de datos interno.</span><span class="sxs-lookup"><span data-stu-id="72747-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="72747-209">Si las latencias de lectura y escritura detectadas por la herramienta de diagnóstico son demasiado elevadas:</span><span class="sxs-lookup"><span data-stu-id="72747-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="72747-210">Configure el análisis de almacenamiento para los servicios de blob y analice la salida para comprender las latencias de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="72747-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="72747-211">Para obtener instrucciones detalladas, vaya a [Habilitación y configuración del análisis de almacenamiento](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="72747-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="72747-212">Si esas latencias también son altas y comparables a las cifras que recibió con la herramienta de diagnóstico de StorSimple, debe registrar una solicitud de servicio con Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="72747-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="72747-213">Si las latencias de la cuenta de almacenamiento son demasiado bajas, póngase en contacto con su administrador de red para que investigue los problemas de latencia de su red.</span><span class="sxs-lookup"><span data-stu-id="72747-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="72747-214">Salida de ejemplo de una prueba de rendimiento ejecutada en un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="72747-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="72747-215">Apéndice: interpretación de la información del sistema</span><span class="sxs-lookup"><span data-stu-id="72747-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="72747-216">Esta es una tabla que describe cuáles, de los diversos parámetros de Windows PowerShell de información del sistema, se deben asignar.</span><span class="sxs-lookup"><span data-stu-id="72747-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="72747-217">Parámetro de PowerShell</span><span class="sxs-lookup"><span data-stu-id="72747-217">PowerShell Parameter</span></span>    | <span data-ttu-id="72747-218">Descripción</span><span class="sxs-lookup"><span data-stu-id="72747-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="72747-219">Id. de instancia</span><span class="sxs-lookup"><span data-stu-id="72747-219">Instance ID</span></span>             | <span data-ttu-id="72747-220">Cada controlador lleva asociado un identificador único o un GUID.</span><span class="sxs-lookup"><span data-stu-id="72747-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="72747-221">Nombre</span><span class="sxs-lookup"><span data-stu-id="72747-221">Name</span></span>                    | <span data-ttu-id="72747-222">El nombre descriptivo del dispositivo, tal y como se configuró mediante el portal de Azure durante la implementación del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="72747-223">El nombre descriptivo predeterminado es el número de serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="72747-224">Modelo</span><span class="sxs-lookup"><span data-stu-id="72747-224">Model</span></span>                   | <span data-ttu-id="72747-225">El modelo de su dispositivo StorSimple de la serie 8000.</span><span class="sxs-lookup"><span data-stu-id="72747-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="72747-226">Puede ser 8100 o 8600.</span><span class="sxs-lookup"><span data-stu-id="72747-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="72747-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="72747-227">SerialNumber</span></span>            | <span data-ttu-id="72747-228">El número de serie del dispositivo se asigna en la fábrica y tiene una longitud de 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="72747-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="72747-229">Por ejemplo, 8600-SHX0991003G44HT indica:</span><span class="sxs-lookup"><span data-stu-id="72747-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="72747-230">8600: es el modelo del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-230">8600 – Is the device model.</span></span><br><span data-ttu-id="72747-231">SHX: es el sitio de fabricación.</span><span class="sxs-lookup"><span data-stu-id="72747-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="72747-232">0991003: indica un producto específico.</span><span class="sxs-lookup"><span data-stu-id="72747-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="72747-233">G44HT: los 5 últimos dígitos se incrementan para crear números de serie únicos.</span><span class="sxs-lookup"><span data-stu-id="72747-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="72747-234">Es posible que no sea un conjunto secuencial.</span><span class="sxs-lookup"><span data-stu-id="72747-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="72747-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="72747-235">TimeZone</span></span>                | <span data-ttu-id="72747-236">La zona horaria del dispositivo, tal y como se configuró en el portal de Azure durante la implementación del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="72747-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="72747-237">CurrentController</span></span>       | <span data-ttu-id="72747-238">El controlador que está conectado mediante la interfaz de Windows PowerShell del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="72747-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="72747-239">ActiveController</span></span>        | <span data-ttu-id="72747-240">El controlador que está activo en el dispositivo y controla todas las operaciones de red y disco.</span><span class="sxs-lookup"><span data-stu-id="72747-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="72747-241">Puede ser el Controlador 0 o el Controlador 1.</span><span class="sxs-lookup"><span data-stu-id="72747-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="72747-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="72747-242">Controller0Status</span></span>       | <span data-ttu-id="72747-243">El estado del Controlador 0 en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="72747-244">El estado del controlador puede ser normal, en modo de recuperación o inaccesible.</span><span class="sxs-lookup"><span data-stu-id="72747-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="72747-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="72747-245">Controller1Status</span></span>       | <span data-ttu-id="72747-246">El estado del Controlador 1 en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="72747-247">El estado del controlador puede ser normal, en modo de recuperación o inaccesible.</span><span class="sxs-lookup"><span data-stu-id="72747-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="72747-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="72747-248">SystemMode</span></span>              | <span data-ttu-id="72747-249">El estado general del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="72747-250">El estado del dispositivo puede ser normal, mantenimiento o dado de baja (corresponde a desactivado en el portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="72747-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="72747-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="72747-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="72747-252">La cadena descriptiva que corresponde a la versión de software del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="72747-253">Para un sistema que ejecuta Update 4, la versión de software descriptiva sería StorSimple 8000 Series Update 4.0.</span><span class="sxs-lookup"><span data-stu-id="72747-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="72747-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="72747-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="72747-255">La versión de software HCS que se ejecuta en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-255">The HCS software version running on your device.</span></span> <span data-ttu-id="72747-256">Por ejemplo, la versión de software HCS correspondiente a StorSimple 8000 Series Update 4.0 es 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="72747-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="72747-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="72747-257">ApiVersion</span></span>              | <span data-ttu-id="72747-258">La versión de software de la API de Windows PowerShell del dispositivo HCS.</span><span class="sxs-lookup"><span data-stu-id="72747-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="72747-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="72747-259">VhdVersion</span></span>              | <span data-ttu-id="72747-260">La versión de software de la imagen de fábrica con la que se envió el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="72747-261">Si se restablece su dispositivo a los valores predeterminados de fábrica, se ejecuta esta versión de software.</span><span class="sxs-lookup"><span data-stu-id="72747-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="72747-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="72747-262">OSVersion</span></span>               | <span data-ttu-id="72747-263">La versión de software del sistema operativo Windows Server que se ejecuta en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="72747-264">El dispositivo StorSimple se basa en Windows Server 2012 R2 que corresponde a 6.3.9600.</span><span class="sxs-lookup"><span data-stu-id="72747-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="72747-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="72747-265">CisAgentVersion</span></span>         | <span data-ttu-id="72747-266">La versión de su agente Cis que se ejecuta en el dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="72747-267">Este agente ayuda a comunicarse con el servicio StorSimple Manager que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="72747-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="72747-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="72747-268">MdsAgentVersion</span></span>         | <span data-ttu-id="72747-269">La versión correspondiente al agente Mds que se ejecuta en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="72747-270">Este agente mueve los datos al servicio de supervisión y diagnóstico (MDS).</span><span class="sxs-lookup"><span data-stu-id="72747-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="72747-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="72747-271">Lsisas2Version</span></span>          | <span data-ttu-id="72747-272">La versión correspondiente a los controladores LSI del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="72747-273">Capacity</span><span class="sxs-lookup"><span data-stu-id="72747-273">Capacity</span></span>                | <span data-ttu-id="72747-274">La capacidad total del dispositivo en bytes.</span><span class="sxs-lookup"><span data-stu-id="72747-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="72747-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="72747-275">RemoteManagementMode</span></span>    | <span data-ttu-id="72747-276">Indica si el dispositivo puede administrarse de manera remota a través de su interfaz de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72747-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="72747-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="72747-277">FipsMode</span></span>                | <span data-ttu-id="72747-278">Indica si el modo FIPS (Federal Information Processing Standard) de Estados Unidos está habilitado en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72747-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="72747-279">El estándar FIPS 140 define algoritmos criptográficos aprobados para su uso por parte de los sistemas informáticos del Gobierno federal de los Estados Unidos a fin de garantizar la protección de los datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="72747-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="72747-280">Para dispositivos que ejecutan Update 4 o posterior, el modo FIPS está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="72747-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="72747-281">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72747-281">Next steps</span></span>

* <span data-ttu-id="72747-282">Conozca acerca de la [sintaxis del cmdlet Invoke-HcsDiagnostics](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="72747-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="72747-283">Más información sobre cómo [solucionar problemas de implementación](storsimple-troubleshoot-deployment.md) en el dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72747-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>

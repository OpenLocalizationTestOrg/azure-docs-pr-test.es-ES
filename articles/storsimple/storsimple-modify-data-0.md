---
title: "Hola aaaModify DATA 0 configuración en un dispositivo StorSimple | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Windows PowerShell para StorSimple tooreconfigure Hola datos interfaz de red 0 en el dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="95889-103">Modificar la configuración de interfaz de red 0 Hola datos en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="95889-103">Modify hello DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="95889-104">Información general</span><span class="sxs-lookup"><span data-stu-id="95889-104">Overview</span></span>
<span data-ttu-id="95889-105">El dispositivo de StorSimple de Microsoft Azure tiene seis interfaces de red, desde DATA 0 tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="95889-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="95889-106">Hola DATA 0 interfaz siempre se configura mediante la interfaz de Windows PowerShell de Hola o de consola serie de Hola y está habilitada para la nube automáticamente.</span><span class="sxs-lookup"><span data-stu-id="95889-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="95889-107">Tenga en cuenta que no se puede configurar la interfaz de red 0 de datos a través de hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="95889-107">Note that you cannot configure DATA 0 network interface through hello Azure classic portal.</span></span> 

<span data-ttu-id="95889-108">Hola DATA 0 interfaz primero se configura a través del Asistente para la instalación de Hola durante la implementación inicial de dispositivo de StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="95889-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="95889-109">Cuando el dispositivo de hello está en un modo de funcionamiento, puede que necesite tooreconfigure DATA 0 configuración.</span><span class="sxs-lookup"><span data-stu-id="95889-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="95889-110">Este tutorial proporciona dos métodos de configuración de red 0 datos toomodify, tanto a través de Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="95889-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="95889-111">Después de leer este tutorial, podrá:</span><span class="sxs-lookup"><span data-stu-id="95889-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="95889-112">Modificar datos 0 los valores a través del Asistente para la instalación de Hola de red</span><span class="sxs-lookup"><span data-stu-id="95889-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="95889-113">Modificar la configuración de red 0 de datos a través de hello `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="95889-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="95889-114">Modificar la configuración de red de DATA 0 mediante el asistente para la instalación</span><span class="sxs-lookup"><span data-stu-id="95889-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="95889-115">Puede volver a configurar la configuración de red 0 de datos por conexión toohello de interfaz de Windows PowerShell del dispositivo StorSimple e iniciar una sesión del Asistente de instalación.</span><span class="sxs-lookup"><span data-stu-id="95889-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="95889-116">Realizar Hola siguiendo los pasos toomodify DATA 0 configuración:</span><span class="sxs-lookup"><span data-stu-id="95889-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="95889-117">configuración de red 0 toomodify datos a través del Asistente para la instalación</span><span class="sxs-lookup"><span data-stu-id="95889-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="95889-118">En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="95889-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="95889-119">Cuando se le solicite proporcionar hello **contraseña de administrador de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="95889-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="95889-120">contraseña de Hello predeterminada es `Password1`.</span><span class="sxs-lookup"><span data-stu-id="95889-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="95889-121">En hello símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="95889-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="95889-122">Se mostrará un asistente de instalación toohelp configurar Hola DATA 0 interfaz del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="95889-122">A setup wizard will appear toohelp you configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="95889-123">Proporcione nuevos valores para la máscara de red, la puerta de enlace y la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="95889-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="95889-124">Hola fijo controladores IP necesitará toobe volver a configurar a través de hello **configurar** página del dispositivo de StorSimple de Hola Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="95889-124">hello fixed controllers IPs will need toobe reconfigured through hello **Configure** page of hello StorSimple device in hello Azure classic portal.</span></span> <span data-ttu-id="95889-125">Para obtener más información, consulte demasiado[modificar interfaces de red](storsimple-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="95889-125">For more information, go too[Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="95889-126">Modificación de la configuración de red de DATA 0 mediante el cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="95889-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="95889-127">Un tooreconfigure de forma alternativa DATA 0 es de interfaz de red mediante el uso de Hola de hello `Set-HcsNetInterface` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="95889-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of  hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="95889-128">Hola cmdlet se ejecuta desde la interfaz de Windows PowerShell de hello de dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="95889-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="95889-129">Cuando se utiliza este procedimiento, IP fijas del controlador hello también pueden configurarse aquí.</span><span class="sxs-lookup"><span data-stu-id="95889-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="95889-130">Realizar Hola siguiendo los pasos toomodify Hola DATA 0 configuración:</span><span class="sxs-lookup"><span data-stu-id="95889-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="95889-131">configuración de red 0 toomodify datos a través del cmdlet Set-HcsNetInterface Hola</span><span class="sxs-lookup"><span data-stu-id="95889-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="95889-132">En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="95889-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="95889-133">Cuando se le solicite proporcionar la contraseña de administrador de dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="95889-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="95889-134">contraseña de Hello predeterminada es `Password1`.</span><span class="sxs-lookup"><span data-stu-id="95889-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="95889-135">En hello símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="95889-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="95889-136">Hola en ángulo corchetes, escriba Hola sigue valores para DATA 0:</span><span class="sxs-lookup"><span data-stu-id="95889-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="95889-137">Dirección IPv4</span><span class="sxs-lookup"><span data-stu-id="95889-137">IPv4 address</span></span>
   * <span data-ttu-id="95889-138">Puerta de enlace IPv4</span><span class="sxs-lookup"><span data-stu-id="95889-138">IPv4 gateway</span></span>
   * <span data-ttu-id="95889-139">Máscara de subred IPv4</span><span class="sxs-lookup"><span data-stu-id="95889-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="95889-140">Dirección IPv4 fija para el controlador 0</span><span class="sxs-lookup"><span data-stu-id="95889-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="95889-141">Dirección IPv4 fija para el controlador 1</span><span class="sxs-lookup"><span data-stu-id="95889-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="95889-142">Para obtener más información sobre el uso de Hola de este cmdlet, vaya demasiado[de Windows PowerShell para StorSimple referencia del cmdlet](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="95889-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95889-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95889-143">Next steps</span></span>
* <span data-ttu-id="95889-144">interfaces de red tooconfigure diferentes a DATA 0, puede usar hello [página de configuración en el portal de Azure clásico hello](storsimple-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="95889-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure page in hello Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="95889-145">Si experimenta problemas al configurar las interfaces de red, consulte demasiado[solucionar problemas de implementación](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="95889-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>


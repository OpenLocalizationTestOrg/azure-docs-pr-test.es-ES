---
title: "Modificación de la configuración de DATA 0 en dispositivos de la serie StorSimple 8000 | Microsoft Docs"
description: "Obtenga información acerca de cómo usar Windows PowerShell para StorSimple para volver a configurar la interfaz de red DATA 0 en el dispositivo StorSimple."
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
ms.openlocfilehash: 90df43e22f17fd32fe642514df098b72700e77af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="e344f-103">Modificación de la configuración de la interfaz de red DATA 0 en dispositivos de la serie StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="e344f-103">Modify the DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="e344f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e344f-104">Overview</span></span>

<span data-ttu-id="e344f-105">El dispositivo Microsoft Azure StorSimple tiene seis interfaces de red: de DATA de 0 a DATA 5.</span><span class="sxs-lookup"><span data-stu-id="e344f-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="e344f-106">La interfaz DATA 0 siempre se configura a través de la interfaz de Windows PowerShell o la consola de serie y se habilita para la nube automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e344f-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="e344f-107">Tenga en cuenta que la interfaz de red DATA 0 no se puede configurar mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e344f-107">Note that you cannot configure DATA 0 network interface through the Azure portal.</span></span>

<span data-ttu-id="e344f-108">La interfaz DATA 0 se configura por primera vez a través del asistente para la instalación durante la implementación inicial del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e344f-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="e344f-109">Cuando el dispositivo está en un modo de funcionamiento, tal vez tenga que volver a establecer la configuración de DATA 0.</span><span class="sxs-lookup"><span data-stu-id="e344f-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="e344f-110">En este tutorial se proporcionan dos métodos para modificar la configuración de red de DATA 0, ambos a través de Windows PowerShell para StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e344f-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="e344f-111">Después de leer este tutorial, podrá:</span><span class="sxs-lookup"><span data-stu-id="e344f-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="e344f-112">Modificar la configuración de DATA 0 mediante el asistente para la instalación</span><span class="sxs-lookup"><span data-stu-id="e344f-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="e344f-113">Modificar la configuración de red de DATA 0 mediante el cmdlet `Set-HcsNetInterface`</span><span class="sxs-lookup"><span data-stu-id="e344f-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="e344f-114">Modificar la configuración de red de DATA 0 mediante el asistente para la instalación</span><span class="sxs-lookup"><span data-stu-id="e344f-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="e344f-115">Puede volver a establecer la configuración de red de DATA 0 conectándose a la interfaz de Windows PowerShell del dispositivo StorSimple e iniciando una sesión del asistente para la instalación.</span><span class="sxs-lookup"><span data-stu-id="e344f-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="e344f-116">Siga estos pasos para modificar la configuración de DATA 0.</span><span class="sxs-lookup"><span data-stu-id="e344f-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="e344f-117">Para modificar la configuración de red de DATA 0 mediante el asistente para la instalación</span><span class="sxs-lookup"><span data-stu-id="e344f-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="e344f-118">En el menú de la consola serie, seleccione la opción 1, **Iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="e344f-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="e344f-119">Cuando se le solicite, proporcione la **contraseña de administrador del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="e344f-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="e344f-120">La contraseña predeterminada es `Password1`.</span><span class="sxs-lookup"><span data-stu-id="e344f-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="e344f-121">En el símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="e344f-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="e344f-122">Aparece un asistente para instalación que le ayudará a configurar la interfaz DATA 0 del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e344f-122">A setup wizard appears to help configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="e344f-123">Proporcione nuevos valores para la dirección IP, la pasarela y la máscara de red.</span><span class="sxs-lookup"><span data-stu-id="e344f-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="e344f-124">Las direcciones IP de los controladores fijos tendrán que reconfigurarse desde la hoja **Configuración de red** del dispositivo StorSimple en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e344f-124">The fixed controllers IPs will need to be reconfigured through the **Network settings** blade of the StorSimple device in the Azure portal.</span></span> <span data-ttu-id="e344f-125">Para obtener más información, vaya a [Modificar las interfaces de red](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="e344f-125">For more information, go to [Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="e344f-126">Modificación de la configuración de red de DATA 0 mediante el cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="e344f-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="e344f-127">Una alternativa para volver a configurar la interfaz de red DATA 0 es mediante el cmdlet `Set-HcsNetInterface` .</span><span class="sxs-lookup"><span data-stu-id="e344f-127">An alternate way to reconfigure DATA 0 network interface is through the use of the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="e344f-128">El cmdlet se ejecuta desde la interfaz de Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e344f-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="e344f-129">Cuando se utiliza este procedimiento, también se puede configurar aquí el controlador de direcciones IP fijas.</span><span class="sxs-lookup"><span data-stu-id="e344f-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="e344f-130">Siga estos pasos para modificar la configuración de DATA 0:</span><span class="sxs-lookup"><span data-stu-id="e344f-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="e344f-131">Para modificar la configuración de la red DATA 0 mediante el cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="e344f-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="e344f-132">En el menú de la consola serie, seleccione la opción 1, **Iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="e344f-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="e344f-133">Cuando se le solicite, proporcione la contraseña del administrador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e344f-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="e344f-134">La contraseña predeterminada es `Password1`.</span><span class="sxs-lookup"><span data-stu-id="e344f-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="e344f-135">En el símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="e344f-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="e344f-136">En los corchetes angulares, escriba los siguientes valores para DATA 0:</span><span class="sxs-lookup"><span data-stu-id="e344f-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="e344f-137">Dirección IPv4</span><span class="sxs-lookup"><span data-stu-id="e344f-137">IPv4 address</span></span>
   * <span data-ttu-id="e344f-138">Puerta de enlace IPv4</span><span class="sxs-lookup"><span data-stu-id="e344f-138">IPv4 gateway</span></span>
   * <span data-ttu-id="e344f-139">Máscara de subred IPv4</span><span class="sxs-lookup"><span data-stu-id="e344f-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="e344f-140">Dirección IPv4 fija para el controlador 0</span><span class="sxs-lookup"><span data-stu-id="e344f-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="e344f-141">Dirección IPv4 fija para el controlador 1</span><span class="sxs-lookup"><span data-stu-id="e344f-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="e344f-142">Para más información sobre cómo usar este cmdlet, vaya a la [referencia de cmdlet de Windows PowerShell para StorSimple](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="e344f-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e344f-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e344f-143">Next steps</span></span>
* <span data-ttu-id="e344f-144">Para configurar interfaces de red que no sean DATA 0, consulte el artículo acerca de la [configuración de opciones de red en Azure Portal](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="e344f-144">To configure network interfaces other than DATA 0, you can use the [Configure network settings in the Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="e344f-145">Si experimenta problemas al configurar las interfaces de red, consulte [Solucionar problemas de implementación](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e344f-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>


---
title: "aaaTroubleshoot problemas de activación de máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Proporciona Hola solucionar pasos para solucionar problemas de activación de máquina virtual de Windows en Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="038c2-103">Solución de problemas de activación de máquinas virtuales Windows de Azure</span><span class="sxs-lookup"><span data-stu-id="038c2-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="038c2-104">Si tienes algún problema al activar la máquina de virtual de Windows Azure (VM) que se crea a partir de una imagen personalizada, puede usar información de hello proporcionada en este problema de hello tootroubleshoot de documento.</span><span class="sxs-lookup"><span data-stu-id="038c2-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="038c2-105">Síntoma</span><span class="sxs-lookup"><span data-stu-id="038c2-105">Symptom</span></span>

<span data-ttu-id="038c2-106">Cuando intente tooactivate una VM de Windows Azure, recibirá un error mensaje es similar a Hola según muestra:</span><span class="sxs-lookup"><span data-stu-id="038c2-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="038c2-107">**Error: Hola 0xC004F074 LicensingService de Software informó de que ese equipo hello no se pudo activar. No Key ManagementService (KMS) could be contacted. Vea Hola registro de eventos de aplicación para obtener información adicional.**</span><span class="sxs-lookup"><span data-stu-id="038c2-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="038c2-108">Causa</span><span class="sxs-lookup"><span data-stu-id="038c2-108">Cause</span></span>
<span data-ttu-id="038c2-109">Por lo general, problemas de activación de la máquina virtual de Azure ocurrir si Hola VM de Windows no está configurada de utilizando Hola correspondiente clave de configuración de cliente KMS u Hola VM de Windows tiene un toohello de problema de conectividad servicio de KMS de Azure (kms.core.windows.net, puerto 1668).</span><span class="sxs-lookup"><span data-stu-id="038c2-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="038c2-110">Solución</span><span class="sxs-lookup"><span data-stu-id="038c2-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="038c2-111">Si está usando una VPN de sitio a sitio y forzar el túnel, vea [Use Azure personalizado enruta tooenable activación de KMS con la tunelización forzada](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="038c2-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="038c2-112">Si usas ExpressRoute y tiene una ruta predeterminada publica, vea [máquina virtual de Azure puede conmutar por error tooactivate ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="038c2-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="038c2-113">Paso 1 Configurar Hola clave KMS apropiada cliente el programa de instalación (para Windows Server 2016 y Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="038c2-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="038c2-114">Para hello máquina virtual que se crea a partir de una imagen personalizada de Windows Server 2016 o Windows Server 2012 R2, debe configurar Hola clave KMS apropiada cliente el programa de instalación para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="038c2-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="038c2-115">Este paso no aplica tooWindows 2012 o Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="038c2-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="038c2-116">Usa la característica de activación de automatización de la máquina Virtual (AVMA) de hello, que solo es compatible con Windows Server 2016 y Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="038c2-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="038c2-117">Ejecute **slmgr.vbs /dlv** en un símbolo del sistema con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="038c2-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="038c2-118">Compruebe Hola valor de descripción en la salida de hello y, a continuación, determine si se creó desde comercial (canal MINORISTA) o medios de licencias por volumen (VOLUME_KMSCLIENT):</span><span class="sxs-lookup"><span data-stu-id="038c2-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="038c2-119">Si **slmgr.vbs /dlv** muestra canal MINORISTA, ejecute hello después Hola de comandos tooset [clave de configuración de cliente KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) para la versión de Hola de Windows Server se utiliza y obligarlo tooretry activación:</span><span class="sxs-lookup"><span data-stu-id="038c2-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="038c2-120">Por ejemplo, para Windows Server 2016 Datacenter, ejecutaría Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="038c2-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="038c2-121">Paso 2 Compruebe la conectividad de hello entre Hola VM y el servicio de KMS de Azure</span><span class="sxs-lookup"><span data-stu-id="038c2-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="038c2-122">Descargue y extraiga hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) carpeta local de herramienta tooa Hola VM que no lo activa.</span><span class="sxs-lookup"><span data-stu-id="038c2-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="038c2-123">Paso tooStart, buscar en Windows PowerShell, haga clic en Windows PowerShell y, a continuación, seleccione Ejecutar como administrador.</span><span class="sxs-lookup"><span data-stu-id="038c2-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="038c2-124">Asegúrese de que ese hello en la que máquina virtual está configurado el servidor de KMS de Azure correcta de toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="038c2-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="038c2-125">toodo esto, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="038c2-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="038c2-126">Hola comando debe devolver: nombre del equipo de servicio de administración de claves establece tookms.core.windows.net:1688 correctamente.</span><span class="sxs-lookup"><span data-stu-id="038c2-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="038c2-127">Comprobar mediante Psping que dispone de conectividad toohello KMS servidor.</span><span class="sxs-lookup"><span data-stu-id="038c2-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="038c2-128">Cambiar carpeta toohello donde extrajo descarga Pstools.zip de hello y, a continuación, ejecute el siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="038c2-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="038c2-129">En línea de segundo al último de Hola de salida de hello, asegúrese de que ve: enviados = 4, recibidos = 4, perdidos = 0 (0% perdidos).</span><span class="sxs-lookup"><span data-stu-id="038c2-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="038c2-130">Si pierde es mayor que 0 (cero), Hola VM no tiene servidor KMS de toohello de conectividad.</span><span class="sxs-lookup"><span data-stu-id="038c2-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="038c2-131">En esta situación, si hello máquina virtual está en una red virtual y se un servidor DNS personalizado especificado, debe asegurarse de que ese servidor DNS es capaz de tooresolve kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="038c2-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="038c2-132">O bien, cambiar Hola DNS server tooone que resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="038c2-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="038c2-133">Tenga en cuenta que si quita todos los servidores DNS de una red virtual, las máquinas virtuales usan el servicio DNS interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="038c2-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="038c2-134">Este servicio pude resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="038c2-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="038c2-135">Compruebe también que firewall de invitado hello no se configuró de forma que bloquearía los intentos de activación.</span><span class="sxs-lookup"><span data-stu-id="038c2-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="038c2-136">Después de comprobar la conectividad correcta tookms.core.windows.net, ejecute hello siguiente comando en ese símbolo del sistema con privilegios elevados de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="038c2-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="038c2-137">Este comando intenta la activación varias veces.</span><span class="sxs-lookup"><span data-stu-id="038c2-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="038c2-138">Una activación correcta devuelve información similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="038c2-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="038c2-139">**Activación de Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … El producto se activó correctamente.**</span><span class="sxs-lookup"><span data-stu-id="038c2-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="038c2-140">P+F</span><span class="sxs-lookup"><span data-stu-id="038c2-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="038c2-141">He creado Hola Windows Server 2016 de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="038c2-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="038c2-142">¿Es necesario tooconfigure clave KMS para activar Hola Windows Server 2016?</span><span class="sxs-lookup"><span data-stu-id="038c2-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="038c2-143">No.</span><span class="sxs-lookup"><span data-stu-id="038c2-143">No.</span></span> <span data-ttu-id="038c2-144">imagen de Hello en Azure Marketplace tiene Hola clave KMS apropiada cliente el programa de instalación ya configurado.</span><span class="sxs-lookup"><span data-stu-id="038c2-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="038c2-145">¿Trabajo de activación de Windows hello misma forma independientemente si Hola VM está usando Azure híbrida uso beneficio (centro) o no?</span><span class="sxs-lookup"><span data-stu-id="038c2-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="038c2-146">Sí.</span><span class="sxs-lookup"><span data-stu-id="038c2-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="038c2-147">¿Qué sucede si el período de activación de Windows expira?</span><span class="sxs-lookup"><span data-stu-id="038c2-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="038c2-148">Cuando ha expirado el período de gracia de Hola y Windows no está activado todavía, Windows Server 2008 R2 y versiones posteriores de Windows mostrará notificaciones adicionales sobre la activación.</span><span class="sxs-lookup"><span data-stu-id="038c2-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="038c2-149">papel tapiz del escritorio Hola permanece negro y Windows Update se instalará la seguridad y actualizaciones críticas únicamente, pero las actualizaciones opcionales no.</span><span class="sxs-lookup"><span data-stu-id="038c2-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="038c2-150">Vea las notificaciones de hello sección final Hola de hello [condiciones de licencias](http://technet.microsoft.com/en-us/library/ff793403.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="038c2-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="038c2-151">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="038c2-151">Need help?</span></span> <span data-ttu-id="038c2-152">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="038c2-152">Contact support.</span></span>
<span data-ttu-id="038c2-153">Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="038c2-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

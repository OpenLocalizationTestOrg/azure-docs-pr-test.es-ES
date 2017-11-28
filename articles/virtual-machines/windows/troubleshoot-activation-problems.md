---
title: "Solución de problemas de activación de máquinas virtuales de Windows en Azure | Microsoft Docs"
description: "Ofrece los pasos de solución de problemas para resolver problemas de activación de máquinas virtuales de Windows en Azure"
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
ms.openlocfilehash: 77ef396e0bf75fab56bda2e76516b481d018c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="0b8ca-103">Solución de problemas de activación de máquinas virtuales Windows de Azure</span><span class="sxs-lookup"><span data-stu-id="0b8ca-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0b8ca-104">Si tiene algún problema al activar una máquina virtual (VM) Windows de Azure que se crea a partir de una imagen personalizada, puede usar la información proporcionada en este documento para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use the information provided in this document to troubleshoot the issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="0b8ca-105">Síntoma</span><span class="sxs-lookup"><span data-stu-id="0b8ca-105">Symptom</span></span>

<span data-ttu-id="0b8ca-106">Al intentar activar una VM Windows de Azure, recibe un mensaje de error similar al del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b8ca-106">When you try to activate an Azure Windows VM, you receive an error message resembles the following sample:</span></span>

<span data-ttu-id="0b8ca-107">**Error: 0xC004F074 The Software LicensingService reported that the computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see the Application Event Log for additional information.** (Error: 0xC004F074 El Servicio de licencias de software ha notificado que el servicio no se ha podido activar. No se ha podido establecer contacto con ningún Servicio de administración de claves (KMS). Vea el registro de eventos de la aplicación para obtener información adicional).</span><span class="sxs-lookup"><span data-stu-id="0b8ca-107">**Error: 0xC004F074 The Software LicensingService reported that the computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see the Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="0b8ca-108">Causa</span><span class="sxs-lookup"><span data-stu-id="0b8ca-108">Cause</span></span>
<span data-ttu-id="0b8ca-109">Por lo general, los problemas de activación de máquinas virtuales de Azure se producen si la VM de Windows no está configurada con la clave de instalación de cliente KMS apropiada o la tiene un problema de conectividad con el servicio de KMS de Azure (kms.core.windows.net, puerto 1668).</span><span class="sxs-lookup"><span data-stu-id="0b8ca-109">Generally, Azure VM activation issues occur if the Windows VM is not configured by using the appropriate KMS client setup key, or the Windows VM has a connectivity problem to the Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="0b8ca-110">Solución</span><span class="sxs-lookup"><span data-stu-id="0b8ca-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="0b8ca-111">Si usa una VPN de sitio a sitio y tunelización forzada, vea [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) (Uso de rutas personalizadas de Azure para permitir la activación de KMS con tunelización forzada).</span><span class="sxs-lookup"><span data-stu-id="0b8ca-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="0b8ca-112">Si usa ExpressRoute y tiene una ruta predeterminada publica, vea [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx) (Es posible que la máquina virtual de Azure no se pueda activar por ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="0b8ca-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-the-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="0b8ca-113">Paso 1 Configuración de la clave de instalación de cliente KMS adecuada (para Windows Server 2016 y Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="0b8ca-113">Step 1 Configure the appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="0b8ca-114">En el caso de máquinas creadas a partir de una imagen personalizada de Windows Server 2016 o Windows Server 2012 R2, hay que configurar la clave de instalación de cliente KMS adecuada para la VM.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-114">For the VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure the appropriate KMS client setup key for the VM.</span></span>

<span data-ttu-id="0b8ca-115">Este paso no se aplica a Windows 2012 o Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-115">This step does not apply to Windows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="0b8ca-116">Usa la característica Automation Virtual Machine Activation (AVMA), que solo es compatible con Windows Server 2016 y Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-116">It uses the Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="0b8ca-117">Ejecute **slmgr.vbs /dlv** en un símbolo del sistema con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="0b8ca-118">Compruebe el valor de Descripción en la salida y determine si se ha creado desde el canal comercial (RETAIL) o desde soportes de licencia por volumen (VOLUME_KMSCLIENT):</span><span class="sxs-lookup"><span data-stu-id="0b8ca-118">Check the Description value in the output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="0b8ca-119">Si **slmgr.vbs /dlv** muestra el canal RETAIL, ejecute los siguientes comandos para establecer la [clave de instalación de cliente KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) de la versión de Windows Server que se usa y haga que vuelva a intentar la activación:</span><span class="sxs-lookup"><span data-stu-id="0b8ca-119">If **slmgr.vbs /dlv** shows RETAIL channel, run the following commands to set the [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for the version of Windows Server being used, and force it to retry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="0b8ca-120">Por ejemplo, para Windows Server 2016 Datacenter, debe ejecutar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0b8ca-120">For example, for Windows Server 2016 Datacenter, you would run the following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-the-connectivity-between-the-vm-and-azure-kms-service"></a><span data-ttu-id="0b8ca-121">Paso 2 Comprobación de la conectividad entre la VM y el servicio KMS de Azure</span><span class="sxs-lookup"><span data-stu-id="0b8ca-121">Step 2 Verify the connectivity between the VM and Azure KMS service</span></span>

1. <span data-ttu-id="0b8ca-122">Descargue la herramienta [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) y extráigala en una carpeta local en la VM que no se activa.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-122">Download and extract the [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool to a local folder in the VM that does not activate.</span></span> 

2. <span data-ttu-id="0b8ca-123">Vaya a Inicio, busque en Windows PowerShell, haga clic con el botón derecho en Windows PowerShell y seleccione Ejecutar como administrador.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-123">Go to Start, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="0b8ca-124">Asegúrese de que la VM está configurada para usar el servidor de KMS de Azure correcto.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-124">Make sure that the VM is configured to use the correct Azure KMS server.</span></span> <span data-ttu-id="0b8ca-125">Para ello, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0b8ca-125">To do this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="0b8ca-126">El comando debe devolver: Key Management Service machine name set to kms.core.windows.net:1688 successfully (El nombre de máquina del servicio de administración de claves se estableció correctamente en kms.core.windows.net:1688).</span><span class="sxs-lookup"><span data-stu-id="0b8ca-126">The command should return: Key Management Service machine name set to kms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="0b8ca-127">Compruebe con Psping que dispone de conectividad con el servidor de KMS.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-127">Verify by using Psping that you have connectivity to the KMS server.</span></span> <span data-ttu-id="0b8ca-128">Vaya a la carpeta en la que extrajo la descarga de Pstools.zip y ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b8ca-128">Switch to the folder where you extracted the Pstools.zip download, and then run the following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="0b8ca-129">En la penúltima línea, asegúrese de que aparece: Enviados = 4, Recibidos = 4, Perdidos = 0 (0 % de pérdida).</span><span class="sxs-lookup"><span data-stu-id="0b8ca-129">In the second-to-last line of the output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="0b8ca-130">Si el valor de perdidos es mayor que 0 (cero), la máquina virtual no tiene conectividad con el servidor de KMS server.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-130">If Lost is greater than 0 (zero), the VM does not have connectivity to the KMS server.</span></span> <span data-ttu-id="0b8ca-131">En este caso, si la VM está en una red virtual y tiene especificado un servidor DNS personalizado, debe asegurarse de que el servidor DNS es capaz de resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-131">In this situation, if the VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able to resolve kms.core.windows.net.</span></span> <span data-ttu-id="0b8ca-132">También puede cambiar el servidor DNS a uno que pueda resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-132">Or, change the DNS server to one that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="0b8ca-133">Tenga en cuenta que si quita todos los servidores DNS de una red virtual, las máquinas virtuales usan el servicio DNS interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="0b8ca-134">Este servicio pude resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="0b8ca-135">Compruebe también que firewall de invitado no está configurado de manera que bloquee los intentos de activación.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-135">Also verify that the guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="0b8ca-136">Después de comprobar la conectividad correcta con kms.core.windows.net, ejecute el siguiente comando en un símbolo del sistema de Windows PowerShell con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-136">After you verify successful connectivity to kms.core.windows.net, run the following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="0b8ca-137">Este comando intenta la activación varias veces.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="0b8ca-138">Una activación correcta devuelve información similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b8ca-138">A successful activation returns information that resembles the following:</span></span>

<span data-ttu-id="0b8ca-139">**Activación de Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … El producto se activó correctamente.**</span><span class="sxs-lookup"><span data-stu-id="0b8ca-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="0b8ca-140">P+F</span><span class="sxs-lookup"><span data-stu-id="0b8ca-140">FAQ</span></span> 

### <a name="i-created-the-windows-server-2016-from-azure-marketplace-do-i-need-to-configure-kms-key-for-activating-the-windows-server-2016"></a><span data-ttu-id="0b8ca-141">He creado Windows Server 2016 desde Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-141">I created the Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="0b8ca-142">¿Tengo que configurar la clave KMS para activar Windows Server 2016?</span><span class="sxs-lookup"><span data-stu-id="0b8ca-142">Do I need to configure KMS key for activating the Windows Server 2016?</span></span> 
 
<span data-ttu-id="0b8ca-143">No.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-143">No.</span></span> <span data-ttu-id="0b8ca-144">La imagen de Azure Marketplace ya tiene configurada la clave de instalación de cliente KMS apropiada.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-144">The image in Azure Marketplace has the appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-the-same-way-regardless-if-the-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="0b8ca-145">¿La activación de Windows funciona siempre igual sin importar que la VM use la Ventaja de uso híbrido (HUB) de Azure?</span><span class="sxs-lookup"><span data-stu-id="0b8ca-145">Does Windows activation work the same way regardless if the VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="0b8ca-146">Sí.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="0b8ca-147">¿Qué sucede si el período de activación de Windows expira?</span><span class="sxs-lookup"><span data-stu-id="0b8ca-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="0b8ca-148">Cuando el período de gracia ha expirado y Windows no está activado todavía, Windows Server 2008 R2 y las versiones posteriores de Windows mostrarán notificaciones adicionales sobre la activación.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-148">When the grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="0b8ca-149">El fondo de pantalla del escritorio permanece negro y Windows Update solo instalará las actualizaciones críticas y de seguridad, pero no las actualizaciones opcionales.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-149">The desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="0b8ca-150">Vea la sección de notificaciones en la parte inferior de la página [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) (Condiciones de licencias).</span><span class="sxs-lookup"><span data-stu-id="0b8ca-150">See  the Notifications section at the bottom of the [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="0b8ca-151">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="0b8ca-151">Need help?</span></span> <span data-ttu-id="0b8ca-152">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-152">Contact support.</span></span>
<span data-ttu-id="0b8ca-153">Si sigue necesitando ayuda, [póngase en contacto con el servicio de soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver el problema rápidamente.</span><span class="sxs-lookup"><span data-stu-id="0b8ca-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
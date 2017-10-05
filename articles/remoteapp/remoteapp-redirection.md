---
title: Uso del redireccionamiento en Azure RemoteApp | Microsoft Docs
description: "Obtenga información acerca de cómo configurar y usar el redireccionamiento en RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="27109-103">Uso del redireccionamiento de RemoteApp de Azure</span><span class="sxs-lookup"><span data-stu-id="27109-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="27109-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="27109-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="27109-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="27109-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="27109-106">Redireccionamiento de dispositivos permite a los usuarios interactuar con aplicaciones remotas mediante los dispositivos conectados a su equipo local, un teléfono o una tableta.</span><span class="sxs-lookup"><span data-stu-id="27109-106">Device redirection lets your users interact with remote apps using the devices attached to their local computer, phone, or tablet.</span></span> <span data-ttu-id="27109-107">Por ejemplo, si proporciona Skype a través de Azure RemoteApp, el usuario tendrá que disponer de la cámara instalada en su equipo para que funcione con Skype.</span><span class="sxs-lookup"><span data-stu-id="27109-107">For example, if you have provided Skype through Azure RemoteApp, your user needs the camera installed on their PC to work with Skype.</span></span> <span data-ttu-id="27109-108">Esto también se aplica a las impresoras, altavoces, monitores y a una amplia gama de periféricos conectados mediante USB.</span><span class="sxs-lookup"><span data-stu-id="27109-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="27109-109">RemoteApp aprovecha el Protocolo de escritorio remoto (RDP) y RemoteFX para proporcionar la redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="27109-109">RemoteApp leverages the Remote Desktop Protocol (RDP) and RemoteFX to provide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="27109-110">¿Qué redireccionamiento está habilitado de manera predeterminada?</span><span class="sxs-lookup"><span data-stu-id="27109-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="27109-111">Al usar RemoteApp, los redireccionamientos siguientes se habilitan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="27109-111">When you use RemoteApp, the following redirections are enabled by default.</span></span> <span data-ttu-id="27109-112">La información entre paréntesis muestra la configuración de RDP.</span><span class="sxs-lookup"><span data-stu-id="27109-112">The information in parentheses show the RDP setting.</span></span>

* <span data-ttu-id="27109-113">Reproducir sonidos en el equipo local (**reproducir en este equipo**).</span><span class="sxs-lookup"><span data-stu-id="27109-113">Play sounds on the local computer (**Play on this computer**).</span></span> <span data-ttu-id="27109-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="27109-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="27109-115">Capturar audio desde el equipo local y enviar al equipo remoto (**Registro desde este equipo**).</span><span class="sxs-lookup"><span data-stu-id="27109-115">Capture audio from the local computer and send to the remote computer (**Record from this computer**).</span></span> <span data-ttu-id="27109-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="27109-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="27109-117">Imprimir en impresoras locales (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="27109-117">Print to local printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="27109-118">Puertos COM (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="27109-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="27109-119">Dispositivo de tarjeta inteligente (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="27109-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="27109-120">Portapapeles (capacidad de copiar y pegar) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="27109-120">Clipboard (ability to copy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="27109-121">Desactivar el suavizado de fuentes (permitir suavizado de fuentes: i:1)</span><span class="sxs-lookup"><span data-stu-id="27109-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="27109-122">Redirigir todos los dispositivos Plug and Play compatibles.</span><span class="sxs-lookup"><span data-stu-id="27109-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="27109-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="27109-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="27109-124">¿Qué otro redireccionamiento está disponible?</span><span class="sxs-lookup"><span data-stu-id="27109-124">What other redirection is available?</span></span>
<span data-ttu-id="27109-125">Existen dos opciones de redireccionamiento deshabilitadas de forma predeterminada:</span><span class="sxs-lookup"><span data-stu-id="27109-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="27109-126">Redireccionamiento de unidad (asignación de unidades): las unidades del equipo local se convierten en las unidades asignadas en la sesión remota.</span><span class="sxs-lookup"><span data-stu-id="27109-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in the remote session.</span></span> <span data-ttu-id="27109-127">Esto permite guardar o abrir los archivos de las unidades locales mientras trabaja en la sesión remota.</span><span class="sxs-lookup"><span data-stu-id="27109-127">This lets you save or open files from your local drives while you work in the remote session.</span></span>
* <span data-ttu-id="27109-128">Redireccionamiento de USB: puede usar los dispositivos USB conectados al equipo local en la sesión remota.</span><span class="sxs-lookup"><span data-stu-id="27109-128">USB redirection: You can use the USB devices attached to your local computer within the remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="27109-129">Cambiar la configuración de redireccionamiento de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="27109-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="27109-130">Puede cambiar la configuración de redireccionamiento de dispositivos para una colección mediante el uso de Microsoft Azure PowerShell con el SDK.</span><span class="sxs-lookup"><span data-stu-id="27109-130">You can change the device redirection settings for a collection by using the Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="27109-131">Después de instalar el nuevo SDK y PowerShell, primero configúrelo para administrar la suscripción como se describe en [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="27109-131">After you install the new PowerShell and SDK, first configure it to manage your subscription as described in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="27109-132">A continuación, utilice un comando similar al siguiente para establecer las propiedades personalizadas de RDP:</span><span class="sxs-lookup"><span data-stu-id="27109-132">Then use a command similar to the following to set the custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="27109-133">(Tenga en cuenta que  *\`n*  se utiliza como delimitador entre las propiedades individuales.)</span><span class="sxs-lookup"><span data-stu-id="27109-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="27109-134">Para obtener una lista de las propiedades personalizadas de RDP que se configuran, ejecute el siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="27109-134">To get a list of what custom RDP properties are configured, run the following cmdlet.</span></span> <span data-ttu-id="27109-135">Tenga en cuenta que solo se muestran las propiedades personalizadas como resultados de salida y no las propiedades predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="27109-135">Note that only custom properties are shown as output results and not the default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="27109-136">Al establecer las propiedades personalizadas debe especificar todas las propiedades personalizadas cada vez; de lo contrario, la configuración se volverá a deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="27109-136">When you set custom properties you must specify all custom properties each time; otherwise the setting reverts to disabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="27109-137">Ejemplos comunes</span><span class="sxs-lookup"><span data-stu-id="27109-137">Common examples</span></span>
<span data-ttu-id="27109-138">Use el siguiente cmdlet para habilitar el redireccionamiento de la unidad:</span><span class="sxs-lookup"><span data-stu-id="27109-138">Use the following cmdlet to enable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="27109-139">Use este cmdlet para habilitar el redireccionamiento USB y de la unidad:</span><span class="sxs-lookup"><span data-stu-id="27109-139">Use this cmdlet to enable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="27109-140">Use este cmdlet para deshabilitar el uso compartido del portapapeles:</span><span class="sxs-lookup"><span data-stu-id="27109-140">Use this cmdlet to disable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="27109-141">Asegúrese de cerrar completamente la sesión de todos los usuarios de la colección (y no solo de desconectarlos) antes de probar el cambio.</span><span class="sxs-lookup"><span data-stu-id="27109-141">Be sure to completely log off all users in the collection (and not just disconnect them) before you test the change.</span></span> <span data-ttu-id="27109-142">Para asegurarse de que los usuarios han cerrado sesión completamente, vaya a la pestaña **Sesiones** de la colección del portal de Azure y cierre la sesión de todos los usuarios que estén desconectados o que hayan iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="27109-142">To ensure users are completely logged off, go to the **Sessions** tab in the collection in the Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="27109-143">A veces es posible que las unidades locales tarden varios segundos en mostrarse en el explorador dentro de la sesión.</span><span class="sxs-lookup"><span data-stu-id="27109-143">Sometimes it can take several seconds for the local drives to show in Explorer within the session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="27109-144">Cambie la configuración de redireccionamiento de USB en el cliente Windows</span><span class="sxs-lookup"><span data-stu-id="27109-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="27109-145">Si desea usar el redireccionamiento de USB en un equipo que se conecta a RemoteApp, hay 2 acciones que se deben realizar.</span><span class="sxs-lookup"><span data-stu-id="27109-145">If you want to use USB redirection on a computer that connects to RemoteApp, there are 2 actions that need to happen.</span></span> <span data-ttu-id="27109-146">1.- El administrador debe habilitar el redireccionamiento USB en el nivel de colección mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27109-146">1 - Your administrator needs to enable USB redirection at the collection level by using Azure PowerShell.</span></span> <span data-ttu-id="27109-147">2 - En cada dispositivo en el que desee usar el redireccionamiento USB, deberá habilitar una directiva de grupo que lo permita.</span><span class="sxs-lookup"><span data-stu-id="27109-147">2 - On each device where you want to use USB redirection, you need to enable a group policy that permits it.</span></span> <span data-ttu-id="27109-148">Este paso debe realizarse para cada usuario que desee usar el redireccionamiento USB.</span><span class="sxs-lookup"><span data-stu-id="27109-148">This step will need to be done for each user that wants to use USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="27109-149">El redireccionamiento USB con RemoteApp de Azure solo se admite en equipos Windows.</span><span class="sxs-lookup"><span data-stu-id="27109-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a><span data-ttu-id="27109-150">Habilitar el redireccionamiento USB para la colección RemoteApp</span><span class="sxs-lookup"><span data-stu-id="27109-150">Enable USB redirection for the RemoteApp collection</span></span>
<span data-ttu-id="27109-151">Utilice el siguiente cmdlet para habilitar la redirección de USB en el nivel de colección:</span><span class="sxs-lookup"><span data-stu-id="27109-151">Use the following cmdlet to enable USB redirection at the collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a><span data-ttu-id="27109-152">Habilitar el redireccionamiento USB para el equipo cliente</span><span class="sxs-lookup"><span data-stu-id="27109-152">Enable USB redirection for the client computer</span></span>
<span data-ttu-id="27109-153">Para configurar el redireccionamiento USB en su equipo:</span><span class="sxs-lookup"><span data-stu-id="27109-153">To configure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="27109-154">Abra el Editor de directivas de grupo local (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="27109-154">Open the Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="27109-155">(Ejecute gpedit.msc desde un símbolo del sistema de comando).</span><span class="sxs-lookup"><span data-stu-id="27109-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="27109-156">Abra **Configuración del equipo\Directivas\Plantillas administrativas\Componentes Windows\Servicios de escritorio remoto\Cliente de conexión de escritorio remoto\Redireccionamiento de dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="27109-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="27109-157">Haga doble clic en **Permitir el redireccionamiento RDP de otros dispositivos USB RemoteFX compatibles desde este equipo**.</span><span class="sxs-lookup"><span data-stu-id="27109-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="27109-158">Seleccione **Habilitado**, y, a continuación, seleccione **Administradores y usuarios en los derechos de acceso de redireccionamiento de RemoteFX USB**.</span><span class="sxs-lookup"><span data-stu-id="27109-158">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="27109-159">Abra un símbolo del sistema de comandos con permisos administrativos y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="27109-159">Open a command prompt with administrative permissions, and run the following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="27109-160">Reinicie el equipo.</span><span class="sxs-lookup"><span data-stu-id="27109-160">Restart the computer.</span></span>

<span data-ttu-id="27109-161">También puede utilizar la herramienta de administración de directivas de grupo para crear y aplicar la directiva de redireccionamiento USB para todos los equipos del dominio:</span><span class="sxs-lookup"><span data-stu-id="27109-161">You can also use the Group Policy Management tool to create and apply the USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="27109-162">Inicie sesión en el controlador de dominio como administrador de dominio.</span><span class="sxs-lookup"><span data-stu-id="27109-162">Log into the domain controller as the domain administrator.</span></span>
2. <span data-ttu-id="27109-163">Abra la consola de administración de directivas de grupo.</span><span class="sxs-lookup"><span data-stu-id="27109-163">Open the Group Policy Management Console.</span></span> <span data-ttu-id="27109-164">(Haga clic en **Inicio > Herramientas administrativas > Administración de directivas de grupo**).</span><span class="sxs-lookup"><span data-stu-id="27109-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="27109-165">Navegue hasta el dominio o unidad organizativa para la que desea crear la directiva.</span><span class="sxs-lookup"><span data-stu-id="27109-165">Navigate to the domain or organizational unit for which you want to create the policy.</span></span>
4. <span data-ttu-id="27109-166">Haga clic con el botón derecho en **Directiva de dominio predeterminada** y, a continuación, haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="27109-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="27109-167">Abra **Configuración del equipo\Directivas\Plantillas administrativas\Componentes Windows\Servicios de escritorio remoto\Cliente de conexión de escritorio remoto\Redireccionamiento de dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="27109-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="27109-168">Haga doble clic en **Permitir el redireccionamiento RDP de otros dispositivos USB RemoteFX compatibles desde este equipo**.</span><span class="sxs-lookup"><span data-stu-id="27109-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="27109-169">Seleccione **Habilitado**, y, a continuación, seleccione **Administradores y usuarios en los derechos de acceso de redireccionamiento de RemoteFX USB**.</span><span class="sxs-lookup"><span data-stu-id="27109-169">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="27109-170">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="27109-170">Click **OK**.</span></span>  


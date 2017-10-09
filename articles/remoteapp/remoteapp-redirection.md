---
title: "redirección de aaaUsing en Azure RemoteApp | Documentos de Microsoft"
description: "Obtenga información acerca de cómo redirección tooconfigure y el uso de RemoteApp"
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
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="cd316-103">Uso del redireccionamiento de RemoteApp de Azure</span><span class="sxs-lookup"><span data-stu-id="cd316-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cd316-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="cd316-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cd316-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="cd316-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cd316-106">Redirección de dispositivos permite a los usuarios interactuar con aplicaciones remotas mediante el equipo local de hello dispositivos tootheir adjunto, teléfono o tableta.</span><span class="sxs-lookup"><span data-stu-id="cd316-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="cd316-107">Por ejemplo, si ha proporcionado Skype a través de RemoteApp de Azure, el usuario necesita cámara Hola instalado en su toowork PC con Skype.</span><span class="sxs-lookup"><span data-stu-id="cd316-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="cd316-108">Esto también se aplica a las impresoras, altavoces, monitores y a una amplia gama de periféricos conectados mediante USB.</span><span class="sxs-lookup"><span data-stu-id="cd316-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="cd316-109">RemoteApp aprovecha la redirección de tooprovide de protocolo de escritorio remoto (RDP) y RemoteFX Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="cd316-110">¿Qué redireccionamiento está habilitado de manera predeterminada?</span><span class="sxs-lookup"><span data-stu-id="cd316-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="cd316-111">Cuando usas RemoteApp, Hola siguen las redirecciones está habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cd316-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="cd316-112">información de Hello entre paréntesis indica la configuración de RDP Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="cd316-113">Reproducir sonidos en el equipo local de hello (**reproducir en este equipo**).</span><span class="sxs-lookup"><span data-stu-id="cd316-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="cd316-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="cd316-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="cd316-115">Captura de audio del equipo local de Hola y equipo remoto de envío toohello (**grabar desde este equipo**).</span><span class="sxs-lookup"><span data-stu-id="cd316-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="cd316-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="cd316-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="cd316-117">Imprimir en impresoras de toolocal (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="cd316-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="cd316-118">Puertos COM (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="cd316-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="cd316-119">Dispositivo de tarjeta inteligente (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="cd316-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="cd316-120">Portapapeles (toocopy de capacidad y pegar) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="cd316-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="cd316-121">Desactivar el suavizado de fuentes (permitir suavizado de fuentes: i:1)</span><span class="sxs-lookup"><span data-stu-id="cd316-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="cd316-122">Redirigir todos los dispositivos Plug and Play compatibles.</span><span class="sxs-lookup"><span data-stu-id="cd316-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="cd316-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="cd316-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="cd316-124">¿Qué otro redireccionamiento está disponible?</span><span class="sxs-lookup"><span data-stu-id="cd316-124">What other redirection is available?</span></span>
<span data-ttu-id="cd316-125">Existen dos opciones de redireccionamiento deshabilitadas de forma predeterminada:</span><span class="sxs-lookup"><span data-stu-id="cd316-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="cd316-126">Redirección de unidad (asignación de unidad): unidades del equipo local se convierten en las unidades asignadas en la sesión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="cd316-127">Esto permite guardar o abrir archivos desde las unidades locales mientras trabaja en una sesión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="cd316-128">Redireccionamiento de USB: puede usar el equipo local del tooyour adjunto de dispositivos USB Hola dentro sesión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="cd316-129">Cambiar la configuración de redireccionamiento de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cd316-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="cd316-130">Puede cambiar configuración de redirección de dispositivos de Hola para una colección mediante Hola Microsoft Azure PowerShell con el SDK.</span><span class="sxs-lookup"><span data-stu-id="cd316-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="cd316-131">Después de instalar Hola PowerShell nueva y SDK, configurarla primero toomanage su suscripción como se describe en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cd316-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="cd316-132">A continuación, use un toohello similar de comando tooset Hola personalizado RDP propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd316-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="cd316-133">(Tenga en cuenta que  *\`n*  se utiliza como delimitador entre las propiedades individuales.)</span><span class="sxs-lookup"><span data-stu-id="cd316-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="cd316-134">tooget una lista de qué propiedades RDP personalizadas configuradas, ejecute hello siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cd316-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="cd316-135">Tenga en cuenta que las propiedades personalizadas solo se muestran como resultados y no Hola propiedades predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="cd316-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="cd316-136">Al establecer las propiedades personalizadas deben especificar todas las propiedades personalizadas cada vez; en caso contrario, valor de hello revierte toodisabled.</span><span class="sxs-lookup"><span data-stu-id="cd316-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="cd316-137">Ejemplos comunes</span><span class="sxs-lookup"><span data-stu-id="cd316-137">Common examples</span></span>
<span data-ttu-id="cd316-138">Usar hello después de la redirección de unidad de tooenable de cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cd316-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="cd316-139">Usar este cmdlet tooenable redireccionamiento de USB y unidad:</span><span class="sxs-lookup"><span data-stu-id="cd316-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="cd316-140">Use este cmdlet toodisable uso compartido del Portapapeles:</span><span class="sxs-lookup"><span data-stu-id="cd316-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="cd316-141">Ser seguro toocompletely cerrar todos los usuarios de la colección de hello (y no solo desconectarlos) antes de probar los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="cd316-142">tooensure a los usuarios se registran completamente off, vaya toohello **sesiones** ficha en la colección de Hola Hola portal de Azure y cerrar todos los usuarios que están desconectados o está firmados.</span><span class="sxs-lookup"><span data-stu-id="cd316-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="cd316-143">A veces puede tardar varios segundos antes de hello tooshow de las unidades locales en el Explorador de dentro de la sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="cd316-144">Cambie la configuración de redireccionamiento de USB en el cliente Windows</span><span class="sxs-lookup"><span data-stu-id="cd316-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="cd316-145">Si desea toouse redireccionamiento de USB en un equipo que se conecta tooRemoteApp, hay 2 acciones que deben toohappen.</span><span class="sxs-lookup"><span data-stu-id="cd316-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="cd316-146">1: el administrador necesita tooenable redireccionamiento de USB en el nivel de colección de hello mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd316-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="cd316-147">2 - en cada dispositivo en el que desea toouse redireccionamiento de USB, deberá tooenable una directiva de grupo que lo permita.</span><span class="sxs-lookup"><span data-stu-id="cd316-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="cd316-148">Este paso será necesario toobe realiza para cada usuario que desea toouse redireccionamiento de USB.</span><span class="sxs-lookup"><span data-stu-id="cd316-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="cd316-149">El redireccionamiento USB con RemoteApp de Azure solo se admite en equipos Windows.</span><span class="sxs-lookup"><span data-stu-id="cd316-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="cd316-150">Habilitar la redirección de USB para hello colección RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cd316-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="cd316-151">Usar hello después de redireccionamiento de USB tooenable de cmdlet en el nivel de colección de hello:</span><span class="sxs-lookup"><span data-stu-id="cd316-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="cd316-152">Habilitar la redirección de USB para el equipo de cliente hello</span><span class="sxs-lookup"><span data-stu-id="cd316-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="cd316-153">configuración de redirección de tooconfigure USB en el equipo:</span><span class="sxs-lookup"><span data-stu-id="cd316-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="cd316-154">Hola abrir Editor de directivas de grupo Local (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="cd316-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="cd316-155">(Ejecute gpedit.msc desde un símbolo del sistema de comando).</span><span class="sxs-lookup"><span data-stu-id="cd316-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="cd316-156">Abra **Configuración del equipo\Directivas\Plantillas administrativas\Componentes Windows\Servicios de escritorio remoto\Cliente de conexión de escritorio remoto\Redireccionamiento de dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="cd316-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="cd316-157">Haga doble clic en **Permitir el redireccionamiento RDP de otros dispositivos USB RemoteFX compatibles desde este equipo**.</span><span class="sxs-lookup"><span data-stu-id="cd316-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="cd316-158">Seleccione **habilitado**y, a continuación, seleccione **administradores y usuarios en hello derechos de acceso de redirección de USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="cd316-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="cd316-159">Abra un símbolo del sistema con permisos administrativos y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="cd316-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="cd316-160">Reinicie el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-160">Restart hello computer.</span></span>

<span data-ttu-id="cd316-161">También puede utilizar toocreate de herramienta de administración de directivas de grupo de Hola y aplicar directiva de redirección de hello USB para todos los equipos del dominio:</span><span class="sxs-lookup"><span data-stu-id="cd316-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="cd316-162">Inicie sesión en el controlador de dominio de hello como administrador del dominio Hola.</span><span class="sxs-lookup"><span data-stu-id="cd316-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="cd316-163">Abra Hola consola de administración de directivas de grupo.</span><span class="sxs-lookup"><span data-stu-id="cd316-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="cd316-164">(Haga clic en **Inicio > Herramientas administrativas > Administración de directivas de grupo**).</span><span class="sxs-lookup"><span data-stu-id="cd316-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="cd316-165">Navegue toohello dominio o unidad organizativa para la que desea que Directiva de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="cd316-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="cd316-166">Haga clic con el botón derecho en **Directiva de dominio predeterminada** y, a continuación, haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="cd316-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="cd316-167">Abra **Configuración del equipo\Directivas\Plantillas administrativas\Componentes Windows\Servicios de escritorio remoto\Cliente de conexión de escritorio remoto\Redireccionamiento de dispositivo USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="cd316-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="cd316-168">Haga doble clic en **Permitir el redireccionamiento RDP de otros dispositivos USB RemoteFX compatibles desde este equipo**.</span><span class="sxs-lookup"><span data-stu-id="cd316-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="cd316-169">Seleccione **habilitado**y, a continuación, seleccione **administradores y usuarios en hello derechos de acceso de redirección de USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="cd316-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="cd316-170">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cd316-170">Click **OK**.</span></span>  

